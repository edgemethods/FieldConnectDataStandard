# Properties

## Fields Definition 

### Compression
“On” or “Off” to indicate if message content is Gzip compressed

Item | Notes
---- | -----
Data type | ```string```
Required | Optional. Default – “On”

### Privacy
Bit field of the privacy states determined by the device

Value | State | Description
----- | ----- | -----------
1 |	Personal |	Contains information about an individual. This could be an operator of a machine, or a person that the device is allocated to.
2 |	Company | Contains information about the company. In cases where a machine is used by multiple people without a user login, the information will be about the company.
4 | Direct Identifiable | Personal or company information can be identified directly from the message. For example, the person’s name, or the customer identifier. This may be subject to regulatory definition. A GPS co-ordinate may be considered directly identifiable in some cases.
8 | Derived Identifiable |Contains information that can be derived when combined with other datasets. For example, machine model numbers or serial numbers could be used to find out which customer is likely to have the machine, or IP addresses may indicate location.
16 | Usage | Indicates that the data can divulge usage information about the person or company. For example, data that records start and stop times of components can be used to derive how much a machine is being used.
32 |Private | Most data should be marked as private. Even a single sensor would indicate that a machine is in use, and the amount of use can be considered private. Some diagnostic messages, where no sensor readings are sent can be considered not private.

Item | Notes
---- | -----
Data type | ```Int64```
Required | Optional. Default value will be added to message during processing

While some questions about the privacy of the data can be derived during server-side processing, the first place that this can be done with any degree of accuracy is within the firmware of the device. If a device sends up data such as the operator name, which is obviously personally identifiable, this needs to be set as a property by the firmware as the server will not necessarily know that personal information is in the payload.

The privacy values must be set as message properties, as this allows for privacy-based routing as soon as possible without even inspecting the message. For example, the IoT hub can be configured to route personal, directly identifiable messages to a completely separate message processing pipeline, if needed.
During message processing, the privacy property is put into the message body as an attribute of the message.

If the privacy property is not set, the message will be set to a default high privacy value, such as 5 (Personal and Direct Identifiable).

### Adjustments
In cases where devices are sending up incorrect data, due to a fault or firmware bug, it is preferred to adjust the data in order to prevent erroneous measurements or to fail the entire message. This is especially valid when other measurements or parts of the message are valid, and when the rollout of updates to devices takes a long time, so continuous manual resubmission of failed messages cannot be done. The adjustment structure preserves the original data and allows for monitoring and logging of automatic adjustments made.

Adjustments can be made anywhere, including the device, or from a UI, but will mostly be done in an edge or cloud gateway.

#### Format

* List of
    * AdjustmentDateTime
    * Processor
    * ReasonCode
    * Reason
    * AdjustmentPropertyPath
    * OriginalFragment

##### AdjustmentDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

##### Processor
```string```

##### ReasonCode
```string```

##### AdjustmentPropertyPath
```string```

##### OriginalFragment
```string```

##### Example
In the example below, a measurement value of 0 is sent, which is not possible, so removed from the measurements.
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

