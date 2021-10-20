# Interval Telemetry Message
## Usage
The Interval Telemetry Message is used to send telemetry on measurements that are sensitive to misinterpretation because of a long sampling frequency.

The crucial data is contained within the [Functions] structure that is a key-value list of the statistical function executed against the sample. There are no agreed abbreviations to statistical functions, so be careful that function names are consistent and meaningful (e.g. avg, ave, average). A rule of thumb is that that [Function] + [Key] should be meaningful, such as[Avg] [Voltage], [Total] [Movement], [First] [Position].
## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* Interval ```object```
    * [FromDateTime](#intervalfromdatetime) ```string```
    * [ToDateTime](#intervaltodatetime) ```string```
* ComponentMeasurements ```object[]```
    * [ComponentCode](#componentmeasurementscomponentcode) ```string``` 
    * [Measurements](#componentmeasurementsmeasurements) ```object[]```
        * [Key](#componentmeasurementsmeasurementskey) ```string``` 
        * [UnitOfMeasure](#componentmeasurementsmeasurementsunitofmeasure) ```string``` 
        * [SampleCount](#componentmeasurementsmeasurementssamplecount) ```Int16```
        * [Functions](#componentmeasurementsmeasurementsfunctions) ```object[]```
            * [Function](#componentmeasurementsmeasurementsfunctionsfunction) ```string``` 
            * [Value](#componentmeasurementsmeasurementsfunctionsvalue) ```string``` 
* [NominalComponentMeasurements](#nominalcomponentmeasurements) ```object[]```
    * [ComponentCode](#nominalcomponentmeasurementscomponentcode) ```string``` 

### MessageType
```string``` = "IntervalTelemetryMessage"
### Spec
```string``` = "1.2.3.1"
### DeviceId
```string``` 
### MessageId
```Int32```
### Interval/FromDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Interval/ToDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### ComponentMeasurements/ComponentCode
```string```

Component only needs to match component model if UnitOfMeasure is not populated
### ComponentMeasurements/Measurements
The list of measurements allows for measurement of different units for a particular sensor. For example, resistance (ohm) and the derived temperature (K). This is a useful aid in the diagnostics of sensor calibration.
### ComponentMeasurements/Measurements/Key
```string``` 
### ComponentMeasurements/Measurements/UnitOfMeasure
```string```

### ComponentMeasurements/Measurements/SampleCount
```Int16```

UnitOfMeasure is optional if component model contains UnitOfMeasure.
### ComponentMeasurements/Measurements/Functions
Functions are the statistical functions that have been run on the sample. Functions could include max, min, mean, sdev.

### ComponentMeasurements/Measurements/Functions/Function
```string```

### ComponentMeasurements/Measurements/Functions/Value
```string```

### NominalComponentMeasurements
If components are in nominal range, based on settings, component names are listed. For example, if the nominal operating range is 240V ± 10V, any values recorded in the range will not be detailed, and can be recorded as nominal. This is useful to reduce the amount of unnecessary data sent.
### NominalComponentMeasurements/ComponentCode
```string```

## Sample
```JSON
{
  "MessageType": "IntervalTelemetryMessage",
  "Spec": "1.2.3.1",
  "DeviceId": "ProtoSaw",
  "MessageId": "9881",
  "Interval": {
    "FromDateTime": "2018-04-18T00:00:39Z",
    "ToDateTime": "2018-04-18T00:00:44Z"
  },
  "ComponentMeasurements": [
    {
      "ComponentCode": "Accel",
      "Measurements": [
        {
          "SampleCount": "221",
          "Key": "X",
          "Functions": [
            {
              "Function": "max",
              "Value": "0.1867"
            },
            {
              "Function": "min",
              "Value": "0.1556"
            },
            {
              "Function": "avg",
              "Value": "0.1721"
            },
            {
              "Function": "stdev",
              "Value": "0.0155"
            }
          ]
        },
        {
          "SampleCount": "221",
          "Key": "Y",
          "Functions": [
            {
              "Function": "max",
              "Value": "-0.0437"
            },
            {
              "Function": "min",
              "Value": "-0.0754"
            },
            {
              "Function": "avg",
              "Value": "-0.0656"
            },
            {
              "Function": "stdev",
              "Value": "0.0146"
            }
          ]
        },
        {
          "SampleCount": "221",
          "Key": "Z",
          "Functions": [
            {
              "Function": "max",
              "Value": "1.0338"
            },
            {
              "Function": "min",
              "Value": "1.0015"
            },
            {
              "Function": "avg",
              "Value": "1.0058"
            },
            {
              "Function": "stdev",
              "Value": "0.0109"
            }
          ]
        },
        {
          "SampleCount": "221",
          "Key": "RSS",
          "Functions": [
            {
              "Function": "max",
              "Value": "0.2150"
            },
            {
              "Function": "min",
              "Value": "0.1674"
            },
            {
              "Function": "avg",
              "Value": "0.1964"
            },
            {
              "Function": "stdev",
              "Value": "0.0179"
            }
          ]
        },
        {
          "SampleCount": "221",
          "Key": "NOISE",
          "Functions": [
            {
              "Function": "stdev",
              "Value": "0.0000"
            },
            {
              "Function": "variance",
              "Value": "0.0000"
            },
            {
              "Function": "sum",
              "Value": "0.0000"
            },
            {
              "Function": "avg",
              "Value": "0.0000"
            }
          ]
        }
      ]
    }
  ],
}
```
## Server-side validations
1.	Interval: Required
    1. [FromDateTime](#intervalfromdatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    2. [ToDateTime](#intervaltodatetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
    3. [FromDateTime](#intervalfromdatetime) must be less than ToDateTime. 
2.	ComponentMeasurements can only be empty if [NominalComponentMeasurements](#nominalcomponentmeasurements) contains data.
3.	If ComponentMeasurements exists:
    1. [ComponentCode](#componentmeasurementscomponentcode): Required.
    2. [Measurements](#componentmeasurementsmeasurements): Required. List cannot be empty.
        1. Key: Required.
        2. [Functions](#componentmeasurementsmeasurementsfunctions): Required. List cannot be empty.
            1.	[Function](#componentmeasurementsmeasurementsfunctionsfunction): Required.
            2.	[Value](#componentmeasurementsmeasurementsfunctionsvalue): Required.
