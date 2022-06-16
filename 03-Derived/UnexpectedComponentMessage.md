# Unexpected Component Message
## Usage
Because there is a high dependency on ComponentCode, and component structure can change frequently, it may be better to generate messages when this validation fails, rather than failing the entire message. The UnexpectedComponentMessage is therefore generated server-side when strong validation is fails against a ComponentCode.
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [DateTime](#datetime) ```string```
* [ComponentCode](#componentcode) ```string```
* [SourceMessageId](#sourcemessageid) ```string```
* [SourceMessageType](#sourcemessagetype) ```string```
* [Process](#process) ```string```

### MessageType
```string``` = UnexpectedComponentMessage
### Spec
```string``` = "1.2.3.2"
### DeviceId
```string``` 
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### ComponentCode
```string``` 
### SourceMessageId
```string``` 
### SourceMessageType
```string``` 
### Process
```string``` 

## Sample
```JSON
{
  "MessageType": "UnexpectedComponentMessage",
  "Spec": "1.2.3.2",
  "DeviceId": "AC2920002",
  "DateTime": "2017-03-12T12:40:42Z",
  "ComponentCode": "HTR",
  "SourceMessageId": 1234,
  "SourceMessageType": "ComponentCycleMessage",
  "Process": "Actions/ComponentCyclesActor"
}
```