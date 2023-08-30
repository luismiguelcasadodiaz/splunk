[Back to index](README.md)
# Quizzes

#### [00.- Intro to Splunk](#_intro_to_splunk) 
#### [01.- Visualizations](#_visualizations)
#### [02.- Working with time](#_working_with_time)
#### [03.- Statistical Processing](#_statistical_processing)
#### [04.- Comparing Values](#4-comparing-values)
#### [05.- Result Modification](#5-result-modification)
#### [06.- Correlation Analysis](#6-correlation-analysis)
#### [07.- Creating Knowledge Objects](#7-creating-knowledge-objects)
#### [08.- Creating Field Extractions](#8-creating-field-extractions)
#### [09.- Data Models](#9-data-models)
#### [10.- Using Choropleth](#10-using-choropleth)
#### [11.- Using Fields](#_using_fields)
#### [12.- Scheduling Reports](#_scheduling_reports_and_alerts)


---
# Intro to Splunk 
93% with bold answers(one is wrong but I did not manage to discover which one.

1.- What is the most efficient way to limit search results returned?
 - index
 - source
 - host
 - **time**

2.- By default, who is able to view a saved report?
 - Any power or admin user
 - **The user who created it.**
 - Any user with a viewport capability

3.- Which of the following booleans can be used in a search?
 - **OR**
 - ALSO
 - **AND**
 - **NOT**

4.-Which character is used in a search before a command?
 - **Pipe** (|)
 - Backtick (`)
 - Quotation mark(")
 - Tilde (~)

5.- Which search mode behaves differently depending on the type of search being run?
 - Verbose
 - **Smart**
 - Variable
 - Fast

6.- Which of the following searches will return the words dail, failure, or failed?
 - fail
 - dail+
 - *fail
 - **fail***

7.- Which of the following searches will return results containing the terms failed, password, or failed password?
 - **failed or password**
 - fail*
 - failed password or "failed password"
 - **failed or password or "failed password"**

8.- Which of the following searches returns results containing the phrase "failed password"?
 - failed password
 - (failed password)
 - **"failed password**
 - `failed password

9.- When a search is run, in what order are events returned?
 - Alphanumerical order
 - **Reverse chronological order**
 - Chronological order
 - Reverse alphanumerical order

10.- Which command can be used to further filter results in a search?
 - filter
 - **search**
 - subset
 - subsearch

11.- Which of the following roles are required to share knowledge objects?
 - Manager
 - **Power**
 - **Admin**
 - User

12.- Which Splunk infraestrucutr component stors ingested data?
 - Dashboards
 - Datasets
 - **index**
 - data models

13.- By default, how long does a search job remain active?
 - 30"
 - **10"**
 - 10 days
 - 7 days

14 What are the default roles in Splunk Enterprise?
 - **Admin**
 - Manager
 - **Power**
 - **User**

15.- What determines the timestamp shown on the returned event in a search?
 - Timestamps are displayed in epoch time
 - **The time zone defined in user settings
 - the time zone where the event originated
 - timestamps are displayed in GMT.
---
## Using Fields
100% with bold answers.

1.- In the fields sidebars, **interesting fields** occur in at least ______ of resulting events.

  - 50%
  - 3%
  - **20%**
  - 10%
    
2.- To **remove** fields from a seach, you would use the _______ command.
  - +fileds
  - fields+
  - **fields-**
  - -fields
    
3.- At search time, in an event that has an equal (=) sign, the data to tl left is treated as _______, and the data to the right is treated as ______.
  - field name, sourcetype
  - lookup, value
  - **field name, value**
  - lookup, sourcetype
   
4.- Which of the following fields are default selected fields?
  - **host**
  - **sourcetype**
  - index
  - **source**
    
5.- True or False: Once you rename a field, the new field name must be used in the rest of the search string.
  - **True**
  - False
    
6.- The fields command allows you to do which of the following:
  - **exclude fields (fields -)**
  - **include fields (fields  )**
  - **include fields (fields +)**
    
7.- True or False: Field are Knowledge objects:
  - **True**
  - False
    
8.- At search time, _____ extract fields from raw event data.
  - **field discovery.**
  - field extractor.
  - field command.
---

## Working with time
88% . i have not the right answer for question 8

1.- @timeUnit will always round up and go forward through time.
 - **False**
 - True

2.- The _______ and ______ time modifiers will override the time range picker in a historical report.
 - **latest**
 - first
 - **earliest**
 - last

3.- Which of the following are default time fields? Select all that apply.
 - **date_mday**
 - **date_year**
 - data_day
 - **date_hour**

4.- When using the following search arguments, what will be returned?
`timechart count span=1h`
 - Events in the last 24 hours.
 - Events with a duration of 1 hour.
 - **Chart of events in 1-hour chunks.**

5.- Date_time always reflects your local time zone and not the time/date from raw events.
 - True
 - **False**

6.- Using `earliest=-30d@d latest=@d` is how to return results from 30 days ago up until the time the search was executed.
 - **False**
 - True

7.- Choose the search that will sort events into one minute groups. Select all that apply.
 - | bin span=1minute
 - | bin_time span=1m
 - | bin_time span=1mins
 - | bin span=1minutes

 8.- What will the strftime function return when using the %H argument with the _time field? Select all that apply.
  - hour of the event generated at index time.
  - **convert the hour into your local time based on your time zone setting of your Splunk web sessions.**
  - time of raw event in UTC
 
 
 ## Scheduling Reports and Alerts
 14/14 100%

 01.- Which **Scheduled report setting** allows you to define a time range for a report to run if it is delayed?
  - Report Window
  - **Schedule Window** OK
  - Schedule Time Range
  - Report Time Range

02.- Which **alert setting** allows you to control how many actions are taken when trigger conditions are met?
 - **Throttle** OK
 - Schedule Priority
 - Schedule Window
 - Limit

03.- Which of the following user roles are able to display a **report** in all apps?
 - Power.
 - **Admin**.
 - The user who created the report.
 - User.

04.- If a **dashboard panel** is powered by a **Scheduled report**, How frecuently will its contents update?
 - The dashboard panel updates based on the underlying report's scheduling settings.
 - **The dashboard panel updates any time the dashboard is opened or manually refreshed.** OK
 - Dashboard panels cannot be lined to scheduled reports.
 - Dashboard panels will update based on the dashboard's time range picker.

05.- Which is a primary benefit of scheduling reports?
 - Dashboard panels require scheduled reports in order to display up-to-date content.
 - **Scheduling a report reduces the demand that concurrently running reports can put on your system hardware.**
 - Scheduled reports take precedence over all activity in your environment.
 - When a scheduled report is run, all existing search jobs are terminated.

06.- When are actions triggered for a **real-time alert**?
 - Within a 60-second window of its cron Schedule.
 - **As soon as alert conditions are met.** OK
 - Within a five-minute window of its corn schedule.
 - As soon as the related report is run.

07.- Which edit setting allows a report to be displayed to users outside of your organization?
 - HTML.
 - Enable.
 - Permissions.
 - **Embed**. OK

08.- Select the two valid types of alerts.
 - Email.
 - Text message (SMS)
 - **Scheduled** OK
 - **Real-time** OK

09.- Which of the following prebuilt **alet actions** can be triggered when a report is run?
 - Run a secondary report
 - **Output results to a lookup** OK
 - Send a text message (SMS)
 - **Send an email** OK

10.- Which **Scheduled report** type will continuously run in the background?
 - **Real-Time** OK
 - Constant
 - Automatic
 - Interval

11.- Which **alert action** allows you to send an event to your Splunk deployment for indexing?
 - **Log event**. OK
 - Generate Event.
 - Generate Log.
 - Create Event.

12.- Which **Scheduled report** setting helps determine when concurrent report will run?
 - Scheduled Order.
 - Report Priority.
 - [**Scheduled Priority.**](https://docs.splunk.com/Documentation/SplunkCloud/latest/Report/PrioritizescheduledreportsinSplunkWeb) OK
 - Report Order.

13.-Which alert action allows you to send a message to an external chat room?
 - **Webhook** OK
 - Output to chat.
 - Output to Text.
 - API Call.

14.- Which of the following user roles are able to display a **report** in the app in which it was created?
 - Power
 - **The user who created the report.** OK
 - User
 - **Admin** OK

[Back to top](#_quizzes)

[Back to index](README.md)
