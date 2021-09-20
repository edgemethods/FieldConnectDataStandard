# Remote Instruction Message

## Usage
Should be used sparingly as the lack of structure in the data is prone to faults. Rather use remote method calling that may exist on the messaging platform, or create more specific command messages.

## Format

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [CreatedDateTime](#createddatetime) ```string```
* [Instruction](#instruction) ```string```
* [Data](#data) ```string```


### MessageType
```string``` = "RemoteInstructionMessage"

### Spec
```string``` = "1.2.3.0"

### DeviceId
```string``` 

### CreatedDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### Instruction
```string```

### Data
```string```

## Sample
```JSON
{
  "DeviceId": "AF000012",
  "Spec": "1.2.3.0",
  "MessageType": "RemoteInstructionMessage",
  "CreatedDateTime": "2016-03-12T12:40:42Z",
  "Instruction": "Reset"
}

```