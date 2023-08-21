# Splunk Core Certified Power User
Splunk lessons

#### [00.- Intro to Splunk](#intro-to-splunk) 
#### [01.- Visualizations](#1-visualizations)
#### [02.- Working with time](#2-working-with-time) KO
#### [03.- Statistical Processing](#3-statistical-processing) KO
#### [04.- Comparing Values](#4-comparing-values)  KO
#### [05.- Result Modification](#5-result-modification) KO
#### [06.- Correlation Analysis](#6-correlation-analysis) KO
#### [07.- Creating Knowledge Objects](#7-creating-knowledge-objects) KO
#### [08.- Creating Field Extractions](#8-creating-field-extractions) KO
#### [09.- Data Models](#9-data-models) KO
#### [10.- Using Choropleth](#10-using-choropleth) KO
#### [11.- Using Fields](#11-using-fields)
#### [99.- Quizzes](#zz-quizzes)

[Back to index](#splunk-core-certified-power-user)
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






---
[Back to index](#splunk-core-certified-power-user)
# 1 Visualizations
I will learn how to visualize and format data into tables and charts using Splunk Search Processing Language (SPL) and Splunk Web Interface (SWI).
## Video one: Using Formatting Commands (6:41).
We use Splunk Search Processing Language (SSPL) and Splunk Web Interface (SWI).

Estoy algo confuso con la nomemclatura. ¿Eventos o registros?. ¿Eventos cuando analizamos archivos de log?¿Registros si analizamos tablas de datos?

 - `fields` limita (incluye o excluye) campos en los resultados de las búsquedas. La restricción de campo hace las búsquedas más rápidas.

    Por defecto incluye el campo mencionado. Los campos internos `_raw` y `_time` se incluyen por defecto en cada búsqueda. Si no los deseamos hay que indicarlo explicitamente con el operador minus `-`.

 - ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0c34fd13-bae9-4f7f-8b72-ddbbb4faa560)

   > `fields product_name price` **agrega** dos campos
   > 
   > `fields -product_name price` **excluye** product_name y **agrega** price
   >
   > ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a03daeff-d6b4-4559-a1c0-3f13bc69459c)

   > `fields - product_name price` **excluye** product name y price. Atneción al ESPACIO EN BLANCO TRAS EL OPERADOR MINUS. EL espacio en blanco hace que el menos afecte a todos los campos enumerados en la lista.
   
   La extracción de los datos referidos por los campos es una de las partes más costosas de la búsqueda. La `inclusión` de los campos se ejecuta antes la
    `Extracción`. La eficiencia en la búsqueda se logra limitando/reducciendo el número de campos a extraer.
   
 - `table` aunque se parece a `fields` por incluir campos en la búsqueda, es un comando de transformación que retiene los datos en forma tabular. Los campos aparecen en la tabla en el mismo orden en que se mencionan en la instruccion table. Usando conjuntamente la instruccion fields y table la búsqueda es más eficiente, primero `fields` y luego `table`. cada fila de la tabla representa un evento.
   
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/cb19b77e-ffa9-40d1-9520-9bcfd2efc284)

   
 - `dedup` Elimina registros con valores repetidos de los resultados de búsqueda. Puede aplicarse a uno o más campos
 - 
 ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ab941cf1-73c7-4a29-978a-b646d70ced0b)

   > `dedup product_name price` elimina todas las líneas en las que se repita el nombre de un producto que tenga el mismo precio.
   
 - `addtotals`, suma por defecto todos **los campos numéricos de un mismo registro/evento de datos** y crea una columna total.
 
 ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/251acb06-54d7-4271-af98-232773878232)

El flag `col=true` crea un total de columnas. El flag `row=false` elimina el comportamiento por defecto que genera un total de fila. El flag `label="Total ventas"`nos permite poner una etiqueta en la fila nueva fila que ha creado el flag `col=true`, esta etiqueta la ponemos debajo de la column indicada con `labelfield="product_name"`. el flag `fieldname="total por fila"` personaliza la etiqueta de total de la dila que este comando crea por defecto.
   
 - `fieldformat`, cambia la representación en la presentación de los datos pero no en el origen. `fieldformat Total = "$" + tostring(Totalt, "comas")`
 - ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/aa480df8-6809-44ef-9ac9-15d865e14b8e)

   
## Video 02: Visualizing data (11:25).
Any search that returns statistical values can be viewed as a chart.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/5c536650-c195-4f9a-9e37-76a4e86e13de)

You can roll over the chart to see the values of each chart element.
You can drill down to events represented by a chart element.
Most visualizations require results structured as tables with at least two columns. In the statistic tab, you can see how many columns or **single series** are available. The first single series provide de x-axis values and the second single series provides de y-axis values.
You can hover the legend to select on single series

### Transforming commands to order search results into a data table.
#### top finds the most common values of given fields
By default shows the top ten. 

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c0c6855f-55c1-46da-89b4-af87cb2299a9)


|clauses| action|
|:-------|------------:|
| limit = int |`limit=20` show the top twenty. `limit=0`shows all|
| countfield = string| Changes the title of the column `count`|
| percentfield = string| Changes the title of the column `percentage`|
| showcount = True/False|Shows/hides the column `count`|
| showperc = True/False | Shows/hides the column `percentage`|
| showother = True/False| Shows/hides the column `others` with the count numbers for results not within the limit|
| otherstr = string|Changes the title of the column `others`|


#### rare
igual que top pero con los valores menos frecuentes.
#### stats
Produces statistics from our search results
[There are about 35 different functions inside this command. its study is out of the scope of this module.]  (https://docs.splunk.com/Documentation/Splunk/latest/SearchReference/CommonStatsFunctions)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c2574950-1365-43c1-b0a9-795ae4b202ec)



#### chart
Can take two clause statements. the `over` clause tells which field you want to be on the x-axis. `by` clause allows you to split data by an additional field. Only one field can be specified after the `by` clause when using the `over` clause. 

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0a7753f0-8616-4968-95e1-b649b75b3143)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8ae82d4c-0a4f-4714-8810-4d39c4ce2f92)

If we use two fields after a `by` clause without the over clause, the first field will be used as the `over` clause.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e7bd8ed9-566f-4e93-abdf-3e6636d37a8a)


![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/42c666b7-3ccd-4498-aa08-ec2fa3a83008)

Los eventos sin contenido en el campo de la claúsula 'by' se agrupan bajo la etieta NULL. POdemos eliminarlos con el argumento `usenull=f`.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ab986c2a-2d21-4b83-9591-94bcef1c04ef)

`chart`por defecto está limitado a 10 single series. Las otras las agrupa en la serie `OTHER` que podemos quitar con el comando`useother=f`.


Tanto `usenull` como  `useother` default to True, por lo que si no se especifica nada NULL y OTHER aparecerá en el Chart.
La claúsula `limit` ajusta el número de **single series** a mostrar en el chart. `limit=0`los muestra todos.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/65d4b5c9-93d4-41c0-82c2-f7d58ef84a17)


#### timechart
Performs stats aggregations against time. Time is always the X-axis. By default, clusters data in time intervals dependent on the time range selected. That behavior can be changed with `span` command

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/356d48ce-0ae8-4203-9551-86dd19ac40e1)


`usenull` y `useother` también están disponibles en `timechart`

#### trendline
Computes the moving average of field values over a period of time giving a clear understanding of how data is trending

|Trendtype|Function|Behavior|
|:--------|:----:|-------------------|
|Simple moving average| SMAtp| Sums data points over a period of time. |
|exponential moving average| EMAtp| Sums data points over a period of time. Assign a heavier weight to more current data points.|
|weighted moving average| WMAtp| Sums data points over a period of time. Assign a heavier weight to more current data points.|

The `time period ` has to be between two and ten thousand (2 .. 10 000)

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a7b1584f-780e-487c-92d1-9401a0368207)
 In this chart whose time range is 7 days the trend line shows that `WMA2` for 2 days

## Video 03: Generating maps (04:50).
Maps represent data including geographic information.
There are some commands that let pull geographic data from the machine data
Interactive Marker maps plot geographic coordinates on a world map.
Choropleth maps use shading to show relative metrics for **predefined** geographic regions.

### iplocation 
Look up and add location information from a third-party database to an event. City, country, region, Latitude, and longitude can be added to events that include external IP addresses. Some location information may not be available for particular IP addresses. this is the nature of geolocation and has to be taken into consideration when searching data. in this case, no additional location information will be added to the event.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7376c278-fbb7-49ce-972d-ec3eec791b7d)
Comparing these two images we can see how location fields show up inside the field sidebar
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/dd63e1b8-af83-4483-b240-d1f211d7dcce)



### geostats
Uses the same functions as the `stats` command but only accepts **one** `by` argument. Column count can be controlled with  `globallimit`
Gestats needs a `latfield` and a `longfield`.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/7920df2c-bab5-4d39-b705-224f5763ea6e)

### When geostats uses the enriched fields from iplocation (lat & lon)
The default names from `iplocation` for `latitude` is `lat` and for `longitude` is `lon`. Feeding these fields into geostats gives a quick geolocation of the accesses to our servers.

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/40a552fb-0742-41f7-a95d-b8e379f24bb2)

## choropleth Maps
Choropleth maps use shading to show relative metrics for **predefined** geographic regions.
we need compressed Keyhole Markup Language files (KMZ) defining region boundaries.
Splunk ships with two KMZ:

- geo_us_states.kmz
- geo_countries.kmz


`geom` add to our events fields that include geographical data structures that match polygons in our map. `geom` requires a KMZ file (also known as a **featureCollection**) where to lookup in his country name a `featureIdField` from my search results.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/e90d8d29-4f18-4f58-983c-954ed46a9deb)


## Video 04: Single value visualizations (02:39).
Disponemos de dos modalidades para visualizar valores únicos: El valor numérico en si y un indicador gráfico de los que tenemos:

| el valor numerico en si|Marcas en escala| indicador de llenado  |  calibres radiales |
|----------------|-------------------------------|---------------------------------|----------------------------|
|![Valor](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/76788796-c182-4151-a40f-14fc9f277091)|![Marcas en escalas](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/30eb2ff4-072f-4e71-a299-103744217e77)|![Indicador de llenado](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8926539c-30ed-464f-80b6-90973c12e762)|![Calibres radiales](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c325ea3e-2cf1-4ad4-b9ab-ff8d32dc5310)|

En cualquiera de las modalidades podemos definir segmentos de rangos con diferenes colores. Once the color range format is set, it stays persistent over the radial, filler or marker gauges.
![Personalización de rangos y colores](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/82a4da04-e269-4bbe-9d40-72e53ab4752c)

Es posible dividir un valor por los elementos de otro campo y mostrar un gráfico tipo trellis. Cuando hay varias visualizaciones mostradas la búsqueda de los datos se ha ejecutado una sola vez para todos

![formato Trellis](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2f985a80-f4ec-4535-a2f9-8f270f48b9e0)

En este caso cambiamos la asignación de color al fondo del valor
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ccae6d80-9ffa-4243-8031-99c21a0349cd)

Hay varias posibilidades y es cuastión de presentar la más adecuada para el que tiene que presentar los datos.
![trellis 3](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6fb8bc66-13f0-46a8-96c7-1fc785f6cabc)



## Video 05: Formatting Visualizatins (02:23).
In the statistics tab, the format that applies to the table. we can overlay a heatmap over the values or a max min shadow.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ad89fbe3-9978-4737-8e11-5bbad0933bc7)

[Back to index](#splunk-core-certified-power-user)
# <a name= "working-with-time">2. Working with time</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "statistical-processing">3. Statistical Processing</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "comparing-values">4. Comparing Values</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "result-modification">5. Result Modification</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "correlation-analysis">6. Correlation Analysis</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "creating-knowledge-objects">7.Creating Knowledge Objects</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "creating-field-extractions">8. Creating Field Extractions</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "data-models">9. Data Models</a>
[Back to index](#splunk-core-certified-power-user)
# <a name= "using-choropleth">10. Using Choropleth



![Visualizations available](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/26bad114-0f68-46fc-aabb-8e0c9c595a48)

![Marcas en escalas](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/30eb2ff4-072f-4e71-a299-103744217e77)
![Indicador de llenado](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8926539c-30ed-464f-80b6-90973c12e762)
![Calibres radiales](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c325ea3e-2cf1-4ad4-b9ab-ff8d32dc5310)


[Back to index](#splunk-core-certified-power-user)

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

[Back to index](#splunk-core-certified-power-user)
# zz Quizzes
## 
1.- What is the most efficient way to limit search results returned.
 - index
 - source
 - host
 - **time**

2.- By default, who is able to view a saved report?
 - Any power or admin user
 - **The user who created it.**
 - Any user with a viewport capability

3.- Which of the following booleans can be used in a search?
 - **OR**
 - ALSO
 - **AND**
 - **NOT**

4.-Which character is used in a search before a command:
 - **Pipe** (|)
 - Backtick (`)
 - Quotation mark(")
 - Tilde (~)

5.- Which search mode behaves differently depending on the type of search being run?
 - Verbose
 - **Smart**
 - Variable
 - Fast

6.- Which of the following searches will return the words dail, failure, or failed?
 - fail
 - dail+
 - *fail
 - **fail***

## Quiz Using Fields 100% with bold answers.
1.- In the fields sidebars, **interesting fields** occur in at least ______ of resulting events.

  - 50%
  - 3%
  - **20%**
  - 10%
    
2.- To **remove** fields from a seach, you would use the _______ command.
  - +fileds
  - fields+
  - **fields-**
  - -fields
    
3.- At search time, in an event that has an equal (=) sign, the data to tl left is treated as _______, and the data to the right is treated as ______.
  - field name, sourcetype
  - lookup, value
  - **field name, value**
  - lookup, sourcetype
   
4.- Which of the following fields are default selected fields?
  - **host**
  - **sourcetype**
  - index
  - **source**
    
5.- True or False: Once you rename a field, the new field name must be used in the rest of the search string.
  - **True**
  - False
    
6.- The fields command allows you to do which of the following:
  - **exclude fields (fields -)**
  - **include fields (fields  )**
  - **include fields (fields +)**
    
7.- True or False: Field are Knowledge objects:
  - **True**
  - False
    
8.- At search time, _____ extract fields from raw event data.
  - **field discovery.**
  - field extractor.
  - field command.
