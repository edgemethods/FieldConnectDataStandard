# Basic Diagnostic Message
## Usage
Particularly with embedded software that is still in development or new, it is useful to send a daily ‘heartbeat’ message to the cloud with some basic information so that the general health of the device can be determined. The basic diagnostic should not be used to send events, settings, or telemetry, but is useful if no external event on the machine is going to trigger a message being sent. 

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [Diagnostics](#diagnostics) ```object[]```
    * [Key](#diagnosticskey) ```string```
    * [Value](#diagnosticsvalue) ```string``` 

### MessageType
```string``` = "BasicDiagnosticMessage"
### Spec
```string``` = "1.1.1.3"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Diagnostics
```object[]```
### Diagnostics/Key
```string```

### Diagnostics/Value
```string```

## Sample
```JSON
{
  "MessageType": "BasicDiagnosticMessage",
  "Spec": "1.1.1.3",
  "DeviceId": "AB5489",
  "MessageId": 1091,
  "DateTime": "2016-03-12T12:40:42Z",
  "Diagnostics": [
    {
      "Key": "RemainingChargePercent",
      "Value": "65"
    },
    {
      "Key": "GSM Signal Strength",
      "Value": "-70dB"
    }
  ]
}
```

## Server-side validations
1.	[DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.	[Diagnostics](#diagnostics): Required. List cannot be empty.
    1. [Key](#settingskey): Required.
    2. [Value](#settingsvalue): Required.
