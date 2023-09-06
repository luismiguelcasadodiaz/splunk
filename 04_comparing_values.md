[Back to index](README.md)
# Comparing values
## Index
[01.-Using eval to compare (7:22)](#using-eval-to-compare)

[02.-Evaluation functions (3:28)](#evaluation-functions)

[03.-Eval: if function (2:40)](#if-function)

[04.-Eval: case function (4:13)](#case-function)

[05.-Eval: validate function (1:15)](#validate-function)

[06.-Eval: in function (2:18)](#in-function)

[07.-Eval: match function (4:57)](#match-function)

[08.-Eval: replace function (5:38)](#replace-function)

[09-Fieldformat command (2:05)](#fieldformat-command)

[10.-Fillnull command (2:16)](#fillnull-command)

[11.-Where  command (8:17)](#where-command)

[12.-My own trials ](#my-own-trials)




## Using eval to compare

We will compare values in our data using conditional statements and commands.
The `eval` command calculates an expression then puts the resulting value into a new or existing field, which can be reused in the search pipeline. When used with  an existing field the eval command overwrites the values of the field with the result of the eval expression at search time **not changing or overwritting any of the indexed data.**.  When we create a new field it will take the values of the expressions but no new data is written into the index. No alteration of the original index happens.

### Supported operators.
the  `+` operator accepts two numbers for addition or two strings for concatenation. The `.`operator concatenates both strings and numbers. Numbers are concatenated in their string representative form.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2fc0132b-704e-4afd-abef-9b6fb66dc08e)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f9cea730-3af2-419f-a7f3-fa2bba7f2d3c)

Field values created using the eval command are treated in a case sensitive manner.
Field names must be unquoted or single quoted when they include an special character like space.
### case example.
Categorization of states in function fo sales.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/21040f49-1858-42ce-9897-9eab8aa45b3a)

### in example.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2c568d8c-10b8-4faa-b0a6-75e3455bcbb3)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8e3d09c9-f2cc-4643-9c3b-2efe82438438)

### Three ways of writting 
Separated, nested or linked with commas.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/74ee7004-5b22-4179-955c-8185e98ae08e)

[Back to top](#index)

## Evaluation functions

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

Genearlly, Evaluation functions will evaluate an expression based on the events and returns a result, but some not evaluata any expression ans instead return a result based on its own funcionality.

We can use these functions with other commands such as `where`, `fieldformat` 
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c2947a62-2551-401c-ba1a-d62fe300f06c)

[Back to top](#index)

## if function

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/728cf1c7-fd01-4a67-be19-09b79f07e0de)
The new field created with the eval command shows in the field sidebar. We can make it a selected field to display it along the bottom row of each event.

[Back to top](#index)

## case function

Will evaluate multiple boolean expressions and return a value based on these multiple else/if statements.
The `case function allows as to enter multiple boolean expresions separated by the argument of what to return if previous expresion evaluates to true. **Only** the argument of the **first expression that evaluates as true will be returned**. if none of the expressions return true, an null value is returned.

### data normalization example
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/58457845-5bb0-4f29-b706-868142910a32)

Case with last condition to `true()` or `1=1`.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c986cf16-eadb-4ff1-bfd8-bcf4b5dc4a97)

[Back to top](#index)
## validate function

The `validate` function works exactly as the `case` except instead evaluating whether or not a statement is true, it returns an argument when an expresion evaluates to false.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8cac3e5e-830f-4f2c-99ac-e5e9b298ee29)

### Example.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/53f7b67a-1403-4c43-bb32-0e802c9d0520)

[Back to top](#index)
## in function
Allows evaluate a value from a field against  a list of possible values and **returns a value of true** it if finds a match. To be  nested in a `if` or `case` function when used in an `eval` command. When used in the `where`command does not requires to be nested inside `if` or `case` functions,
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/de452b46-a714-4a6e-8f67-7322160086b3)

### Example.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f038223e-4da1-49dd-8014-063da6d83093)


[Back to top](#index)
## match function
Matching functions that return true or false if a supplied condition is matched by returned values.
### searchmatch
The `searchmatch` function is a function of the `eval` command the must be embedded wihtin the `if` function of the `eval` command. it will return true or false  depending on whether an **event matches** the search string  passed in as an argument.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/896809f7-b904-4414-bdc8-4eabeab336a1)

#### Examples.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0f1932e0-95e9-491e-b4c8-83d002d1c2e0)


### cidrmatch
The `cidrmatch(x, Y) ` eval function will return true or false if the IP address passed in `Y` matched the subnet specified by `X`.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0b77a1b3-b25f-4cc9-84bc-3248839cf0cf)


### match
The `match(SUBJECT, "<regex>")` uses a regular expression to match on the `SUBJECT`argument returning true if Matche happens.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f32f8898-a501-4590-96c8-cb1873ff6e63)

`match` can be made to behave like the `searchmatch` function passing `_raw`  subject field. `searchmatch` **by default works off of the _raw data**.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b4fec75d-865e-4568-b9ae-91b46c7a9b63)


[Back to top](#index)
## replace function
To replace characters in field's values. `replace` is helpful for **masking**, **at search time**,  any sensitive information within the data, such as exposed accoutn codes, DNI, credit card numbers, **which should ideally be masked prior to onboarding the data into Splunk**. 
`X` is a string of fieldname.
`Y` is a regular expression to be matched on the values in `X`.
`Z` the value to replace the `X` vaues that match `Y` regular expression.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/f27e058d-fb6d-4e14-83f5-0181bdc9a1db)

### Examples.
Masking 4 last digits of an account code.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0f3fcf6a-943f-4f27-8c85-36ee352219c3)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/620d7399-13cc-49da-97bb-31769b0cb41f)

Masking central octets of an ip address.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d9f0e99d-ce82-45d3-be42-f26c96e41a0e)

[Back to top](#index)
## Fieldformat command
To format values without changing the underlaying value characteristics. `fieldformat` command uses the same functions as the `eval` command.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c8de7860-2738-4bc1-b045-b72cd2075b6e)

Once these results are formatted they cannot be modified  by any subsequent commands

### Example.
Format a numeric result into an string wiht commas.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/39142fc9-d5e7-4ff0-a372-7f858ef5cc93)


[Back to top](#index)
## Fillnull command
When the results of a search contains **null values** and the results display with **empty fields**, they can be subtituted for a more readable output wiht the `fillnull` command. By default `fillnull` replaces null values inside all fielsd with zero. Instead of zero, a different value can be indicate with `value = "N/A"`. Use the `field-list'  to restrict the fields where null values will be replaced.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/46545b92-d146-4c19-b4b6-e2fc6cf3deb7)

### Example.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0e4da910-2ce5-466d-8dcc-57e04dd39abb)


[Back to top](#index)
## Where command

`where` uses same syntax as the `eval` command and support same functions but filters the events to only keep the results that evaluate the expression as true. 
Interprets **unquoted or single quoted strings as fields** and **double quoted strings as field values** and treats field values in case-sensitive manner.

Comparing `search` and  `where` commands, `where` **allows**  for field-on-field comparison, use mathematical and boolean operators (with case-sensitiviness)  to evaluate values with in the eval expression returning true or false. The `search` command **does not support** field-on-field comparison.


![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8b2e2265-1239-44fa-be3c-7d4763e12513)

### Operators 

![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/73a8ed38-b41d-4d19-88e6-0149acc18822)

### Boolean operator precedence rules

![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/279759d4-5451-4478-b8f7-3a54af9720c2)

### wildcard % and _

`where` command interprest `*` , the `search` command wildcard, as a literal character  or a mathematical operator. Use instead `%` for multiple characters and `_` for a single character. Use them either with the `like` operator or the `like(string, pattern)` function.

![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6dc58ef2-7631-4cf6-b6c8-1023cff35f29)

### Example.
Filter usersname starting with adm.

![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/789774d2-4d31-4456-aef9-fb79a40ff556)

Filtering null values.

![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7a5bffa6-4a4c-4b18-b759-d907ebbe3549)

Identify period of times with no sales.

![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e8cadeb3-7348-43ab-8baa-baa0503c68da)

[Back to top](#index)

## My own trials 
Visualize evolution on time of partition space usability.
![imagen](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9469c7eb-889f-438a-a1cf-bd781c2a4533)

Count how many events fall in each quartil according the normalized value of data.Key_count
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7ac54f37-e635-470d-8146-1abb6e9b7aca)


[Back to top](#index)

[Back to index](README.md)
