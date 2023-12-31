[Back to index](README.md)

# [11 Using Fields]
## Introduction (0:44)
- Use fields in Splunks' Search processing language to filter data to return needed results.
- Select which fields are extracted from the index versus search time.
- Learn the difference between persistent and temporary fields.
- Do more whit data through the use of knowledge objects.
  
## Using the fields Sidebar (01:42)
Shows all the fields extracted at search time split into two categories
- **Selected** fields. Show at the events' bottom together with the default fields (host, source, and sourcetype)
- **interesting** fields. are fields that have values in at least 20% of the events.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ee650aad-37ec-42e9-ae1b-a6cde0354c0d)

  `a` in front of the field name denotes a string field.  `#` in front of the field name denotes a numeral field.
Clicking on a field show values for the field, a count of the values, and a percentage of the events the value shows up in. 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e8584629-ea05-455e-81e6-0a4ae5dc6574)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5f80d4bc-c6ca-4d05-9f81-b7666b50c5c6)

You can add a field value pair `Country=Germany` to the search by clicking on it.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c15d28b4-efeb-4e4b-bb5e-54fbfb04d725)

You can launch quick reports based on the field (top/Rare Values or top values by time as shown below)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9a6a5b08-8b9f-481f-9d65-84c026da6e6c)

When you add a field to the selected fields list
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e0ae6519-3083-4f6e-a4b7-3708f25b7dae)

aside from showing up at the event, it will persist for subsequent searches
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7e727bee-8a99-44ef-9899-fb24955eff89)

From the fields sidebar, either with the `all-fields` button

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/930e2e66-ddcc-4b9b-a329-977c422f24ab)
or the `more fileds` link
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a5334317-d610-412b-9d58-62fccfb8f7f1)

we can see all fields for the search, filter them, see the number of distinct values in the field, the **coverage** or percentage of the events that have a value in the field, and add a field to the selected fields.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5bf12d92-e0b0-434b-bc4e-2940457bd78d)

## Using Fields in Search (04:02)
You can  refine and run more efficient searches using fields.
Field names are case-sensitive while values are not
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4cbbefbe-29ef-4967-81cb-8839d2ca3a79)

|Operator| Field Operator Usage|
|:------:|---------------------|
|=,  != | with Numerical or string values|
|>, >0, <, <=|wiht numerical values|

Wild cards and booleans are allowed ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5738154f-8e2a-4acf-8dad-578ec1a28bc1)
For fields containing an IP address, wildcards are subnet and CIDR aware ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0677509b-be89-4f19-97fe-50388bfa61bc)

### `!=` is not equal field operator versus `NOT`boolean
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/178665d0-ca74-4705-8066-8da98cc7e577)


They do not always return the same results or the same number of events. The tops search only returns events where the status field is not 200 while the bottom search returns all events that do not have a field where status equals 200. Meaning that if an event does not have a status field at all, it will be included in the results.
Me parece que esto es debido a que implicitamente el operador AND anda por ahí.

### `IN` operator can be used as an alternative to chaining several operators
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8c8ae06c-f461-462e-a790-6aa8b03283ee)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/923cefe6-040e-458a-8520-eaa63a4cf763)

### `fields` command
Can be used to include (`+` plus operator) or exclude (`-` minus operator) fields from the search.
We can make our search more efficient by adding a field command to include only the needed fields.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f663a3f1-8fd2-4ac8-8ca6-bf630a038d3a)

Filtering as early as possible in a search is a best practice.
Fields default to inclusion, so if not operator is specified the supplied fields will be included in the search

### `rename`command.
Can be used to rename fields in the search to give them more meaningful or user-friendly names.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d641a352-cc70-4255-b046-19d240b19132)


## Fields in Search Results (7:05)
Splunk returns 
### Indexing versus search time field extraction
Some fields are extracted at index time while others are extracted at search time.
At data ingestion, a selected number of fields are automatically extracted (metadata: host, source, sourcetype, _time ( Event's timestamp), and _raw (original raw data of an event)
At search time, **field discovery** extracts additional fields from the raw event data based on its assigned sourcetype, and key-value pairs found in the data. These fields are persistent and will be extracted every time a search is run containing the same search terms unless no inclusion is specified.
### temporary fields
Are created on an ad-hoc basis with the command `eval`, which is used to calculate and manipulate field values.
Results of eval can be written at search time  to a new temporary field or to replace an existing field value.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/bc3bf8e1-7d67-4b1b-8e3b-df6475f1b789)
Since we used a non-existing field name for the results, a new temporary field  `bandwidth` is created.

### Field Extraction
The utility `field extractor` can be used to extract new,  **persistent across searches**,   data fields that were not automatically extracted from the data accordingly with the assigned sourcetype.
The commands `rex` and `rex` can also be used to extract **temporal** fields at search time.

#### erex command
`erex` new_field_name `fromfield` (is the field in our data to match on) `examples` (a list of sample data)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a78f83f6-59aa-46ca-a10e-b3da44cc7057)



When the search is run, Splunk builds a regular expression based on the sample data, checks it against _raw event data  field, and ad matched values to the `character` field.
`Erex'  only knows what to look for based on the sample i gave it.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e09cdf82-6828-4055-acf7-84d8d6d5285e)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e6ad3ad7-8612-4b84-bd98-97431ae710e6)

Using the `where` command with the `isnull` function sw can see some missed character names we can add to the sample data list.

We can see RegEx generated by `erex` in the job menu
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f5bce1f8-d490-4d76-89cc-8a1709cf7264)

#### rex command
we will use the capture groups to extract values at search time from field values or raw data.
Rex allows matching multiple groups resulting in multiple fields.
Let's extract USER and CHARACTER name values
`rex` field= field_to_match_on "regular expresion between double quotes 
_raw field will be used by default if not field argument is given.
Run rex over _raw can have a performance impact. Is better to used it wiht an already extracted field.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/38316eba-8862-4dfd-9b55-d939a06a8bbc)
this regex captures  email addresses.
We continue the expression to return a Characte field. Behind our capture group, we add an apostrophe `'`, followed by a `\s` to match the white space. To match caracter name `[a-zA-Z:]+` follows by another `'` apostrophe. then we create another capture grodp `(?P<Charactar>[a-zA-Z0-9.-]+)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f23fcefb-83eb-4672-8b70-5a5f8221df8b)

### Erex versus rex
|                  |erex|rex|
|------------------|--------|-------|
|Usage|easier| sofisticated|
|Requires Regular expression knowledge|no|yes|
|Requires sample data|yes|no|
|Generates Regular Expresion|yes|no|
|Help|| can use Erex-generated Regular expression as a starting point|
|Advice|| When possible use rex|

My own try
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d557ffb4-da13-4549-8a09-e4626604d99a)


## Enriching Data with Knowledge objects (03:02)
### calculated fields
With the eval command, we created a temporary field to convert bytes into megabytes. As it is not a persistent solution we need to write such a conversion every time we want to make it. 
The calculated field is a better option for that:

From `settings` menu

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/426318d3-00fc-42cb-a9bb-d4581ea17958)
in the  `fields` option

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b059ec9f-3471-4ae2-9b47-ad943d1495bc)
we find the `calculated fields` dialog

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/60c9646c-74e5-4f88-b1e8-589fa841652b)

that if filled properly
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6a2f0990-f717-4669-a0a1-c83a7ac904e3)
will allow Splunk to create the field at search time  every time the search contains the bytes field in the run.

Calculated fields can only reference fields that are already present in the event returned by a search. So for calculated fields to perform correctly make sure they are configured to reference a field that has already been extracted.
### field aliases
Allow to assign alternate names to fields in the data. If you have fields from multiple sourcetypes that all contain similar values
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/76029f9a-1b8b-4c70-a9ed-bc438e503d77)
the field alias group together similar values. This allows us to search for all values at once in the shared field alias. field aliases do not replace or remove the original field name so you can search data usin the original name or its alias.

### Lookups
Adds to the events other fields and values that are not part of the indexed data
From `settings` menu

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/426318d3-00fc-42cb-a9bb-d4581ea17958)
in the  `lookups` option
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/fb8a7cf9-50b0-4cb4-805d-7c260ab858d8)

the value pairs can be configured to automatically append to events in the search at search time allowing to add related information

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/08185364-16c8-4d39-9232-e92e4514feda)

## Search time operations order

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ac5363fa-0bd6-4eb9-b34c-4d867edc3650)

`Field extractions` are evaluated first in the pipeline. That means that `Calculated fields` can add additional context to `extracted fields`, but a `field alias` cannot reference a value from a `lookup`

[Back to index](README.md)
