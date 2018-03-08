# Machine Location Message
## Usage
For the occasional updating of machine location. Mobile assets that need journeys tracked in detail should not send multiple location messages, but rather a journey message. Can be sent together with an AlertMessage, for location-based responses.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [FixedAtDateTime](#fixedatdatetime) ```string```
* [Latitude](#latitude) ```double```
* [Longitude](#longitude) ```double```
* [Altitude](#altitude) ```double```
* [Heading](#heading) ```double```
* [Speed](#speed) ```double```
* [HorizontalAccuracy](#horizontalaccuracy) ```Int32```
* [ManualLocation](#manualLocation) ```string```

### MessageType
```string``` = "MachineLocationMessage"
### Spec
```string``` = “1.1.0.0”
### DeviceId
```string``` 
### MessageId
```Int32```
### FixedAtDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Latitude
```double``` 
### Longitude
```double``` 
### Altitude
```double``` 
### Heading
```double```

Degrees
### Speed
```double``` 

metres/second
### HorizontalAccuracy
```Int32``` 

Accuracy of the fix in metres. The device should round to nearest metre (to fit in byte), as centimetres of accuracy is irrelevant. Devices may get inaccurate fixes based on GSM cell locations. The threshold for rejection of the fix may be set in server-side configuration parameters, and positions with an inaccurate fix rejected.

metres
### ManualLocation
```string``` 

Can be used to record a building location that is manually captured, in cases where GPS co-ordinates are not available.

## Sample
```JSON
{
  "MessageType": "MachineLocationMessage",
  "Spec": "1.1.0.0",
  "DeviceId": "AB000002",
  "MessageId": 101,
  "DateTime": "2016-03-12T12:40:42Z",
  "Latitude": 53.024712,
  "Longitude": -2.239847,
  "HorizontalAccuracy": 10
}
```

## Server-side validations
1. [FixedAtDateTime](#fixedatdatetime): Required. Standard DateTime validation.
2. Must contain either (Latitude and Longitude) or (ManualLocation).
3. If Latitude and Longitude are provided, it must be a valid GPS coordinate (Latitude (+/–)90°, Longitude (+/–)180°)