---
title: Asistente de IA para Adobe Experience Platform
description: Aprenda a utilizar el asistente de IA para navegar y comprender los conceptos de Experience Platform y Real-time Customer Data Platform, así como la información de uso sobre los objetos.
badge: Alfa
hide: true
hidefromtoc: true
source-git-commit: e84f5aff6885535b58874a4fe02db2944e1d9b7f
workflow-type: tm+mt
source-wordcount: '2629'
ht-degree: 0%

---

# Asistente de IA para Adobe Experience Platform

>[!NOTE]
>
>El asistente de IA para Adobe Experience Platform se encuentra actualmente en Alpha. La funcionalidad y la documentación están sujetas a cambios.

El asistente de IA para Adobe Experience Platform es una función de la interfaz de usuario que puede utilizar para desplazarse por los conceptos de Experience Platform y Real-time Customer Data Platform, y comprender su uso, así como la información sobre sus objetos.

Puede consultar el asistente de IA para obtener información como:

* Directrices sobre cómo realizar tareas relativas a datos y audiencias.
* Estados y métricas de los objetos de datos existentes en su organización.
* Utilice ejemplos de casos y matices para comprender mejor los objetos de datos, incluidos atributos, conjuntos de datos, destinos, esquemas, segmentos y fuentes.

Este documento proporciona información sobre cómo puede acceder al asistente de IA y utilizarlo para hacer preguntas y recibir respuestas acerca de los conceptos de Experience Platform y Real-Time CDP.

>[!BEGINSHADEBOX]

**¿Cómo funciona el asistente de IA?**

El asistente de inteligencia artificial aplicada responde a las preguntas enviadas consultando una base de datos y luego traduciendo los datos de la base de datos a una respuesta legible en lenguaje natural.

Esta representación interna de los datos subyacentes también se conoce como Gráfico del conocimiento: una red completa de conceptos, datos y metadatos para una respuesta determinada.

El gráfico de conocimiento consta de subgráficos a los que se hace referencia cada vez que se envían consultas:

* Datos de uso del cliente.
* Datos de uso del cliente en varias metatiendas.
* Documentación del Experience League.

Hay dos clases de preguntas que se deben tener en cuenta antes de consultar el asistente de IA:

* **Preguntas sobre conceptos**: Las preguntas de concepto tratan sobre conceptos de Adobe relacionados con datos o audiencias. Algunos ejemplos de preguntas conceptuales son:
   * ¿Cuál es la diferencia entre la segmentación por lotes y la segmentación por streaming?
   * ¿Existen modelos de datos del sector y cómo puedo utilizarlos?
   * ¿Para qué se utiliza Real-Time CDP?
* **Preguntas de uso**: Las preguntas de uso tratan sobre los objetos de datos dentro de la organización. Algunos ejemplos de preguntas de uso son:
   * ¿Cuántos conjuntos de datos tengo?
   * ¿Cuántos atributos de esquema nunca se han utilizado?
   * ¿Qué segmentos se han activado?

>[!ENDSHADEBOX]

## Acceso al asistente de IA para Experience Platform en la IU de

Puede acceder al asistente de IA desde el encabezado de navegación en la interfaz de usuario de Experience Platform.

Seleccione el **[!UICONTROL Icono de asistente de IA]** en el encabezado para iniciar el panel Asistente de IA.

![La página de inicio de la interfaz de usuario del Experience Platform con el icono Asistente de IA seleccionado.](./images/ai-assistant/ai-assistant.png)

Desde aquí, puede introducir la pregunta en el cuadro de texto y consultar al asistente de IA conceptos relacionados con los datos o las audiencias. También puede hacer preguntas sobre los objetos de datos para comprender mejor cómo puede utilizarlos para su caso de uso respectivo.

### Ejemplo de caso de uso: Utilice el Asistente de IA para acelerar el proceso de creación de esquemas

>[!NOTE]
>
>El siguiente flujo de trabajo de ejemplo utiliza el proceso de creación de esquemas de ExperienceEvent para ilustrar cómo se puede utilizar el asistente de IA al utilizar la interfaz de usuario de Experience Platform.

Considere un caso de uso en el que esté creando una **Esquema de comercio de dispositivos en evento**. Durante el proceso de creación del esquema de ExperienceEvent, se encuentra con el `eventType` field. En este punto, puede dejar el flujo de trabajo y consultar la documentación en [conceptos básicos de una composición de esquema](../xdm/schema/composition.md)o puede utilizar el asistente de IA para recuperar respuestas inmediatas para sus preguntas.

Para empezar, escriba su pregunta en el cuadro de texto proporcionado. En el siguiente ejemplo, se proporciona al asistente de IA la pregunta: &quot;**¿Qué es el campo eventType en un esquema de Experience Event?**&quot;

![El asistente de IA para Experience Platform tiene la siguiente pregunta preparada para la consulta: &quot;¿Qué es el campo eventType en un esquema ExperienceEvent?](./images/ai-assistant/question.png)

A continuación, el asistente de IA consulta su base de conocimiento y calcula una respuesta. Después de unos momentos, el asistente de IA devuelve una respuesta y sugerencias relacionadas que puede utilizar como preguntas de seguimiento.

![El asistente de IA para el Experience Platform con una respuesta a la consulta anterior.](./images/ai-assistant/answer.png)

Puede obtener más información sobre un tema en particular haciendo una pregunta de seguimiento. En el siguiente ejemplo, se pregunta al asistente de IA cómo se puede utilizar eventType en la segmentación.

![Se muestra una pregunta y una respuesta de seguimiento en el asistente de IA para Experience Platform.](./images/ai-assistant/follow-up-answer.png)

También puede hacer preguntas al asistente de IA sobre el uso de los datos. Al consultar sobre el uso de datos, debe estar en una zona protegida activa para que el asistente de IA pueda responder a su consulta.

![Una pregunta sobre el uso de datos, que pregunta cuántos segmentos tiene un usuario.](./images/ai-assistant/data-usage-question.png)

Con cada respuesta, el asistente de IA le ofrece una forma de validar la respuesta viendo su origen. Se proporcionan vínculos a la documentación para preguntas de concepto, mientras que las preguntas de uso de datos se pueden comprobar con una consulta SQL que muestra cómo se calculó la respuesta.

>[!BEGINSHADEBOX]

**Se han solicitado sus comentarios**

Durante esta fase Alpha, se le invita a proporcionar comentarios sobre las respuestas que reciba del Asistente de IA. Todas las respuestas y los comentarios enviados se revisan para seguir mejorando la experiencia del asistente de inteligencia artificial.

Para proporcionar comentarios, seleccione los pulgares hacia arriba o hacia abajo después de recibir una respuesta del asistente de IA y, a continuación, introduzca sus comentarios en el cuadro de texto proporcionado. A continuación, seleccione **[!UICONTROL Enviar comentarios]** para enviar.

>[!ENDSHADEBOX]

>[!BEGINTABS]

>[!TAB Mostrar origen]

Seleccionar **[!UICONTROL Mostrar origen]** para obtener una lista de vínculos a la documentación a la que hace referencia el asistente de IA para calcular su respuesta.

![Los vínculos al origen se muestran en el asistente de IA.](./images/ai-assistant/show-sources.png)

>[!TAB Pulgares hacia arriba]

Seleccione el icono de miniaturas hacia arriba para proporcionar comentarios sobre lo que ha salido bien con su experiencia con el asistente de IA.

![La ventana de comentarios positivos.](./images/ai-assistant/positive-feedback.png)

>[!TAB Pulgar hacia abajo]

Seleccione el icono de pulgares hacia abajo para proporcionar comentarios sobre lo que se puede mejorar en función de su experiencia con el asistente de IA. Durante este paso, también puede proporcionar comentarios específicos sobre la experiencia. Los comentarios proporcionados en los comentarios se revisan diariamente.

![La ventana de comentarios negativos.](./images/ai-assistant/negative-feedback.png)

>[!TAB Indicador]

Seleccione el icono de indicador para proporcionar más informes sobre su experiencia con el asistente de IA.

![La ventana de resultados del informe.](./images/ai-assistant/report-results.png)

>[!ENDTABS]

### Ideas para empezar

También puede utilizar las indicaciones preconfiguradas que proporciona el asistente de IA para empezar.

![Las indicaciones proporcionadas en el panel Asistente de IA.](./images/ai-assistant/ideas.png)

## Más información

Consulte esta sección para obtener más información sobre el asistente de IA para Experience Platform.

### Ámbito

El asistente de IA puede responder a consultas en función de la documentación y el uso de los datos.

#### Documentación

Puede hacer preguntas sobre la documentación en función de Real-time Customer Data Platform y Audiencias. Actualmente, el índice de documentación cubre Adobe Experience Platform (Real-Time CDP y Audiencias). El índice se actualiza periódicamente.

El modelo de recuperación de documentación está formado en Experience Platform (Real-Time CDP y Audiencias). Preguntas que no entran en el ámbito de Adobe Experience Platform, como las preguntas sobre otros productos de Adobe como Adobe Target y el grupo de Creative Cloud, no pueden responderse.

#### Uso de datos

También puede hacer preguntas al asistente de IA sobre el uso de datos en los siguientes dominios:

* Atributos
* Conjuntos de datos
* Destinos
* Esquemas
* Segmentos
* Fuentes

En el caso de las consultas de datos de uso, las respuestas pueden no reflejar el estado actual de la interfaz de usuario. Los datos que respaldan estas preguntas se actualizan cada 12 a 24 horas. Es posible que tenga que dar formato a preguntas como: &quot;Cuándo fue el segmento con el título {TITLE} creado?&quot; en lugar de, &quot;¿Cuándo fue la {TITLE} ¿segmento creado?&quot;

Deberá iniciar sesión en una zona protegida para consultar sobre datos específicos relacionados con objetos como esquemas, conjuntos de datos, atributos, destinos y segmentos.

+++Seleccione para obtener una lista de preguntas de uso de datos compatibles

A continuación se muestra una lista de las preguntas de uso de datos admitidas actualmente agrupadas por dominio.

>[!BEGINTABS]

>[!TAB Segmentos]

* ¿Hay segmentos duplicados?
* Mostrar todos los segmentos de flujo continuo.
* Es un segmento con nombre {SEGMENT_ID} evaluado en lote o flujo?
* ¿Qué segmentos son duplicados?
* ¿Cuántos segmentos hay en total?
* ¿Hay segmentos con los mismos nombres pero ID diferentes?
* ¿Cuál es la distribución de los métodos de evaluación (por lotes, Edge, streaming) entre segmentos?
* Muéstreme una lista de los segmentos que se modificaron por última vez en el último mes.
* ¿Qué segmentos se han modificado en la última semana?
* ¿Hay algún segmento que no se haya modificado en los últimos seis meses?
* Enumerar los segmentos creados en el último año.
* Muéstreme los segmentos que se modificaron por última vez antes de hoy.
* ¿Existen patrones o tendencias en las fechas de creación de segmentos durante el año pasado?
* ¿Puede identificar los segmentos que no se han modificado desde su creación?
* ¿Hay algún segmento que no se haya modificado desde su creación?
* ¿Cuál es la tendencia en la creación de segmentos a lo largo del tiempo?
* ¿Cuál es la distribución de las fechas de creación de segmentos?
* ¿Cuál es la distribución de las fechas de modificación de segmentos?
* ¿Qué segmentos tienen la mayor cantidad de perfiles de usuario?
* ¿Qué segmentos tienen el menor número de perfiles de usuario?
* Enumerar todos los segmentos por lotes.
* Enumerar todos los segmentos de Edge.
* ¿Qué segmentos están activados?
* ¿Qué segmentos se reenvían a Facebook?
* ¿El segmento llamado &quot;Clientes de APAC&quot; es por lotes o por streaming?
* ¿Cuántos perfiles tiene el segmento de Trabajo activo?
* ¿Alguno de mis segmentos tiene 0 perfiles?
* ¿Qué conjuntos de datos afectan al segmento de lealtad de Bronze?
* ¿Qué definiciones de segmento utilizan campos XDM que contienen &quot;género&quot;?
* ¿Qué campos XDM rellenados se producen en los segmentos de flujo continuo?
* ¿Cuántos campos XDM hay en todas las definiciones de segmentos?
* ¿Qué segmentos afectan al conjunto de datos &quot;Usuarios profesionales&quot;?
* ¿Qué segmentos se reenvían a la API HTTP?
* De los segmentos activados, ¿cuáles se activan con la mayor cantidad de tipos de destino?
* ¿Cuál es el recuento total de segmentos activados?
* ¿Cuántos segmentos están activados?
* ¿Cuántos segmentos duplicados están activados?
* ¿Cuántos segmentos se activan para cada destino?
* ¿Qué segmentos se activan en 0, 1 o varios destinos? Mostrar la distribución.
* ¿Qué segmentos se activan con la mayor cantidad de destinos?
* ¿Qué segmentos duplicados están activados?
* ¿Qué segmentos se activan en Adobe Target?
* En todos los segmentos, ¿cuántas veces se utiliza cada política de combinación?

>[!TAB Esquemas]

* ¿Cuántos esquemas XDM se definen?
* ¿Cuáles son los esquemas creados más recientemente?
* ¿Cuántos esquemas para cada clase XDM?
* ¿Qué esquema utiliza el conjunto de datos &quot;Ingesta de segmentos&quot;?
* ¿Qué esquemas no se utilizan en ningún conjunto de datos?

>[!TAB Destinos]

* ¿Cuántos destinos hay?
* ¿Cuáles son los destinos creados más recientemente?
* ¿Qué destinos están asociados a cada segmento?

>[!TAB Fuentes]

* ¿Cuántas fuentes se han creado?
* ¿Cuáles son los orígenes creados más recientemente?
* ¿Cuántas fuentes hay disponibles, desglosadas por categoría?
* ¿Puedo crear una conexión de origen desde S3?
* ¿Qué fuentes contribuyeron al conjunto de datos Mutual365?

>[!TAB Conjuntos de datos]

* ¿Cuántos conjuntos de datos hay?
* ¿Cuáles son los conjuntos de datos creados más recientemente?
* ¿Qué conjuntos de datos están habilitados para el perfil unificado?
* ¿Hay un TTL definido para el conjunto de datos de ingesta de segmentos?
* ¿Cuál es el TTL para el conjunto de datos de usuarios profesionales?
* ¿Qué conjuntos de datos utilizan el esquema Usuarios profesionales?

>[!TAB Atributos]

* ¿Qué campos XDM se rellenan con mayor frecuencia en todos los conjuntos de datos?
* ¿Qué campos y atributos XDM se utilizan con mayor frecuencia en todos los esquemas?
* ¿Qué campos y atributos XDM se utilizan en el esquema de usuarios profesionales?
* Enumeración de los atributos utilizados para este segmento con ID {SEGMENT_ID}.
* ¿Cuántos campos XDM se utilizan en más de 2 segmentos?
* ¿Qué campos se utilizan con mayor frecuencia en los segmentos?
* ¿Hay campos que se utilicen en un solo segmento?
* ¿Qué atributos se utilizan para el segmento de fidelidad Bronce?
* ¿Qué atributos no se utilizan en ningún segmento?
* ¿Qué atributos se utilizan con mayor frecuencia en los segmentos?

>[!ENDTABS]

+++

### Experiencia de conversación

Debe tener en cuenta varios matices con respecto a la experiencia conversacional al consultar el asistente de IA.

>[!NOTE]
>
>Estas limitaciones son temporales y se están mejorando a lo largo del curso del alfa.

>[!BEGINTABS]

>[!TAB No se puede deducir el contexto de la conversación anterior]

En la actualidad, el asistente de inteligencia artificial no puede hacer referencia a debates anteriores como contexto para una pregunta determinada. Consulte la tabla siguiente para ver ejemplos:

| Pregunta ambigua | Borrar pregunta | Nota |
| --- | --- | --- |
| <ul><li>Primera pregunta: &quot;¿Qué es un segmento?&quot;</li><li>Pregunta de seguimiento: &quot;¿Hay diferentes tipos de ellos?&quot;</li></ul> | <ul><li>Primera pregunta: &quot;¿Qué es un segmento?&quot;</li><li>Pregunta de seguimiento: &quot;¿Existen diferentes tipos de **segmentos**?&quot;</li></ul> | El asistente de IA no puede inferir lo que significa &quot;ellos&quot;. |
| <ul><li>Primera pregunta: &quot;¿Qué es un segmento?&quot;</li><li>Pregunta de seguimiento: &quot;¿Puede dar más detalles?&quot;</li></ul> | <ul><li>Primera pregunta: &quot;¿Qué es un segmento?&quot;</li><li>Pregunta de seguimiento: &quot;Explique en profundidad qué es un segmento&quot;</li></ul> | El asistente de IA no puede hacer referencia de forma inteligente a la documentación en función de &quot;más&quot;. |
| <ul><li>Primera pregunta: &quot;¿Qué es un segmento?&quot;</li><li>Pregunta de seguimiento: &quot;¿Puede darme un ejemplo de uno?&quot;</li></ul> | <ul><li>Primera pregunta: &quot;¿Qué es un segmento?&quot;</li><li>Pregunta de seguimiento: &quot;¿Puede darme un ejemplo de un segmento?&quot;</li></ul> | El asistente de IA no puede deducir de qué desea un ejemplo. |
| <ul><li>Primera pregunta: &quot;¿Qué es un segmento por lotes?&quot;</li><li>Pregunta de seguimiento: &quot;¿En qué se diferencia de un segmento de flujo continuo?&quot;</li></ul> | <ul><li>Primera pregunta: &quot;¿Qué es un segmento por lotes?&quot;</li><li>Pregunta de seguimiento: &quot;¿Puede comparar un segmento de flujo continuo con un segmento por lotes?&quot;</li></ul> | El asistente de IA no puede inferir a qué se refiere &quot;it&quot; y, por lo tanto, no puede comparar el segmento de flujo continuo. |
| <ul><li>Primera pregunta: &quot;¿Cuántos segmentos tengo?&quot;</li><li>Pregunta de seguimiento: &quot;¿Cuántos utilizan Facebook como destino?&quot;</li></ul> | <ul><li>Primera pregunta: &quot;¿Cuántos segmentos tengo?&quot;</li><li>Pregunta de seguimiento: &quot;¿Cuántos de los segmentos que tengo utilizan Facebook como destino?&quot;</li></ul> | El asistente de IA no puede inferir a qué se refiere &quot;ellos&quot;. |

{style="table-layout:auto"}

>[!TAB No se puede deducir el contexto de una página]

Al preguntar al asistente de IA sobre un elemento concreto de la página de la interfaz de usuario de Experience Platform en la que se encuentra, debe definir claramente el elemento específico dentro de la pregunta.

| Pregunta ambigua | Borrar pregunta | Nota |
| --- | --- | --- |
| &quot;¿Qué hace esto?&quot; | &quot;¿Qué hace {PAGE_NAME} ¿hacer? | El asistente de IA no puede inferir a qué se refiere &quot;esto&quot;. Debe proporcionar el elemento de página específico que está consultando. |
| &quot;¿Por qué no ahorra?&quot; | &quot;¿Por qué no puedo guardar una nueva zona protegida llamada {NAME}?&quot; | El asistente de IA no puede inferir a qué se refiere &quot;it&quot; y no puede saber que tiene problemas con una entidad. |

{style="table-layout:auto"}

Además, el asistente de IA solo puede responder preguntas relacionadas con los mensajes de error, ya que el error está documentado en Experience League.

>[!TAB Ambigüedad]

Debe formular sus preguntas con claridad y enmarcarlas dentro de un producto, aplicación o dominio, ya que el asistente de IA actualmente no puede desambiguar las preguntas.

| Pregunta ambigua | Borrar pregunta | Nota |
| --- | --- | --- |
| &quot;¿Cómo se crea un filtro? | ¿Cómo se crea un filtro en el lenguaje de consulta de perfil? | Debe especificar la función para la que está filtrando, ya que varias funciones de Experience Platform admiten el filtrado. |
| &quot;¿Cómo empiezo? | ¿Cómo empiezo a utilizar los destinos? | Debe proporcionar claridad sobre sus objetivos y casos de uso, ya que los conceptos demasiado amplios pueden dar como resultado respuestas genéricas o innecesariamente específicas. |

{style="table-layout:auto"}

>[!ENDTABS]

### Conversaciones pequeñas limitadas

Puede mantener una pequeña conversación con el asistente de IA, pero esta capacidad es actualmente limitada.

### Preguntas de funcionalidad

El asistente de IA puede dar una impresión inexacta de lo que puede hacer. Puede responder incorrectamente a los siguientes tipos de preguntas:

| Pregunta de ejemplo | Nota |
| --- | --- |
| &quot;¿Puedes responder preguntas sobre {ENTITY}?&quot; | Siempre que el asistente de IA pueda encontrar una sola página que haga referencia a una entidad determinada en su índice, responderá afirmativamente. |
| &quot;¿Lo sabes? **x** ¿idioma?&quot; | Actualmente, el asistente de IA solo admite inglés, pero puede responder &quot;sí&quot; debido a que el modelo subyacente puede admitirlo. |
| &quot;¿Puedes hacer...?&quot; | El asistente de IA puede responder que sí, aunque no pueda hacerlo. |

### Sugerencias

#### Las preguntas pueden responderse con la fuente de información incorrecta

Hay casos en los que la pregunta acerca de los datos de uso puede dar como resultado una respuesta basada en la documentación. Esto se debe a que el asistente de IA puede enrutar incorrectamente la pregunta a la fuente de información incorrecta. Para evitarlo, haga lo siguiente:

* Reformulando la pregunta para utilizar un lenguaje más similar a SQL
* Llamar explícitamente a la fuente de información para usar.

Lea la tabla siguiente para ver ejemplos:

| Pregunta incorrecta | Buena pregunta | Notas |
| --- | --- | --- |
| ¿Cuál es mi segmento más grande? | ¿Cuál es mi segmento más grande? Uso de datos. | Indique explícitamente al asistente de IA que desea que la respuesta se base en los datos. |
| ¿Cuál es mi segmento más grande? | Enumerar mi segmento más grande. | Hay casos en los que una pregunta de &quot;qué...&quot; se puede confundir con una pregunta basada en documentación. El uso de un comando como &quot;lista&quot; es un indicador más seguro de que está haciendo una pregunta con datos en contexto. |
| ¿Cuántos conjuntos de datos tengo? | Contar mis conjuntos de datos. | La pregunta original funciona para segmentos, pero es posible que no funcione con conjuntos de datos. |
