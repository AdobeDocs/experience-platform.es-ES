---
title: Guía de preguntas para el asistente de IA
description: Lea este documento para conocer las preguntas de ejemplo que puede utilizar al consultar el Ayudante de IA.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: fc87c28d7019e123d974e4d2ad307928a3d3fe89
workflow-type: tm+mt
source-wordcount: '1524'
ht-degree: 1%

---

# Guía de preguntas para el asistente de IA

Lea este documento en para ver un conjunto de preguntas de ejemplo que puede utilizar al consultar el asistente de IA.

También puede usar este documento para obtener sugerencias sobre [cómo formular sus preguntas](#phrasing-your-questions) para obtener respuestas óptimas del Asistente de IA.

## Preguntas basadas en objetivos {#objectives-questions}

Las siguientes preguntas de ejemplo se agrupan por objetivos que puede lograr al utilizar el Asistente para IA:

| Objetivo | Descripción | Ejemplo |
| --- | --- | --- |
| Conceptos de aprendizaje y flujos de trabajo continuos | <ul><li>Como usuario novato, puede utilizar el asistente de IA para aprender los conceptos de Real-Time CDP y Adobe Journey Optimizer e incorporarse a productos y funciones con los que no está familiarizado.</li><li>Como usuario experimentado, puede utilizar el Asistente de IA para resolver un caso extremo que pueda estar bloqueando el flujo de trabajo. | <ul><li>¿Cómo configuro un tablero en Recorrido Analytics?</li><li>Dime algunos casos de uso para Real-Time CDP.</li></ul> |
| Resolución de problemas | Utilice el Asistente de IA para aprender a depurar los errores básicos que pueden producirse en el flujo de trabajo. | <ul><li>¿Qué significa este error {ERROR_MESSAGE}?</li><li>¿Por qué no puedo eliminar la audiencia denominada &quot;Luma: Audiencia por correo electrónico&quot;?</li></ul> |
| Higiene de zona protegida | Utilice el asistente de IA para identificar duplicados u objetos que no se utilicen, de modo que pueda mantener de forma eficaz la zona protegida. | <ul><li>¿Puede mostrarme audiencias que sean similares?</li><li>¿Hay algún esquema que no tenga un conjunto de datos asociado?</li></ul> |
| Análisis de valor | Utilice el asistente de IA para identificar los objetos de datos más utilizados, evaluar cualquier indicador de rendimiento o encontrar los objetos de datos más valiosos. | <ul><li>¿Cuántos perfiles hay en nuestra definición de segmento &quot;Luma: Audiencia de correo electrónico&quot;?</li><li>¿Cuándo se activaron las audiencias en el destino de Audiencias del Experience Cloud?</li></ul> |
| Buscar | Utilice el Ayudante de IA para buscar objetos de Experience Platform admitidos, como audiencias, conjuntos de datos, destinos, esquemas y fuentes. | <ul><li>Enumere las audiencias que contienen &quot;Luma&quot; en el nombre y que se crearon en el último trimestre.</li><li>¿Qué atributos hay en el esquema XDM &quot;Luma: Custom Actions&quot;?</li></ul> |
| Análisis de impacto | Utilice el asistente de IA para identificar objetos de datos que se han utilizado en determinados flujos de trabajo y así poder evaluar el impacto de cualquier cambio. | <ul><li>¿Qué audiencias utilizan `homeAddress.city` en el esquema &quot;Luma: PersonProfiles&quot;?</li><li>¿En qué conjuntos de datos está almacenado el atributo de perfil `consents.marketing.push.val`?</li></ul> |

{style="table-layout:auto"}

## Perspectivas operativas por entidad y preguntas de conocimiento del producto{#objects-questions}

Las preguntas siguientes están agrupadas por objetos de datos y se clasifican como [datos operativos](./home.md#operational-insights) o [conocimiento del producto](./home.md#product-knowledge).

![](./images/prompt.png)

* **Audiencias - Datos operativos**
   * ¿Qué audiencias utilizan otras audiencias?
   * ¿Cuál es la distribución del número de perfiles entre audiencias?
   * Mostrar las audiencias que se modificaron por última vez antes de {RELATIVE_DATE}.
   * ¿Qué audiencias tienen 0 perfiles?
   * ¿Se utiliza {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} en otras audiencias?
* **Atributos - Datos operativos**
   * ¿Qué audiencias tienen el atributo xdm {ATTRIBUTE_PATH} en su definición de segmento?
   * ¿Cuántos atributos de esquema XDM no se utilizan en ninguna audiencia?
   * ¿Qué esquemas contienen el atributo xdm {ATTRIBUTE_PATH}?
   * ¿Qué atributos XDM están activados?
   * ¿Qué atributos XDM se utilizan en audiencias con más de 10 perfiles?
* **Flujos de datos - Datos operativos**
   * ¿Qué flujos de datos contribuyen al conjunto de datos {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * ¿Qué flujos de datos de origen no se utilizan o ya no reciben datos?
   * Enumerar los flujos de datos de origen que tengo.
   * ¿Qué flujos de datos se configuran para cada conector de origen?
* **Conjuntos de datos - Datos operativos**
   * ¿Cuántos conjuntos de datos se han introducido utilizando el mismo esquema?
   * ¿Qué conector de origen está asociado con el conjunto de datos {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}?
   * ¿Qué conjuntos de datos se utilizan en cada audiencia?
   * ¿Qué esquemas no se utilizan en ningún conjunto de datos?
   * ¿Cuántos conjuntos de datos tengo?
* **Destinos - Datos operativos**
   * ¿Qué destinos están en estado activo?
   * ¿Qué cuentas de destino tienen 0 audiencias activadas?
   * ¿Cuántas audiencias se activan para cada destino?
   * ¿Qué destinos tienen el número más alto de audiencias activadas?
* **Recorridos - Datos operativos**
   * ¿Cuántos recorridos tengo?
   * ¿Qué recorridos se han creado en {RELATIVE_DATE} (por ejemplo, la última semana) o {RELATIVE_DATE} (por ejemplo, antes/después/en una fecha específica)?
   * ¿Desea mostrarme la lista de recorridos que se modificaron en {RELATIVE_DATE} (por ejemplo, la última semana) o {RELATIVE_DATE} (por ejemplo, antes/después/en una fecha específica)?
   * Enumerar los recorridos activos que tengo.
   * Enumerar las audiencias que se utilizan en recorridos activos.
* **Fuentes - Datos operativos**
   * ¿Qué fuentes están en estado activo?
   * Qué conector de origen está asociado con el conjunto de datos {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * ¿Qué conector de origen tiene el número más alto de cuentas asociadas?
   * Mostrar los flujos de datos y sus conectores de origen asociados.
* **Aprendizaje puntual: conocimiento del producto (Real-Time CDP y Journey Optimizer)**
   * ¿Qué son las audiencias de similitud?
   * ¿Cómo se relacionan los grupos de usuarios con las funciones?
   * ¿Cuándo debo usar un tipo de datos o un grupo de campos?
   * ¿Cuál es la diferencia entre una identidad y una clave principal o externa?
   * ¿Cómo se calcula la riqueza de perfiles?
* **Solución de problemas - Conocimiento del producto (Real-Time CDP y Journey Optimizer)**
   * ¿En qué puede ayudar el Asistente de IA?
   * ¿Puedo eliminar un esquema habilitado para perfiles después de la ingesta de datos?
   * ¿Por qué no puedo eliminar una audiencia?
   * ¿Cuánto tiempo tardan las audiencias en evaluarse y los resultados en estar disponibles para la segmentación?

## Formulación de preguntas {#phrasing-your-questions}

Debe formular sus preguntas al asistente de IA con claridad y contexto para obtener una respuesta lo más precisa posible. Consulte la siguiente lista de sugerencias para obtener instrucciones sobre cómo hacer una pregunta clara con contexto:

* Exponga su tarea y/o pregunta de forma concisa.
* Evite el lenguaje ambiguo o la sintaxis demasiado compleja para facilitar la comprensión.
* Proporcione un contexto relevante con respecto a su tarea o pregunta, ya que el contexto puede ayudar al Asistente de IA a generar respuestas más relevantes.

Lea las tablas siguientes para obtener más orientación sobre las prácticas recomendadas que deben seguirse al hacer preguntas al asistente de IA.

En las tablas siguientes se describen las prácticas recomendadas que puede seguir al utilizar el Asistente para IA:

| Hacer | Ejemplo |
| --- | --- |
| <ul><li>Sea específico sobre el objeto o la información que desea recuperar o analizar.</li><li>Intente poner los nombres de los objetos de datos entre comillas. Si sólo conoce una parte del nombre del objeto, también puede especificarlo en la pregunta.</li><li>Use [autocompletar objeto](./ui-guide.md#use-auto-complete) para ayudar al Asistente de IA a comprender mejor el contexto de su consulta.</li></ul> | <ul><li>¿Qué conjuntos de datos utilizan el esquema &quot;Lealtad de Luma&quot;?</li><li>Muéstreme los segmentos activados que tienen &quot;Luma&quot; en sus nombres. Clasificarlos por recuento de perfiles.</li></ul> |
| <ul><li>Evite la ambigüedad y utilice un lenguaje claro</li><li>Utilice una terminología precisa para garantizar una mejor claridad en la consulta.</li><li>Cuando haga preguntas sobre Adobe Experience Platform, intente utilizar una terminología específica de Experience Platform para mejorar la relevancia de las respuestas.</li></ul> | <ul><li>¿Cuántos perfiles tengo en &quot;Audiencia ACME&quot;?</li><li>Mostrar los 5 atributos XDM principales utilizados en audiencias activadas.</li></ul> |
| <ul><li>Proporcione contexto o especifique un criterio para filtrar los resultados.</li><li>Utilice un criterio de filtro en las preguntas para limitar el volumen de datos en la respuesta.</li></ul> | <ul><li>Mostrar audiencias que no se hayan activado y creado hace más de 6 meses y que nunca se hayan modificado.</li><li>Mostrar las audiencias activadas en &quot;Destino ACME&quot; y tener más de 10000 perfiles.</li></ul> |

{style="table-layout:auto"}

| No lo hagas | Ejemplo |
| --- | --- |
| Utilice un lenguaje vago o ambiguo. | <ul><li>Proporcionarme información sobre conjuntos de datos.</li><li>¿Cuántos usuarios tengo en &quot;Audiencia ACME&quot;?</li><li>Mostrar segmentos.</li><li>Atributos de lista.</li></ul> |
| Realizar solicitudes incompletas. | &quot;Luma: Conjunto de datos de fidelización&quot; |
| Asumir el conocimiento sin contextos. | <ul><li>Audiencias en los últimos 6 meses.</li><li>Cree una consulta para mí.</li></ul> |
| Formular consultas demasiado complejas. | Proporcionar un análisis completo del linaje de datos en todos los objetos y sus dependencias. |
| Omitir criterios o parámetros. | Mostrar conjuntos de datos. |

{style="table-layout:auto"}

## Ejemplos de preguntas no admitidas {#unsupported-questions}

A continuación se muestra una lista de ejemplos de preguntas que el asistente de IA no admite actualmente.

+++Seleccione esta opción para ver ejemplos de preguntas no admitidas

### Datos operativos

* ¿Cuántos perfiles de esta zona protegida viven en California? (**Nota**: para preguntas similares, debe proporcionar un criterio específico para dar contexto suficiente a la solicitud, en este caso, el criterio específico es &quot;vivir en California&quot;).
* ¿En qué segmentos se encuentra este perfil {PROFILE_INFO/ATTRIBUTE_VALUE}?
* ¿Cuántos perfiles del conjunto de datos tienen un correo electrónico?
* ¿Qué conjunto de datos constituye el máximo número de perfiles en esta zona protegida?
* ¿Qué conjunto de datos tiene el número más alto de registros?
* ¿Cuántos segmentos se han eliminado en {RELATIVE_DATE}?
* ¿Cuál de mis conjuntos de datos tiene el tamaño más grande?
* Dame un perfil en {AUDIENCE_NAME}.
* Cuál es el número total de perfiles en mi zona protegida
* ¿Cuántas áreas de nombres de identidad están asociadas con la audiencia {AUDIENCE_NAME}?
* Mostrarme un informe de todos los segmentos de audiencia que se evaluaron hoy
* ¿Cuántos segmentos tienen perfiles superpuestos?
* Cuántos lotes se están cargando en {DATASET_NAME}
* ¿Cuántas ofertas activas tengo?
* ¿Cuántas campañas activas tengo?
* ¿De dónde provienen mis fuentes de datos?
* ¿Cuál es el conjunto de datos o fuente de datos más grande?
* ¿Puedo obtener la lista de usuarios que han creado estos esquemas?

### Resolución de problemas

* ¿Por qué sigue procesándose este lote {BATCH_NAME/BATCH_ID}?
* ¿Por qué nadie cumple los requisitos para esta audiencia {AUDIENCE_NAME}?
* No puedo ver la inteligencia artificial aplicada al cliente, ¿por qué y cómo puedo solucionarla?
* No puedo ver la previsualización del conjunto de datos, ¿por qué y cómo puedo corregirlo?
* ¿Por qué no puedo eliminar {SEGMENT/DATASET/SCHEMA_NAME}?
* ¿Tengo acceso al servicio de consultas?

### Tarea y automatización

* Escriba una consulta que me proporcione un registro de {DATASET_NAME}.
* Escriba una llamada de API de ejemplo a /schemas/{schemaId}/fields/{fieldPath}/values.
* Configure una fuente/destino para mí.
* Crear una audiencia para mí con los criterios {USER_SPECIFIC_CRITERIA}.

+++

## Pasos siguientes

Al leer este documento, ahora comprende cómo optimizar sus preguntas para AI Assistant. Para obtener información sobre cómo usar la característica durante los flujos de trabajo, lea la [guía de la interfaz de usuario del Asistente de IA](ui-guide.md).
