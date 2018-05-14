# Common Fields

## Required

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [CreatedDateTime](#createddatetime) ```string```

### MessageType
```string``` 

Contains a string of the message type, as per the details in the individual message types specification. e.g. "SpotTelemetryMessage", "EventMessage"
### Spec
```string``` = "1.1.0.0"

Spec is important for versioning of message processing where breaking changes are made to the standard.
### DeviceId
```string``` 

Uniquely identifies each device on IoT service. On Azure IoT Hub, this needs to match with the [DeviceId]. 

### CreatedDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

DateTime that the message was created (and possibly sent to the messaging platform). Messages can be created by a server or client process.

## Optional

* [DeliveryAcknowledgement](#deliveryacknowledgement) ```string```
* [RequireCommandResponse](#requirecommandResponse) ```byte```

### DeliveryAcknowledgement
```string``` 

This is used to record if the message was successfully ‘completed’ by the device. A message may be successfully delivered, but can be abandoned, rejected or completed. See the [message lifecycle](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-devguide-messages-c2d) documentation for more information on how this works on Azure IoT Hub.

As part of the IoT Hub API, the available options are - _full_, _negative_, and _positive_. This data does not need to be parsed by the device, and is retained in the sent message storage for operational purposes. The _complete_ method on the device API will send the relevant data to the service for operational handling.

Default to _negative_ if not provided.

### RequireCommandResponse
```byte``` 

While the messaging platform DeliveryAcknowledgement provides some feedback on sent messages, it may not be enough. Setting this value to (_0 – Not required or 1 – Required_) indicates that the service expects a [CommandResponseMessage](../01-DeviceToCloud/CommandResponseMessage) once the message is processed. This is necessary where additional information is needed as to the result of the execution. For example, a firmware upgrade message may have a delayed execution (on reboot) and a rollback message if it fails.