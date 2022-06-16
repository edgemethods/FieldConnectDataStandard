# Alert Message
## Usage
Alert messages are sent when the device detects an abnormal or dangerous condition that, at the very least, shuts down equipment or warns the operator. Where the condition is not abnormal or dangerous, consider using an Event Message instead.

The [ActionsTaken] structure is useful for recording what the device/thing/operator did in real time in response to the alert. [ResponseRequired] is used to mark the message for further server-side processing, but this should not be relied upon to effect real-time control.
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [AlertDateTime](#alertdatetime) ```string```
* [AlertName](#alertname) ```string```
* [AlertMessage](#alertmessage) ```string```
* [AlertData](#alertdata) ```string```
* [ComponentCode](#componentcode) ```string```
* [Severity](#severity) ```byte```
* [ResponseRequired](#responserequired) ```string```
* [ActionsTaken](#ActionsTaken) ```object[]```
    * [Action](#action) ```string```
    * [ActionDateTime](#actiondateTime) ```string``` 

### MessageType
```string``` = "AlertMessage"
### Spec
```string``` = "1.2.3.2"
### DeviceId
```string``` 
### MessageId
```Int32```
### AlertDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### AlertName
```string```
### AlertMessage
```string``` 

Human-readable message 
### AlertData
```string``` 

Data that can be used in diagnosis or response. Binary data is permitted, but must be UTF8 encoded.

### ComponentCode 
```string```
### Severity
```byte```

Zero-ordered number where 0 is the most critical.
### ResponseRequired
```byte```

The device may have resolved the error, and no response is required from the service, in which case it is a notification of a resolved alert. 0 – No response required. 1+ – Response required with possible response code.

### ActionsTaken
List of actions that may have already taken place on the device in response to the alert

## Sample
```JSON
{
  "DeviceId": "AF000012",
  "Spec": "1.2.3.2",
  "MessageType": "AlertMessage",
  "MessageId": 988,
  "AlertDateTime": "2016-03-12T12:40:42Z",
  "AlertName": "CurrentExceeded",
  "AlertMessage": "Current on A1 exceeds threshold of 25A",
  "AlertData": "28.2A",
  "ComponentCode": "RefrigeratorBase",
  "Severity": 3,
  "ResponseRequired": 0,
  "ActionsTaken": [
        {
          "Action": "Halt startup process",
          "ActionDateTime": "2016-03-12T12:40:52Z"
        },
        {
          "Action": "Display error on control panel",
          "ActionDateTime": "2016-03-12T12:41:52Z"
        }
      ]
}

```
## Server-side validations
1.	[AlertDateTime](#alertdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.	[AlertMessage](#alertmessage): Required.
3.	[Severity](#severity): Required.
4.	[ResponseRequired](#responserequired). If exists, can only be 0 or 1.
5.	If [ActionsTaken](#ActionsTaken) exists
    1. [Action](#action): Required
    2. [ActionDateTime](#actiondateTime): [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
