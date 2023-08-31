[Back to index](README.md)
# comparing values
## index
##### [Using eval to compare](#using-eval-to-compare)
##### [-Evaluation functions](#evaluation-functions)
##### [-Eval: if function](#if-function)
##### [04.-Eval: case function]() (4:13)
##### [05.-Eval: validate function]() (1:15)
##### [06.-Eval: in function]() (2:18)]
##### [07.-Eval: match function]() (4:57)
##### [08.-Eval: replace function]() (5:38)
##### [09-Fieldformat command](#fieldformat-command) (2:05)
##### [10.-Fillnull command](#fillnull-command) (2:16)
##### [11.-Where command](#where-command) (8:17)





## Using eval to compare(7:22)
We will compare values in our data using conditional statemenst and commands.
The `eval` command calculates an expression then puts the resulting value into a new or existing field, which can be reused in the search pipeline. When used with  an existing field the eval command overwrites the values of the field with the result of the eval expression at search time **not changing or overwritting any of the indexed data.**.  When we create a new field it will take the values of the expressions but no new data is written into the index. No alteration of the original index happens.

### Supported operators.
the  `+` operator accepts two numbers for addition or two strings fro concatenation. the `.`operator concatenates both strings and numbers. Numbers are concatenated in their string representative form.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2fc0132b-704e-4afd-abef-9b6fb66dc08e)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f9cea730-3af2-419f-a7f3-fa2bba7f2d3c)

Field values created using the eval command are treated in a case sensitive manner.
Field names must be unquoted or single quoted when they include an special character like space
### case example
Categorization of states in fucntion fo sales.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/21040f49-1858-42ce-9897-9eab8aa45b3a)

### in example
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2c568d8c-10b8-4faa-b0a6-75e3455bcbb3)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8e3d09c9-f2cc-4643-9c3b-2efe82438438)

### three ways of writting 
Separated, nested or linked with commas.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/74ee7004-5b22-4179-955c-8185e98ae08e)

[Back to top](#index)

## Evaluation functions(3:28)
There are 11 categories of [evaluation functions](https://docs.splunk.com/Documentation/Splunk/9.1.0/SearchReference/CommonEvalFunctions)
- Comparison & Conditional (THis is not a full list, just a few of them)
  ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/3d2e868b-a938-4ce9-9798-f4fcd11a48cc)
  ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/375ca22c-3ae7-4eaa-8113-3be213c0f469)

  
- Conversion
- Cryptographic (md5, sha1, sha256, sha512)
- Data & time
- Informational
- JSON
- Mathematical (round(X,Y), pow). A `round` without `Y` returns `X`as integer. 
- Multivalue
- Statistical (avg, max, min, random). `random`returns a Psudo-random integer ranging from zero to 2³¹-1
- Text
- Trigonometry and hyperbolic

Genearlly, Evaluation functions will evaluate an expression based on the events ans returns a result, but some not evaluata any expression ans insteead return a result based on its own funcionality

We can use these functions with other commands such as `where`, `fieldformat` 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c2947a62-2551-401c-ba1a-d62fe300f06c)

[Back to top](#index)

## if function (2:40)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/728cf1c7-fd01-4a67-be19-09b79f07e0de)
The new field created wiht the eval command shows int the field sidebar. We can make it a selected field to display it along the bottom row of each event.
[Back to top](#index)

## Eval: case function (4:13)
Will evaluate multiple boolean expressions and return a value based on these multiple else/if statements
[Back to top](#index)
## Eval: validate function (1:15)
[Back to top](#index)
## Eval: in function (2:18)
[Back to top](#index)
## Eval: match function (4:57)
[Back to top](#index)
## Eval: replace function (5:38)
[Back to top](#index)
## Fieldformat command(2:05)
[Back to top](#index)
## Fillnull command(2:16)
[Back to top](#index)
## Where command(8:17)


[Back to index](README.md)
