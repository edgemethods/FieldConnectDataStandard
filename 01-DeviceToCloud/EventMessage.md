# Event Message
## Usage
Event messages are used to mark when a detected event occurred. Event detection can take place on the device, gateway, or server-side processing. Where events are paired as a start/stop or beginning/end of a process, rather use a component cycle.

There is a risk that event messages are used as a replacement for a log file, where data contained within the message is unstructured, difficult to parse, and ultimately of minimal value. Implementers need to make careful use of event messages to check that they’re not using event messages instead of more appropriate message types.
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [ComponentCode](#componentcode) ```string```
* [EventName](#eventname) ```string```
* [EventDateTime](#eventdatetime) ```string```
* [Data](#data) ```string```

### MessageType
```string``` = "EventMessage"
### Spec
```string``` = "1.2.1.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### ComponentCode 
```string```
### EventName
```string```
### EventDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Data
```string```

Arbitrary data that the device may send up with the message. Not intended to be parsed by message processing
## Sample
```JSON
{
  "DeviceId": "AF000002",
  "Spec": "1.2.1.0",
  "MessageType": "EventMessage",
  "MessageId": 988,
  "EventName": "DAC started",
  "EventDateTime": "2016-03-12T12:40:42Z",
  "ComponentCode": "DAC600",
  "Data": "start params /c=100"
}
```
## Server-side validations
1.	[EventName](#eventname): Required.
2.	[EventDateTime](#eventdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).


