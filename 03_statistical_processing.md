[Back to index](README.md)

# Statistical Processing


## Index
[01.-What is a data series? (01:29)](#what-is-a-data-series)

[02.-Chart Command (06:57)](#chart-command)

[03.-Timechart Command (07:21)](#timechart-command)

[04.-Top Command (04:00)](#top-command)

[05.-Rare Command (00:27)](#rare-command)

[06.-Stats Command (02:52)](#stats-command)

[07.-Functions of the stats Command (06:56)](#functions-of-the-stats-command)

[08.-Transforming commands Summary (01:18)](#transforming-commands-summary)

[09.-Eval Command (06:43)](#eval-command)

[10.-Functions of the Eval Command (04:24)](#functions-of-the-eval-command)

[11.-Eval as a Function (01:06)](#eval-as-a-function)

[12.-Rename Command (02:38)](#rename-command)

[13.-Sort Command (03:11)](#sort-command)


## What is a data series
A data series is a sequence of related data points that are plotted in a visualization:
  - Single Series: Compares values of a simple data category.
  - Multi-Series: Compares values of two or more data categories.
  - Time-Series: Compares values over time, which can be either single or multi-series

Transforming commands can be used in searches to organize your results into a statistical table containing a data series that can be visualized. (Chart, timechart, top, rare, stats)
We will learn how transforming commands can be used to structure searches to generate the results you need for the visualization you want.

[Back to top](#index)

## Chart Command
Take results and return them formatted into a table that can be displayed as a visualization.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/fe3703b5-aa8f-46e4-976e-9fddf76f78c6)

  - Y-axis is defined with `stats-func(field)`. where `stats-func` is a supported  statistical function:
    
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/07933baf-90ac-4b4e-bd79-c68c3b806339)

  - `field` is a field with numeric values.

  - `over row-spli` specifies the X-axis and defines the first column in our resulting table. Creates a single series.
  - `by column-split` Further split data, resulting in multi-series data-series.
  - Further control of our results.
    - span (with categorical fields). By default, Splunk will display individual columns for the top 10 values found in the field used to execute multi-series split (the field after `by`)
    - span (with numerical fields). will group the event into buckets. Splunk Shift overlapped values to the higher grouping. 400 falls into 400-500, instead of 300-400.
    - limit: overrides that top 10 to whatever whole value you find appropriate. Less frequent values than those indicated in `limit` argument get aggregated into the `other` column. ´limit` argument sets a limit across the entire dataset. `limit=0` means no limit at all. When there are too many values to display inside the legend, the list will include a down arrow to scroll through the values.
    - useother=True/False: **Visually** Removes the `OTHER`column. There is no recalculation or research
    - usenull: Removes the `NULL`Column if one exists. it is for events that do not contain the field used to create the multi-series series
      
Each time you invoke the stats command, you can use one or more functions. However, you can only use one `BY` clause.
unlike the `stats` command, the `chart` command **can only be split over two** fields or dimensions. A chart command with two arguments after the `by` clause   is equivalent to using an over and by clause. The values for a second split are represented by individually colored columns.

Some examples:

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a1e3420e-970a-4294-a436-37e615810fe2)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/87e3b5a5-b617-4965-acc4-2c2f0c803cf9)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d34a75a4-4209-4724-aa48-e14fddbf37d5)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1e111437-fe42-4c57-adf4-7f274039e4b3)

[Back to top](#index)

## Timechart Command
Performs stats aggregations against time and returns a time series chart or table where _time  field is always the X-axis.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/fffb004d-f695-4a3b-ab16-4f8f37c85c3e)

`stats-func(field)` populates the Y-axis. `count` is the only function that does not require field specification.
Function and argument used in `Stat` and `chart` can also be used with `timechart`.

 `by <split-by-field>` spit our result table. A key difference between `chart` and `timechart` is that `timechart` **only supports a single additional split**. This is because the X-axis is automatically segmented or bucketed based on time. Each distinct value of the `split-by-field` will become a series.

 The functional equivalent of the search, using `chart` would be chart count by time and usage, but `timechart` automatically applies a bucket command to set the time span to a preset sampling interval that depends on the time range of  the search. We can see this reflected in the stats table output. Each row represents a chunk or bucket of aggregated data
 
 ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/753088c7-83e0-47e3-b1b1-0d1a4db283ab)


### Default bin span according to the picker time range.

|Time range|Default time bucket|
|----------|-------------------|
|last 30 days|1 day|
|last 7 days|1 day|
|last 24 hours| 30 minutes|
|last hour|1 minute|
|last 15 minutes|10 secodns|

When the period Spluck uses is not appropriate, you can override it using the `span` argument, which forces SPlunk to group bucket on the best-fit time range.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/61cc63db-7cdf-4c1b-bbe7-b01c2b0f4036)

`limit` argument controls the number of values returned for our multi-series split. Without it, we get the top 10 values in 11 lines in our chart, which has an additional `other` series.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ee5890c5-8bd1-46c3-8551-92eb7eb26361)

compared with

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6522c148-0e0b-4b72-a18b-ded02e7df48a)

### chart versus timechart

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0b77c9d6-7919-473c-9182-95e8d0675ff6)
There is no time aggregation

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/49e68674-7739-4849-80d1-cb26144b0782)
Automatically aggregates count in one-day buckets because the time range is 7 days.

When running a multi-series time chart, we have an option for how we want our data to be displayed. As our timechart can sometimes appear more cluttered, we have the option to toggle a feature called multi-series mode. This option shows in `format` `General`  `Multi-series mode`. This will separate out the different series into their own trendline sharing the same X-axis, but with individual  Y-axis that share the floor and ceiling values.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/daf364b9-7490-4ead-bd44-4334260f9e01)


[Back to top](#index)

## Top Command
Finds the most common values from a given **list of fields** in a result set. We can group results together based on a shared field with the `by` clause.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/586a04b2-8fe0-46fc-a553-8f080f3c284a)

By default output top 10 results in table format. This can be overridden with the limit argument
`countfield': Renames the count field specifying a string.
'showperc', Defaults to True. `showperf=f` or  `showperc=0` prevents the percentage column.

### examples 
Which IP addresses generated the most attacks in the last 60 minutes? Without any argument, we get the `count` or number of events and the percentage.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/23fa4cda-8071-4d23-87e1-f66b9e6f27b5)

With only one field: 10 most common values in the Grout field. Column values are unique.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/51ec03a9-ad6a-48b7-83cc-ec0b2a39329a)

With two fields. All combinations of group and name are unique
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/001e3bc4-2566-4b81-aa6a-5914479a1a9f)

two top names by group
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e5d68d98-6646-450b-bd65-eeb38fbe780e)

Two top groups by name
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c92a58c1-fc7a-4be1-99df-4ae485e38a30)


Renaming Count Column
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/378a9575-17c1-4f85-b512-ebae9344fd55)

### run top command from the UI:

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7da88e5c-2d04-4d3a-b30a-4953767b85ea)
Note that when you use this method the limit argument is set by default to 20
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/045565c8-24d3-41fe-b3fd-6f4e285bcc51)

[Back to top](#index)

## Rare Command
Essentially, is the opposite of the top command, which returns the least common values of a result set.. Has the same options., By default, results are sorted in ascending order based on count.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3326fbcd-019c-4357-86fe-c72a4b9b13ff)

[Back to top](#index)

## Stats Command

We produce statistics from our search results with the stats command. The **output is a table**. `by <field list>` clause groups the result for each different value of each field in the field list.  Differently from `chart` and  `timechart`, `stats` allows continuous splitting  of your data. (`timechart` splits only by one field. `chart` command splits by two fields).

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d0c17253-ea63-4931-8e66-63cf9c768d67)

Use `as` clause to rename the resulting column to override default column names according to search syntax. It is a very convenient option to avoid confusion when statistics for several fields are calculated.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/be2c29ed-57e4-4003-b357-744dbe0d27ab)


in `stats` statistical functions can support multiple fields
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c8a9fee8-aec3-4c67-aac0-557ea21a70f1)

`count` differs from `count(field)` in that the former counts all events and the latter counts only events with a value in the field.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3475ff97-4b4a-43a9-b15b-80d989d2e41b)

The order of fields in `by <field list>` has a big  impact on the search results as the data will first be grouped by the first field given, then grouped by the second field given, and so on.

[Back to top](#index)

## Functions of the Stats Command
There are four categories of statistical functions:
  - Aggregate: Summarizes event values to create a single value
    - `count`, `count(x)`, `dc(x) or distinct_count(x)`, `estdc(x)`, and `estdc_error(x)`  estimated count of the distinct values in the field specified.
    - `min(x)`, `max(x)`,  `range(x)`.
    - `sum(x)`, `sumsq(x)`. Sum and sum squares
    - `avg(x)`, `median(x)`, `mode(x)`. Average ignores events without an specific value or without numeric values in the field
    - `stdev(x)`, `stdevp(x)`,`var(x)´, `varp(x)´.
    - `percentile<percentile>(x) or p<percentile>(x)`, `upperperc<percentile>(x)`, `exactperc<percentile>(x)`
  - Event Order: Returns values from fields based on processing order.
    - The `first(x)` seen value in the field x.
    - The `lastst(x)` seen value in the field x.
  - Multivalue: Returns a list of values for a field.
    - list(x): Returns a list of up to 100 values in a field as a multivalue entry. The order of the values reflects the order of input events. 
    - values(x): Returns the list of all distinct values in a field as a multivalue entry. The order of the values is lexicographical.
    - ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/00019d36-d96f-46dc-ae05-d527397ce288)


  - Time: Returns values based on time.
    -   Returns the chronologically `earliest(x)` (oldest) or  `latest(x)` (most recent) seen occurrence of a value in a field.
    -   Returns the UNIX time of the `earliest_time(x)` (oldest) or  `latest_time(x)` (most recent) to calculate the rate of increase for an accumulating counter.
    -   
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1181bd20-7da5-4ad8-a630-5ea7e9aeb6a1)

[Back to top](#index)

## Transforming Commands Summary
`stats`, `chart`, and `timechart` share similar features. Use **proper** command to get wanted results: `stats` for the table, and the others for visualizations.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/56146202-fdeb-4f2e-8a05-d35f227356a7)

[Back to top](#index)

## Eval Command
Performs calculations with values in our data.
An eval expression is a combination of literals. fields, operators, and functions that represent the values of the destination field.
Calculates the expression and puts the resulting values into a new field or overwrites an existing one.
Creates a new field on the fly, populated with the expression's result, that can be used as any regular field in the remainder of the search expression.
Nothing written with the eval command is kept after the lifetime of the search it was used in. The new field **is not saved** in the index nor it will be available again after the search is completed.
Either that the eval command temporally can overwrite the values present in a previously existing field, no change of our data is permanent. **New values are not written to disk** anyway.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4fc5d8d9-e56f-41f5-ba49-47e00d51bba5)

Eval involves:
  - Mathematical operation.
  - String concatenation. Use `+` for String or character and  `.` for any data type.
  - Comparison expression.
  - Boolean expressions.
  - A call to an `eval` function.
    These are the operators
    ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/acb52173-a065-4fc6-94d3-5592062ff57d)

### Eval Syntax
Field values are case-sensitive
Strings must be double-quoted
Field names must be single-quoted when contain special characters
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f7e0fdcc-7309-468b-8e09-9cd146993e01)

### Usage examples
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/dd5628ed-800c-46d4-a171-3b08f3202484)![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a76ae2dd-dc6c-4685-a18a-72e062675bf8)![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/63092157-753a-4455-b787-df5618dd772e)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/22cf7943-b588-4787-9ef6-37d57953be57)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/53c3fa7d-d755-4d83-9e49-8a583c7b2fdf)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/4113d108-4f30-4388-94c2-ddfa40f96a3e)

[Back to top](#index)

## Functions of the Eval Command
There are 11 categories of [evaluation functions](https://docs.splunk.com/Documentation/Splunk/9.1.0/SearchReference/CommonEvalFunctions)
- Comparison & Conditional
- Conversion
- Cryptographic (md5, sha1, sha256, sha512)
- Data & time
- Informational
- JSON
- Mathematical (round(X,Y), pow). A `round` without `Y` returns `X` as an integer. 
- Multivalue
- Statistical (avg, max, min, random). `random` returns a Pseudo-random integer ranging from zero to 2³¹-1
- Text
- Trigonometry and hyperbolic

Generally, Evaluation functions will evaluate an expression based on the events and return a result, but some do not evaluata any expression and instead return a result based on its own functionality

### Examples
Create five random groups of users.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2a122143-4a9e-494c-95c4-4a3fbe78c172)

Eval usage without functions.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c8672b97-3b0a-4ad3-8384-93b8c68321c7)

[Back to top](#index)

## Eval as a Function
The eval command can be used as a function within the `stats` command. 
Nest eval inside a `stats count` to count events with a calculated value.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/fc6663b6-337e-4e6e-8c08-12d452801767)

**Requires** an `as` clause to rename the field.

[Back to top](#index)

## Rename Command
Helps to display a more useful or meaningful field name.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5aabcc13-199c-468d-b53f-998c84f34551)

Double quote the new field name if has to contain any special character.
Multiple field renaming is possible in a single command. **notice commas**
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f822f2e1-26f2-433b-b387-144db0e3232d)

Once a field is renamed Splunk will only respond to or be able to use the new name of that field in the rest of the search.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f418ba66-3eb9-4afb-9d33-b985ba03419b)

Wildcare usage in renaming fields

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2e05d9a7-46ff-460a-8a93-9eaca8cc1e1e)

[Back to top](#index)

## Sort Command
Sorts in ascending order by default. `-` changes it to descending order. `+` is implicit so not required.
Double quote field name when containing special characters or white spaces.
limit the number of results with the `limit` argument or just put an integer.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/09ecfaa9-5c5e-4fc8-9391-96233d803228)

Splunk determines the data type of values present in the field and sorts appropriately:
  - Alphabetic Strings: Lexicographically. **uppercase letters before lowercase**
  - numbers: Numerically
  - Combination: Depending on the first character lexicographically or numerically.

### Examples
Please notice the white spaces after `-`, it applies to both fields. In the first example, orders descend on both of them. But in the second example, without white space,  `-` only applies to the first field being the second field ordered in ascending mode.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/42c979a9-6256-40d3-bb4e-ed88d472ba76)![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3cd1d008-130a-49e9-a4fa-108e4dbc8d23)

[Back to top](#index)

[Back to index](README.md)
