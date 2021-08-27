# Suspect Device Message
## Usage
Generated when a potential fault is detected by server-side processes. Because there is no way to tell the difference between a faulty device and a compromised one, ‘faults’ are regarded as suspicious until they have been correctly resolved.
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [DateTime](#datetime) ```string```
* [Suspector](#suspector) ```string```
* [Reason](#reason) ```string```
### MessageType
```string``` = "SuspectDeviceMessage"
### Spec
```string``` = "1.2.2.0"
### DeviceId
```string``` 
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Suspector
```string```

Can be a process or function name, or a user name if suspicion is picked up manually.
### Reason
```string```

## Sample
```JSON
{
  "MessageType": "SuspectDeviceMessage",
  "Spec": "1.2.2.0",
  "DeviceId": "AC2920002",
  "DateTime": "2018-03-12T12:40:52Z",
  "Suspector": "Gateway/Validation",
  "Reason": "Same message id with different data"
}
```