[Back to index](README.md)

# Working-with-time

## Index
[01.-What is a data series? (01:29)](#what-is-a-data-series)

[01.-Searching with Time (25:36)](#Searching-with-time)

[02.-Formating Time (06:12)](#formating-time)

[03.-Using time commands (09:29)](#using-time-commands)

[04.-Working with time zones (2:43)](#working-with-time-zones)

## What is a data series

Time is one of the most important components to consider when working with data.
We will learn:
 - How to work with time in searches. `earliest=@d`,  `latest=@d`
 - Time base functions (`now()`, `time()`, `strftime()`, `strptime()`)
 - Time commands (`timechart`, `timewrap`)
 - Understand how time zones are represented in the data

[Back to top](#index)


## Searching with Time
What does time mean to Splunk?
When an event is ingested, its timestamp is stored in the `_time` field that is used to implement the event timeLine in the Splunk Web interface. 
The `_time` field is stored with the event in the index **prior** to the search time, along with default fields such as host, source, and source type (also the index name in which it is stored.
Timestamps are expressed in Unix or epoch time (_time = 1619736430) and translated to human-readable time (Thu, 29 Apr 2021 22:47:10 GMT) **during the search** operation process.
All events are sorted by time, thus time is the most efficient filter.

The timestamp displayed in the Time Column of each event is adjusted to the user's local time zone, **As long as the time zone is set** within the account settings.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9c72ff16-da73-40d4-876c-0cb7e6133af2)

### Timeline Mouse actions
The timeline is an overall distribution of the events in relation to the specific time range set for the search.
- Zoom in, Zoom Out.
- Hover to view the event count for a specific time.
- Format the x and y-axis.
- Rearrange the time range with the `click and drag' (acts as a filter without re-running the search).
- and undo with the `deselect` or `zoom to selection` **RUNNING A BRAND NEW SEARCH**
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e0eae503-aeb9-48a9-9630-8200b70461c5)

### Time Range picker
We can control the overall time range for our search with a bit more detail using the time range picker:
We can customize preset options in the menu Settings/user interface/time ranges.

Splunk Enterprise version
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/99b41171-8bc8-4f7f-a71f-0d368e64b7e6)

Splunk Cloud version

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f5bba99e-d155-4361-8c4a-4adb233fb681)

 - real-time search: return results up to the second they are coming in. The benefit of that is that we see data as it's coming into Splunk in real-time. Real-time searches **are resource intensive**. They consume an entire CPU-CORE. They continuously update search results as the events arrive. Multiple real-time searches could impact the overall performance. One alternative is to Schedule a report.
 - ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/158419c6-b536-4ddd-9cec-1873477a6036)

 - Relative time option;
   - earliest time range.
   - latest (now or at a beginning of the current hour)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ba3152ab-7359-46dc-a4b6-dace23d90131)

  - Data Range & date & Tiem range (between, before, since
    ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c48a61e8-63cb-4e44-9b7e-acc612cf284b)
    ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/06bfc863-f795-44a7-a68c-60e68781dd02)

 - Advanced: we can express **time unit abbreviations** which allows us to be even more specific about our time.
 - 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/15c3dcd7-dbc9-49a0-a068-05197a4b7f24)
Please note the absolute times below the field texts.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6576e2e6-6c76-4fdb-9b0a-c83c06b2c5cd)

## Time modifiers

   Time unit abbreviations can also be used within the `earliest` and `latest` time modifiers in our search to override the TimeRange Picker settings.
   Syntax starts with `plus +` or `minus -` to look forward or back in time. Continues with a number (1 is implicit) and a specific time unit, and we can round down to a specific time unit using  `@` symbol
   
#### Time units table
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6a5573b3-4acf-4cb4-9acd-eb9dd1c7d075)

For week days we can use w1(Monday)... w6(Saturday, w6 or w0 (Sunday).


  ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e4fcfc44-cdfb-4925-a5e3-79d288484ff1)
 ### Examples
 For understanding this example let's assume is exactly 9:45 AM on April 1st, 2021.

 |current time |modifier| meaning|
 |-------------|--------|--------|
 |9:45 AM on April 1st, 2021.|-30m@h| `-30m` 30 minutes before ==>  9:15 AM   `@h` rounded down to hours ==> 9:00 AM|
 |9:45 AM on April 1st, 2021.|-h@h| `-h` one hour before ==>  8:45 AM   `@h` rounded down to hours ==> 8:00 AM|
 |9:45 AM on April 1st, 2021.|earliest=-mon@mon latest=@mom| `-mon` one mon before ==> 9:45 AM on march 1 st   `@m` rounded down to mon ==>  9:45 AM on march 1 st .. 00:00 AM April 1st, 2021|
 |9:45 AM on April 1st, 2021.|earliest=-7d@d| `-7d` seven days before ==> 9:45 AM on march 25th   `@d` rounded down to day ==>  00:00 AM on march 25th .. 9:45 AM on April 1st, 2021|
 |9:45 AM on April 1st, 2021.|earliest=@d+3h| `@d` rounded down to day ==>  00:00 AM on march Apro 1st `+3h` plus 3 hours ==> 03:00 .. 9:45 AM on April 1st,201|
 
In this example, the time range picker was settled `-5h@h`, but the search textbox has a restriction to view only the last five minutes `earliest=-5m@m latest=now`
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4cc1e8e6-1a25-44be-93e8-5a9c8e678739)
In this dual specification, the restriction specified in the search textbox has a prevalence. `earliest`and `latest` modifiers have prevalence over time Range picker.

[Time Unit Documentation](https://docs.splunk.com/Documentation/SplunkCloud/9.0.2209/Search/Specifytimemodifiersinyoursearch)
## Default Time fields
There are a set of fields that are available in most cases for controlling the time of our searches. All begin with `date_` prefix followed by a specific unit time (hour, mday (month_day) minute, month, second, wday (weekday) year, zone. These `date_` fields are **only generated for events where inside the raw event, Splunk is able to extract the timestamp.** 
¿Do not all events that Splunk logs have timestamps assigned to them?

Every single event will be assigned a value for `_time`, but not all source events have an actual timestamp value in them. In this case, the `_time` field is filed with the even's indexation time.
As this event has a timestamp inside `_raw` field, Splunk extracts all `date_*` 
In a lot of log files, the first value will be a timestamp, and Spluck's default event processing is that it wants to break the event at the timestamp. Whenever it sees another timestamp it will want to break it into a new event.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ed082bc0-d6b4-468f-b755-c4c667b7d4b3)

The difference between the `_raw`timestamp and the time under the `Time`columns is due to the time zone preference of the account settings.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b74b210b-22a7-47a5-ada1-790738f7f5ef)

When I removed such a setting the `_raw`timestamp and the time under the `Time` columns becomes the same.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5a28b3f8-ad7a-4c1e-953f-8780697edbed)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/458535f2-eb9b-421a-8935-d19929b9df0b)

We can see in this other set of events without a timestamp that `date_*` fields are not generated and we can see also that time under `Time` column is the same for all events. That timestamp comes from  **index time**. When Splunk does not manage to find a timestamp by default uses **index time**. It is the time the events were indexed.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b238a2c9-c587-4a9d-85b8-f69e33ee0d35)


When the default time fields `date_*`are present we can use them to solve specific use cases in our searches.
### Time Modifiers and Time Fields

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/87e1fff2-8539-4afc-937e-36397d9cd33d)

`Earliest` is looking back two days ago `-2d` to the beginning of day `@d` and `latest` is rounding down to the beginning of the current day.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ab420b7a-43ef-41b4-8108-dbafb4d9ff48)

And we are interested in displaying early-morning events from 2 AM until 5 AM in UNIX TIME.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/588d26e3-2ef2-4236-8c59-f9c63963f226)

### bin command and _time field
The bin command helps us bucket up our events. We can put numerical values into discrete sets or bins. The bin command has a `span` option  that is set to an integer or time-scale that allows us to set the size for each bin.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/04c7a226-297a-4010-a7c8-7fdcc05206df)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ab14cf24-d725-4cf9-8b09-ada375ca0da7)

In this example, I try to bin the events in intervals of 15 minutes and made some statistics over the events intra-bin. Count a number of file names as indexations. Distinct count of file names as indexes, a ratio of times each index is indexed, and the sum of the file sizes.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0ab4babb-f7c0-4341-8881-33d6f6475b1d)


[Back to top](#index)

## Formating Time
You can define how time is formatted in the search results using the time functions of the eval command.
### eval command
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e7ba3b44-aaf9-407d-8d27-963606bc6165)

Calculates an expression and puts the resulting value into a new o existing field that can be reused in the search pipeline.
Supports a vast assortment of functions.
Can exist as an expression.

- `now()` function returns the time that a search was started.

- `time()` function returns the time an event was processed by eval command.

- `relative_time(X, Y)` function returns an **epoch timestamp** relative (Y) to a supplied time(X)

- `strftime(X, Y)` function converts a epoch timestamp (X) into a string representing a time accordingly to the format (Y)  expressed by a string. From Epoch to formatted. 

- `strptime(X, Y)` function converts a  string (X) representing a time, into a Unix Timestaps based on a format (Y)  expresseed by a string. From Formatted to Epoch.



![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/77750b9b-e273-4031-b859-979d4919d14c)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b1a8e47a-a4c0-438e-b684-e5a7e6d06905)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/93e1752e-9323-45ad-a69c-212ceb26a070)


 ### Date and time Function Format Variables
 ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2470ffd3-c9d1-4aa4-ad4a-fb4960e333af)

[Documentaition link] (https://docs.splunk.com/Documentation/SCS/current/Search/Timevariables)

[Back to top](#index)

## Using time commands
### `Timechart`

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b7ae054e-3c93-4943-9087-1c3fabc87ddb)

`Timechart` performs statistical aggregations against time.
It is a **transforming command** that allows plotting data over time where `_time` is always the x-axis and the leftmost column of our table.
Support the same family of functions that the `stats` and `chart` commands.
Has a built option `span` that allows us to control the time gap of our bins.
The result can be split by another field with the `by` clause.
Timechart are best visualized as a line or area chart.

This simple command produces a **Single series** time series.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c6f59281-5403-41cd-9ddc-425ca4c2cd9d)

Using the `by` clause we can get `NULL` column that counts the events with no value on the field used in the `by` clause.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4b88e1d1-db12-40b6-8c21-fe163614ecfe)

The `by` clause creates a **multi-series time series**.

### Default bin span according to the picker time range.

|Time range|Default time bucket|
|----------|-------------------|
|last 30 days|1 day|
|last 7 days|1 day|
|last 24 hours| 30 minutes|
|last hour|1 minute|
|last 15 minutes|1o secodns|

### Span definition
Uses an integer and a time unit to define de bucket size we want the aggregation to be made.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/005ad5a0-be2c-4f9a-ad32-b759d6f37bb2)
### Limit definition
By default, the  `by` clause shows the top 10 series in a multi-series time series. If there are more, are grouped into an `OTHER` single series.
`Limit = 1` shows the most important single series
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6734e2a3-6c98-4f43-b927-15be837f0984)

 If set to limit=0, all distinct values are used. All other values are grouped into an  'OTHER', as long as `useother´ is not set to false
 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/abf4dba7-2d02-4bf7-a428-6337105caf47)


### `Timewrap`
Helps to display  the result of  `timechart` command in such a way that each time period is a separate series. We can compare data over a specific time period
`tiemwrap` tipically will follow a `timechart`command

Transforms a regular timechart like this one.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1e546a45-c52a-437f-9930-56bc5243ea7f)

Into a chart to compare 6 hours periods where you can see that recent peaks have been under control in the last six hours. Be aware of how legend changes and adapts its titles  to discriminate each single series.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3d4e8575-1582-474f-a197-b1568a3102ce)


[Back to top](#index)


## Working with time zones
Working with time base data for multiple geographic locations can be tricky.
We see here how time zones are represented in the data and how to use strftime function to correct time zones in search results.
**FIRST: Verify that results return what we are expecting.
If you wait for results between 2 and 5 AM, but the results display times between 9 to 11 PM
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f5bd05bb-8daf-4726-b251-7f1fdc64a65d)

the `date_*` fields do not reflect my local time. They are the values directly from the raw events.
To determine your time zones:

1.- In preferences, set the time zone to **Default system timeZone**.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9f5cc7dc-3c6f-4486-b602-40031fcc6a91)

2.- Run a search over the last 15 minutes.

3.- Read the event time stamps and compare them with your local time.

I did it from Spain, timezone GMT+1 at local time is 20:34 and I got the results od 18:24, two hours before

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3d6782ab-f5c6-4f87-9db2-b466e3088175)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/64fd0596-895f-4d65-8ed6-b4358da85cff)


After changing again the time zone....

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/73fb8d78-9d25-42c3-b17c-1744534e4c95)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1988ad18-0c48-4c40-9163-4b0ec08816b9)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c2214993-3932-4705-be9f-66f93ec80a3d)


Do not take into account the time zone of the Splunk Web. We have to ensure that we set our time zone to the default system time, or as an alternative we use the `strftime` function to organize our data and normalize it.

`%H`modifier makes `strftime` display data with the user's time zone preference

In previous examples, `my_hour` takes into account the timezone that is set. Date_hour field does not adjust the hour based on Splunk web time zone.

According to what we have learned we rearrange the previous search to consider my_hour calculated with `strftime` instead of date_hour.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/580fc5ac-9cf6-4564-958f-0561849438de)


[Back to top](#index)

[Back to index](README.md)
