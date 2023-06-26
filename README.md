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
Disponemos de dos formatos para visualizar valores únicos: El valor numérico en si y un indicador gráfico de los que tenemos:

| el valor numerico en si|Marcas en escala| indicador de llenado  |  calibres radiales |
|----------------|-------------------------------|---------------------------------|----------------------------|
|![Valor](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/76788796-c182-4151-a40f-14fc9f277091)||![Marcas en escalas](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/30eb2ff4-072f-4e71-a299-103744217e77)|![Indicador de llenado](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/8926539c-30ed-464f-80b6-90973c12e762)|![Calibres radiales](https://github.com/luismiguelcasadodiaz/splunk/assets/19540140/c325ea3e-2cf1-4ad4-b9ab-ff8d32dc5310)|

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











