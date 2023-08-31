[Back to index](README.md)
# comparing values
## index
##### [Using eval to compare](#using-eval-to-compare)
##### [Evaluation functions](#evaluation-functions)
##### [Eval: if function](#if-function)
##### [Eval: case function]() (4:13)
##### [Eval: validate function]() (1:15)
##### [Eval: in function]() (2:18)]
##### [Eval: match function]() (4:57)
##### [Eval: replace function]() (5:38)
##### [Fieldformat command](#fieldformat-command) (2:05)
##### [Fillnull command](#fillnull-command) (2:16)
##### [Where command](#where-command) (8:17)





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
Separates, nextes or liked with commas
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/74ee7004-5b22-4179-955c-8185e98ae08e)





## Evaluation functions(3:28)
## if function (2:40)
## Eval: case function (4:13)
## Eval: validate function (1:15)
## Eval: in function (2:18)
## Eval: match function (4:57)
## Eval: replace function (5:38)
## Fieldformat command(2:05)
## Fillnull command(2:16)
## Where command(8:17)


[Back to index](README.md)
