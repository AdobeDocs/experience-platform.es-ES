---
keywords: Experience Platform;insights;attribution ai;popular topics;attribution ai insights
solution: Experience Platform
title: Descubrimiento de perspectivas en Attribution AI
topic: Attribution AI insights
description: Este documento sirve como guía para interactuar con perspectivas de instancias de servicio en la interfaz de usuario de Adobe Intelligent Services.
translation-type: tm+mt
source-git-commit: 69c27fc45aa9d9acaaed29c2324d02ebd471d63d
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 0%

---


# Descubrimiento de perspectivas en Attribution AI

Las instancias de servicio de Attribution AI proporcionan perspectivas que pueden utilizarse para ayudar a tomar y medir las decisiones de marketing relacionadas con el rendimiento de marketing y el retorno de la inversión. La selección de una instancia de servicio proporciona visualizaciones y filtros para ayudarle a comprender el impacto de cada interacción con los clientes en cada fase del viaje del cliente.

Este documento sirve como guía para interactuar con perspectivas de instancias de servicio en la interfaz de usuario de Adobe Intelligent Services.

## Primeros pasos

Para utilizar perspectivas para Attribution AI, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite la guía [de la interfaz de usuario de](./user-guide.md)Attribution AI. Si ha creado recientemente una instancia de servicio y aún está en formación y puntaje, espere 24 horas para que termine de ejecutarse.

## Información general sobre perspectivas de instancias de servicio

En la [!DNL Adobe Experience Platform] interfaz de usuario, seleccione **[!UICONTROL Servicios]** en el panel de navegación izquierdo. Aparece el navegador **[!UICONTROL Servicios]** y muestra los servicios inteligentes de Adobe disponibles. En el contenedor de Attribution AI, seleccione **[!UICONTROL Abrir]**.

![Acceso a la instancia](./images/insights/open_Attribution_ai.png)

Aparece la página de servicio de Attribution AI. Esta página lista las instancias de servicio de Attribution AI y muestra información sobre ellas, incluido el nombre de la instancia, los eventos de conversión, la frecuencia con la que se ejecuta la instancia y el estado de la última actualización. Seleccione un nombre de instancia de servicio para comenzar.

>[!NOTE]
>
>Solo se pueden seleccionar las instancias de servicio que hayan completado correctamente las ejecuciones de puntuación.

![Crear instancia](./images/insights/select-service-instance.png)

A continuación, se abre la página de perspectivas de esa instancia de servicio, donde se le proporcionan visualizaciones y una serie de filtros para interactuar con sus datos. Las visualizaciones y filtros se explican con más detalle en esta guía.

![página de configuración](./images/insights/landing-page.png)

### Detalles de instancia de servicio

Para vista de detalles adicionales para una instancia de servicio, seleccione **[!UICONTROL Mostrar más]** en la parte superior derecha.

![mostrar más](./images/insights/show-more.png)

Aparece una lista detallada. Para obtener más información sobre cualquiera de las propiedades enumeradas, visite la guía del usuario de [Attribution AI](./user-guide.md).

![mostrar detalles](./images/insights/advanced-details.png)

### Editar una instancia

Para editar una instancia, seleccione **[!UICONTROL Editar]** en la navegación superior derecha.
![haga clic en el botón de edición](./images/insights/edit-button.png)

Aparece el cuadro de diálogo de edición, que le permite editar el nombre, la descripción y la frecuencia de puntuación de la instancia. Si el estado de la instancia está desactivado, no se puede editar la frecuencia de puntuación. Para confirmar los cambios y cerrar el cuadro de diálogo, seleccione **[!UICONTROL Guardar]** en la esquina inferior derecha.

![editar pover](./images/insights/edit-popover.png)

### Más acciones {#more-actions}

El botón **[!UICONTROL Más acciones]** se encuentra en la navegación superior derecha junto a **[!UICONTROL Editar]**. Al seleccionar **[!UICONTROL Más acciones]** se abre un menú desplegable que permite seleccionar una de las siguientes operaciones:

- **[!UICONTROL Clonar]**: Clona la instancia.
- **[!UICONTROL Eliminar]**: Elimina la instancia.
- **[!UICONTROL Descargar datos]** de resumen: Descarga un archivo CSV que contiene los datos de resumen.
- **[!UICONTROL Puntuaciones]** de acceso: Al seleccionar **[!UICONTROL Access score]** , se le redirige a las puntuaciones de [acceso para el tutorial](./download-scores.md)de Attribution AI.
- **[!UICONTROL Historial]** de ejecución de vistas: Aparece una ventana emergente que contiene una lista de todas las ejecuciones de puntuación asociadas con la instancia de servicio.

![más acciones](./images/insights/more-actions.png)

## Filtrado de datos

Las perspectivas de Attribution AI le permiten filtrar los datos y actualizar automáticamente los elementos visuales de la interfaz de usuario en función de los filtros seleccionados.

### Evento de conversión

Cuando se crea una nueva instancia en Attribution AI, uno de los campos obligatorios es &quot;eventos de conversión&quot;. Los eventos de conversión son objetivos comerciales que identifican el impacto de las actividades de mercadotecnia, como los pedidos de comercio electrónico, las compras en el almacén y las visitas al sitio web.

Desde la instancia, la lista desplegable eventos **[!UICONTROL de]** conversión permite seleccionar cualquiera de los eventos definidos para la instancia a fin de filtrar los datos. Al seleccionar eventos específicos, se cambian las visualizaciones de la interfaz de usuario para rellenar solo las conversiones que pertenecen a esos eventos.

![evento de conversión](./images/insights/conversion-event.png)

### Modelo de atribución

Al seleccionar Modelo **[!UICONTROL de atribución]** se abre una lista desplegable con todos los modelos de atribución disponibles. Puede seleccionar varios modelos para comparar los resultados. Para obtener más información sobre los distintos modelos de atribución y cómo funcionan, visite la información general de [Attribution AI](./overview.md) que contiene una tabla con información sobre cada modelo.

![modelo de atribución](./images/insights/attribution-model.png)

### Región

>[!NOTE]
>
>Este filtro solo está presente si ha realizado el modelado [opcional basado en](./user-guide.md#region-based-modeling-optional) región de pasos en la guía de interfaz de usuario de Attribution AI al crear la instancia de servicio.

Este filtro le permite seleccionar cualquier región que configure en el proceso de creación de instancias.

### Añadir filtros

Puede agregar filtros adicionales seleccionando el icono de **filtro** para abrir la ventana emergente **[!UICONTROL Añadir filtros]** . La ventana emergente **[!UICONTROL Añadir filtros]** le permite filtrar por Canal, geografía, tipo de medio y producto. La ventana emergente sólo rellena los filtros aplicables para una instancia de servicio. Por ejemplo, si no proporcionó datos geográficos o un tipo de medio, esos atributos de filtro no estarán disponibles para su instancia.

![filtros adicionales](./images/insights/additional-filters.png)

![ventana emergente de filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Canal]:** La selección del atributo canal permite filtrar cualquiera de los canales de mercadotecnia disponibles. Puede seleccionar varios canales para compararlos.
- **[!UICONTROL Geografía]:** La selección del atributo geográfico permite filtrar los códigos de país en función de los modelos basados en regiones. Según sus datos, este filtro puede estar presente o no. Los códigos de país tienen dos caracteres. Consulte la lista completa del código de país [aquí](https://datahub.io/core/country-list).
- **[!UICONTROL Tipo]de medio:** La selección del atributo de tipo de medio le permite filtrar cualquiera de los tipos de medios definidos.
- **[!UICONTROL Producto]:** La selección del atributo product permite filtrar desde cualquier producto que se haya ingerido inicialmente en la creación de la instancia.

### Date Range

Seleccione el icono de calendario para abrir la ventana emergente de intervalo de fechas. Las fechas de evento de conversión inicial y final determinan la cantidad de datos rellenados en la interfaz de usuario. Puede elegir reducir o ampliar el intervalo de fechas para enfocar o expandir la cantidad de datos rellenados.

![intervalo de fechas](./images/insights/display-date-range.png)

## Información general sobre sus datos

La tarjeta **[!UICONTROL Información general]** muestra las conversiones totales según el modelo de atribución. El número total cambia en función de la cantidad específica que realice la búsqueda mediante los filtros descritos anteriormente en este documento. Al seleccionar más modelos, se agregan círculos adicionales a la Información general, cada uno con su propio color correspondiente a la leyenda.

![sobre validación](./images/insights/Overview.png)

## Tendencias semanales

La tarjeta de tendencias **** semanales desglosa la conversión total según el intervalo de fechas definido durante el proceso de filtrado.

Al seleccionar las elipses en la parte superior derecha de la tarjeta de tendencias **** semanales, se muestra un menú desplegable que permite seleccionar las tendencias diarias, semanales o mensuales.

Al pasar el ratón sobre la línea de datos de un modelo de atribución específico, se crea una ventana emergente que muestra el número total de conversiones para esa fecha.

![tendencias](./images/insights/weekly-trends.png)

## Desglose por canal

El **[!UICONTROL desglose por tarjeta de canal]** se utiliza para determinar el número total de conversiones en relación con cada canal. Esta tarjeta puede utilizarse para ayudar a tomar decisiones sobre la efectividad de cada canal y el rendimiento de la inversión.

Al seleccionar las elipses en la parte superior derecha de la tarjeta **[!UICONTROL Desglosar por canal]** , se abre una lista desplegable que permite rellenar datos en función de los puntos de contacto.

![canal de desglose](./images/insights/channel-breakdown.png)

## Campañas principales

La tarjeta campañas **** principales muestra información general sobre sus campañas y el rendimiento de la campaña en cada canal. Esta tarjeta puede ayudar a informar a su equipo de la efectividad de una campaña específica para un canal determinado y proporcionar perspectivas como las campañas en las que debe invertir más.

![campañas principales](./images/insights/top-campaigns.png)

## Desglose por posición del punto de contacto

Al seleccionar la ficha Análisis **[!UICONTROL de]** ruta, se carga el **[!UICONTROL desglose por posición]** de punto de contacto y los gráficos de rutas **[!UICONTROL de conversión]** principales.

El gráfico de **[!UICONTROL desglose por posición]** de punto de contacto es un desglose de las conversiones atribuidas por posición del punto de contacto en comparación con todas las rutas de conversión. Este gráfico ayuda a comprender qué puntos de contacto son más eficaces en las distintas etapas de la ruta de conversión. Los escenarios son el comienzo, el jugador y más cerca.

- **Inicio:** Indica que el punto de contacto fue el primer toque de una ruta de conversión.
- **Reproductor:** Indica que el punto de contacto no fue el primer o el último toque que llevó a una conversión.
- **Más cerca:** Indica que el punto de contacto fue el último toque antes de una conversión.

>!![NOTE]
La suma de la contribución porcentual para un modelo de atribución en todos los puntos de contacto y posiciones debe ser igual a 100.

![touchpoint de desglose de ruta de usuario](./images/insights/user-paths.png)

## Rutas de conversión principales

El gráfico de rutas **[!UICONTROL de conversión]** principales muestra las puntuaciones algorítmicas e influenciadas en las rutas de conversión principales de las regiones seleccionadas. Este gráfico le permite visualizar qué puntos de contacto contribuyen a las conversiones y cuál es la puntuación de atribución para cada punto de contacto. Puede utilizar esta información para vista de las rutas más frecuentes de una región determinada y ver si algún patrón surge entre los distintos conjuntos de puntos de contacto.

![Rutas de usuario más comunes](./images/insights/Touchpoint-paths.png)

## Eficacia de Touchpoint

Al seleccionar la ficha **[!UICONTROL Eficacia]** de los puntos de contacto, se carga la tarjeta de eficacia **[!UICONTROL de los puntos de]** contacto. Esta tarjeta utiliza la distribución de datos de Attribution AI para mostrar la información de cada punto de contacto. Los datos de esta tabla solo se generan para períodos de tiempo específicos como se indica en el **[!UICONTROL A partir]** de la fecha en la parte superior derecha de la tarjeta.

![selección de efectividad de touchpoint](./images/insights/Touchpoint-effectiveness.png)

Puede utilizar la información de la tarjeta de eficacia **[!UICONTROL de]** Touchpoint para comprender cómo un touchpoint contribuye a una conversión. También puede ver la eficacia de cada punto de contacto con las siguientes métricas de rendimiento:

**Las rutas tocaron**: Esta métrica muestra un porcentaje de rutas que alcanzan o no la conversión para el punto de contacto. Verá conversiones atribuidas más altas si la proporción de rutas (porcentaje) que alcanzan la conversión a rutas que no alcanzan la conversión es alta.

![Métrica de rutas afectadas](./images/insights/Touchpoint-metrics.png)

**Medición** de eficiencia: Esta métrica muestra las estrellas en una escala de uno a cinco. La escala indica la importancia relativa de un punto de contacto para realizar una conversión.

>[!NOTE]
Un mayor volumen de puntos de contacto no garantiza una medida de mayor eficiencia.

**Volumen** total: Número acumulado de veces que un usuario tocó un punto de contacto. Esto incluye los puntos de contacto que aparecen en una ruta que alcanza la conversión, así como las rutas que no resultan en una conversión.

## Pasos siguientes

Una vez que haya terminado de filtrar los datos y pueda mostrar la información adecuada, tiene la opción de acceder a las puntuaciones. Para obtener una guía detallada sobre cómo acceder a las puntuaciones, visite las puntuaciones de [acceso en el tutorial de Attribution AI](./download-scores.md) . Además, también puede descargar los datos de resumen como se indica en [más acciones](#more-actions). Al seleccionar &quot;Descargar datos de resumen&quot; se descargan los datos de resumen agregados por fechas.

## Recursos adicionales

El siguiente vídeo está diseñado para ayudarle en el aprendizaje de cómo utilizar la página de perspectivas de Attribution AI para comprender el ROI de los canales y campañas de mercadotecnia.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)