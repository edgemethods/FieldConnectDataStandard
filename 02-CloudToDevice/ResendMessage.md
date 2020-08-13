# Resend Message

## Usage
On devices that store previous messages (or are in a debug state to store data) the server can request that a message gets resent if it is somehow lost during processing.

## Format

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [CreatedDateTime](#createddatetime) ```string```
* [MessageId](#messageid) ```Int32```


### MessageType
```string``` = "ResendMessage"

### Spec
```string``` = "1.2.0.1"

### DeviceId
```string``` 

### CreatedDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### MessageId
```Int32```

Refers to as MessageId that may have been previously sent by the device.

## Sample
```JSON
{
  "DeviceId": "AF000012",
  "Spec": "1.2.0.1",
  "MessageType": "ResendMessage",
  "CreatedDateTime": "2016-03-12T12:40:42Z",
  "MessageId": 1289
}

```