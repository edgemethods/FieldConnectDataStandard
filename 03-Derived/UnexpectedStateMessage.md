# Unexpected State Message
## Usage
Generated server-side when the stored component (cycle) state doesn’t match with the state requested in a ComponentCycleMessage. For example, this message will be generated if an open (CycleState=1), but the component is already in an open state.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [DateTime](#datetime) ```string```
* [ComponentCode](#componentcode) ```string```
* [StoredState](#sourcemessageid) ```string```
* [RequestedCycleState](#sourcemessagetype) ```byte```
* [ComponentCycleMessageId](#componentcyclemessageid) ```Int32```

### MessageType
```string``` = UnexpectedStateMessage
### Spec
```string``` = "1.2.0.1"
### DeviceId
```string``` 
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### ComponentCode
```string``` 
### StoredState
```string```

Possible values:

  "On", "Off", "Fault"
### RequestedCycleState
```byte```

Possible values:

  1 – Open

  2 - Close
  
  3 – Open Close

### ComponentCycleMessageId
```Int32``` 

MessageId of the ComponentCycleMessage

## Sample
```JSON
{
  "MessageType": "UnexpectedStateMessage",
  "Spec": "1.2.0.1",
  "DeviceId": "AC2920002",
  "MessageId": 984,
  "ComponentCode": "HTR",
  "StoredState": "On",
  "RequestedCycleState": 1,
  "ComponentCycleMessageId": 23459
}
```