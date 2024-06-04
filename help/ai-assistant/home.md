---
title: Información general sobre el asistente de IA en Adobe Experience Platform
description: Obtenga información sobre el asistente de IA, sus matices y casos de uso, y cómo puede utilizarlo para acelerar el flujo de trabajo con Adobe Experience Platform y Real-time Customer Data Platform.
source-git-commit: dd3a7d07c0c78d76c552affef892d5e5c0f0bfb5
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 0%

---

# Asistente de IA en Adobe Experience Platform

Lea este documento para obtener más información sobre el asistente de IA en Adobe Experience Platform.

El asistente de IA de Adobe Experience Platform es una experiencia conversacional que puede utilizar para acelerar los flujos de trabajo en aplicaciones de Adobe. Puede utilizar el asistente de IA para comprender mejor el conocimiento del producto, solucionar problemas o buscar a través de la información y encontrar perspectivas operativas. El asistente de IA es compatible con Experience Platform, Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

>[!IMPORTANT]
>
>* Debe aceptar lo siguiente [un acuerdo de usuario](https://adobe.sharepoint.com/:w:/s/ExCUserExperience/EVzJv1jFBiZGnaFEufsfIqwBC_9ehv3KaXTkEMTGpQFRpg?e=qzwOo8) antes de poder usar el asistente de IA. El contrato de usuario también contiene el contrato de versión beta pública. Esto es para que pueda utilizar funciones adicionales del asistente de IA a medida que se implementan en una capacidad beta.

![Interfaz del asistente de IA con la primera experiencia del usuario activada.](./images/blank.png)

## Explicación del asistente de IA {#understanding-ai-assistant}

El asistente de IA responde a las preguntas enviadas consultando una base de datos y luego traduciendo los datos de la base de datos a una respuesta legible en lenguaje natural.

Esta representación interna de los datos subyacentes también se conoce como **[!DNL Knowledge Graph]** : una amplia red de conceptos, datos y metadatos para una respuesta determinada.

El [!DNL Knowledge Graph] consta de subgráficos a los que se hace referencia cada vez que se envían consultas:

* Perspectivas operativas del cliente.
* Perspectivas operativas del cliente en varias metatiendas.
* Documentación del Experience League.

Hay dos clases de preguntas que se deben tener en cuenta antes de consultar el Asistente de IA:

### Conocimiento del producto {#product-knowledge}

El conocimiento del producto hace referencia a conceptos y temas basados en la documentación del Experience League. Las preguntas sobre conocimientos del producto se pueden especificar en los siguientes subgrupos:

| Conocimiento del producto | Ejemplos |
| --- | --- |
| Aprendizaje puntual | <ul><li>¿Cuál es la diferencia entre una identidad y una clave principal o externa?</li><li>¿Cómo se calcula la riqueza de perfiles?</li></ul> |
| Abrir detección | <ul><li>¿Cómo puedo exportar este conjunto de datos?</li><li>¿Existen esquemas para los clientes del sector sanitario?</li></ul> |
| Resolución de problemas | <ul><li>¿Por qué no puedo activar un esquema propiedad de Adobe para el perfil?</li><li>¿Por qué no puedo eliminar un segmento?</li></ul> |

{style="table-layout:auto"}

### Perspectivas operativas {#operational-insights}

>[!IMPORTANT]
>
>Las respuestas de Operational Insights están en versión beta. Cualquier persona que tenga acceso a **Ver perspectivas operativas** El permiso de tendrá acceso a las respuestas de información operativa.

Perspectivas operativas se refiere a las respuestas que genera AI Assistant sobre los objetos de metadatos (atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes), incluidos los recuentos, las búsquedas y el impacto en el linaje. No observa ningún dato dentro de la zona protegida.

* ¿Cuántos conjuntos de datos tengo?
* ¿Cuántos atributos de esquema nunca se han utilizado?
* ¿Qué audiencias se han activado?

Puede hacer preguntas al asistente de IA sobre sus perspectivas operativas en los siguientes dominios:

* Atributos
* Públicos
* Flujos de datos
* Conjuntos de datos
* Destinos _(Las preguntas relativas a las cuentas y algunas preguntas sobre el flujo de datos no se pueden responder en este momento)._
* Recorridos
* Esquemas _(Las preguntas relativas a los grupos de campos no se pueden responder en este momento)._
* Fuentes _(Las preguntas relativas a las cuentas no se pueden responder en este momento)._

Para las preguntas de información operativa, es posible que las respuestas no reflejen el estado actual de la interfaz de usuario. Los datos que respaldan estas preguntas se actualizan una vez cada 24 horas. Por ejemplo, los cambios que los usuarios realizan en Real-Time CDP durante el día se sincronizan con los almacenes de datos por la noche y, a continuación, están disponibles para que los usuarios formulen preguntas por la mañana. Deberá iniciar sesión en una zona protegida para consultar sobre datos específicos relacionados con los objetos.

### Alcance de la función {#feature-scope}

En la actualidad, el ámbito del asistente de IA es el siguiente:

* [Conocimiento del producto](./home.md#product-knowledge): el asistente de IA puede responder preguntas de conocimiento del producto para Experience Platform, Real-time Customer Data Platform y Adobe Journey Optimizer. También puede profundizar en los temas de conocimiento del producto para Customer Journey Analytics, pero solo a través de la interfaz de usuario de Customer Journey Analytics.
* [Perspectivas operativas](./home.md#operational-insights): puede hacer preguntas al asistente de IA sobre las perspectivas operativas en los siguientes objetos de datos: atributos, audiencias, flujos de datos, conjuntos de datos, destinos, recorridos, esquemas y fuentes.

## Acceso a funciones {#feature-access}

El acceso al asistente de IA se rige por los siguientes parámetros:

* **Acceda a la aplicación:** Puede acceder al asistente de IA en Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer y [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
* **Acceso contractual:** Su empresa debe aceptar determinadas [!DNL GenAI]Términos legales relacionados con el cliente antes de que su organización pueda utilizar AI Assistant. Póngase en contacto con el administrador de su organización o con el equipo de cuenta de Adobe si no puede acceder al asistente de IA.
* **Permisos:** Utilice el [IU de permisos](../access-control/abac/ui/permissions.md) para conceder o revocar el acceso al Asistente de IA de su organización. Para utilizar el asistente de IA, un usuario determinado debe pertenecer a una función que se proporcione con **Habilitar el asistente de IA** y **Ver perspectivas operativas** permisos.
   * Como administrador, puede agregar lo siguiente **Habilitar el asistente de IA** a una función determinada y añada un usuario a esa función para permitirle acceder al asistente de IA de su organización.
   * Como administrador, puede agregar lo siguiente **Ver perspectivas operativas** a una función determinada y añada un usuario a esa función, para permitirles utilizar las capacidades de perspectivas operativas del asistente de IA. Las perspectivas operativas están actualmente en fase beta.

![La página de la interfaz de usuario de permisos con los permisos Habilitar el asistente de IA y Ver perspectivas operativas incluidos en una función determinada.](./images/permissions.png)

## Ejemplos de preguntas {#example-questions}

Esta sección describe preguntas de ejemplo a las que puede hacer referencia durante los flujos de trabajo. Las preguntas se agrupan en tres secciones: perspectivas operativas, objetivos y objetos.

### Ejemplos de preguntas agrupadas por perspectivas operativas {#operational-insights-questions}

+++Seleccione esta opción para ver ejemplos de preguntas de perspectiva operativa y sus respectivos casos de uso:

| Tipo de pregunta | Caso de uso | Ejemplos |
| --- | --- | --- | 
| Linaje de datos | Rastrear el uso de uno o varios objetos en otros objetos de Experience Platform | <ul><li>¿Qué conjuntos de datos utilizan el esquema &quot;esquema ACME&quot;?</li><li>¿Cuántos conjuntos de datos se han introducido utilizando el mismo esquema?</li><li>¿Qué conjuntos de datos se han utilizado en audiencias activadas?</li><li>Enumerar los esquemas que tienen atributos utilizados en audiencias activadas.</li><li>Muéstreme las audiencias que están activadas en &quot;Destinos ACME&quot; y que tienen más de 1000 perfiles.</li><li>Muéstreme los atributos que se utilizan en las audiencias activadas que se han modificado después de enero de 2023.</li><li>¿Cuáles son los conjuntos de datos ingeridos mediante la fuente &quot;ACME Amazon S3&quot;?</li><li>¿Qué flujos de datos están asociados con el &quot;flujo de datos de fidelidad ACME&quot;?</li><li>Enumera los esquemas relacionados con las audiencias activadas y creados en el último año.</li></ul> |
| Distribución y agregaciones | Preguntas basadas en resumen sobre el uso de objetos de Experience Platform | <ul><li>¿Cuál es el porcentaje de audiencias activadas?</li><li>¿Cuántos campos se utilizan en la segmentación?</li><li>¿Qué audiencias se activan para la mayor cantidad de destinos?</li><li>Enumerar audiencias duplicadas.</li><li>Muéstreme las audiencias activadas en &quot;Destinos ACME&quot; y clasifíquelas por tamaño de perfil.</li><li>¿Cuál es el porcentaje de audiencias que no se han activado pero que tienen más de 100 perfiles? Muéstrame sus nombres.</li><li>Enumerar los 3 conectores de origen que consumen datos en mis conjuntos de datos.</li><li>Enumere los 5 atributos principales utilizados en las audiencias activadas en función de su ocurrencia.</li></ul> |
| Búsqueda de objetos | Recupere o acceda a un objeto Experience Platform o a sus propiedades. | <ul><li>Qué conjuntos de datos no tienen ningún esquema asociado</li><li>¿Enumerar los atributos utilizados para &quot;Audiencia ACME&quot;?</li><li>Dame la lista de esquemas que tienen un perfil habilitado, pero que no se han modificado desde su creación.</li><li>¿Qué audiencias se han modificado en la última semana?</li><li>Enumerar las audiencias que tienen las mismas definiciones de segmento junto con su fecha de creación.</li><li>Qué conjuntos de datos tienen habilitado el perfil e incluyen también cuántas audiencias se han creado a partir de cada conjunto de datos.</li><li>¿Qué cuentas de origen están asociadas al conjunto de datos XYZ?</li><li>Muéstreme la definición del segmento y la fecha de modificación de &quot;Audiencia ACME&quot;.</li></ul> |
| Comparación de objetos | Identificar audiencias duplicadas. | <ul><li>En función de su definición de segmento, enumere las audiencias que están duplicadas.</li><li>Qué audiencias duplicadas están activadas en &quot;Destinos ACME&quot;.</li></ul> |

{style="table-layout:auto"}

+++

### Ejemplos de preguntas agrupadas por objetivos {#objectives-questions}

+++Seleccione esta opción para ver una lista de objetivos que puede lograr con el Asistente de IA

| Objetivo | Descripción | Ejemplo |
| --- | --- | --- |
| Conceptos de aprendizaje y flujos de trabajo continuos | <ul><li>Como usuario novato, puede utilizar el asistente de IA para aprender los conceptos de Real-Time CDP y Adobe Journey Optimizer e incorporarse a productos y funciones con los que no está familiarizado.</li><li>Como usuario experimentado, puede utilizar el Asistente de IA para resolver un caso extremo que pueda estar bloqueando el flujo de trabajo. | <ul><li>¿Cómo configuro un tablero en Recorrido Analytics?</li><li>Dime algunos casos de uso para Real-Time CDP.</li></ul> |
| Resolución de problemas | Utilice el Asistente de IA para aprender a depurar los errores básicos que pueden producirse en el flujo de trabajo. | <ul><li>¿Qué causa este error? {ERROR_MESSAGE} ¿Mentiroso?</li><li>¿Por qué no puedo eliminar la audiencia denominada &quot;Luma: Audiencia por correo electrónico&quot;?</li></ul> |
| Higiene de zona protegida | Utilice el asistente de IA para identificar duplicados u objetos que no se utilicen, de modo que pueda mantener de forma eficaz la zona protegida. | <ul><li>¿Puede mostrarme audiencias que sean similares?</li><li>¿Hay algún esquema que no tenga un conjunto de datos asociado?</li></ul> |
| Análisis de valor | Utilice el asistente de IA para identificar los objetos de datos más utilizados, evaluar cualquier indicador de rendimiento o encontrar los objetos de datos más valiosos. | <ul><li>¿Cuántos perfiles hay en nuestra definición de segmento &quot;Luma: Audiencia de correo electrónico&quot;?</li><li>¿Cuándo se activaron las audiencias en el destino de Audiencias del Experience Cloud?</li></ul> |
| Buscar | Utilice el Ayudante de IA para buscar objetos de Experience Platform admitidos, como audiencias, conjuntos de datos, destinos, esquemas y fuentes. | <ul><li>Enumere las audiencias que contienen &quot;Luma&quot; en el nombre y que se crearon en el último trimestre.</li><li>¿Qué atributos hay en el esquema XDM &quot;Luma: Custom Actions&quot;?</li></ul> |
| Análisis de impacto | Utilice el asistente de IA para identificar objetos de datos que se han utilizado en determinados flujos de trabajo y así poder evaluar el impacto de cualquier cambio. | <ul><li>Qué audiencias utilizan `homeAddress.city` en el esquema &quot;Luma: PersonProfiles&quot;?</li><li>Qué conjuntos de datos son los `consents.marketing.push.val` atributo de perfil almacenado en?</li></ul> |

{style="table-layout:auto"}

+++

### Ejemplos de preguntas agrupadas por objetos {#objects-questions}

+++Seleccione esta opción para ver una lista de preguntas de ejemplo con las que el Asistente de IA puede ayudarle:

| Objeto | Descripción |
| --- | --- |
| Audiencias: perspectivas operativas | <ul><li>¿Qué audiencias utilizan otras audiencias?</li><li>¿Cuál es la distribución del número de perfiles entre audiencias?</li><li>Mostrar las audiencias que se modificaron por última vez antes {RELATIVE_DATE}.</li><li>¿Qué audiencias tienen 0 perfiles?</li><li>Es {USE_AUTOCOMPLETE_TO_FILL_AUDIENCE_NAME} ¿se utiliza en otras audiencias?</li></ul> |
| Atributos: perspectivas operativas | <ul><li>Qué audiencias tienen un atributo XDM {ATTRIBUTE_PATH} ¿en su definición del segmento?</li><li>¿Cuántos atributos de esquema XDM no se utilizan en ninguna audiencia?</li><li>Qué esquemas tienen el atributo XDM {ATTRIBUTE_PATH} ¿en ellos?</li><li>¿Qué atributos XDM están activados?</li><li>Qué atributos XDM se utilizan en audiencias con más de 10 perfiles</li></ul> |
| Flujos de datos: perspectivas operativas | <ul><li>A qué flujos de datos contribuyen {DATASET_NAME} conjunto de datos?</li><li>¿Qué flujos de datos de origen no se utilizan o ya no reciben datos?</li><li> |
| Conjuntos de datos: perspectivas operativas | <ul><li>¿Cuántos conjuntos de datos se han introducido utilizando el mismo esquema?</li><li>Con qué conector de origen está asociado {DATASET_NAME} conjunto de datos></li><li>¿Qué conjuntos de datos se utilizan en cada audiencia?</li><li>¿Qué esquemas no se utilizan en ningún conjunto de datos?</li><li>¿Cuántos conjuntos de datos tengo?</li></ul> |
| Destinos: perspectivas operativas | <ul><li>¿Qué destinos están en estado activo?</li><li>¿Qué cuentas de destino tienen 0 audiencias activadas?</li><li> |
| Recorridos: perspectivas operativas | <ul><li>¿Cuántos recorridos tengo?</li><li>Qué recorridos se han creado en {RELATIVE_DATE} (por ejemplo, la semana pasada) o {RELATIVE_DATE} (por ejemplo, antes/después/en una fecha específica)?</li><li>Mostrar la lista de recorridos modificados en {RELATIVE_DATE} (por ejemplo, la semana pasada) o {RELATIVE_DATE} (por ejemplo, antes/después/en una fecha específica)?</li><li>Enumerar los recorridos que tengo.</li><li>Enumerar las audiencias que se utilizan en recorridos activos.</li></ul> |
| Esquemas: perspectivas operativas | <ul><li>¿Qué campos del esquema han contribuido a la mayoría de las audiencias?</li><li>¿Cuántos esquemas tienen habilitado el perfil?</li><li>Enumerar todos los esquemas modificados en la última semana.</li><li>¿Qué esquemas no se utilizan en ningún conjunto de datos?</li><li>Enumerar todos los esquemas creados en la última semana.</li></ul> |
| Fuentes: perspectivas operativas | <ul><li>¿Qué fuentes están en estado activo?</li><li>Qué conector de origen está asociado al conjunto de datos {DATASET_NAME}?</li><li>¿Qué conector de origen tiene el número más alto de cuentas asociadas?</li><li>Mostrar los flujos de datos y sus conectores de origen asociados.</li></ul> |
| Aprendizaje específico: conocimiento del producto (Real-Time CDP y Journey Optimizer) | <ul><li>¿En qué puede ayudar el Asistente de IA?</li><li>¿Qué son las audiencias de similitud?</li><li>¿Cómo se relacionan los grupos de usuarios con las funciones?</li><li>¿Cuándo debo usar un tipo de datos o un grupo de campos?</li><li>¿Cuál es la diferencia entre una identidad y una clave principal o externa?</li><li>¿Cómo se calcula la riqueza de perfiles?</li></ul> |
| Solución de problemas: conocimiento del producto (Real-Time CDP y Journey Optimizer) | <ul><li>¿En qué puede ayudar el Asistente de IA?</li><li>¿Puedo eliminar un esquema con perfil habilitado después de la ingesta de datos?</li><li>¿Por qué no puedo eliminar una audiencia?</li><li>¿Cuánto tiempo tardan las audiencias en evaluarse y los resultados en estar disponibles para la segmentación?</li></ul> |

{style="table-layout:auto"}

+++

## Formulación de preguntas {#phrasing-your-questions}

Debe formular sus preguntas al asistente de IA con claridad y contexto para obtener una respuesta lo más precisa posible. Consulte la siguiente lista de sugerencias para obtener instrucciones sobre cómo hacer una pregunta clara con contexto:

* Exponga su tarea y/o pregunta de forma concisa.
* Evite el lenguaje ambiguo o la sintaxis demasiado compleja para facilitar la comprensión.
* Proporcione un contexto relevante con respecto a su tarea o pregunta, ya que el contexto puede ayudar al Asistente de IA a generar respuestas más relevantes.

Lea las tablas siguientes para obtener más orientación sobre las prácticas recomendadas que deben seguirse al hacer preguntas al asistente de IA.

+++Seleccione esta opción para ver ejemplos de prácticas recomendadas a seguir al formular preguntas

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

+++

## Pasos siguientes

Ahora que tiene una comprensión general de AI Assistant, puede continuar y utilizar AI Assistant durante los flujos de trabajo. Consulte la siguiente documentación para obtener más información:

* [Guía de IU del asistente de IA](./ui-guide.md)
* [Privacidad, seguridad y administración en el asistente de IA](./privacy.md)
* [Preguntas frecuentes](./faq.md)