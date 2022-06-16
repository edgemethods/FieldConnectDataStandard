# Errors Message
## Usage
Device embedded software tends to have some device-side error handling and logging. In some cases, device errors can, and should, be sent as events. In others, it may be better to ‘log’ errors and transmit them in bulk so that server-side statistics and diagnostics can be done on device errors. The errors message allows device-errors that are logged to be sent.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [Errors](#errors) ```object[]```
    * [DateTime](#errorsdatetime) ```string```
    * [Message](#errorsmessage) ```string``` 

### MessageType
```string``` = "ErrorsMessage"
### Spec
```string``` = "1.2.3.2"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Settings
```object[]```
### Errors/DateTime
```string```

### Errors/Message
```string```

## Sample
```JSON
{
  "MessageType": "ErrorsMessage",
  "Spec": "1.2.3.2",
  "DeviceId": "AB000589",
  "MessageId": 1991,
  "DateTime": "2017-03-12T14:45:22Z",
  "Errors": [
    {
      "DateTime": "2017-03-12T14:05:22Z",
      "Message": "Initialisation of COM1 failed"
    },
    {
      "DateTime": "2017-03-12T14:05:32Z",
      "Message": "Cannot locate detector on USB01"
    }
  ]
}
```

## Server-side validations
1.	[DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.	[Errors](#errors): Required. List cannot be empty.
    1. [DateTime](#errorsdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    2. [Message](#errorsmessage): Required.
