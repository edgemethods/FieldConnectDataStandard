# Current Settings Message
## Usage
Most edge devices will have some configuration data or settings stored on the device. The current settings message is a <key,value> list of individual settings. 

The Current Settings Message can be used as needed – where configuration has changed, in response to an instruction, or according to some frequency – or not at all, it settings are able to be read and set by a device twin mechanism that may exist on the IoT platform. It is likely, however, that use may be made of it in legacy environments.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [Settings](#settings) ```object[]```
    * [Key](#settingskey) ```string```
    * [Value](#settingsvalue) ```string``` 

### MessageType
```string``` = "CurrentSettingsMessage"
### Spec
```string``` = "1.1.1.4"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Settings
```object[]```
### Settings/Key
```string```

### Settings/Value
```string```

Settings values, including binary values, must be UTF8 encoded.

## Sample
```JSON
{
  "MessageType": "CurrentSettingsMessage",
  "Spec": "1.1.1.4",
  "DeviceId": "OI000002",
  "MessageId": 101,
  "DateTime": "2016-03-12T12:40:42Z",
  "Settings": [
    {
      "Key": "TelemetrySendFrequency",
      "Value": "1Hz"
    },
    {
      "Key": "LogLevel",
      "Value": "1"
    }
  ]
}
```

## Server-side validations
1.	[DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.	[Settings](#settings): Required. List cannot be empty.
    1. [Key](#settingskey): Required.
    2. [Value](#settingsvalue): Required.

