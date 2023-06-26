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
## Video one : Using Formatting Commands
We use Splunk Search Processing Language (SSPL) and Splunk Web InterfaceSWI
 - `fields` incluye o excluye campos en las búsquedas. POr defecto incluye el campo mencionado. Los cmapor internos `_raw` y `_time` se incluyen por defecto en cada búsqueda. si no los deseamos hya eu indicarlo explicitamente con el operador minus.
   > `fields procut_name price' **agrega** dos campos
   > 'fields -product_name price' **excluye** product_name y **agrega** price
   > `fields - product_name price` **excluye** product name y price
   La inclusion sucede antes que la exclusion. La eficiencia en la búsqueda se logra limitando la extracción de campos.
 - `table`
 - `dedup`
 - `addtotals`
 - `fieldformat`

# <a name= "working-with-time">2. Working with time</a>

# <a name= "statistical-processing">3. Statistical Processing</a>

# <a name= "comparing-values">4. Comparing Values</a>

# <a name= "result-modification">5. Result Modification</a>

# <a name= "correlation-analysis">6. Correlation Analysis</a>
# <a name= "creating-knowledge-objects">7.Creating Knowledge Objects</a>
# <a name= "creating-field-extractions">8. Creating Field Extractions</a>
# <a name= "data-models">9. Data Models</a>
# <a name= "using-choropleth">10. Using Choropleth</a>












