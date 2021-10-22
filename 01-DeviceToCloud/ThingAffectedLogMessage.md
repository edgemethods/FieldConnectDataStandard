# Thing Affected Log Message
## Usage
Used to record *interesting events* and activities that may be made against the digital twin of a thing. It is used to record known activities that are not obvious (although they may be derivable) from telemetry or state changes. Consumers of the digital twin should be able to have a single and consolidated record of important updates and data changes.

Most of the time data changes that affect the thing are server-side activities, through APIs or batch jobs. Embedded software implementers may only use this message in very few cases where devices will know about impactful changes, such as when configuration changes are sent through. Even then, since the ThingIdentifier is required and devices generally do not know what thing they are fitted to, this message will seldom be sent with an [Origin](../01-DeviceToCloud/CommonFields.md#origin) of 1 or 2.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [ThingIdentifier](#thingidentifier) ```string```
* [Source](#source) ```string```
* [Processor](#processor) ```string```
* [Summary](#summary) ```string```
* [Adjustment](#Adjustment) ```string```
* [Upn](#upn) ```string```
* [Tags](#tags) ```string[]```

### MessageType
```string``` = "ThingAffectedLogMessage"
### Spec
```string``` = "1.2.3.1"
### DeviceId
```string``` 
### MessageId
```Int32```
### DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```
### ThingIdentifier
```string``` 

Because the affected log is against thing, the ThingIdentifier is required.
### Source
```string```

Friendly name for the application, source event, or source system that triggered the change. e.g. ComponentStructureMessage, Asgard
### Processor
```string```

Details on the specific processor that transacted the change. Could be a function name, or app url.
### Summary
```string```

Human-readable summary of the change. It is important that the user can understand the upstream reason why the thing was affected.
### Adjustment
```string```

Used to hold data about the change that allows it to be detailed or rolled back. Could be a JSON fragment of the before state of an object, or a reference to a SQL, gremlin or other query. Does not need to be humand-readable.

### Upn
```string```

When things are changed by users in apps, it is encouraged that upns are recorded so that people can be approached to understand why a thing was changed.
### Tags
```string[]```

Used to be able to filter potentially long lists of affected log messages.
## Sample
```JSON
{
  "MessageType": "ThingAffectedLogMessage",
  "Spec": "1.2.3.1",
  "DeviceId": "AF-DEV-001",
  "DateTime": "2020-03-12T12:40:42Z",
  "ThingIdentifier": "AF000002",
  "Source": "ComponentStructureMessage",
  "Processor": "https://em-actions-dev-01.azurewebsites.net",
  "Summary": "Received ComponentStructure message resulted in fitment to deviceId AF-DEV-001",
  "Tags": ["Actions"]
}
```
## Server-side validations
1. [ThingIdentifier](#thingidentifier): Required.
2. [DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
3. [Summary](#summary): Required
4. Either [Upn](#upn) or [Processor](#processor) need to be non-null