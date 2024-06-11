---
title: Guía de preguntas para el asistente de IA
description: Lea este documento para conocer las preguntas de ejemplo que puede utilizar al consultar el Ayudante de IA.
exl-id: d16d1262-cc2d-45c9-94c4-b86132183442
source-git-commit: 26e27e7a62731fe43ef203741121b22226078b28
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Guía de preguntas para el asistente de IA

Lea este documento en para ver un conjunto de preguntas de ejemplo que puede utilizar al consultar el asistente de IA.

También puede utilizar este documento para obtener sugerencias sobre [cómo formular sus preguntas](#phrasing-your-questions) para obtener respuestas óptimas de AI Assistant.

## Preguntas basadas en objetivos {#objectives-questions}

Las siguientes preguntas de ejemplo se agrupan por objetivos que puede lograr al utilizar el Asistente para IA:

| Objetivo | Descripción | Ejemplo |
| --- | --- | --- |
| Conceptos de aprendizaje y flujos de trabajo continuos | <ul><li>Como usuario novato, puede utilizar el asistente de IA para aprender los conceptos de Real-Time CDP y Adobe Journey Optimizer e incorporarse a productos y funciones con los que no está familiarizado.</li><li>Como usuario experimentado, puede utilizar el Asistente de IA para resolver un caso extremo que pueda estar bloqueando el flujo de trabajo. | <ul><li>¿Cómo configuro un tablero en Recorrido Analytics?</li><li>Dime algunos casos de uso para Real-Time CDP.</li></ul> |
| Resolución de problemas | Utilice el Asistente de IA para aprender a depurar los errores básicos que pueden producirse en el flujo de trabajo. | <ul><li>¿Qué causa este error? {ERROR_MESSAGE} ¿Mentiroso?</li><li>¿Por qué no puedo eliminar la audiencia denominada &quot;Luma: Audiencia por correo electrónico&quot;?</li></ul> |
| Higiene de zona protegida | Utilice el asistente de IA para identificar duplicados u objetos que no se utilicen, de modo que pueda mantener de forma eficaz la zona protegida. | <ul><li>¿Puede mostrarme audiencias que sean similares?</li><li>¿Hay algún esquema que no tenga un conjunto de datos asociado?</li></ul> |
| Análisis de valor | Utilice el asistente de IA para identificar los objetos de datos más utilizados, evaluar cualquier indicador de rendimiento o encontrar los objetos de datos más valiosos. | <ul><li>¿Cuántos perfiles hay en nuestra definición de segmento &quot;Luma: Audiencia de correo electrónico&quot;?</li><li>¿Cuándo se activaron las audiencias en el destino de Audiencias del Experience Cloud?</li></ul> |
| Buscar | Utilice el Ayudante de IA para buscar objetos de Experience Platform admitidos, como audiencias, conjuntos de datos, destinos, esquemas y fuentes. | <ul><li>Enumere las audiencias que contienen &quot;Luma&quot; en el nombre y que se crearon en el último trimestre.</li><li>¿Qué atributos hay en el esquema XDM &quot;Luma: Custom Actions&quot;?</li></ul> |
| Análisis de impacto | Utilice el asistente de IA para identificar objetos de datos que se han utilizado en determinados flujos de trabajo y así poder evaluar el impacto de cualquier cambio. | <ul><li>Qué audiencias utilizan `homeAddress.city` en el esquema &quot;Luma: PersonProfiles&quot;?</li><li>Qué conjuntos de datos son los `consents.marketing.push.val` atributo de perfil almacenado en?</li></ul> |

{style="table-layout:auto"}

## Perspectivas operativas por entidad y preguntas de conocimiento del producto{#objects-questions}

Las preguntas siguientes están agrupadas por objetos de datos y se clasifican como [perspectivas operativas](./home.md#operational-insights) o [conocimiento del producto](./home.md#product-knowledge).

* **Audiencias: perspectivas operativas**
   * ¿Qué audiencias utilizan otras audiencias?
   * ¿Cuál es la distribución del número de perfiles entre audiencias?
   * Mostrar las audiencias que se modificaron por última vez antes {RELATIVE_DATE}.
   * ¿Qué audiencias tienen 0 perfiles?
   * Es {USE_AUTO_COMPLETE_TO_FILL_AUDIENCE_NAME} ¿se utiliza en otras audiencias?
* **Atributos: perspectivas operativas**
   * Qué audiencias tienen el atributo xdm {ATTRIBUTE_PATH} en su definición de segmento?
   * ¿Cuántos atributos de esquema XDM no se utilizan en ninguna audiencia?
   * Qué esquemas tienen el atributo xdm {ATTRIBUTE_PATH} ¿en ellos?
   * ¿Qué atributos XDM están activados?
   * ¿Qué atributos XDM se utilizan en audiencias con más de 10 perfiles?
* **Flujos de datos: perspectivas operativas**
   * A qué flujos de datos contribuyen {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} conjunto de datos?
   * ¿Qué flujos de datos de origen no se utilizan o ya no reciben datos?
   * Enumerar los flujos de datos de origen que tengo.
   * ¿Qué flujos de datos se configuran para cada conector de origen?
* **Conjuntos de datos: perspectivas operativas**
   * ¿Cuántos conjuntos de datos se han introducido utilizando el mismo esquema?
   * Con qué conector de origen está asociado {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME} conjunto de datos?
   * ¿Qué conjuntos de datos se utilizan en cada audiencia?
   * ¿Qué esquemas no se utilizan en ningún conjunto de datos?
   * ¿Cuántos conjuntos de datos tengo?
* **Destinos: perspectivas operativas**
   * ¿Qué destinos están en estado activo?
   * ¿Qué cuentas de destino tienen 0 audiencias activadas?
   * ¿Cuántas audiencias se activan para cada destino?
   * ¿Qué destinos tienen el número más alto de audiencias activadas?
* **Recorridos: perspectivas operativas**
   * ¿Cuántos recorridos tengo?
   * Qué recorridos se han creado en {RELATIVE_DATE} (por ejemplo, la última semana) o {RELATIVE_DATE} (por ejemplo, antes/después/en una fecha específica)?
   * Mostrar la lista de recorridos modificados en {RELATIVE_DATE} (por ejemplo, la última semana) o {RELATIVE_DATE} (por ejemplo, antes/después/en una fecha específica)?
   * Enumerar los recorridos activos que tengo.
   * Enumerar las audiencias que se utilizan en recorridos activos.
* **Fuentes: perspectivas operativas**
   * ¿Qué fuentes están en estado activo?
   * Qué conector de origen está asociado al conjunto de datos {USE_AUTO_COMPLETE_TO_FILL_DATASET_NAME}.
   * ¿Qué conector de origen tiene el número más alto de cuentas asociadas?
   * Mostrar los flujos de datos y sus conectores de origen asociados.
* **Aprendizaje específico: conocimiento del producto (Real-Time CDP y Journey Optimizer)**
   * ¿Qué son las audiencias de similitud?
   * ¿Cómo se relacionan los grupos de usuarios con las funciones?
   * ¿Cuándo debo usar un tipo de datos o un grupo de campos?
   * ¿Cuál es la diferencia entre una identidad y una clave principal o externa?
   * ¿Cómo se calcula la riqueza de perfiles?
* **Solución de problemas: conocimiento del producto (Real-Time CDP y Journey Optimizer)**
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
| <ul><li>Sea específico sobre el objeto o la información que desea recuperar o analizar.</li><li>Intente poner los nombres de los objetos de datos entre comillas. Si sólo conoce una parte del nombre del objeto, también puede especificarlo en la pregunta.</li><li>Uso [autocompletar objeto](./ui-guide.md#use-auto-complete) para ayudar al asistente de IA a comprender mejor el contexto de la consulta.</li></ul> | <ul><li>¿Qué conjuntos de datos utilizan el esquema &quot;Lealtad de Luma&quot;?</li><li>Muéstreme los segmentos activados que tienen &quot;Luma&quot; en sus nombres. Clasificarlos por recuento de perfiles.</li></ul> |
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

## Pasos siguientes

Al leer este documento, ahora comprende cómo optimizar sus preguntas para AI Assistant. Para obtener información sobre cómo utilizar la función durante los flujos de trabajo, lea la [Guía de IU del asistente de IA](ui-guide.md).
