# Event Message
## When
1.	On the start or end of a process, or
2.	When the logic controller has determined that an event has happened based on a set of conditions measured by sensors, combined with device state.
## Logical Contents
Event name, and datetime of the event, with accompanying data that may be necessary or useful.
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```string```
* [ComponentCode](#componentcode) ```string```
* [EventName](#eventname) ```string```
* [EventDateTime](#eventdatetime) ```string```
* [Data](#data) ```string```

### MessageType
```string``` = “EventMessage”
### Spec
```string``` = “1.1.0.0”
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

Arbitrary data that the device may send up with the machine. Not intended to be parsed by message processing
## Sample
```JSON
{
  "DeviceId": "OI000002",
  "Spec": "1.1.0.0",
  "MessageType": "EventMessage",
  "MessageId": 988,
  "EventName": "off()",
  "EventDateTime": "2016-03-12T12:40:42Z",
  "ComponentCode": "DCU600",
  "Data": "called"
}
```
## Server-side validations
1.	[EventName](#eventname): Required.
2.	[EventDateTime](#eventdatetime): Required. Standard DateTime validation.
3.	[ComponentCode](#componentcode): Required. If not against a component, must be ‘Machine’.


