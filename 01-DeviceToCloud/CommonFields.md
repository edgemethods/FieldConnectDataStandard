# Common Fields

## Required

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```

### MessageType
```string``` 

Contains a string of the message type, as per the details in the individual message types specification. e.g. "SpotTelemetryMessage", "EventMessage"
### Spec
```string``` = "1.2.1.0"

Spec is important for versioning of message processing where breaking changes are made to the standard.
### DeviceId
```string``` 

Uniquely identifies each device on IoT service. On Azure IoT Hub, this needs to match with the [DeviceId].

Required where [Origin](#origin) in [1,2,3,4]

### MessageId
```Int32```

MessageId is a sequential counter of messages on the device. It can be duplicated (restart at 0, reset on firmware change), but is used for message ordering and fault identification, so ensuring that it is used correctly improves overall quality.

MessageId is required for messages originating on the device (Origin=2), but not where messages for a device are generated as a side-effect of processing (server-side, edge gateways, etc.) due to other processes not being able to determine what the next MessageId would be.

Required where [Origin](#origin) = 2 or [Origin](#origin) = null

## Optional

* [Tags](#tags) ```string[]```
* [Origin](#origin) ```Int32```
* [Adjustments](#adjustments) ```object```
* [ThingIdentifier](#thingidentifier) ```string```

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

### ThingIdentifier
```string```

Used when a single device can be used simulaneously or dynamically on multiple 'things'. For example, a PC (as a device) that is connected to multiple machines may need to record telemetry for each machine rather than as itself, or a laptop that is plugged in to different machines from time to time. Consider carefully when using this as it may be better to model a single 'thing' with multple components, rather than multiple 'things'. 

Be aware that ThingIdentifier is only possible if the device is 'smart' enough to know about things or able to be remotely configured. Often the device only knows about itself, such as a room sensor device that knows it's deviceId, but has no context or knowledge about the room (as a thing). It most cases it is better to rely on server-side device management or fitment to know which device is associated to which 'thing'.