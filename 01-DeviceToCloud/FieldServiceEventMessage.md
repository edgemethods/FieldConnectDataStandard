# Field Service Event Message
## Usage
Used to record a field service event when API or system access to field service tools is not available. These messages will mostly be captured by users, either on the directly on the  device, or via a web app or mobile app. Automated recording of field service events is permissable if the data is meaningful, but consider using an [Event Message](EventMessage.md) or [Alert Message](AlertMessage.md) instead. It may also be desirable to take a feed from server-side field service tools and turn them into Field Service Event Messages, although a more direct integration approach may be preferable.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [ThingIdentifier](#thingidentifier) ```string```
* [ServiceDateTime](#servicedatetime) ```string```
* [ComponentCode](#componentcode) ```string```
* [Upn](#upn) ```string```
* [Source](#source) ```string```
* [Summary](#summary) ```string```
* [ReferenceNumber](#referencenumber) ```string```
* [Tags](#tags) ```string[]```

### MessageType
```string``` = "FieldServiceEventMessage"
### Spec
```string``` = "1.2.3.2"
### DeviceId
```string``` 
### MessageId
```Int32```
### ThingIdentifier
```string``` 

Because FieldServiceEventMessages can be manually captured, the DeviceId may be null, in which case the ThingIdentifier is required.
### ServiceDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

Does not have to be the current clock time, it can be a date in the past when the actual event took place.
### ComponentCode 
```string```

### Upn
```string```

Identity of the user. Required.
### Source
```string```

Friendly name for the application, source event, or source system that triggered the event. e.g. FieldServiceApp, Asgard
### Summary
```string```

Human-readable summary of the field service event. To add information that needs to be parsed by applications, consider using [tags](#tags).
### ReferenceNumber
```string```

Reference number or code provided by the field service tool, such as a case or ticket number.
### Tags
```string[]```

Used to be able to filter or parse messages.
## Sample
```JSON
{
  "MessageType": "FieldServiceEventMessage",
  "Spec": "1.2.3.2",
  "ThingIdentifier": "AF000002",
  "ServiceDateTime": "2020-03-12T12:40:42Z",
  "ComponentCode":"PrimaryPumpAssembly",
  "Upn":"engineer@serviceoptimisation.onmicrosoft.com",
  "Source": "ServicePhoneApp v2.1",
  "Summary": "Pump runs in an intermittent state",
  "ReferenceNumber":"A30567",
  "Tags": ["FirmwareIssue"]
}
```
## Server-side validations
1. [DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2. [Upn](#upn): Required