# Interval Event Message
## Usage
When lots of similar events occur and the device either receives a count from an interface board (DAQ) or there is a reason to send an aggregate of events, the Interval Event Message can be used. It contains a count of events on a component during an interval.
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* Interval ```object```
    * [FromDateTime](#intervalfromdatetime) ```string```
    * [ToDateTime](#intervaltodatetime) ```string```
* EventCount ```object[]```
    * [ComponentCode](#eventcountcomponentcode) ```string```
    * [EventName](#eventcounteventname) ```string```
    * [Count](#eventcountcount) ```Int32```

### MessageType
```string``` = "IntervalEventMessage"
### Spec
```string``` = "1.2.0.1"
### DeviceId
```string``` 
### MessageId
```Int32```
### Interval/FromDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

Required
### Interval/ToDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

Required
### EventCount/ComponentCode
```string```

Required
### EventCount/EventName
```string```

Required
### EventCount/Count
```Int32```

Required

## Sample
```JSON
{
  "DeviceId": "C0002",
  "Spec": "1.2.0.1",
  "MessageType": "IntervalEventMessage",
  "MessageId": 0,
  "Interval": {
    "FromDateTime ": "2017-03-11T18:50:48Z",
    "ToDateTime ": "2017-03-12T18:51:48Z"
  },
  "EventCount": [
    {
      "ComponentCode": "M-001",
      "EventName": "Motor start",
      "Count": 32
    },
    {
      "ComponentCode": "B-001",
      "EventName": "Boom extension",
      "Count": 12,
      "Data": "Full"
    },
    {
      "ComponentCode": "B-001",
      "EventName": "Boom extension",
      "Count": 2,
      "Data": "Partial"
    }
  ]
}
```
## Server-side validations
1.	Interval: Required
    1. [FromDateTime](#intervalfromdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    2. [ToDateTime](#intervaltodatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    3. [FromDateTime](#intervalfromdatetime) must be less than ToDateTime. 
2.	EventCount: Required. List cannot be empty.
    1. [ComponentCode](#eventcountcomponentcode): Required.
    2. [EventName](#eventcounteventname): Required.
    3. [Count](#eventcountcount): Required.