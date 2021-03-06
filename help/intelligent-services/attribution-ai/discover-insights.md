---
keywords: Experience Platform;perspectivas;ai de atribución;temas populares;perspectivas de ai de atribución
feature: Attribution AI
title: Descubra las perspectivas en Attribution AI
topic-legacy: Attribution AI insights
description: Este documento sirve como guía para interactuar con perspectivas de instancias de servicio en la interfaz de usuario de Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Descubra perspectivas en Attribution AI

Las instancias de servicio de Attribution AI proporcionan perspectivas que pueden utilizarse para ayudar a tomar y medir decisiones de marketing relacionadas con el rendimiento de marketing y la rentabilidad de la inversión. La selección de una instancia de servicio proporciona visualizaciones y filtros que le ayudarán a comprender el impacto de cada interacción con los clientes en cada fase del recorrido de los clientes.

Este documento sirve como guía para interactuar con perspectivas de instancias de servicio en la interfaz de usuario de Adobe Intelligent Services.

## Primeros pasos

Para utilizar perspectivas para la Attribution AI, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite la [guía de la interfaz de usuario de Attribution AI](./user-guide.md). Si ha creado recientemente una instancia de servicio y sigue siendo de formación y puntuación, espere 24 horas para que termine de ejecutarse.

## Información general sobre perspectivas de instancias de servicio

En la interfaz de usuario de [!DNL Adobe Experience Platform], seleccione **[!UICONTROL Services]** en el panel de navegación izquierdo. Aparece el explorador **[!UICONTROL Services]** y muestra los servicios inteligentes de Adobe disponibles. En el contenedor para Attribution AI, seleccione **[!UICONTROL Abrir]**.

![Acceso a la instancia](./images/insights/open_Attribution_ai.png)

Aparecerá la página del servicio de Attribution AI. Esta página enumera las instancias de servicio de Attribution AI y muestra información sobre ellas, como el nombre de la instancia, los eventos de conversión, la frecuencia con la que se ejecuta la instancia y el estado de la última actualización. Seleccione un nombre de instancia de servicio para comenzar.

>[!NOTE]
>
>Solo se pueden seleccionar las instancias de servicio que hayan completado correctamente las ejecuciones de puntuación.

![Crear instancia](./images/insights/select-service-instance.png)

A continuación, aparecerá la página de perspectivas de esa instancia de servicio, en la que se le proporcionarán visualizaciones y una serie de filtros para interactuar con los datos. Las visualizaciones y los filtros se explican con más detalle en esta guía.

![página de configuración](./images/insights/landing-page.png)

### Detalles de instancias de servicio

Para ver detalles adicionales de una instancia de servicio, seleccione **[!UICONTROL Mostrar más]** en la parte superior derecha.

![mostrar más](./images/insights/show-more.png)

Aparecerá una lista detallada. Para obtener más información sobre cualquiera de las propiedades enumeradas, visite la [guía del usuario de Attribution AI](./user-guide.md).

![mostrar detalles](./images/insights/advanced-details.png)

### Editar una instancia

Para editar una instancia, seleccione **[!UICONTROL Edit]** en el panel de navegación superior derecho.
![haga clic en el botón editar](./images/insights/edit-button.png)

Aparece el cuadro de diálogo de edición, que le permite editar el nombre, la descripción y la frecuencia de puntuación de la instancia. Si el estado de la instancia está deshabilitado, no se puede editar la frecuencia de puntuación. Para confirmar los cambios y cerrar el cuadro de diálogo, seleccione **[!UICONTROL Guardar]** en la esquina inferior derecha.

![editar popover](./images/insights/edit-popover.png)

### Más acciones {#more-actions}

El botón **[!UICONTROL Más acciones]** se encuentra en la navegación superior derecha junto a **[!UICONTROL Editar]**. Al seleccionar **[!UICONTROL Más acciones]** se abre un menú desplegable que le permite seleccionar una de las siguientes operaciones:

- **[!UICONTROL Clonar]**: Clona la instancia.
- **[!UICONTROL Eliminar]**: Elimina la instancia.
- **[!UICONTROL Descargar datos]** de resumen: Descarga un archivo CSV que contiene los datos de resumen.
- **[!UICONTROL Puntuaciones]** de acceso: Si selecciona  **[!UICONTROL Puntuaciones de]** acceso, se le redirigirá a las puntuaciones de  [acceso para el tutorial](./download-scores.md) de Attribution AI.
- **[!UICONTROL Ver el historial]** de ejecución: Aparece una ventana emergente que contiene una lista de todas las ejecuciones de puntuación asociadas con la instancia de servicio.

![más acciones](./images/insights/more-actions.png)

## Filtrado de datos

Las perspectivas de Attribution AI le permiten filtrar sus datos y actualizar automáticamente los elementos visuales de la interfaz de usuario en función de los filtros seleccionados.

### Evento de conversión

Cuando se crea una nueva instancia en Attribution AI, uno de los campos obligatorios es &quot;Eventos de conversión&quot;. Los eventos de conversión son objetivos empresariales que identifican el impacto de las actividades de marketing, como pedidos de comercio electrónico, compras en el almacén y visitas a sitios web.

Desde la instancia, la lista desplegable **[!UICONTROL Conversion events]** permite seleccionar cualquiera de los eventos definidos para la instancia a fin de filtrar los datos. Al seleccionar eventos específicos, se cambian las visualizaciones de la interfaz de usuario para rellenar solo las conversiones que pertenecen a esos eventos.

![evento de conversión](./images/insights/conversion-event.png)

### Modelo de atribución

Al seleccionar **[!UICONTROL Attribution Model]** se abre un menú desplegable con todos los modelos de atribución disponibles. Puede seleccionar varios modelos para comparar los resultados. Para obtener más información sobre los distintos modelos de atribución y cómo funcionan, visite la [Attribution AI](./overview.md) información general que contiene una tabla con información sobre cada modelo.

![modelo de atribución](./images/insights/attribution-model.png)

### Región

>[!NOTE]
>
>Este filtro solo está presente si ha realizado el paso opcional [modelado basado en regiones](./user-guide.md#region-based-modeling-optional) en la guía de la interfaz de usuario de Attribution AI al crear la instancia de servicio.

Este filtro permite seleccionar cualquier región configurada en el proceso de creación de instancias.

### Añadir filtros

Puede agregar filtros adicionales seleccionando el icono **filter** para abrir la ventana emergente **[!UICONTROL Add filters]**. La ventana emergente **[!UICONTROL Add filters]** permite filtrar por canal, geografía, tipo de medio y producto. Solo los filtros aplicables a una instancia de servicio se rellenan con el indicador . Por ejemplo, si no ha proporcionado datos geográficos ni un tipo de medios, esos atributos de filtro no estarán disponibles para su instancia.

![filtros adicionales](./images/insights/additional-filters.png)

![apertura de filtros](./images/insights/filter-popover.png)

- **[!UICONTROL Canal]:** la selección del atributo de canal permite filtrar cualquiera de los canales de marketing disponibles. Puede seleccionar varios canales para compararlos.
- **[!UICONTROL Geografía]:** la selección del atributo geografía permite filtrar los códigos de país según los modelos de región. Este filtro puede estar presente o no en función de los datos. Los códigos de país tienen dos caracteres. Consulte la lista completa de código de país [aquí](https://datahub.io/core/country-list).
- **[!UICONTROL Tipo] de medio:** la selección del atributo de tipo de medio permite filtrar cualquiera de los tipos de medios definidos.
- **[!UICONTROL Producto]:** la selección del atributo de producto le permite filtrar desde cualquier producto que se haya introducido inicialmente en la creación de la instancia.

### Date Range

Seleccione el icono de calendario para abrir la ventana emergente de intervalo de fechas. Las fechas del evento de conversión de inicio y finalización determinan la cantidad de datos rellenados en la interfaz de usuario. Puede optar por reducir o ampliar el intervalo de fechas para centrar o ampliar la cantidad de datos rellenados.

![intervalo de fechas](./images/insights/display-date-range.png)

## Información general sobre los datos

La tarjeta **[!UICONTROL Overview]** muestra las conversiones totales por modelo de atribución. El número total cambia en función de la especificidad de la búsqueda con los filtros descritos anteriormente en este documento. Al seleccionar más modelos, se agregan círculos adicionales a la Información general, cada uno con su propio color correspondiente a la leyenda.

Información general del ![](./images/insights/Overview.png)

## Tendencias semanales

La tarjeta **[!UICONTROL Weekly Trends]** desglosa la conversión total por el intervalo de fechas establecido durante el proceso de filtrado.

Al seleccionar los puntos suspensivos en la parte superior derecha de la tarjeta **Weekly Trends** , se muestra un menú desplegable que le permite seleccionar tendencias diarias, semanales o mensuales.

Al pasar el ratón por encima de la línea de datos de un modelo de atribución específico, se crea una ventana emergente que muestra el número total de conversiones para esa fecha.

![tendencias](./images/insights/weekly-trends.png)

## Desglose por canal

La tarjeta **[!UICONTROL Breakdown by channel]** se utiliza para determinar el número total de conversiones en relación con cada canal. Esta tarjeta puede utilizarse para ayudar a tomar decisiones sobre la eficacia de cada canal y el retorno de la inversión.

Al seleccionar los puntos suspensivos en la parte superior derecha de la tarjeta **[!UICONTROL Breakdown by channel]** se abre un menú desplegable que le permite rellenar datos en función de los puntos de contacto.

![canal de desglose](./images/insights/channel-breakdown.png)

## Campañas principales

La tarjeta **[!UICONTROL Principales campañas]** muestra información general sobre las campañas y el rendimiento de la campaña en cada canal. Esta tarjeta puede ayudar a informar a su equipo de la eficacia de una campaña específica para un canal determinado y proporcionar perspectivas como en qué campañas debería invertir más.

![campañas principales](./images/insights/top-campaigns.png)

## Desglose por posición del punto de contacto

Al seleccionar la pestaña **[!UICONTROL Path Analysis]** , se cargan los gráficos **[!UICONTROL Breakdown by touchpoint position]** y **[!UICONTROL Top conversion paths]**.

El gráfico **[!UICONTROL Desglose por posición del punto de contacto]** es un desglose de las conversiones atribuidas por posición del punto de contacto comparado entre todas las rutas de conversión. Este gráfico le ayuda a comprender qué puntos de contacto son más efectivos en las distintas etapas de la ruta de conversión. Los escenarios son el inicio, el reproductor y más cercanos.

- **Inicio:** indica que el punto de contacto fue el primer contacto en una ruta de conversión.
- **Reproductor:** indica que el punto de contacto no fue el primer o el último contacto que produjo una conversión.
- **Más cerca:** indica que el punto de contacto fue el último contacto antes de una conversión.

>!![NOTE]
La suma de la contribución porcentual para un modelo de atribución en todos los puntos de contacto y posiciones debe ser igual a 100.

![punto de contacto de desglose de ruta de usuario](./images/insights/user-paths.png)

## Rutas de conversión principales

El gráfico **[!UICONTROL Principales rutas de conversión]** muestra las puntuaciones algorítmicas y con influencia en las rutas de conversión principales de las regiones seleccionadas. Este gráfico le permite visualizar qué puntos de contacto contribuyen a las conversiones y cuál es la puntuación de atribución para cada punto de contacto. Puede utilizar esta información para ver las rutas más frecuentes de una determinada región y ver si surgen patrones entre los distintos conjuntos de puntos de contacto.

![Rutas de usuario más comunes](./images/insights/Touchpoint-paths.png)

## Eficacia de los puntos de contacto

Al seleccionar la ficha **[!UICONTROL Eficacia de los puntos de contacto]**, se carga la tarjeta **[!UICONTROL Eficacia de los puntos de contacto]**. Esta tarjeta utiliza la distribución de datos de Attribution AI para mostrar información para cada punto de contacto. Los datos de esta tabla solo se generan para períodos de tiempo específicos según se indica en la fecha **[!UICONTROL As of]** en la parte superior derecha de la tarjeta.

![selección de efectividad de touchpoint](./images/insights/Touchpoint-effectiveness.png)

Puede utilizar la información de tarjeta **[!UICONTROL Touchpoint effective]** para comprender cómo un touchpoint contribuye a una conversión. También puede ver la eficacia de cada punto de contacto con las siguientes métricas de rendimiento:

**Las rutas tocaron**: Esta métrica muestra un porcentaje de rutas que logran o no lograr la conversión para el punto de contacto. Verá conversiones atribuidas más altas si la proporción de rutas (porcentaje) que logran la conversión en rutas que no logran la conversión es alta.

![Métrica tocada de rutas](./images/insights/Touchpoint-metrics.png)

**Medición** de eficiencia: Esta métrica muestra las estrellas en una escala de uno a cinco. La escala indica la importancia relativa de un punto de contacto para realizar una conversión.

>[!NOTE]
Un mayor volumen de puntos de contacto no garantiza una medida de mayor eficiencia.

**Volumen** total: El número agregado de veces que un usuario tocó un punto de contacto. Esto incluye los puntos de contacto que aparecen en una ruta para lograr la conversión, así como las rutas que no generan una conversión.

## Pasos siguientes

Una vez que haya terminado de filtrar los datos y pueda mostrar la información adecuada, tiene la opción de acceder a las puntuaciones. Para obtener una guía detallada sobre cómo acceder a sus puntuaciones, visite el tutorial [access score in Attribution AI](./download-scores.md) . Además, también puede descargar los datos de resumen como se indica en [más acciones](#more-actions). Al seleccionar &quot;Descargar datos de resumen&quot; se descargarán los datos de resumen agregados por fechas.

## Recursos adicionales

El siguiente vídeo está diseñado para ayudarle a aprender a utilizar la página de perspectivas de Attribution AI para comprender el ROI de los canales y campañas de marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
