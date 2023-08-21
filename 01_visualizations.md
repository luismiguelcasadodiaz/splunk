[Back to index](README.md)
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


[Back to index](README.md)
