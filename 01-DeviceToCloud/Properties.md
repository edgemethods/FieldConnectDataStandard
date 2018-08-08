# Common Properties
Properties can be set on every message that is sent via the messaging protocol (MQTT, AMQP, etc). Properties are used where the content of the message cannot or may not be read.

* [Compression](#compression) ```string```
* [Privacy](#privacy) ```int64```
* [HighImportance](#highimportance) ```byte```

## Compression
```string```

"On" or "Off" to indicate if message content is Gzip compressed

### Validation
* Optional 
* Default = "On"

### Privacy
```int64```

Bit field of the privacy states determined by the device

### Validation
* Optional 
* Default = 32


Value | State | Description
----- | ----- | -----------
1 |	Personal |	Contains information about an individual. This could be an operator of a machine, or a person that the device is allocated to.
2 |	Company | Contains information about the company. In cases where a machine is used by multiple people without a user login, the information will be about the company.
4 | Direct Identifiable | Personal or company information can be identified directly from the message. For example, the person’s name, or the customer identifier. This may be subject to regulatory definition. A GPS co-ordinate may be considered directly identifiable in some cases.
8 | Derived Identifiable |Contains information that can be derived when combined with other datasets. For example, machine model numbers or serial numbers could be used to find out which customer is likely to have the machine, or IP addresses may indicate location.
16 | Usage | Indicates that the data can divulge usage information about the person or company. For example, data that records start and stop times of components can be used to derive how much a machine is being used.
32 |Private | Most data should be marked as private. Even a single sensor would indicate that a machine is in use, and the amount of use can be considered private. Some diagnostic messages, where no sensor readings are sent can be considered not private.

While some questions about the privacy of the data can be derived during server-side processing, the first place that this can be done with any degree of accuracy is within the firmware of the device. If a device sends up data such as the operator name, which is obviously personally identifiable, this needs to be set as a property by the firmware as the server will not necessarily know that personal information is in the payload.

The privacy values must be set as message properties, as this allows for privacy-based routing as soon as possible without even inspecting the message. For example, the IoT hub can be configured to route personal, directly identifiable messages to a completely separate message processing pipeline, if needed.
During message processing, the privacy property is put into the message body as an attribute of the message.

### HighImportance
```byte```

Allows high importance messages to be routed as soon as possible in the pipeline. Handling of high importance messages is up to the server-side platform. Set to 1 to indicate that the message is of high importance.