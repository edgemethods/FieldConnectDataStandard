# File Upload Message
## Usage
Devices should not need to upload files, as they should send structured telemetry. There are cases where uploading of files is needed, such as:
1.	Where legacy data needs to be transmitted
2.	Where binary data, such as an image or video, that is larger than what can be handled by the message broker.

While a device can upload a file anywhere, it is important that the chain of trust between the device and the cloud is preserved. The best way to do this is to piggy-back on the message-oriented trust protocol that has been established for all other data. The File Upload Message is part of this chain of trust, where the device can confirm that the file originated on the device.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [Reason](#reason) ```string```
* [StartDateTime](#startdatetime) ```string```
* [EndDateTime](#enddatetime) ```string```
* [FileName](#filename) ```string```

### MessageType
```string``` = "FileUploadMessage"
### Spec
```string``` = "1.2.0.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### Reason
```string```
### StartDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### EndDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### FileName
```string```

When calling the IoT Hub API, set the filename to be prefixed by a path containing the MessageId, for example the file in the example below would be sent to the API as 101/Calib001.txt. This is in order to allow for the same file(name) to be uploaded multiple times.

## Sample
```JSON
{
  "MessageType": "FileUploadMessage",
  "Spec": "1.2.0.0",
  "DeviceId": "AF000002",
  "MessageId": 101,
  "Reason": "Calibration",
  "StartDateTime": "2016-03-12T12:40:42Z",
  "EndDateTime": "2016-03-12T12:40:42Z",
  "FileName": "Calib001.txt"
}
```

## Server-side validations
1.	[StartDateTime](#startdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.	[EndDateTime](#enddatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
3.	[EndDateTime](#enddatetime) must be greater than StartDateTime.
4.	[FileName](#filename): Required.
