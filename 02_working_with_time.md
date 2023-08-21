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

### Tiem Range picker
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

### Time Unit Abbreviations

   Time unit abbreviations can also be used within the `earliest` and `latest` time modifiers in our search to override the TimeRange Picker settings.
   Syntax starts with `plus +` or `minus -` to look forward or back in time. Continues with a number (1 is implicit) and a specific time unit, and we can round down to a specific time unit using  `@` symbol
   
#### Time units table
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6a5573b3-4acf-4cb4-9acd-eb9dd1c7d075)

  ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e4fcfc44-cdfb-4925-a5e3-79d288484ff1)
 ### Examples
 For understanding this example let's assume is exactly 9:45 AM on April 1st, 2021.

 |current time |modifier| meaning|
 |-------------|--------|--------|
 |9:45 AM on April 1st, 2021.|-30m@h| `-30m` 30 minutes before ==>  9:15 AM   `@h` rounded down to hours ==> 9:00am|
 |9:45 AM on April 1st, 2021.|-h@h| `-h` one hour before ==>  8:45 AM   `@h` rounded down to hours ==> 8:00am|

 ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/822ec956-4e3e-4a04-b90b-ff3b23ea0670)


[Time Unit Documentation](https://docs.splunk.com/Documentation/SplunkCloud/9.0.2209/Search/Specifytimemodifiersinyoursearch)

## Formating Time (06:12)
## Using time commands (9:29)
## Working with time zones (2:43)
[Back to index](README.md)
