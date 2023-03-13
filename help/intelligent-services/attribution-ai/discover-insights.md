---
keywords: Experience Platform;perspectivas;inteligencia artificial aplicada a la atribución;temas populares;perspectivas de ia de atribución
feature: Attribution AI
title: Descubra perspectivas en Attribution AI
description: Este documento sirve como guía para interactuar con las perspectivas de la instancia de servicio en la interfaz de usuario de Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Descubra perspectivas en Attribution AI

Las instancias de servicio de Attribution AI proporcionan perspectivas que pueden utilizarse para ayudar a tomar y medir decisiones de marketing relacionadas con el rendimiento de marketing y el retorno de la inversión. Al seleccionar una instancia de servicio, se proporcionan visualizaciones y filtros que le ayudan a comprender el impacto de cada interacción con el cliente en cada fase del recorrido con el cliente.

Este documento sirve como guía para interactuar con las perspectivas de la instancia de servicio en la interfaz de usuario de Adobe Intelligent Services.

## Primeros pasos

Para utilizar las perspectivas para la Attribution AI de, necesita tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite la [guía de interfaz de usuario de Attribution AI](./user-guide.md). Si ha creado recientemente una instancia de servicio que aún se está entrenando y puntuando, espere 24 horas para que finalice la ejecución.

## Resumen de perspectivas de instancia de servicio

En el [!DNL Adobe Experience Platform] IU, seleccione **[!UICONTROL Servicios]** en el panel de navegación izquierdo. El **[!UICONTROL Servicios]** aparece el explorador y muestra los servicios inteligentes de Adobe disponibles. En el contenedor de Attribution AI, seleccione **[!UICONTROL Abrir]**.

![Acceso a su instancia](./images/insights/open_Attribution_ai.png)

Aparecerá la página de servicio de Attribution AI. En esta página se enumeran las instancias de servicio de Attribution AI y se muestra información sobre ellas, incluido el nombre de la instancia, los eventos de conversión, la frecuencia con la que se ejecuta y el estado de la última actualización. Seleccione el nombre de una instancia de servicio para empezar.

>[!NOTE]
>
>Solo se pueden seleccionar las instancias de servicio que hayan completado ejecuciones de puntuación correctas.

![Crear instancia](./images/insights/select-service-instance.png)

A continuación, aparecerá la página de perspectivas para esa instancia de servicio, donde se le proporcionarán visualizaciones y una serie de filtros para interactuar con los datos. Las visualizaciones y filtros se explican con más detalle en esta guía.

![página de configuración](./images/insights/landing-page.png)

### Detalles de instancia del servicio

Para ver detalles adicionales de una instancia de servicio, seleccione **[!UICONTROL Mostrar más]** en la parte superior derecha.

![mostrar más](./images/insights/show-more.png)

Aparecerá una lista detallada. Para obtener más información sobre cualquiera de las propiedades enumeradas, visite la [Guía del usuario del Attribution AI](./user-guide.md).

![mostrar detalles](./images/insights/advanced-details.png)

### Edición de una instancia

Para editar una instancia, seleccione **[!UICONTROL Editar]** en la barra de navegación superior derecha.
![haga clic en el botón editar](./images/insights/edit-button.png)

Aparecerá el cuadro de diálogo de edición, que le permitirá editar el nombre, la descripción y la frecuencia de puntuación de la instancia. Si el estado de la instancia está desactivado, no se puede editar la frecuencia de puntuación. Para confirmar los cambios y cerrar el cuadro de diálogo, seleccione **[!UICONTROL Guardar]** en la esquina inferior derecha.

![editar ventana emergente](./images/insights/edit-popover.png)

### Más acciones {#more-actions}

El **[!UICONTROL Más acciones]** situado en la barra de navegación superior derecha junto a **[!UICONTROL Editar]**. Seleccionar **[!UICONTROL Más acciones]** abre un menú desplegable que le permite seleccionar una de las siguientes operaciones:

- **[!UICONTROL Clonar]**: Clona la instancia.
- **[!UICONTROL Eliminar]**: elimina la instancia.
- **[!UICONTROL Descargar datos de resumen]**: descarga un archivo CSV que contiene los datos de resumen.
- **[!UICONTROL Puntuaciones de acceso]**: seleccionando **[!UICONTROL Puntuaciones de acceso]** le redirige a [tutorial de puntuaciones de acceso para Attribution AI](./download-scores.md).
- **[!UICONTROL Ver historial de ejecución]**: Aparece una ventana emergente que contiene una lista de todas las ejecuciones de puntuación asociadas con la instancia de servicio.

![más acciones](./images/insights/more-actions.png)

## Filtrado de datos

Las perspectivas de Attribution AI le permiten filtrar los datos y actualizar automáticamente los elementos visuales de la interfaz de usuario en función de los filtros seleccionados.

### Evento de conversión

Al crear una nueva instancia en Attribution AI, uno de los campos obligatorios es &quot;Eventos de conversión&quot;. Los eventos de conversión son objetivos comerciales que identifican el impacto de las actividades de marketing, como los pedidos de comercio electrónico, las compras en la tienda y las visitas a sitios web.

Desde la instancia, la variable **[!UICONTROL Eventos de conversión]** La lista desplegable permite seleccionar cualquiera de los eventos definidos para la instancia a fin de filtrar los datos. Si se seleccionan eventos específicos, las visualizaciones de la interfaz de usuario se cambian para rellenar únicamente las conversiones que pertenecen a esos eventos.

![evento de conversión](./images/insights/conversion-event.png)

### Modelo de atribución

Seleccionar **[!UICONTROL Modelo de atribución]** abre una lista desplegable con todos los diferentes modelos de atribución disponibles. Puede seleccionar varios modelos para comparar los resultados. Para obtener más información sobre los diferentes modelos de atribución y cómo funcionan, visite la [Attribution AI](./overview.md) información general que contiene una tabla con información sobre cada modelo.

![modelo de atribución](./images/insights/attribution-model.png)

### Región

>[!NOTE]
>
>Este filtro solo está presente si ha realizado el paso opcional [modelado basado en regiones](./user-guide.md#region-based-modeling-optional) en la guía de la interfaz de usuario de Attribution AI al crear la instancia de servicio.

Este filtro permite seleccionar cualquier región configurada en el proceso de creación de instancias.

### Añadir filtros

Puede añadir filtros adicionales seleccionando la variable **filter** para abrir el **[!UICONTROL Añadir filtros]** popover. El **[!UICONTROL Añadir filtros]** La ventana emergente le permite filtrar por canal, geografía, tipo de medios y producto. La ventana emergente solo rellena los filtros aplicables para una instancia de servicio. Por ejemplo, si no ha proporcionado datos geográficos o un tipo de medios, esos atributos de filtro no van a estar disponibles para su instancia.

![filtros adicionales](./images/insights/additional-filters.png)

![ventana emergente de filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Canal]:** La selección del atributo de canal le permite filtrar cualquiera de los canales de marketing disponibles. Puede seleccionar varios canales para compararlos.
- **[!UICONTROL Geografía]:** La selección del atributo de geografía permite filtrar los códigos de país según los modelos basados en regiones. En función de los datos, este filtro puede estar presente o no. Los códigos de país tienen dos caracteres. Ver la lista completa de códigos de país [aquí](https://datahub.io/core/country-list).
- **[!UICONTROL Tipo de medio]:** La selección del atributo de tipo de medio permite filtrar cualquiera de los tipos de medio definidos.
- **[!UICONTROL Product]:** La selección del atributo de producto le permite filtrar cualquier producto que se haya introducido inicialmente en la creación de la instancia.

### Date Range

Seleccione el icono de calendario para abrir la ventana emergente de intervalo de fechas. Las fechas de los eventos de conversión inicial y final determinan la cantidad de datos que se rellenan en la interfaz de usuario. Puede elegir reducir o ampliar el intervalo de fechas para enfocar o expandir la cantidad de datos rellenados.

![intervalo de fecha](./images/insights/display-date-range.png)

## Información general sobre los datos

El **[!UICONTROL Información general]** La tarjeta muestra las conversiones totales por modelo de atribución. El número total cambia en función de lo específico que realice la búsqueda con los filtros descritos anteriormente en este documento. Al seleccionar más modelos, se añaden círculos adicionales a la Información general, cada uno con su propio color correspondiente a la leyenda.

Información general del ![](./images/insights/Overview.png)

## Tendencias semanales

El **[!UICONTROL Tendencias semanales]** La tarjeta desglosa la conversión total según el intervalo de fechas establecido durante el proceso de filtrado.

Selección de los puntos suspensivos en la parte superior derecha de la **Tendencias semanales** La tarjeta muestra una lista desplegable que le permite seleccionar tendencias diarias, semanales o mensuales.

Al pasar el ratón por encima de la línea de datos de un modelo de atribución específico, se crea una ventana emergente que muestra el número total de conversiones para esa fecha.

![tendencias](./images/insights/weekly-trends.png)

## Desglose por canal

El **[!UICONTROL Desglose por canal]** se utiliza para determinar el número total de conversiones en relación con cada canal. Esta tarjeta se puede utilizar para ayudar a tomar decisiones sobre la eficacia de cada canal y el retorno de la inversión.

Selección de los puntos suspensivos en la parte superior derecha de la **[!UICONTROL Desglose por canal]** La tarjeta abre un menú desplegable que le permite rellenar datos en función de los puntos de contacto.

![canal de desglose](./images/insights/channel-breakdown.png)

## Campañas principales

El **[!UICONTROL Campañas principales]** Esta tarjeta muestra una descripción general de las campañas y del rendimiento de la campaña en cada canal. Esta tarjeta puede ayudar a informar a su equipo de la eficacia de una campaña específica para un canal determinado y proporcionar perspectivas como en qué campañas debe invertir más.

![campañas principales](./images/insights/top-campaigns.png)

## Desglose por posición de punto de contacto

Selección de la **[!UICONTROL Análisis de rutas]** carga la pestaña **[!UICONTROL Desglose por posición de punto de contacto]** y **[!UICONTROL Rutas de conversión principales]** gráficos.

El **[!UICONTROL Desglose por posición de punto de contacto]** el gráfico es un desglose de las conversiones atribuidas por posición del punto de contacto comparado en todas las rutas de conversión. Este gráfico le ayuda a comprender qué puntos de contacto son más efectivos en diferentes etapas de la ruta de conversión. Las etapas son inicio, jugador y más cerca.

- **Motor de arranque:** Indica que el punto de contacto fue el primer contacto en una ruta de conversión.
- **Reproductor:** Indica que el punto de contacto no fue el primer ni el último contacto que provocó una conversión.
- **Más cerca:** Indica que el punto de contacto fue el último contacto antes de una conversión.

>!![NOTE]
La suma de la contribución porcentual para un modelo de atribución en todos los puntos de contacto y posiciones debe ser igual a 100.

![punto de contacto de desglose de ruta de usuario](./images/insights/user-paths.png)

## Rutas de conversión principales

El **[!UICONTROL Rutas de conversión principales]** El gráfico muestra las puntuaciones influenciadas y algorítmicas de las rutas de conversión principales en las regiones seleccionadas. Este gráfico le permite visualizar qué puntos de contacto contribuyen a las conversiones y cuál es la puntuación de atribución para cada punto de contacto. Puede utilizar esta información para ver las rutas más frecuentes en una región determinada y ver si surge algún patrón entre los diferentes conjuntos de puntos de contacto.

![Rutas de usuario más comunes](./images/insights/Touchpoint-paths.png)

## Eficacia de Touchpoint

Selección de la **[!UICONTROL Eficacia de Touchpoint]** carga la pestaña **[!UICONTROL Eficacia de Touchpoint]** Tarjeta de. Esta tarjeta utiliza la distribución de datos de Attribution AI para mostrar información de cada punto de contacto. Los datos de esta tabla solo se generan para periodos de tiempo específicos indicados por la variable **[!UICONTROL A partir de]** fecha en la parte superior derecha de la tarjeta.

![selección de efectividad de touchpoint](./images/insights/Touchpoint-effectiveness.png)

Puede usar el complemento **[!UICONTROL Eficacia de Touchpoint]** información de la tarjeta para comprender cómo contribuye un punto de contacto a una conversión. También puede ver la eficacia de cada punto de contacto con las siguientes métricas de rendimiento:

**Rutas tocadas**: Esta métrica muestra un porcentaje de rutas que logran/no logran la conversión para el punto de contacto. Verá conversiones atribuidas más altas si la proporción de rutas (porcentaje) que logran la conversión en rutas que no logran la conversión es alta.

![Métrica de rutas tocadas](./images/insights/Touchpoint-metrics.png)

**Medida de eficiencia**: Esta métrica muestra las estrellas en una escala de uno a cinco. La escala indica la importancia relativa de un punto de contacto para realizar una conversión.

>[!NOTE]
Un volumen de punto de contacto más alto no garantiza una medida de eficiencia más alta.

**Volumen total**: el número agregado de veces que un usuario ha tocado un punto de contacto. Esto incluye puntos de contacto que aparecen en una ruta que logra la conversión, así como rutas que no resultan en una conversión.

## Pasos siguientes

Una vez que haya terminado de filtrar los datos y haya podido mostrar la información adecuada, tiene la opción de acceder a las puntuaciones. Si desea obtener una guía detallada sobre cómo acceder a sus puntuaciones, visite la [puntuaciones de acceso en Attribution AI](./download-scores.md) tutorial. Además, también puede descargar los datos de resumen como se indica en [más acciones](#more-actions). Al seleccionar &quot;Descargar datos de resumen&quot;, se descargan los datos de resumen agregados por fechas.

## Recursos adicionales

El siguiente vídeo está diseñado para ayudarle a aprender a utilizar la página de perspectivas de Attribution AI con el fin de comprender el ROI de los canales y campañas de marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
