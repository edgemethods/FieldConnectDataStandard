# System Test Message
## Usage
For testing the overall system, including connectivity, message processing, digital twin meta data, storage, etc. Can be sent by individual devices as needed, or as part of a virtual device that acts as a system hearbeat.

For sending data about device-side tests, rather use a [Basic Diagnostic Message](BasicDiagnosticMessage.md).

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [ThingIdentifier](#thingidentifier) ```string```
* [TestPurpose](#testpurpose) ```string```
* [TestData](#testprocess) ```string```

### MessageType
```string``` = "SystemTestMessage"
### Spec
```string``` = "1.2.2.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### ThingIdentifier
```string```
### TestPurpose
```string```

Required.
### TestData
```string```

Optional.
## Sample
```JSON
{
  "MessageType": "SystemTestMessage",
  "Spec": "1.2.2.0",
  "DeviceId": "AF-DEV-001",
  "DateTime": "2020-03-12T12:40:42Z",
  "ThingIdentifier": "AF000002",
  "TestPurpose": "FullPipelineTest"
}
```
## Server-side validations
1.	[DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.  [TestPurpose](#testpurpose): Required.
