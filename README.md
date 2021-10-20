# Field Connect Data Standard
Field Connect Data standard is a schema for the structuring of data that sent to and from IoT devices. The Field Connect Data Standard is not a protocol. Any protocol, such as AMQP, MQTT or HTTP can be used. It is also not an encoding format. The initial implementations and samples refer to JSON for encoding, but other encoding that supports complex structures, such as Avro can be used.

## Origins
The Field Connect Data Standard came about from our frustration, as server-side developers, with the variety of ways that data was being sent to us. Sometimes it was a well thought-through binary structure but often the structure of the data was up to the whims of embedded software developers that had to send us data, how much they cared when the requirement came to their desk, and what structures they already had in place.
This led to a lot of server-side effort to transform incoming data into something more usable, which led to the expectation to get data into the best format possible at the point of origin – namely the device.

## Objectives
 * Since device-side and server-side developers are frequently in different teams or organisations blaming one or the other for decoding problems is a cause for conflict or delays. A well-defined specification that is human readable and independently verifiable message payload was needed to reduce friction.
 * Because IoT data is expected to be stored for a long time and analysed in the distant future, a specification was needed that would:
   * Reduce the need for downstream cold analytics processes to put too much effort into transformation.
   * Be as understandable as possible for an analytics data engineer without having to understand much of the origin context.
   * Not drift too much over time as application features are added.
 * The specification should appeal to, and make sense to, engineers. Hardware engineers, embedded software engineers, server-aide developers, and specialist product engineers.

## Implementation
Some basic points about the implementation that support the objectives.
 * Uses an object-oriented schema that, at least in this implementation, considers JSON as the primary encoding format.
 * Is implemented to be human-readable. This has the negative side-effect of field names being verbose.
 * While being considerate of data types, is not overly restrictive. With JSON as an encoding format, there is no difference between an Int16 and an Int32.
 * Uses a restrictive ISO8601 date format as a string. This is to try and reduce datetime decoding problems.
 * Allows for a string-based encoding format (such as JSON) to be (gzip) compressed.
 * Makes use of common fields. This allows for extensibility and server-side processes to handle messages in a generic way within the processing pipeline.
 * Assumes that each device has a unique identifier.
 * Assumes that the device can incrementally number messages that are generated on the device. This may be important and useful for server-side processes.
 * Assumes that the device knows what the current UTC time is.
 * Encourages the use of standard units of measure and properties that are recognisable to engineers.

## Bias 
The Field Connect Data Standard has its roots in making ‘dumb machines smarter’. The bias therefore is more towards individual smart 'things' that are industrial in nature. Some areas that have been explicitly excluded, so far, include:
 * Consumer devices. Particularly those that have complex UIs or ones that collect significant personal data.
 * The component and component cycle structures provide enough for basic processes the Field Connect Data Standard does to include a model for complex industrial processes.

## Getting started
Most of the specification relates to device-to-cloud telemetry data. Each message type has detail on the schema and an example, which should be self explanatory. Look at the [Common Fields](./01-DeviceToCloud/CommonFields.md) for an understanding of the common fields. Follow that up with looking at a simple message, like an [EventMessage](./01-DeviceToCloud/EventMessage.md), and a complex message, such as [IntervalTelemetryMessage](./01-DeviceToCloud/IntervalTelemetryMessage.md) to see how a range of messages are implemented.

## Sponsor
Work on the Field Connect Data Standard is sponsored by [EdgeMethods](http://edgemethods.com). EdgeMethods is a UK-based IoT products and services company that focusses on building IoT solutions on the Microsoft IoT platform.

## Contact
Please use github issues with specific usage questions. For general enquiries contact simon.munro (at) edgemethods.com.

## Examples

### EventMessage
The EventMessage is the most basic message to record event data:

```JSON
{
  "MessageType": "EventMessage",
  "Spec": "1.2.3.1",
  "DeviceId": "ProtoSaw",
  "MessageId": "1408",
  "EventDateTime": "2018-05-22T20:35:44+00:00",
  "ComponentCode": "Machine",
  "Data": "Off",
  "EventName": "Turned On"
}
```
### IntervalTelemetryMessage
The IntervalTelemetryMessage is used to record measurements in an interval. An interval implies more than one spot measurement being possible, so focusses on the statistical nature of data that is recorded.

```JSON
{
  "MessageType": "IntervalTelemetryMessage",
  "Spec": "1.2.3.1",
  "DeviceId": "ProtoSaw",
  "MessageId": "140973",
  "Interval": {
    "FromDateTime": "2018-05-18T10:23:19Z",
    "ToDateTime": "2018-05-18T10:23:24Z"
  },
  "ComponentMeasurements": [
    {
      "ComponentCode": "Accel",
      "Measurements": [
        {
          "SampleCount": "220",
          "Key": "X",
          "Functions": [
            {
              "Function": "max",
              "Value": "0.1556"
            },
            {
              "Function": "min",
              "Value": "0.1245"
            }
          ]
        },
        {
          "SampleCount": "220",
          "Key": "Y",
          "Functions": [
            {
              "Function": "max",
              "Value": "-0.0437"
            },
            {
              "Function": "min",
              "Value": "-0.0437"
            }
          ]
        },
        {
          "SampleCount": "220",
          "Key": "Z",
          "Functions": [
            {
              "Function": "max",
              "Value": "1.0338"
            },
            {
              "Function": "min",
              "Value": "1.0015"
            }
          ]
        }
      ]
    }
  ],
  "Origin": 2
}
```