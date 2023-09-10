[Back to index](README.md)
# Result Modification
How to modify result sets and normalize data using Commands and functions.

## Index
[01.-Appendpipe Command (09:50)](#appendpipe-command)

[02.-Eventstats Command (08:54)](#eventstats-command)

[03.-Streamstats Command (06:09)](#streamstats-command)

[04.-Xyseries Command (02:21)](#Xyseries-command)

[05.-Untable Command (02:48)](#untable-command)

[06.-Working with Xyseries and Untable (12:11)](#working-with-xyseries-and-untable)

[07.-Foreach Command (01:52)](#foreach-command)

[08.-Modifing Field Values with Eval (11:57)](#modifing-field-values-with-eval)

[09.-Eval Conversion Functions (11:14)](#eval-conversion-functions)

[10.-Eval text Functions (06:12)](#eval-text-functions)

[11.-Eval Substr Functions (02:25)](#eval-substr-function)

[12.-Eval Coalescence Function (02:07)](#eval-coalescence-function)



## Appendpipe Command
The `appendpipe` command will allow us to take existing results and push them into the **sub pipeline**, meaning the results of the search specified in the `appendpipe` command are appended to **the end/bottom of the outer result set**. the sub pipeline is executed when Splunk reaches the `appendpipe` command:
  - Contains one or more transforming commands.
  - Does not overwrite original results; instead, appends output as new lines to the bottom of the original result set.
  - Multiple `appenpipe` commands can exist in a search.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3d8aaae3-5760-4b7b-bdb2-34241e2500b4)

The `appendpipe` command is preceded by a `search (...|) ` command and then followed in square brackets by the sub pipeline. The results of the wrapped-in-brackets search are what are appended to the results of the outer/previous/preceding search.

This command helps me to add a subtotal lines in a report.

### Example

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/bf0f46a0-4878-4951-bd6f-5c4bf0f29b58)


### my own trial
From the free cloud trial....

`index="_internal" component=Metrics name=parsing`. I will process only the events with the value "Metrics" in the `component` field and the value "parsing" in the field `name`.

I want the average executions by processor and ingest pipe. I will add a sub-average  row per processor and a grand average per the last 15 minutes.

The search `index="_internal" component=Metrics name=parsing | stats avg(executes) as my_avg by the processor, ingest_pipe`, produces this table (a 3-column table).

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0d75c0c7-1545-477b-9b19-7f55a4467cf6)

The `appendpipe [stats avg(my_avg) as my_avg by processor ` command appends at the end a table with the average per processor such as this one. (a 2-column table). Please notice that `appendpipe` search uses the given name to the aggregation column of the outer/previous/precedent search `my_avg` .

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/05f74164-9cc1-49cb-ad34-41d9ce2f9fe8)

The command `sort processor` sorts the rows in such a way that subtotal rows appear at the end of each `processor` value.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5b230c9d-9391-4389-a521-05bc8470a63e)

To fill in the third column of the latter 2-column table, I create with 'eval' command  a new column `eval ingest_pipe = "Average for ". processor`.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/1216eca3-4058-4e37-899f-ef5445ac3240)

Finally, to add a grand Average, I need to calculate the averages of the processor's average. I do that with a new `appendpipe` command that aggregates the table's rows  lines with "Average for". 
`| appendpipe [ search ingest_pipe = "Average for*" | stats avg(my_avg) as my_avg | eval ingest_pipe = " ===== ALL PROCESSOR AVERAGE ======"]`

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/32f08e79-928d-4a5e-94c1-a6ca8f480038)

Here is the full search command.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c3a59e71-c752-4ad4-8b7f-2406319afc99)



[Back to top](#index)

## Eventstats Command

[Back to top](#index)

## Streamstats Command

[Back to top](#index)

## Xyseries Command

[Back to top](#index)

## Untable Command

[Back to top](#index)

## Working with Xyseries and Untable

[Back to top](#index)

## Foreach Command

[Back to top](#index)

## Modifing Field Values with Eval

[Back to top](#index)

## Eval Conversion Functions

[Back to top](#index)

## Eval text Functions

[Back to top](#index)

## Eval Substr Function

[Back to top](#index)

## Eval Coalescence Function

[Back to top](#index)
