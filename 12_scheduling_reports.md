[Back to index](README.md)
# Scheduling Reports & alerts
## Creating Scheduled Reports (04:57)
A scheduled report is a report that runs on a scheduled interval. 
The report can be automatically sent by email or trigger additional actions.
The report can be used to power dashboard panels to prevent Splunk from running multiple concurrent ad hoc searches.

1.- Create the search we want the report to be based on.

2.- From the Save As menu, select a report.

3.- Give the report a name according to your company naming policy.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f9031323-9b2b-4b89-83d5-e439e6d5ed40)

4.- As this is a Scheduled report, do not select a Time Range picker.

5.- Select Schedule Option.


![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/901f76c2-27ac-4fa5-b00c-2e24bfc2f731)

6.- Select the frequency to run the report (Hour, day, week, month,  or cron Schedule). Each frequency has its own parameters for fine-tuning.

7.- Select the Time Range that the report will cover. It will be relative to the schedule.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4aa3ed6d-7fc5-45f9-94b8-16d48b492a7a)


Running **concurrent reports**, and the searches behind them can put a big demand on your system hardware even if everything is configured to the recommender specs.

8.- Select Schedule Priority. It is available only for Admin users. Choose between default, higher, and highest. Giving a Scheduled report a greater priority will make sure that it takes priority over other searches being run on the system at that time.

9.-  Select the Schedule Windows to set a time frame (5, 15, 30 minutes, 1, 2, 4, 8, hours, custom, auto),  in which to run our report. so if we have other reports scheduled to run at the same time, we can provide a window in which to run a report. This provides some time flexibility as to when the report is actually executed. If the system is busy our report will be delayed as long as it falls within our acceptable window. Include a Schedule Window only it the report does not have to start at a specific time and you are ok with the delay. `Auto will allow Splunk to automatically determine the best time window in which to run the report.

10.- Select the workload pool. A workload pool is a logical container that allows prioritization of workloads in the pool. Splunk Cloud Platform provides three pre-defined workload pools for searches. Each pool is allocated a percentage of CPU (5% low, 35% standard 60% High) and memory resources:

Options in points 8, 9, ad 10 help us manage our scheduled reports so that they put less strain on our deployment.


11.-Choose what action to trigger when the scheduled report is run.
  -  Log an event to a Splunk receiver endpoint
  -  Output results to lookup
  -  sending results to a telemetry endpoint
  -  Run a script
  -  Send an email
  -  POST to an external url.
  -  Manage Actions Install or build custom alert actions depending on your user role. Admin user will have the option to manage and add prebuilt alert actions
 
  ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a3532994-f53e-4f0d-8e08-a141c5dd09f6)

12.- Fill required parameters for the previously selected action.

Please note that [search, results, job,  server or dashboard tokens](https://docs.splunk.com/Documentation/Splunk/latest/Alert/EmailNotificationTokens) can customize fill-in parameters (to, cc, bcc, Subject, Message, footer).

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/10878bc6-4dd7-4387-b578-4d5d3373b77e)

13.- Indicate what to links include in the email and what documents to attach:


## Managing Reports (02:08)
From `Settings` menu / `Searches, reports, and alerts` option. You get a quick overview of our report including when it is scheduled to run next. 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9b3a2e29-8c26-4d48-b67c-1386d2edf714)

Clicking the name of the report, we get quick access to change the search string and time range.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1e01ae7d-5a07-4054-88ff-ed6754377763)



From `reports` tap in the search and repost app. Clicking on the name  will display the results of our scheduled report. Use the edit button to change settings from this location. 

Users with power role have the option to display this report for themselves  or other users of the app. Displaying a report for all apps requires an admin role.
Selecting App allows us to grant read and write access to all users in our organization or users based on their role
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/721280a2-6461-4907-8163-fc59be28156b)

To make a report available to folks who do not have access to the Splunk instance  we use the `embed` option from the edit menu.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c2f1a4b6-9b36-49a0-88e2-4f40148fefa3)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9c0a64be-cf1e-40d9-bba9-cc78a3b257c8)

**Be very cautious** when doing this. AM embedded report will be viewable by anyone who has access to the webpage that it is inserted in.
AN embedded report **will not** show data until the scheduled search is run.
Once the report is embedded we will no longer be able to edit attributes for the report

There is also the option to add a scheduled report on a dashboard



## What are Alerts? (00:31)
Alerts are based on searches that run on a scheduled interval or in real-time. Splunk can alert you when the result of the search meet a defined condition
Alerts are triggered once the search is completed
Alerts can;
  - List in the Splunk Interface.
  - Log events.
  - Be outputted to a lookup.
  - Send to a telemetry endpoint.
  - Trigger Script
  - Send mails
  - Use webhooks
  - Run a custom alert.


## Creating Alerts (03:10).
1.- Define a search
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3795be0e-f7f7-477d-8f4d-ecd241076120)

2.- From the save as button choose alert
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/bd8d9b9b-8805-4619-934b-1ec6368fa4f1)

3.- Enter a title according to your organization's Naming policy and explain what this alert is for.

4.- Set Permission. `Private` (Only you can access, edit and view it). `Shared in App` (the result will be displayed for all app users. All have read access. **Only power user has write access** to it ).

5.- Set Alert type. 
  - `Scheduled Alert Type´ allows you to set a schedule and time range for the search to be run
  - ´Real-Time Alert type` the search will be run continuously in the background. As soon as alert conditions are satisfied an action is triggered. Since Real-Time alerts run continuously can place more overhead on system performance. When we would like to know as soon as our trigger condition is met, a real-time alert type is a better fit.

6.- Set trigger condition 
  - Per result: Trigger whenever search returns a result.
  - per Number of results: Trigger based on a number of search results during a rolling window of time.
  - Per Number of Hosts: Triggers based on the number of hosts returned during a rolling window of time.
  - Per number of sources: same as above but with Source default field.
  - Custom conditions: Defined using Splunk search language.

Since many issues may trigger an alert we would like to confirm a problem **before** sending an alert
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0c367172-0a57-4ba7-99bc-2847386662ed)

It could be easy to inundate users with alerts. We can set the number of times to trigger the alert and throttle how often the alert is executed allowing them to be ignored or filtered out.
if our alert is set to trigger every time more than 2 errors happen in 60 minutes, with 6 errors in 60 minutes then we will get:
- one email with `once` the action will be fired once within the scheduled time we have selected.
- Five emails with  `For each result` as it will be fired  every time conditions are met.

We can make this setting more granular usin the Throllle checkbox
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/56587410-c5e0-409c-b01a-e0cef588ac18)


## Using Alert Actions (02:24)
## Manging Alerts (01:58)
[Back to index](README.md)
