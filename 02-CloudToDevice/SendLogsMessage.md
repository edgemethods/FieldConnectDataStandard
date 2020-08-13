# Send Logs Message

## Usage
Devices may store log data on the device that is unnecessary or too verbose to collect, but may be useful when diagnosing problems. This message requests that the device send up those detailed logs. The standard does not specify how logs are sent, but most implementations will upload a file and send a [FileUploadMessage](../01-DeviceToCloud/FileUploadMessage.md).

## Format

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [CreatedDateTime](#createddatetime) ```string```
* [LogDateTimeFrom](#logdatetimefrom) ```string```
* [LogDateTimeTo](#logdatetimefrom) ```string```


### MessageType
```string``` = "SendLogsMessage"

### Spec
```string``` = "1.2.0.1"

### DeviceId
```string``` 

### CreatedDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### LogDateTimeFrom
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### LogDateTimeTo
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

## Sample
```JSON
{
  "DeviceId": "AF000012",
  "Spec": "1.2.0.1",
  "MessageType": "SendLogsMessage",
  "CreatedDateTime": "2018-03-12T12:40:42Z",
  "LogDateTimeFrom": "2018-03-12T00:00Z",
  "LogDateTimeTo": "2018-03-13T00:00Z",
}

```