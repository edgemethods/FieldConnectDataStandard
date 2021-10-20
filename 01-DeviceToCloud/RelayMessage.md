# Relay Message
## Usage
Relay messages are used where data from an existing data structure, or data that is not telemetry, or data that is from a different standard, needs to be sent via the IoT channel and appropriately validated and stored.

Relay messages should be used sparingly, they’re effectively better-structured blobs that retain the disadvantage of needing specialised processing, so where possible, telemetry data should be reworked to fit to the data standard.

Relay messages contain arbitrary (JSON) data that has additonal data standard-centric fields on that allow for message processing. Once basic validation is done, the message is forwarded to storage *as-is*, so the other fields and structures can be anything.

## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [DateTime](#datetime) ```string```
* [ThingIdentifier](#thingidentifier) ```string```
* [RelayTag](#relaytag) ```string```
* *\<any other properties\>*

### MessageType
```string``` = "RelayMessage"
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
### RelayTag
```string```

Required. Used for describe the schema or type of message.
## Sample
```JSON
{
  "MessageType": "RelayMessage",
  "Spec": "1.2.3.1",
  "DeviceId": "AF-DEV-001",
  "DateTime": "2020-03-12T12:40:42Z",
  "ThingIdentifier": "AF000002",
  "RelayTag": "RawAdcValues",
  "ADCData": "0 0 0 0 0 190 234 267 232 243 268 256 279 272",
  "ADC0Preset": "00-D1",
  "ADC1Preset": "3E-4F"
}
```
## Server-side validations
1.	[DateTime](#datetime): Required. [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2.  [RelayTag](#relaytag): Required