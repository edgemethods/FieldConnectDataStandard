# DateTime Format
All DateTime fields need to be in a subset of ISO8601, as follows:

```YYYY-MM-DDThh:mm:ss.sssZ```

All DateTimes must be in UTC time (as per the ‘Z’ above)

Where seconds and milliseconds are not required, hh:mm can be used:

```YYYY-MM-DDThh:mmZ```

All DateTime’s require hh:mm and in cases where there is no known time, 00:00 must be used.

Examples:

```2017-05-13T08:48:11Z```

```2017-05-13T23:48:11.123Z```

```2017-05-13T08:48Z```

```2017-05-13T00:00Z```

## Standard DateTime Validation
Unless explicitly stated, DateTime values must be in the past, and within the last year.
