# Entity Tag Message
## Usage
Tags an entity in the server-side digital twin. Usually created server-side but can be created on devices. Used for non-process features (processes are in the component cycle).

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [Entity](#entity) ```string```
* [SetTags](#settags) ```string[]```
* [ClearTags](#cleartags) ```string[]```
* [Note](#note) ```string```

### MessageType
```string``` = "EntityTagMessage"
### Spec
```string``` = "1.2.3.0"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### Entity
```string``` 

Example entities are: Customer, Thing, Device

### SetTags
```string[]```

Tags must be either set or cleared. Either one can have a value, but both cannot be null.

### ClearTags
```string[]```

Tags must be either set or cleared. Either one can have a value, but both cannot be null.

### Note
```string``` 

Optional

## Sample
```JSON
{
  "MessageType": "EntityTagMessage",
  "Spec": "1.2.3.0",
  "DeviceId": "C000112",
  "MessageId": 501,
  "Entity": "Device",
  "DateTime": "2017-03-12T12:40:42Z",
  "SetTags": [ "Installed", "Calibrated" ]
}

```

## Server-side validations
1. [Entity](#entity): Required
2. [DateTime](#datetime): Reuqired. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
3. [SetTags](#settags) or [ClearTags](#cleartags): Required. Either one can be set, but both cannot be null.

