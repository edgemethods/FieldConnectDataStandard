# Journey Message
## Usage
Generally used to record when an asset has *made a journey*, as oppposed to a location ping. A *journey* will generally have a begin and an end and will generally refer to starting up/engaging, moving somewhere, and shutting down/disengaging. Journey messages can also be send on a frequent interval or specific time of day as a collection of GPS co-ordinates for that period.


## Format
* [MessageType](#messagetype) ```string```
* [Spec](#spec) ```string```
* [DeviceId](#deviceid) ```string```
* [MessageId](#messageid) ```Int32```
* [PreviousMessageId](#previousmessageid) ```Int32```
* [StartDateTime](#startdatetime) ```string```
* [EndDateTime](#startdatetime) ```string```
* [Distance](#distance) ```Int32```
* [JourneyPositions](#journeypositions)  ```object[]```
    * [DateTime](#journeypositionsdatetime) ```string```
    * [Latitude](#journeypositionslatitude) ```double```
    * [Longitude](#journeypositionslongitude) ```double```
    * [Altitude](#journeypositionsaltitude) ```double```
    * [HorizontalAccuracy](#journeypositionshorizontalaccuracy) ```Int32```
    * [Speed](#journeypositionsspeed) ```Int32```

### MessageType
```string``` = "JourneyMessage"
### Spec
```string``` = "1.2.3.1"
### DeviceId
```string``` 
### MessageId
```Int32```
### PreviousMessageId
```Int32```

Used when a single journey is split across multiple messages. Journeys may be split across multiple messages because limitations on the broker message size may not be enough for long journeys.

For example, if the start of a journey has a MessageId of 1234, which is continued in 1235, the 1235 message will have a PreviousMessageId of 1234
### StartDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

Start and end datetimes can be empty strings, and together indicate the completeness of the journey message. This allows for journeys to be transmitted at intervals, not just when motion stops:
1.	Start not empty and end not empty: Indicates a complete journey in a single message.
2.	Start not empty and end empty: Indicates a journey that has started, but is continued in a further message
3.	Start empty and end not empty: Indicates the completion of a journey started in a previous message.
4.	Start empty and end empty: Indicates an incomplete journey that was started in an earlier message.

### EndDateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

See notes in [StartDateTime](#startdatetime) above.

### Distance
```Int32```

The calculated distance of the journey in metres. It is important that this value is provided by GPS chipset firmware, as calculating distance based on GPS co-ordinates only is inaccurate due to the varying quality of GPS fixes.

For journeys split across multiple messages, the distance should be placed in the last message, where other messages can be null.

### JourneyPositions
```object[]```

For intervals where no GPS fix could be made, simply exclude the interval from the list of positions. For example, a journey may have a start time of 08:00:00 but take 30 seconds to get a fix, and the first position will be at 08:00:30. 

### JourneyPositions/DateTime
```string``` in DateTime Format ```yyyy-MM-ddTHH:mm:ssZ```

### JourneyPositions/Latitude
```double``` 
### JourneyPositions/Longitude
```double``` 
### JourneyPositions/Altitude
```double``` 
### JourneyPositions/Heading
```double```

Degrees
### JourneyPositions/Speed
```double``` 

metres/second
### JourneyPositions/HorizontalAccuracy
```Int32``` 

Accuracy of the fix in metres. The device should round to nearest metre (to fit in byte), as centimetres of accuracy is irrelevant. Devices may get inaccurate fixes based on GSM cell locations. The threshold for rejection of the fix may be set in server-side configuration parameters, and positions with an inaccurate fix rejected.

## Sample
```JSON
{
  "MessageType": "JourneyMessage",
  "Spec": "1.2.3.1",
  "DeviceId": "AB000002",
  "MessageId": 101,
  "StartDateTime": "2016-03-21T13:43:55Z",
  "EndDateTime": "2016-03-21T13:43:56Z",
  "Distance": 55,
  "JourneyPositions": [
        {
            "DateTime": "2016-03-21T13:43:55Z",
            "HorizontalAccuracy": 5,
            "Latitude": 51.557769775390625,
            "Longitude": -0.15323375165462494,
            "Speed": 595
        },
        {
            "DateTime": "2016-03-21T13:43:56Z",
            "HorizontalAccuracy": 5,
            "Latitude": 51.557769775390625,
            "Longitude": -0.15323375165462494,
            "Speed": 595
        }
    ]
}
```

## Server-side validations
1. [StartDateTime](#startdatetime): [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
2. [EndDateTime](#startdatetime): [Standard DateTime validation](../00-UsageNotes/DateTime-Formatting.md#standardddateTimevalidation).
3. If [EndDateTime](#startdatetime) is null (indicates that this is a multi-message journey)
    1. [Distance](#distance): must be null (has not reached end of journey)
4. If [StartDateTime](#startdatetime) is null (indicates that this is a multi-message journey)
    1. [PreviousMessageId](#previousmessageid): Required
4. If [EndDateTime](#startdatetime) is not null (indicates that this is the end of a multi-message journey)
    1. [Distance](#distance): Required
5. [JourneyPositions](#journeypositions): Required. List cannot be empty.
    1. [DateTime](#journeypositionsdatetime): Required
    2. [Latitude](#journeypositionslatitude): Required. Valid for GPS co-ordinate (+/–)90°
    3. [Longitude](#journeypositionslongitude): Required. Valid for GPS co-ordinate (+/–)180°)
    4. [HorizontalAccuracy](#journeypositionshorizontalaccuracy): Required