# Common Fields

## Required

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```

### MessageType
```string``` 

Contains a string of the message type, as per the details in the individual message types specification. e.g. "SpotTelemetryMessage", "EventMessage"
### Spec
```string```

Spec is important for versioning of message processing where breaking changes are made to the standard.

#### Server-side validations
1. Should one of the spec versions in [Revisions](/Revisions.md)

## Optional

* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32?```
* [Tags](#tags) ```string[]```
* [Origin](#origin) ```Int32```
* [ThingIdentifier](#thingidentifier) ```string```
* [Processor](#processor) ```string```
* [Upn](#upn) ```string```
* [DataPolicyId](#dataPolicyId) ```string```
* [ScopedTags](#scopedtags) ```object```
* [Identifiers](#identifiers) ```object```
* [Adjustments](#adjustments) ```object```

### DeviceId
```string``` 

Uniquely identifies each device that connects to the cloud services.

#### Server-side validations
1. Required where [Origin](#origin) in [1,2,3,4]
2. Required where [ThingIdentifier](#thingIdentifier) is null
3. If using Azure IoT hub, this must be a valid Azure IoT Hub device identifier.

### MessageId
```Int32?```

MessageId is a sequential counter of messages on the device. It can be duplicated (restart at 0, reset on firmware change), but is used for message ordering and fault identification, so ensuring that it is used correctly improves overall quality.

MessageId is required for messages originating on the device (Origin=2), but not where messages for a device are generated as a side-effect of processing (server-side, edge gateways, etc.) due to other processes not being able to determine what the next MessageId would be.

#### Server-side validations
1. Required where [Origin](#origin) = 2 
2. Required where [Origin](#origin) = null

### Tags
```string[]```

Tags are set on messages to aid cold analytics. For example, messages can be tagged as _Test_ to ensure that setup and test message to do not affect real-world analytics.

### Origin
```Int32```

Used for marking of ‘derived’ messages, where the origin of the message is not the active device. Important for understanding (e.g. count statistics) device versus server-side event detection.

Standard origins are listed below. Others can be added as needed.
  1. Interface board (DAQ)
  2. Device (default if null)
  3. Edge gateway
  4. Cloud gateway
  5. Server-side near real-time
  6. Server-side cold analytics
  7. External systems
  8. User

#### Server-side validations
1.	If [Origin](#origin) = 8: [Upn](#upn) is required.

### ThingIdentifier
```string```

Used when a single device can be used simulaneously or dynamically on multiple 'things'. For example, a PC (as a device) that is connected to multiple machines may need to record telemetry for each machine rather than as itself, or a laptop that is plugged in to different machines from time to time. Consider carefully when using this as it may be better to model a single 'thing' with multple components, rather than multiple 'things'. 

Be aware that ThingIdentifier is only possible if the device is 'smart' enough to know about things or able to be remotely configured. Often the device only knows about itself, such as a room sensor device that knows it's deviceId, but has no context or knowledge about the room (as a thing). It most cases it is better to rely on server-side device management or fitment to know which device is associated to which 'thing'.

#### Server-side validations
1. Required where [Origin](#origin) >= 5 
2. Required where [DeviceId](#deviceid) is null

### Processor
```string```

When messages are derived or created server-side the Porcessor field contains details on the specific processor that generated the message. Could be a function name, or app url.

### Upn
```string```

When telemetry is created by users, such as manual capturing of events or meter-read data, the upn of the user needs to be recorded against the data. The data standard does not specify authentication or authorisation mechanisms.

#### Server-side validations
1.	If [Upn](#upn) is not null: [Origin](#origin) must equal 8.


### DataPolicyId
```string```

Internet of Customer Things data policy that applies to the data.

#### Server-side validations
1.	If [DataPolicyId](#dataPolicyId) is not null:: Internet of Customer Things DataPolicy must be valid for the customer of the thing that the device is fitted to.

### Identifiers
```object[]```

Allows for identifiers as key-value pairs, that may or may not be unique, to be attached to a message for later processing. Example uses include:

* Adding a token that can be used to access related data that is stored elsewhere
* Adding a correlation identifier so that message processing can be tracked

#### Format
Array of Identifier object

* Key ```string```
* Value ```string```

#### Example
```JSON
    "Identifiers" : {
        {
            "Key": "ScopedTagToken:Customer",
            "Value": "5a9244c7-a071-97bb-ba7d-5a741770c96d"
        },
        {
            "Key": "ConversationId",
            "Value": "158bfc57-c994-959f-5863-30d48070e06c"
        }        
    }
```
#### Server-side validations
1. [Identifiers](#identifiers) object is not required
2. If [Identifiers](#identifiers) is not null:
    
    1. Key: Required. Cannot be null or empty string
    2. Value: Required. Cannot be null or empty string

### ScopedTags
```object[]```

ScopedTags allows for arbitrary key-value pairs to be attached to a message that can be processed by downstream services. They can be set of different 'scopes' which can be used for different behaviour based on security or origin scopes.

There are other places where similar data can be attached to a message are listed below. Be considerate of which is the better option for a particular use case:
1. Common fields [Tags](#tags)
2. Component Structure Message component [Properties](ComponentStructureMessage.md#componentsproperties)

#### Format
Array of ScopedTag object

* Key ```string```
* Value ```string```
* Scope ```string```

#### Example
```JSON
    "ScopedTags": [
        {
            "Key": "ProjectCode",
            "Value": "SecretProject5",
            "Scope": "Customer"
        },
        {
            "Key": "SampleId",
            "Value": "DH3546",
            "Scope": "Customer"
        },
        {
            "Key": "ImagingAlgorithm",
            "Value": "RJ45",
        }
    ]
```
#### Server-side validations
1. [ScopedTags](#scopedtags) object is not required
2. If [ScopedTags](#scopedtags) is not null:
    
    1. Key: Required. Cannot be null or empty string
    2. Value: Required. Cannot be null or empty string
    3. Scope: Optional.

### Adjustments
```object[]```

In cases where devices are sending up incorrect data, due to a fault or firmware bug, it is preferred to adjust the data in order to prevent erroneous measurements or to fail the entire message. This is especially valid when other measurements or parts of the message are valid, and when the rollout of updates to devices takes a long time, so continuous manual resubmission of failed messages cannot be done. The adjustment structure preserves the original data and allows for monitoring and logging of automatic adjustments made.

Adjustments can be made anywhere, including the device, or from a UI, but will mostly be done in a field or cloud gateway or on the gatekeeper.

#### Format
Array of Adjustment object

* AdjustmentDateTime ```string```
* Processor ```string```
* ReasonCode ```string```
* Reason ```string```
* AdjustmentPropertyPath ```string```
* OriginalFragment ```object```

#### Example
In the example below, a measurement value of null is sent, which is not possible, so removed from the measurements.
```JSON
"Adjustments": [
    {
      
      "AdjustmentDateTime": "2016-11-03T11:20:43Z",
      "Processor": "SK-Gateway",
      "ReasonCode": "SK-Zero-Amps",
      "Reason": "Heater null amps removed",
      "AdjustmentPropertyPath": "ComponentMeasurements[2].Measurements[0]",
      "OriginalFragment": 
        {
          "Key": "Phase1",
          "UnitOfMeasure": "Amps",
          "Value": "null"
        }
    }
  ]
```