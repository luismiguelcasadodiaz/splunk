[Back to index](README.md)
# Scheduling Reports & alerts
## Creating Scheduled Reports (04:57)
A scheduled report is a report that runs on a scheduled interval. 
The report can be automatically sent by email or trigger additional actions.
The report can be used to power dashboard panels to prevent Splunk from running multiple concurrent ad hoc searches.

1.- Create the search we want the report to be based on.
2.- From the Save As menu, select a report.
3.- Give the report a name according to your company naming policy

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f9031323-9b2b-4b89-83d5-e439e6d5ed40)
4.- As this is a Scheduled report do not a Time Range picker.
5.- Select Schedule Option

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
  -  POST to an external url
  -  Manage Actions Install os build custom alert actions depending on your user role. Admin user will have the option to manage and add prebuilt alert actions
 
  [image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a3532994-f53e-4f0d-8e08-a141c5dd09f6)

12.- Fill required parameters for the previously selected action.
Please note that [search, results, job,  server or dashboard tokens] (https://docs.splunk.com/Documentation/Splunk/latest/Alert/EmailNotificationTokens) can customize fill-in parameters (to, cc, bcc, Subject, Message, footer)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/10878bc6-4dd7-4387-b578-4d5d3373b77e)

13.- Indicate what to links include in the email and what documents to attach:


## Managing Reports (02:08)
## What are Alerts? (00:31)
## Creating Alerts (03:10)
## Using Alert Actions (02:24)
## Manging Alerts (01:58)
[Back to index](README.md)
