[Back to index](README.md)
# [03 working-with-time]
Time is one of the most important components to consider when working with data.
we will learn:
 - How to work with time in searches. `earliest=@d`,  `latest=@d`
 - time base functions (`now()`, `time()`, `strftime()`, `strptime()`)
 - time commands (`timechart`, `timewrap`)
 - Understand how time zones are represented in the data

## Searching with Time (25:36)
What does time mean to Splunk?
When an event is ingested, its timestamp is stored in the _time field that is used to implement the event timeLine in the Splunk Web interface. 
The _time field is stored with the event in the index **prior** to the search time, along with default fields such as host, source, and source type (also de-index name in which it is stored in.
Timestamps are expressed in Unix or epoch time (_time = 1619736430) and translated to human-readable time (Thu, 29 Apr 2021 22:47:10 GMT) **during the search** operation process.
All events are sorted by time, thus time is the most efficient filter.

The timestamp displayed in the Time Column of each event is adjusted to the user's local time zone, **As long as the time zone is set** within the account settings
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9c72ff16-da73-40d4-876c-0cb7e6133af2)

### Timeline Mouse actions
The timeline is an overall distribution of the events in relation to the specific time range set for the search
- Zoom in, Zoom Out,
- Hover to view the event count for a specific time,
- Format the x and y-axis,
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

 - real-time search: return results up to the second they are coming in. The benefit of that is that we see data as it's coming into Splucnk in real-time. Real .time searches **are resource intensive**. They consume an entire CPU-CORE. They continuously update search results as the events arrive. Multiple real-time searches could impact the overall performance. One alternative is to Schedule a report.
 - ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/158419c6-b536-4ddd-9cec-1873477a6036)

 - Relative time option;
   - earliest time range.
   - latest (now or at a beginning of the current hour)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ba3152ab-7359-46dc-a4b6-dace23d90131)

  - Data Range & date & Tiem range (between, before, since
    ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c48a61e8-63cb-4e44-9b7e-acc612cf284b)
    ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/06bfc863-f795-44a7-a68c-60e68781dd02)

 - Advanced: we can express time unit abbreviations which allows us to be even more specific about our time.
  ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/15c3dcd7-dbc9-49a0-a068-05197a4b7f24)
Please not the absolute times below field texts
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6576e2e6-6c76-4fdb-9b0a-c83c06b2c5cd)


### Time Unit Abbreviations

   Time unit abbreviations can also be used within the `earliest` and `latest` time modifiers in our search to override the TimeRange Picker settings.
   Syntax starts with `plus +` or `minus -` to look forward or back in time. Continues with a number (1 is implicit) and a specific time unit, and we can round down to a specific time unit using  `@` symbol
   
#### Time units table
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6a5573b3-4acf-4cb4-9acd-eb9dd1c7d075)

Fort week days we can use w1(Monday)... w6(Saturday, w6 or w0 (Sunday).


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
 
In this example, the time range picker was settled `-5h@h`, but in the search textbox there is a restriction to view only the last five minutes `earliest=-5m@m latest=now`
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4cc1e8e6-1a25-44be-93e8-5a9c8e678739)
In this dual specification, the case has a prevalence is the restriction specified in the search textbox. èarliest`and `latest` modifiers have prevalence over time Range picker.

[Time Unit Documentation](https://docs.splunk.com/Documentation/SplunkCloud/9.0.2209/Search/Specifytimemodifiersinyoursearch)
## default Time fields
There are a set of fields that are available in most cases for controlling the time of our searches. All begin with `date_` prefix followed by a specific unit time (hour, mday (month_day) minute, month, second, wday (weekday) year, zone. These `date_` fields are **only generated for events where inside the raw event, Splunk is able to extract the timestamp.** 
¿Do not all events that Splunk logs have timestamps assigned to them?

Every single event will be assigned a value for `_time`, but not all source events have an actual timestamp value in them. In this case, the `_time` field is filed with the even's indexation time.
as this event has a timestamp inside `_raw` field, Splunk extracts all `date_*` 
In a lot of log files, the first value will be a timestamp, and Spluck's default event processing is that it wants to break the event at the timestamp. whenever it sees another timestamp it will want to break it into a new event.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ed082bc0-d6b4-468f-b755-c4c667b7d4b3)
the difference between the `_raw`timestamp and the time under the `Time`columns is due to the time zone preference of the account settings.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b74b210b-22a7-47a5-ada1-790738f7f5ef)

When I removed such a setting the `_raw`timestamp and the time under the `Time` columns becomes the same.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5a28b3f8-ad7a-4c1e-953f-8780697edbed)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/458535f2-eb9b-421a-8935-d19929b9df0b)



## Formating Time (06:12)
## Using time commands (9:29)
## Working with time zones (2:43)
[Back to index](README.md)
