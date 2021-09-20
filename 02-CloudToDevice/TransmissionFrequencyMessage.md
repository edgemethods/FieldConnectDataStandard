# Transmission Frequency Message

## Usage
Used to instruct the device to change the frequency that data is transmitted.

## Format

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [CreatedDateTime](#createddatetime) ```string```
* [TransmissionType](#logdatetimefrom) ```string```
* [Frequency](#frequency) ```int32```


### MessageType
```string``` = "TransmissionFrequencyMessage"

### Spec
```string``` = "1.2.3.0"

### DeviceId
```string``` 

### TransmissionType
```string``` 

Used to set different frequencies for different types of transmissions. Eg 'Primary', 'Aggregate', etc.

### Frequency
```int32``` 

Frequency of the transmission in seconds

## Sample
```JSON
{
  "DeviceId": "AF000012",
  "Spec": "1.2.3.0",
  "MessageType": "TransmissionFrequencyMessage",
  "CreatedDateTime": "2018-03-12T12:40:42Z",
  "TransmissionType": "Primary",
  "Frequency": 30,
}

```