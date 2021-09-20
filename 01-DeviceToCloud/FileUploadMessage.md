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
```string``` = "1.2.3.0"
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

#### Allowable characters
The characters in the filename are limited, at the very least, by URI naming schemes that are available in RFC 1738, RFC 2616, Section 2.2: Basic Rules and RFC 3987. As a device developer, be cognizant of limitations that downstream systems may have in processing filenames that contain characters that may signify something different of that platform, such as the use of forward slash ("/"), which while a valid filename, may be problematic because downstream systems may treat it as part of a storage folder. Any character that needs to be escaped in a URI scheme is likely to cause downstream problems.

#### Unique filenames
This data standard does not set guidance for how files are handled server-side, and some server-side processing may overwrite files with the same name, and others may not. If keeping every file is important, try to name the file uniquely. For example, pre- or suffix the filename with the MessageId or a guid, in order to reduce the likelihood of overwritten or rejected files. This is, however, dependent on how the particular server-side processing handles files. Some server-side processing may have mechanisms in place where multiple files with the same name can be stored.

_We have yet to receive a proposal for a property in the message such as "OverwriteExistingFile":1, to attempt to force a file of the same name (and size?) to be overwritten. If you need such a feature, please raise an issue on github._

## Sample
```JSON
{
  "MessageType": "FileUploadMessage",
  "Spec": "1.2.3.0",
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
