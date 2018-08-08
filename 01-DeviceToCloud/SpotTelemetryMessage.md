# Spot Telemetry Message
## Usage
The Spot Telemetry Message is the most basic telemetry structure. It records a sensor value at a specific datetime. Component codes are required so as not to land up with meaningless sensor values that are difficult to correlate with other data in downstream processing. Units of measurement are included so that the measurement is clear for downstream processing.

Spot Telemetry suffers from a potential problem that where the measured environment is noisy, or has a non-linear pattern (e.g. AC voltage), the frequency at which spot telemetry is sent could yield meaningless results. Where there may be significant fluctuation over the sampling frequency, consider using Interval Telemetry instead. 
## Format
JSON object with the following structure:
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [MeasurementDateTime](#measurementdatetime) ```string```
* ComponentMeasurements ```object[]```
    * [ComponentCode](#componentmeasurementscomponentcode) ```string``` 
    * [MeasureDateTime](#componentmeasurementsmeasuredatetime) ```string``` 
    * [Measurements](#componentmeasurementsmeasurements) ```object[]```
        * [Key](#componentmeasurementsmeasurementskey) ```string``` 
        * [UnitOfMeasure](#componentmeasurementsmeasurementsunitofmeasure) ```string``` 
        * [Value](#componentmeasurementsmeasurementsvalue) ```string``` 
* [NominalComponentMeasurements](#nominalcomponentmeasurements) ```object[]```
    * [ComponentCode](#nominalcomponentmeasurementscomponentcode) ```string``` 
        

### MessageType
```string``` = "SpotTelemetryMessage"
### Spec
```string``` = "1.1.0.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### MeasurementDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### ComponentMeasurements/ComponentCode 
```string```
Component only needs to match component model if UnitOfMeasure is not populated
### ComponentMeasurements/MeasureDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
Optional and is only used when the datetime of the measurement differs from the overall spot telemetry MeasurementDateTime.
### ComponentMeasurements/Measurements
The list of measurements allows for measurement of different units for a particular sensor. For example, resistance (ohm) and the derived temperature (K). This is a useful aid in the diagnostics of sensor calibration.
### ComponentMeasurements/Measurements/Key
```string``` 
### ComponentMeasurements/Measurements/UnitOfMeasure
```string```

UnitOfMeasure is optional if component model contains UnitOfMeasure.
### ComponentMeasurements/Measurements/Value
```string``` 
### NominalComponentMeasurements
If components are in nominal range, based on settings, component names are listed. For example, if the nominal operating range is 240V ± 10V, any values recorded in the range will not be detailed, and can be recorded as nominal. This is useful to reduce the amount of unnecessary data sent.
### NominalComponentMeasurements/ComponentCode
```string``` 
## Sample
```JSON
{
  "DeviceId": "AX000002",
  "Spec": "1.1.0.0",
  "MessageType": "SpotTelemetryMessage",
  "MessageId": 0,
  "MeasurementDateTime": "2016-11-03T11:20:43Z",
  "NominalComponentMeasurements": [ "P2", "V12" ],
  "ComponentMeasurements": [
    {
      "ComponentCode": "P2",
      "MeasureDateTime": "2016-11-03T11:20:43Z",
      "Measurements": [
        {
          "Key": "Condense",
          "UnitOfMeasure": "Bar",
          "Value": "0.397775416312299"
        }
      ]
    },
    {
      "ComponentCode": "PT2 Head",
      "MeasureDateTime": "2016-11-03T11:20:40Z",
      "Measurements": [
        {
          "Key": "T",
          "UnitOfMeasure": "K",
          "Value": "0"
        },
        {
          "Key": "R",
          "UnitOfMeasure": "Ohm",
          "Value": "0"
        }
      ]
    }
  ]
}
```
## Server-side validations
1.	[MeasureDateTime](#componentmeasurementsmeasuredatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation)
2.	ComponentMeasurements can only be empty if NominalComponentMeasurements contains data.
3.	If ComponentMeasurements exists:
    1.	[ComponentCode](#componentmeasurementscomponentcode): Required if any [UnitOfMeasure](#componentmeasurementsmeasurementsunitofmeasure) in Measurements is null
    2.	[MeasureDateTime](#componentmeasurementsmeasuredatetime) : [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    3.	Measurements: Required. List cannot be empty.
        1.	[Key](#componentmeasurementsmeasurementskey): Required.
        2.	[Value](#componentmeasurementsmeasurementsvalue): Required.
