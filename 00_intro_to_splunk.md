
[Back to index](README.MD)
# Intro to Splunk
## main functions:
1. Index data. It is the heart (collects data from any source)
2. Search & investigate.
3. Add Knowledge.
4. Monitor & Alert.
5. Report & analyses.

El indexador analiza el flujo entrante. Cuando encuentra un match con un modelo de datos de una fuente lo etiqueta con el sourcetype.
Conocido el sourcetype, descompone el flujo de datos en evento únicos al que se les pone un timestampo normalizado según la zona horaria del usuario de la cuenta.

Los evento se guardan en el index donde pueden ser investigados con el **Splunk Search Language**. Haremos queries.
A los eventos se les puede añadir etiquetas y aportarles conocimiento del dominio de negocio para ayudar a interpretarlos.

Se pueden poner alertas de monitoreso que disparen acciones.

## roles:
### admin
 - Install apps.
 - Ingest data.
 - Create Knowledge objects for all users.
 - Defines apps other users can see.
### Power
 - Create Knowledge objects for users of an app.
 - Do real-time searches.
### User
 - See only knowledge objects shared with him.


## Apps (pre-configured environments that extend pre-built knowledge and capabilities)
 - two default apps: ``Home app``: (sets a custom dashboard as a default dashboard) and ``Search and reporting app``
 - **SplunkBase** has hundreds of them
 - We can create our own apps.

### Search and reporting app (has 8 components).
#### 1. Splunk Bar.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b78ab40d-bd01-4044-808a-1e7b96ce6eb5)

menus to navigate
#### 2. Search Bar.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a34378af-264d-49f5-afd6-bb45c8619348)

Keyword plus time filter.
There is a ``save as`` menu to save the search as a knowledge object.
#### 3. Search button.
#### 4. Time range picker.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/706673ae-fa4b-4f7a-9995-17494444eeb1)

#### 5. How to search Pannel.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ad6e5cf9-1e2b-4c3e-9e79-d3cb34f20769)

#### 6. Data summary button.
Breaks down data  by Host (IP, FQDN, or Hostname), Source or Source type. The source is the data's file or directory path 
#### 7. Table views.
Allows data study without Splunk Search Processing language.
#### 8. Search History.
To view and rerun past searches
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0993ca01-9687-4592-85f9-82dc31ecae47)

#### 9. Search result tabs.
Limiting a search by time is key to faster results and it is a good practice.

When the search is sent to Splunk, becomes a ``search job``.

whit the result we got:


##### Save as menu
Allows us to save the search as a knowledge object
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/299221b3-5bb2-4503-ac65-b612967ff0dd)

##### Search result tabs
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/32c9b448-ea30-4ed2-9ad5-cd3831bfd1b4)

###### - Events.
###### - Patterns. Allows to see patterns in the data
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ac30bdf1-efc5-4723-bd64-dc89b60d68de)

###### - Statistics & visualizations
If the search command does not generate statistics or visualizations nothing shows here aside from the 3 default links.
Commands that generate statistics or visualizations are called **transforming commands**. Transform event data into data tables

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/915fb700-9690-4e93-a273-cdba960c15f5)

##### Search Action Buttons
Edit job, send it to the background, inspect, delete, Pause, stop, share, print, export (Raw, CSV, XML, JSON) 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6f4ee29a-a102-4d51-9a29-cb315e4f48f0)

When sharing a search we get a link.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/72bea11d-ab1a-4395-ae3a-ffbf8988615b)

By default, a search job will remain active for 10 minutes. After 10 minutes Splunk needs to run it again to return results.
A shared search remains active for seven days. Anyone I shared the job with will see the same result I saw the first time I ran it.
If the job is not accessed in the specified time period the job is removed.

##### Search mode selector
- Fast: Field discovery **off**.  Only return information on default fields and fields required to fulfill the search.
  
- Verbose: Field discovery **on**. Returns as many fields and even data as possible.
  
- Smart: toggle mode depending search type we are running.
  
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/861a1bc6-0bc5-4913-9d94-c5c6d12fe548)

##### Search Timeline

Where it is possible to drill into the time axis. clicking and dragging filter results.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/80995d7b-a28a-4f1a-bc7a-a817f2b6ce8c)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/64a0a10a-03f5-4818-8a9e-65686130e54f)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/20b22100-6e74-4ca2-9b1f-5c4b92f04a80)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d2b70e6c-8a85-4507-9ca3-20a14df72920)

##### Event list

In reverse chronological order.
Time is normalized in the index to a consistent format based on the time zone settled in the user account.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9392633b-a693-4f6b-8d49-f687b5485ec3)

For each event, we visualize the default fields (host, source & source type)

Easily we can add more fields to search and launch a new search
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/66bdfaf8-2b87-413d-bfd4-497b16dd3e98)


##### Fields sidebar
Shows all fields extracted
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b2db4c0e-9528-4677-a6b2-d26518c335bc)


## Search processing language
Wildcards accepted.
search terms **are not** case sensitive. (FAILED, failed, FaiLeD give same results)
3 uppercased boolean operators with this precedence order 1.-NOT 2.-OR & 3.-AND. Parenthesis can change such precedence order.
When the boolean operator is not explicit AND is implicit.
Use quotes for exact search. Escape a quote with a backslash if it is part of an exact search.
### commands have 5 components
 - Search terms ==> query events
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4927c716-3700-4bf6-af25-ab523a3671a7)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/555e5740-6c6e-4ece-8c97-d731c0b76648)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3f7acc1f-7f57-45d4-a20a-d8a806a65445)


 - Commands ==> What to do with the results: Charts, computing statistics & formatting
 - Functions ==> how we want to chart, evaluate or compute the results
 - Arguments ==>Variables to apply in functions
 - Clauses ==> Group results

Commands, functions, and clauses **are not** case sensitive.
If a command references a specific value, such value will be case-sensitive.

### best practices
Filtering fields before the first pipe produces better results
Using time is the most efficient way of filtering
The fewer data to search the faster
Default fields extracted at indexing time that do not need to be extracted at search time:
- time
- index
- host
- source
- source type

The more you tell the search engine, the more likely it is that you get good results.
Is better to search ``failed password`` than ``password``.
Inclusion is better than exclusion.
Searching for ``"access denied"`` is better than searching for ``NOT "access granted"``.
When possible use the OR or IN operator instead of wildcards.
Apply filtering commands as early as possible in your search limits the number of events, making future data manipulation faster.

## Knowledge objects (Discover and analyze data):
Created by one user and shared with other users.
Saved and reused by multiple people or in multiple apps.
Can be used in a search.
Became powerful tools for Splunk deployment.

A **knowledge manager** has to take care of general policies that rule the creation of knowledge objects. the aim of such rules is to create a clean and efficient toolbox.
1. Oversee Knowledge object creation and usage.
2. implement a naming convention.
3. Normalize event data.
4. Create data models for Pivot users.

It is convenient that all Splunk users are aware of the  5 categories.
- Data Interpretation: Depending on source type,  some fields are **automatically** extracted from data, but we can extract more **manually**. it is possible to set **calculated field** on previous ones.
  
- Data Classification: **Event types** allow to categorize events. A **transaction** is any group of conceptually-related events that spans time, such as a series of events related to the online reservation of a hotel room by a single customer.
- Data Enrichment: **Lookups** add other fields and data to the event not included in the indexed data. **Workflow actions** are links within events that interact with external resources (Use the field values in an HTTP error event to create a new entry in an external issue management system) or narrow or search.
- Data Normalization: **Tags** or descriptive names for key-value pairs. We can search on tags. you could have an IP address related to your main office with the value 192.168.1.2. Tag that IPaddress value as "mainoffice". **Field aliases** normalize data over multiple sources. One data model might have a field called ``http_referrer``. This field might be misspelled in your source data as ``http_referer``. Use field aliases to capture the misspelled field in your original source data and map it to the expected field name.
- Data Models (Search-time mapping of Knowledge): are hierarchically structured datasets (events, search or transactions)

## Reports and Dashboards.
Before start saving reports define a naming convention.
Saving and sharing searches is easy with reports. We can do it in the ``save as`` menu.
 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4006f464-4010-426c-b08d-7aca0fc4f97f)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/702a8445-0809-47af-8bbc-59bb28b225ba)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7c3bf4c7-6be6-4800-b979-48c2247424cb)

The option to display a report in all apps is available only to admin role users.

By default, the report will be available only to the owner who created it. 

Power users are granted read & write permission on the report.

Changing the setting to App, a report can be shared with all users of the app **in which the report was created**.

The ``run as`` dialog has to be treated carefully in case the report shows sensitive data. 
If not all users can see it, is better to execute the repost as a user. in this way, only the data right for the level of authorization of the user will be shown
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/fff538c9-8fee-4d90-a309-f1a112363e88)

A report can be scheduled to be executed at regular time triggering different events. 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/49695eca-705b-4de1-bc9c-908c41687aa9)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f7269e83-6e55-49c2-b444-14d02547c649)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9423fffd-e349-4345-8c0f-a339bcf483b4)



All reports are available from de reports tab in the application menu.
Any search that returns statistical values can be seen as a chart. Charta can be based on numbers, time, and location.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/01d88528-1516-4c06-aece-8283b3f257cf)

Charts are interactive allowing one to hover over the details or drill down to the events behind.
Any chart can be saved as a dashboard.

A dashboard is a collection of reports
[Back to index](README.MD)
