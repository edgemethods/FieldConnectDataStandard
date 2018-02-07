# Command Response Message
## Usage
When command messages are sent from the cloud, they can request that a response is set using [RequireCommandResponse]. This is more than delivery acknowledgement, which is part of a basic messaging protocol, and requests that the device report back on the execution of the command.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [MessageReceivedId](#messagereceivedid) ```string```
* [CommandIdentifier](#commandidentifier) ```string```
* [ReceivedMessageType](#receivedmessagetype) ```string```
* [ExecutionDateTime](#executiondatetime) ```string```
* [ErrorCode](#errorcode) ```byte```
* [ExecutionResultMessage](#executionresultmessage) ```string```
* [ExecutionLog](#executionlog) ```object[]```
    * [DateTime](#executionlogdatetime) ```string```
    * [Log](#executionloglog) ```string``` 

### MessageType
```string``` = “CommandResponseMessage”
### Spec
```string``` = “1.1.0.0”
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### MessageReceivedId
```string```

The identifier of the message from the message broker. In Azure IoT Hub this will be [MessageId] from the [DeviceClient message](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.devices.client.message.messageid)
### CommandIdentifier
```string```

An server-generated identifier that can be used to correllate this response with the message sent. Should be unique, such as a GUID.

### ReceivedMessageType
```string```

Command message type that was received.

### ExecutionDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### ErrorCode
```byte```

0 - Success, 1+ - Error code

### ExecutionResultMessage
```string```

### ExecutionLog
```object[]```

List of log items that may have resulted from the command

### ExecutionLog/DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### ExecutionLog/Log
```string```

## Sample
```JSON
{
  "MessageType": "CommandResponseMessage",
  "Spec": "1.1.0.0",
  "DeviceId": "AB000589",
  "MessageId": 19051,
  "DateTime": "2017-03-12T14:45:22Z",
  "MessageReceivedId": "f400af00-39a6-4654-89b7-9f3a8e8d0778",
  "ReceivedMessageType": "UpdateFirmwareMessage",
  "ExecutionDateTime": "2017-03-12T12:25:12Z",
  "ErrorCode": 0,
  "ExecutionResultMessage": "Success",
  "Errors": [
    {
      "DateTime": "2017-03-12T14:05:22Z",
      "Message": "Firmware 8.3.4.2 downloaded"
    },
    {
      "DateTime": "2017-03-12T14:06:18Z",
      "Message": "Firmware 8.3.4.2 applied"
    }
  ]  
}
```

## Server-side validations
1.	[DateTime](#datetime): Required. Standard DateTime validation.
2.	If [CommandIdentifier](#commandidentifier) is null 
    1. [MessageReceivedId](#messagereceivedid): Required.
    2. [ReceivedMessageType](#receivedmessagetype): Required.
4.	[ExecutionDateTime](#executiondatetime): Required. Standard DateTime validation.
5.	[ErrorCode](#errorcode): Required.
