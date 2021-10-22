# Debug State Message

## Usage
Used to send a command to the device to get it into a known debugging state that may be useful for understanding problems. A changed debug state could send data more freqeuntly, keep a modem turned on, increase logging verbosity, etc.

## Format

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [CreatedDateTime](#createddatetime) ```string```
* [DebugState](#debugstate) ```byte```

### MessageType
```string``` = "DebugStateMessage"

### Spec
```string``` = "1.2.3.1"

### DeviceId
```string``` 

### CreatedDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### DebugState
```byte```

Default = 0 – Not debugging. 1+ platform-specific debug states.

## Sample
```JSON
{
  "DeviceId": "AF000012",
  "Spec": "1.2.3.1",
  "MessageType": "DebugStateMessage",
  "CreatedDateTime": "2016-03-12T12:40:42Z",
  "DebugState": 3
}

```