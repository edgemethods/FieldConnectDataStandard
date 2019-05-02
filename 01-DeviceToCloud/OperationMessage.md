# Operation Message
## Usage
To record that a named human operator has performed an operation on a 'thing'. For example, can be used on devices where a named operator can login to factory equipment (e.g. IPAF code).

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [OperatorCode](#operatorcode) ```string```
* [StartDateTime](#startdatetime) ```string```
* [EndDateTime](#startdatetime) ```string```
* [Task](#task) ```string```

### MessageType
```string``` = "OperationMessage"
### Spec
```string``` = "1.2.0.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### OperatorCode
```string``` 

Should match existing operator that has been setup on server-side systems.
### StartDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### EndDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Task
```string``` 

Optional and can be used to record the specific function, task, process, etc. that the operator used or performed.

## Sample
```JSON
{
  "MessageType": "OperationMessage",
  "Spec": "1.2.0.0",
  "DeviceId": "C000112",
  "MessageId": 401,
  "OperatorCode": "59483A",
  "StartDateTime": "2017-03-12T12:40:42Z",
  "EndDateTime": "2017-03-12T13:23:12Z",
  "Task": "Calibration"
}
```

## Server-side validations
1. [OperatorCode](#operatorcode): Required
2. [StartDateTime](#startdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
3. [EndDateTime](#startdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
4. [StartDateTime](#startdatetime) must be less than [EndDateTime](#startdatetime). 