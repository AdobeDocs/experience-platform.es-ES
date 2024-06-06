---
title: Asistente de IA en Adobe Experience Platform
description: Aprenda a utilizar el asistente de IA para desplazarse por los conceptos de Experience Platform y Real-time Customer Data Platform, y comprender sus conceptos, así como la información de uso de sus objetos.
exl-id: 3fed2b1d-75fc-47ce-98d1-a811eb8a1d8e
source-git-commit: 1c228eb95075d4302ab6d3544fff8766087411bf
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Guía de IU del asistente de IA

Lea esta guía para aprender a utilizar el asistente de IA en la interfaz de usuario de Adobe Experience Platform.

## Acceso al Asistente de IA en la IU de Experience Platform

Para iniciar el asistente de IA, seleccione **[!UICONTROL Icono de asistente de IA]** desde el encabezado superior de la interfaz de usuario de Experience Platform.

![La página de inicio del Experience Platform, con el icono Asistente de IA seleccionado y la interfaz del asistente de IA abierta.](./images/ai-assistant-full-icon.png)

Aparecerá la interfaz del Asistente de IA, que le proporcionará inmediatamente información para empezar. Puede utilizar las opciones que se proporcionan en [!UICONTROL Ideas para empezar] para responder preguntas y comandos como:

* [!UICONTROL ¿Cuál de mis audiencias está activada?]
* [!UICONTROL ¿Qué es un esquema?]
* [!UICONTROL Casos de uso comunes de Real-Time CDP]

## Guía de IU del asistente de IA

>[!NOTE]
>
>El siguiente flujo de trabajo es un ejemplo que utiliza el proceso de creación de esquemas de eventos de experiencia para ilustrar cómo puede utilizar el Asistente de IA al utilizar la interfaz de usuario de Experience Platform.

Considere un caso de uso en el que esté creando una **Esquema de comercio de dispositivos en evento**. Durante el proceso de creación del esquema del evento de experiencia, se encuentra con el `eventType` field. &quot;En este punto, tiene la opción de salir del flujo de trabajo y consultar [conceptos básicos de una composición de esquema](../xdm/schema/composition.md) o puede utilizar AI Assistant para recuperar respuestas a sus preguntas y encontrar recursos adicionales a través de los vínculos de documentación recomendados por AI Assistant&quot;.

Para empezar, escriba su pregunta en el cuadro de texto proporcionado. En el siguiente ejemplo, se proporciona un asistente de IA con la pregunta: &quot;**¿Qué es el campo eventType en un esquema ExperienceEvent?**&quot;

![Asistente de IA para Experience Platform con la siguiente pregunta preparada para la consulta: &quot;¿Qué es el campo eventType en un esquema ExperienceEvent?](./images/question.png)

A continuación, el asistente de IA consulta su base de conocimiento y calcula una respuesta. Después de unos momentos, el Asistente de IA devuelve una respuesta y sugerencias relacionadas que puede utilizar como preguntas de seguimiento.

![Asistente de IA para el Experience Platform con una respuesta a la consulta anterior.](./images/answer.png)

Después de recibir una respuesta del Asistente de IA, puede seleccionar entre una serie de opciones para decidir cómo desea continuar.

### Funciones del asistente de IA {#features}

Esta sección describe las diferentes funciones del asistente de IA que puede utilizar durante los flujos de trabajo en Experience Platform.

### Ver objetos de datos operativos {#view-operational-data-objects}

Según la consulta, el asistente de IA proporciona información adicional perteneciente a los datos de la zona protegida. Para ver cómo se aplica la respuesta a la consulta a su zona protegida particular, seleccione **[!UICONTROL En su zona protegida].**

Al ver datos pertenecientes a su zona protegida, el Asistente de IA puede proporcionar vínculos directos a páginas de interfaz de usuario específicas que muestran los datos consultados.

+++Seleccione para ver el ejemplo

En este ejemplo, el asistente de IA devuelve información adicional sobre los esquemas XDM existentes en la zona protegida, incluido su recuento total y los cinco campos más utilizados.

![Se abre la ventana desplegable &quot;en la zona protegida&quot;, que muestra información adicional sobre los esquemas.](./images/in-your-sandbox.png)

+++

### Ver citas {#view-citations}

Puede verificar las respuestas que le devuelve AI Assistant revisando las citas disponibles con cada respuesta de conocimiento del producto.

+++Seleccione esta opción para ver un ejemplo de cómo mostrar orígenes

Para ver las citas y validar la respuesta del asistente de IA, seleccione **[!UICONTROL Mostrar orígenes]**.

![La respuesta del asistente de IA con &quot;Mostrar fuentes&quot; seleccionado.](./images/show-sources.png)

El asistente de IA actualiza la interfaz y le proporciona vínculos a documentación que corrobora la respuesta inicial. Además, cuando las citas están habilitadas, el Asistente de IA actualiza la respuesta para incluir notas al pie de página que indican las partes específicas de la respuesta que hacen referencia a la documentación proporcionada.

![Un menú desplegable de las citas que AI Assistant proporciona para preguntas de concepto.](./images/citations.png)

También puede utilizar las sugerencias que ofrece el Asistente de IA en **[!UICONTROL Sugerencias relacionadas]** para explorar más en profundidad los temas relacionados con la pregunta original.

![Una lista de sugerencias proporcionadas por AI Assistant.](./images/related-suggestions.png)

+++

### Perspectivas operativas {#operational-insights}

Debe encontrarse en una zona protegida activa para que el asistente de IA responda suficientemente a una pregunta sobre sus perspectivas operativas.

+++Seleccione esta opción para ver un ejemplo de una pregunta de información operativa

En el siguiente ejemplo, se realiza la siguiente consulta al asistente de IA: **&quot;Mostrar los flujos de datos creados con la fuente de Amazon S3&quot;**.

![Una pregunta sobre perspectivas operativas.](./images/op-insights-question.png)

A continuación, el asistente de IA responde con una tabla que enumera los flujos de datos y sus ID correspondientes. Para ver toda la tabla de datos, seleccione el icono de expansión en la parte superior derecha.

![Una respuesta de perspectivas operativas](./images/op-insights-answer.png)

Aparece una vista expandida de la tabla, que le proporciona una lista más completa de flujos de datos basados en los parámetros de la consulta.

![Una vista de la tabla expandida.](./images/table.png)

Cuando se le solicita una pregunta de perspectivas operativas, AI Assistant proporciona una explicación de cómo calculó la respuesta. En el ejemplo siguiente, AI Assistant describe los pasos que realizó para identificar los flujos de datos creados con el [!DNL Amazon S3] origen.

![Un asistente de IA que proporciona una explicación sobre cómo calcula su respuesta.](./images/answer-explained.png)

También puede proporcionar filtros y modificaciones a las preguntas, y puede indicar al Asistente de inteligencia artificial que procese sus conclusiones en función de los filtros que incluya. Por ejemplo, puede pedir al Asistente de IA que le muestre una tendencia del recuento de definiciones de segmento en el orden de su fecha de creación, elimine definiciones de segmento con perfiles totales cero y utilice nombres de mes en lugar de enteros al mostrar los datos.

**Nota:** Las respuestas de Operational Insights se encuentran actualmente en fase beta. Seleccione el icono de información de objeto en la interfaz de usuario del Ayudante de IA para ver el aviso Beta y un vínculo a la documentación.

![Icono de información del asistente de IA seleccionado.](./images/op-insights-beta-note.png)

+++

### Usar completado automático {#use-auto-complete}

Puede utilizar la función de autocompletar para recibir una lista de los objetos de datos que existen en su zona protegida. Las recomendaciones de autocompletar están disponibles para los siguientes dominios: audiencias, esquemas, conjuntos de datos, fuentes y destinos.

+++Seleccione esta opción para ver un ejemplo de autocompletado

Se puede utilizar el completado automático incluyendo el símbolo más (**`+`**) en la consulta. Como alternativa, también puede seleccionar el signo más (**`+`**) situado en la parte inferior del cuadro de entrada de texto. Aparece una ventana con una lista de los objetos de datos recomendados de la zona protegida.

![Ejemplo de autocompletar](./images/autocomplete.png)

+++

### Uso de giro múltiple {#use-multi-turn}

Puede utilizar las capacidades de varias vueltas de AI Assistant para tener una conversación más natural durante su experiencia. El asistente de IA puede responder a las preguntas de seguimiento que se le formulen. ese contexto se puede inferir de una interacción anterior.

+++Seleccione esta opción para ver un ejemplo de varias vueltas

En el siguiente ejemplo, se solicita al asistente de IA primero el número total de flujos de datos y, a continuación, se le solicita que enumere los 10 flujos de datos más recientes.

![Ejemplo de giro múltiple](./images/multiturn.png)

Para restablecer, seleccione los puntos suspensivos (**`...`**) en la interfaz del asistente de IA y, a continuación, seleccione **[!UICONTROL Iniciar nueva conversación]**. Esto informa al Asistente de IA de que tiene intención de cambiar los temas y puede resultar especialmente útil para solucionar problemas de consultas que dan error o hacen referencia a información incorrecta.

![Los puntos suspensivos seleccionados y la opción Iniciar nueva conversación seleccionada.](./images/reset.png)

+++

### Uso de detectabilidad {#use-discoverability}

Puede utilizar la función de detección del asistente de IA para ver una lista de los temas generales, agrupados en entidades, que admite.

+++Seleccione esta opción para ver un ejemplo de la capacidad de detección

Para ver la detección, seleccione el icono de la bombilla en el encabezado superior de la interfaz del asistente de IA.

![La función de detección del asistente de IA.](./images/lightbulb.png)

A continuación, seleccione una categoría y, a continuación, seleccione una solicitud de la lista proporcionada. Puede utilizar esta función para tener una mejor idea de los tipos de preguntas que AI Assistant puede responder. También puede actualizar las solicitudes preexistentes con detalles específicos relacionados con su zona protegida utilizando texto libre o [autocompletar](#use-auto-complete).

![El Ayudante de IA solicita la detección.](./images/prompt.png)

+++

## Proporcionar comentarios {#feedback}

Puede proporcionar comentarios sobre su experiencia con el asistente de IA mediante las opciones que se proporcionan con la respuesta.

Para proporcionar comentarios, seleccione los pulgares hacia arriba, hacia abajo o un indicador después de recibir una respuesta del asistente de IA y, a continuación, introduzca sus comentarios en el cuadro de texto proporcionado.

![La opción de comentarios del asistente de IA.](./images/provide-feedback.png)

+++Seleccione para ver más ejemplos

>[!BEGINTABS]

>[!TAB Pulgares hacia arriba]

Seleccione el icono de miniaturas hacia arriba para proporcionar comentarios sobre lo que ha salido bien con su experiencia con el asistente de IA.

![La ventana de comentarios positivos.](./images/thumbs-up.png)

>[!TAB Pulgar hacia abajo]

Seleccione el icono de pulgares hacia abajo para proporcionar comentarios sobre lo que se puede mejorar en función de su experiencia con el asistente de IA. Durante este paso, también puede proporcionar comentarios específicos sobre la experiencia. Los comentarios proporcionados en los comentarios se revisan diariamente.

![La ventana de comentarios negativos.](./images/thumbs-down.png)

>[!TAB Indicador]

Seleccione el icono de indicador para proporcionar más informes sobre su experiencia con el asistente de IA.

![La ventana de resultados del informe.](./images/flag.png)

>[!ENDTABS]

+++
