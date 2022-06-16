# Component Cycle Message
## Usage
The Component Cycle Message is the primary structure to record telemetry relating to utilisation and running processes. A component cycle is an open and close, with the accompanying DateTime, of a component. There are no other states of components, they can only be on or off. To have interim states or processes, a hierarchical structure of virtual components can be used.

It is encouraged that component cycles are created as close to the edge as possible but can be derived server-side if enough other telemetry is available.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [ComponentCode](#componentcode) ```string```
* [CycleState](#cyclestate) ```byte```
* [CycleIdentifier](#cycleidentifier) ```string```
* [OpenDateTime](#opendatetime) ```string```
* [CloseDateTime](#closedatetime) ```string```
* [OpenMessageId](#openmessageid) ```Int32```
* [OpenTriggeringEvent](#opentriggeringevent) ```object```
    * [ComponentCode](#opentriggeringeventcomponentcode) ```string```
    * [EventName](#opentriggeringeventeventname) ```string```
    * [EventDateTime](#opentriggeringeventeventdatetime) ```string```
    * [Data](#opentriggeringeventdata) ```string```
* [CloseTriggeringEvent](#closetriggeringevent) ```object```
    * [ComponentCode](#closetriggeringeventcomponentcode) ```string```
    * [EventName](#closetriggeringeventeventname) ```string```
    * [EventDateTime](#closetriggeringeventeventdatetime) ```string```
    * [Data](#closetriggeringeventdata) ```string```    
* [ReportOnExpectedState](#reportonexpectedstate) ```byte```

### MessageType
```string``` = "ComponentCycleMessage"
### Spec
```string``` = "1.2.3.2"
### DeviceId
```string``` 
### MessageId
```Int32```
### ComponentCode 
```string```

### CycleState
```byte```

Possible values:

  1 – Open

  2 - Close

  3 – Open Close

### CycleIdentifier 
```string```

Used to reconcile two separate open and close messages where a device is unable to track the OpenMessageId (see note 2). Must be uniquely identifiable using a [Device,CycleIdentifier] key (suggest using a GUID). The CycleIdentifier must be put in *both* messages i.e. the Open (CycleState=1) and Close (CycleState=2).

### OpenDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### CloseDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### OpenMessageId
```Int32```

Required where CycleState=2 and CycleIdentifier is not used. A component cycle can be sent in two separate messages, one where CycleState=1 and another where CycleState=2. When two messages are sent the closing message needs to contain the MessageId of the open message, so that the correct cycle is closed off. If an open cycle with the OpenMessageId cannot be found server-side, any open cycles for that component will be closed. A cycle can be closed (CycleState=2) without an open (by not setting OpenMessageId), which will set the component to a (known) off state.

### OpenTriggeringEvent
```object```

Event data can be sent with the cycle if necessary. For example, an alert cycle could be triggered by a high voltage reading.

### OpenTriggeringEvent/ComponentCode 
```string```

If ComponentCode is not contained in the event data. An event will be created with the ComponentCode of the cycle.
### OpenTriggeringEvent/EventName
```string```
### OpenTriggeringEvent/EventDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### OpenTriggeringEvent/Data
```string```

Arbitrary data that the device may send up with the message. Not intended to be parsed by message processing

### CloseTriggeringEvent
```object```

Event data can be sent with the cycle if necessary. For example, an alert cycle could be triggered by a high voltage reading.

### CloseTriggeringEvent/ComponentCode 
```string```

If ComponentCode is not contained in the event data. An event will be created with the ComponentCode of the cycle.
### CloseTriggeringEvent/EventName
```string```
### CloseTriggeringEvent/EventDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### CloseTriggeringEvent/Data
```string```

Arbitrary data that the device may send up with the message. Not intended to be parsed by message processing

### ReportOnExpectedState
 ```byte``` optional. Default=1

If set to 1, when a CycleState or 1 or 2 (either an open or close), if the server-side state does not match (i.e. when CycleState =1 and stored state is already open, or CycleState =2 and stored state is already closed), an Unexpected State Message is generated.

## Samples
### Open only sample
```JSON
{
  "MessageType": "ComponentCycleMessage",
  "Spec": "1.2.3.2",
  "DeviceId": "P00122",
  "MessageId": 984,
  "ComponentCode": "Boom",
  "CycleState": 1,
  "OpenDateTime": "2016-03-11T18:50:48Z",
  "OpenTriggeringEvent": {
      "ComponentCode": "EStart",
      "EventName": "On()",
      "EventDateTime": "2016-03-11T18:49:48Z",
      "Data": "A456789"
  }
}
```
### Close only sample
```JSON
{
  "MessageType": "ComponentCycleMessage",
  "Spec": "1.2.3.2",
  "DeviceId": "P00122",
  "MessageId": 1055,
  "ComponentCode": "Boom",
  "CycleState": 2,
  "CloseDateTime": "2016-03-11T19:50:48Z",
  "OpenMessageId": 984
}
```
### Open and Close Sample
```JSON
{
  "MessageType": "ComponentCycleMessage",
  "Spec": "1.2.3.2",
  "DeviceId": "P00122",
  "MessageId": 1095,
  "ComponentCode": "Motor",
  "CycleState": 3,
  "OpenDateTime": "2016-03-11T18:43:22Z",
  "CloseDateTime": "2016-03-11T19:50:48Z"
}
```

## Server-side validations
1.	[ComponentCode](#componentcode): Required
2.	[CycleState](#cyclestate) in [1,2,3]. Required.
3.	If [CycleState](#cyclestate) = 1
    1. [OpenDateTime](#opendatetime):  Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
4.	 If [CycleState](#cyclestate) = 2
    1. [CloseDateTime](#closedatetime):  Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    2. If [CycleIdentifier](#cycleidentifier) is null: OpenMessageId: Required.
5.	If [CycleState](#cyclestate) = 3
    1. [OpenDateTime](#opendatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    2. [CloseDateTime](#closedatetime):  Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
6.	If [OpenTriggeringEvent](#opentriggeringevent) not null
    1. [EventName](#opentriggeringeventeventname): Required.
    2. [EventDateTime](#opentriggeringeventeventdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    3. [CycleState](#cyclestate) in [1,3]
7.	If [CloseTriggeringEvent](#closetriggeringevent) not null
    1. [EventName](#closetriggeringeventeventname): Required.
    2. [EventDateTime](#closetriggeringeventeventdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    3. [CycleState](#cyclestate) in [2,3]
