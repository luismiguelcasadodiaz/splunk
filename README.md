# Intro to Splunk
## main functions:
1. Index data. It is the heart (collects data from any source)
2. Search & investigate.
3. Add Knowledge.
4. Monitor & Alert.
5. Report & analyses.

El indexador analiza el flujo entrante. Cuando encuentra un match con un modelo de datos de una fuente lo etiqueta con el sourcetype.
Conocido el sourcetype, descompone el flujo de datos en evento únicos al que se les pones un timestampo normalizado según la zona horaria del ususrio de la cuenta.

Los evento se guardan en el index donde pueden ser investigados con el **Splunk Search Language**. Haremos queries.
A los evento se les peude añadir etiquetas y aportarles conocimiento del dominio de negocio para ayudar a interpretarlos.

Se puedn poner alertas de monitoreso que disparen acciones.

## roles:
### admin
 - Install apps.
 - Ingest data.
 - Create Knowledge objects for all users
 - Defines apps other users can see
### Power
 - Create Knowledge objects for users of an app.
 - Do real-time searches.
### User
 - See only knowledge objects shared with him.


## Apps (pre-configured environments that extend pre-built knowledge and capabilities)
 - two default apps: ``Home app``: (sets a custom dashboard as a default dashboard) and ``Search and reporting app``
 - SplunkBases has hundreds of them
 - We can create our own apps.

### Search and reporting app (has 8 components)
#### 1. Splunk Bar
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b78ab40d-bd01-4044-808a-1e7b96ce6eb5)

menus to navigate
#### 2. Search Bar
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/a34378af-264d-49f5-afd6-bb45c8619348)

Keyword plus time filter
There is a ``save as`` menu to save the search as a knowledge object.
#### 3. Search button
#### 4. Time range picker
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/706673ae-fa4b-4f7a-9995-17494444eeb1)

#### 5. How to search Pannel
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ad6e5cf9-1e2b-4c3e-9e79-d3cb34f20769)

#### 6. Data summary button
Breaks down data  by Host (IP, FQDN, or Hostname), Source or Source type. The source is the data's file or directory path 
#### 7. Table views
Allows data study without Splunk Search Processing language.
#### 8. Search History
To view and rerun past searches
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0993ca01-9687-4592-85f9-82dc31ecae47)

#### 9. Search result tabs
limiting a search by time is key to faster results and it is a good practice.

When the search is sent to Splunk, becomes a ``search job``
wiht te result we got a 

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
Commands that generate statistics or visualizations are called **transforming commands**. Transfomr event data into data tables

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
- Verbose: Field discovery **on**. Returns as much field and even data as possible,
- Smart: toggle mode depending search type we are running.
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/861a1bc6-0bc5-4913-9d94-c5c6d12fe548)

##### Search Timeline

Where it is possible to drill into time axis

![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/80995d7b-a28a-4f1a-bc7a-a817f2b6ce8c)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/64a0a10a-03f5-4818-8a9e-65686130e54f)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/20b22100-6e74-4ca2-9b1f-5c4b92f04a80)
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/d2b70e6c-8a85-4507-9ca3-20a14df72920)

##### Event list
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/9392633b-a693-4f6b-8d49-f687b5485ec3)

##### Fields sidebar
Shows all fields extracted
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/b2db4c0e-9528-4677-a6b2-d26518c335bc)






 

# Splunk Core Certified Power User
Splunk lessons

#### [1. Visualizations](#visualizations)
#### [2. Working with time](#working-with-time)
#### [3. Statistical Processing](#statistical-processing)
#### [4. Comparing Values](#comparing-values)
#### [5. Result Modification](#result-modification)
#### [6. Correlation Analysis](#correlation-analysis)
#### [7.Creating Knowledge Objects](#creating-knowledge-objects)
#### [8. Creating Field Extractions](#creating-field-extractions)
#### [9. Data Models](#data-models)
#### [10. Using Choropleth](#using-choropleth)



---

# <a name="visualizations">1. Visualizations</a>
## Video one: Using Formatting Commands (6:41).
We use Splunk Search Processing Language (SSPL) and Splunk Web Interface (SWI).

Estoy algo confuso con la nomemclatura. ¿Eventos o registros?. ¿Eventos cuando analizamos archivos de log?¿Registros si analizamos tablas de datos?

 - `fields` limita (incluye o excluye) campos en las búsquedas. Por defecto incluye el campo mencionado. Los campos internos `_raw` y `_time` se incluyen por defecto en cada búsqueda. Si no los deseamos hay que indicarlo explicitamente con el operador minus `-`.
 - 
   > `fields product_name price` **agrega** dos campos
   > 
   > `fields -product_name price` **excluye** product_name y **agrega** price
   > 
   > `fields - product_name price` **excluye** product name y price. Atneción al ESPACIO EN BLANCO TRAS EL OPERADOR MINUS.
   
   La inclusion sucede antes que la exclusion. La eficiencia en la búsqueda se logra limitando/reducciendo el número de campos a extraer.
   
 - `table` aunque se parece a `fields` por incluir campos en la búsqueda, es un comando de transformación que retiene los datos en forma tabular. Los campos aparecen en la tabla en el mismo orden en que se mencionan en la instruccion table. Usando conjuntamente la instruccion fields y table la búsqueda es más eficiente, primero `fields` y luego `table`.
   
   > fields JSESSIONSID Price Product_name
   > table JSESSIONSID Price Product_name
   
 - `dedup` Elimina registors de los resultados de búsqueda. puede aplicarse a uno o más campos
   > `dedup product_name price` elimina todas las líneas en las que se repita el nombre de un producto que tenga el mismo precio.
   
 - `addtotals`, suma por defecto todos los campos numéricos de un mismo registro de datos y crea una columna total. El flag `col=true` crea un total de columnas. El flag `row=false` elimina el comportamiento por defecto que genera un total de fila. El flag `label="Total ventas"`nos permite poner una etiqueta a la fila nueva fila que ha creado el flag `col=true`, esta etiqueta la ponemos debajo de la column indicada con `labelfield="product_name"`. el flag `fieldname="total por fila"` personaliza la etiqueta de total de la dila que este comando crea por defecto.

 > ![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/0588b4c2-eee2-4025-83fd-f3c69952c470)

   
 - `fieldformat`, cambia la representación en la presentación de los datos pero no en el origen. `fieldformat Total = "$" + tostring(Totalt, "comas")`
## Video 02: Visualizating data (11:25).
## Video 03: Generating maps (04:50).
## Video 04: Single value visualizations (02:39).
Disponemos de dos modalidades para visualizar valores únicos: El valor numérico en si y un indicador gráfico de los que tenemos:

| el valor numerico en si|Marcas en escala| indicador de llenado  |  calibres radiales |
|----------------|-------------------------------|---------------------------------|----------------------------|
|![Valor](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/76788796-c182-4151-a40f-14fc9f277091)|![Marcas en escalas](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/30eb2ff4-072f-4e71-a299-103744217e77)|![Indicador de llenado](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8926539c-30ed-464f-80b6-90973c12e762)|![Calibres radiales](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c325ea3e-2cf1-4ad4-b9ab-ff8d32dc5310)|

En cualquiera de las modalidades podemos definir segmentos de rangos con diferenes colores.
![Personalización de rangos y colores](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/82a4da04-e269-4bbe-9d40-72e53ab4752c)

Es posible dividir un valor por los elementos de otro campo y mostrar un gráfico tipo trellis.

![formato Trellis](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/2f985a80-f4ec-4535-a2f9-8f270f48b9e0)

En este caso cambiamos la asignación de color al fondo del valor
![image](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/ccae6d80-9ffa-4243-8031-99c21a0349cd

Hay varias posibilidades y es cuastión de presentar la más adecuada para el que tiene que presentar los datos.
![trellis 3](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/6fb8bc66-13f0-46a8-96c7-1fc785f6cabc)



## Video 05: Formatting Visualizatins (02:23).

# <a name= "working-with-time">2. Working with time</a>

# <a name= "statistical-processing">3. Statistical Processing</a>

# <a name= "comparing-values">4. Comparing Values</a>

# <a name= "result-modification">5. Result Modification</a>

# <a name= "correlation-analysis">6. Correlation Analysis</a>
# <a name= "creating-knowledge-objects">7.Creating Knowledge Objects</a>
# <a name= "creating-field-extractions">8. Creating Field Extractions</a>
# <a name= "data-models">9. Data Models</a>
# <a name= "using-choropleth">10. Using Choropleth</a>



![Visualizations available](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/26bad114-0f68-46fc-aabb-8e0c9c595a48)

![Marcas en escalas](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/30eb2ff4-072f-4e71-a299-103744217e77)
![Indicador de llenado](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8926539c-30ed-464f-80b6-90973c12e762)
![Calibres radiales](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c325ea3e-2cf1-4ad4-b9ab-ff8d32dc5310)











