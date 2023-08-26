[Back to index](README.md)

# 03 Statistical Processing
## What is a data series?(01:29)
A data series is a sequence of related data points that are plotted in a visualization:
  - Single Series: Compares values of a simple data category.
  - Multi-Series: Compares values of two or more data categories.
  - Time-Series: Compares values over time, which can be either single or multi-series

Transforming commands can be used in searches to organize your results into a statistical table containing a data series that can be visualized. (Chart, timechart, top, rare, stats)
We will learn how transforming commands can be used to structure searches to generate the results you need for the visualization you want.

## Chart Command (06:57)
Take results and return them formatted into a table that can be displayed as a visualization.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/fe3703b5-aa8f-46e4-976e-9fddf76f78c6)

  - Y-axis is defined with `stats-func(field)`. where `stats-func` is a supported  statistical function:
    
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/07933baf-90ac-4b4e-bd79-c68c3b806339)

  - `field` is a field with numeric values.

  - `over row-spli` specify X-axis and defines the first column in our resulting table. Creates a single-series.
  - `by column-split` Further split data, resulting in multi-series data-series.
  - Further control of our results.
    - span (with categorical fields). By default, Splunk will display individual columns for the top 10 values found in the field used to execute multi-series split (the field after `by`)
    - span (with numerical fields). will group the event into buckets. Splunk Shift overlapped values to the higher grouping. 400 falls into 400-500, instead on 300-400.
    - limit: overrides that top 10 to whatever whole value you find appropriate. Less frequent values than the indicated in `limit` argument get aggregated into the `other` column. ´limit` argument sets a limit across the entire dataset. `limit=0` means no limit at all. When there are too many values to display inside the legend, the list will include a down arrow to scroll through the values.
    - useother=True/False: **Visually** Removes the `OTHER`column. There is no recalculation or research
    - usenull: Removes the `NULL`Column if one exists. it is for events that do not contain the field used to create the multi-series series
      
Each time you invoke the stats command, you can use one or more functions. However, you can only use one ´BY` clause.
unlike the `stats` command, the `chart` command **can only be split over two** fields or dimensions. A chart command with two arguments after the `by` clause   is equivalent to using an over and by clause. The values for a second split are represented by individually colored columns.

Some examples:

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a1e3420e-970a-4294-a436-37e615810fe2)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/87e3b5a5-b617-4965-acc4-2c2f0c803cf9)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d34a75a4-4209-4724-aa48-e14fddbf37d5)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1e111437-fe42-4c57-adf4-7f274039e4b3)





## Timechart Command (07:21)
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

`limit`argument controls the number of values returned for our multi-series split. Without it, we get the top 10 values in 11 lines in our chart, which has an additional `other` series.

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




## Top Command (04:00)
## Rare Command (00:27)
## Stats Command (02:52)
## Functions of the Stast Command (06:56)
## Transforming Commands Summary (01:18)
## Eval Command (06:43)
## Functions of the Eval Command(04:24)
## Eval as a Function (01:06)
## Rename Command (02:38)
## Sort Command (03:11)

[Back to index](README.md)
