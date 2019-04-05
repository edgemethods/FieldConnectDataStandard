# Calibration Message
## Usage
Devices can set calibration values that may be used in downstream analytics. Calibration can be done through a specific process, such as at manufacture, or during operation, such as at startup. For example, an accelerometer sensor will never be fitted perfectly level and will need to send the at-rest values across three axes at startup.

* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [CalibrationDateTime](#calibrationdatetime) ```string```
* [CalibrationProcess](#calibrationprocess) ```string```
* [ComponentCalibrations](#componentcalibrations) ```object[]```
    * [ComponentCode](#componentcalibrationscomponentcode) ```string``` 
    * [Calibrations](#componentcalibrationscalibrations) ```object[]```
        * [Key](#componentcalibrationscalibrationskey) ```string``` 
        * [UnitOfMeasure](#componentcalibrationscalibrationsunitofmeasure) ```string``` 
        * [Value](#componentcalibrationscalibrationsvalue) ```string``` 

### MessageType
```string``` = "CalibrationMessage"
### Spec
```string``` = "1.1.1.3"
### DeviceId
```string``` 
### MessageId
```Int32```
### CalibrationDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### CalibrationProcess
```string``` 

Optional. Used to record the device process in which the calibtration has been done.

### ComponentCalibrations
```object[]```

Required

### ComponentCalibrations/ComponentCode 
```string```

Required

### ComponentCalibrations/Calibrations
```object[]```

### ComponentCalibrations/Calibrations/Key
```string``` 

Required

### ComponentCalibrations/Calibrations/UnitOfMeasure
```string``` 

### ComponentCalibrations/Calibrations/Value
```string``` 

Required

## Sample
```JSON
{
  "DeviceId": "AX000002",
  "Spec": "1.1.1.3",
  "MessageType": "CalibrationMessage",
  "MessageId": 120,
  "CalibrationDateTime": "2016-11-03T11:20:43Z",
  "CalibrationProcess": "Startup",
  "ComponentCalibrations": [
    {
      "ComponentCode": "P2",
      "Calibrations": [
        {
          "Key": "X",
          "UnitOfMeasure": "g",
          "Value": "0.8"
        },
        {
          "Key": "Y",
          "UnitOfMeasure": "g",
          "Value": "0.01"
        },
        {
          "Key": "Z",
          "UnitOfMeasure": "g",
          "Value": "0.3"
        }
      ]
    }
  ]
}
```
## Server-side validations
1.	[CalibrationDateTime](#calibrationdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation)
2.	[ComponentCalibrations](#componentcalibrations): Required
    1.	[ComponentCode](#componentcalibrationscomponentcode): Required. List cannot be empty.
    2.	[Calibrations](#componentcalibrationscalibrations): Required. List cannot be empty.
        1.	[Key](#componentcalibrationscalibrationskey): Required.
        2.	[Value](#componentcalibrationscalibrationsvalue): Required.