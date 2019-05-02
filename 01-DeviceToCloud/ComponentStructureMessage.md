# Component Structure Message
## Usage
The list of components attached to a 'thing', is usually administered in the cloud. However, in cases where the components of the thing can change in the field, such as when an additional component is plugged in and detected by a device, the device needs to be able to communicate the change in the connected components.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [UpdateComponentCodeRoot](#updatecomponentcoderoot) ```string``` 
* [Components](#components) ```object[]```
    * [ComponentCode](#componentscomponentcode) ```string```
    * [PartNumber](#componentspartnumber) ```string```
    * [ComponentName](#componentscomponentname) ```string```
    * [SerialNumber](#componentsserialnumber) ```string```
    * [UnitsOfMeasure](#componentsunitsofmeasure) ```object[]```
        * [Key](#componentsunitsofmeasurekey) ```string```
        * [UnitOfMeasure](#componentsunitsofmeasureunitofmeasure) ```string```
    * [Properties](#componentsproperties) ```object[]```
        * [Key](#componentspropertieskey) ```string```
        * [Value](#componentspropertiesvalue) ```string```
    * [Components](#components) ```object[]```

### MessageType
```string``` = "ComponentStructureMessage"
### Spec
```string``` = "1.2.0.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### UpdateComponentCodeRoot
The node in the tree that is is used as the 'root' for updates when partial updates are applied.

If this property is not set, the entire confirguration is updated.

If this property is set, and the component code exists in the tree, the entire 'branch' of the tree is deleted and created from the list in the message.

The UpdateComponentCodeRoot must be the same as the root (and first) item in [Components](#components) list.

### Components
```object[]```

The component list is a hierarchical structure 
### Components/ComponentCode
```string```
### Components/PartNumber
```string```
### Components/ComponentName
```string```
### Components/SerialNumber
```string```
### Components/UnitsOfMeasure
```object[]```

A list of possible units of measure against which telemetry can be sent such as in [SpotTelemetryMessage validation](./SpotTelemetryMessage.md##componentmeasurementsmeasurementsunitofmeasure).
### Components/UnitsOfMeasure/Key
```string```
### Components/UnitsOfMeasure/UnitOfMeasure
```string```
### Components/Properties
```object[]```
### Components/Properties/Key
```string```
### Components/Properties/Value
```string```

## Sample
```JSON
{
  "MessageType": "ComponentStructureMessage",
  "Spec": "1.2.0.0",
  "DeviceId": "AF0002",
  "MessageId": 101,
  "DateTime": "2016-03-12T12:40:42Z",
  "Components": [
    {
      "ComponentCode": "Pump001",
      "PartNumber": "AV-RSU-998-Z",
      "ComponentName": "Pump 1",
      "UnitsOfMeasure": [
        {
          "Key":"Pressure",
          "UnitOfMeasure":"PSI"
        }
      ]
    },
    {
      "ComponentCode": "RefrigeratorBase",
      "ComponentName": "Refrigerator Base",
      "Components": [
          {
            "ComponentCode": "RB-Pump002",
            "ComponentName": "Refrigerator Base Pump 2",
            "SerialNumber": "AF-987EG-0034",
            "UnitsOfMeasure": [
              {
                "Key":"Pressure",
                "UnitOfMeasure":"PSI"
              },
              {
                "Key":"CurrentDraw",
                "UnitOfMeasure":"A"
              }
            ]
          },
          {
            "ComponentCode": "RB-Valve01",
            "ComponentName": "Refrigerator Base Valve 1",
            "Properties": [
              {
                "Key": "Channel",
                "Value": "65"
              },
              {
                "Key": "PowerOnState",
                "Value": "Open"
              }
            ]
          }
      ]
    }
    ]
}
```

## Server-side validations
1.	[DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.	If [Components](#components) not null
    1. [ComponentCode](#componentscomponentcode): Required. Must be unique in the (full tree) component structure for the thing.
    2. [ComponentName](#componentscomponentname): Required.
3. If [Components/UnitsOfMeasure](#componentsunitsofmeasure) not null
    1. [Components/UnitsOfMeasure/Key](#componentsunitsofmeasurekey) Required
    2. [Components/UnitsOfMeasure/UnitOfMeasure](#componentsunitsofmeasureunitofmeasure) Required
4. If [Components/Properties](#componentsproperties) not null
    1. [Components/Properties/Key](#componentspropertieskey) Required
    2. [Components/Properties/Value](#componentspropertiesvalue) Required
5. If [UpdateComponentCodeRoot](#updatecomponentcoderoot) not null
    1. [Components](#components)[0][ComponentCode](#componentscomponentcode) == [UpdateComponentCodeRoot](#updatecomponentcoderoot) (first item in component list must match update root)