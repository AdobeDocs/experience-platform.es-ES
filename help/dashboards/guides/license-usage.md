---
keywords: Experience Platform;interfaz de usuario;IU;personalización;tablero de uso de licencias;tablero;uso de licencias;asignación de derechos;consumo
title: Tablero de uso de licencias
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca del uso de licencias de su organización.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 1c31ef58eec727638cab28202afc762da0e226a2
workflow-type: tm+mt
source-wordcount: '3125'
ht-degree: 22%

---

# Panel de uso de licencias {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Cuadro de diálogo de prueba que no debería estar visible"
>abstract="El objeto {name} se está viendo el {date}."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Tabla de productos principales"
>abstract="Los productos principales enumerados en la tabla tienen sus propias métricas, seguimiento de uso y vistas de obtención de detalles a nivel de zona protegida. Estos productos principales proporcionan las métricas clave para el seguimiento y todos los complementos se incluyen en estas métricas."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Tabla de complementos"
>abstract="La tabla de complementos enumera los productos cuyas cantidades de licencias se combinan con las métricas admitidas por los productos principales. Estos complementos no tienen métricas independientes, pero mejoran el seguimiento de uso de los productos principales con los que están asociados."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Panel de uso de licencias"
>abstract="El panel de uso de licencias ofrece datos de los productos de Adobe Experience Platform que ha adquirido. La información general del panel muestra las métricas principales de sus productos, incluido el uso de cada una de las métricas principales y el importe de la licencia contratada. El espacio de trabajo de detalles muestra un desglose de las métricas de cada producto dentro de zonas protegidas específicas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=es" text="Caducidades de conjuntos de datos automatizados"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Panel de uso de licencias"
>abstract="El panel de uso de licencias ofrece datos de los productos de Adobe Experience Platform que ha adquirido. La información general del panel muestra las métricas principales de sus productos, incluido el uso de cada una de las métricas principales y el importe de la licencia contratada. El espacio de trabajo de detalles muestra un desglose de las métricas de cada producto dentro de zonas protegidas específicas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=es" text="Caducidades de conjuntos de datos automatizados"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="Horas calculadas previstas"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para evaluar o reducir las horas de cálculo, vaya a Consultas > Registro para revisar el historial de consultas. Si no tiene permiso para acceder al espacio de trabajo Consultas, póngase en contacto con el administrador."
>additional-url="https://experience.adobe.com/#/platform/query/log.html?lang=es" text="Espacio de trabajo Registro de consultas"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Público destinatario previsto"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=es" text="Caducidades de eventos de experiencia"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Perfiles atractivos previstos"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=es" text="Caducidades de eventos de experiencia"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Perfil del empresario previsto"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=es" text="Caducidades de eventos de experiencia"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Horario principal previsto"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=es" text="Caducidades de eventos de experiencia"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Volumen total de datos previsto"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=es" text="Caducidades de eventos de experiencia"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Filas de CJA previstas disponibles"
>abstract="Su uso podría alcanzar la cantidad bajo licencia. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=es" text="Caducidades de eventos de experiencia"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

Puede ver información importante sobre el uso de licencias de su organización en el panel de control de Adobe Experience Platform [!UICONTROL Uso de licencias]. La información que se muestra aquí se captura durante una captura diaria de la instancia de Platform.

Los informes de uso de licencias proporcionan un alto grado de granularidad sobre las métricas de uso de licencias. El panel proporciona métricas de uso para cada producto comprado (y complementos asociados), el uso consolidado de métricas en todas las zonas protegidas de producción o desarrollo y la métrica de uso de una zona protegida específica. Las siguientes aplicaciones de Experience Platform se pueden rastrear con métricas de uso: Real-Time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

Esta guía describe cómo acceder y trabajar con el tablero de uso de licencias en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el tablero.

Para obtener una descripción general de la IU de Platform, consulte la [guía de la IU de Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL Uso de licencias] datos de tablero

El tablero [!UICONTROL Uso de licencias] muestra una lista de todos los productos de Experience Platform que ha comprado y los complementos de dichos productos. Desde este panel, puede encontrar una instantánea de los datos relacionados con las licencias de su organización para Experience Platform en cualquier zona protegida asociada.

Los datos de este tablero se muestran exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y el panel no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Exploración del tablero de uso de licencias {#explore}

Para navegar al panel de uso de licencias dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Uso de licencias]** en el carril izquierdo. Se abre la pestaña [!UICONTROL Información general], que muestra una lista de los productos disponibles.

>[!NOTE]
>
>El panel de uso de licencias no está habilitado de forma predeterminada. Los usuarios deben tener permiso para &quot;Ver tablero de uso de licencias&quot; para poder ver el tablero. Para obtener los pasos sobre la concesión de permisos de acceso para ver el tablero de uso de licencias, consulte la [guía de permisos de tablero](../permissions.md).

![Pestaña Información general del tablero de uso de licencias, con uso de licencias resaltado en la barra lateral de navegación izquierda.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Ficha Información general] {#overview-tab}

El panel [!UICONTROL Uso de licencias] muestra dos tablas independientes: **Productos principales** y **Complementos**.

- **[!UICONTROL Tabla de productos principales]**: Esta tabla enumera los principales productos de Adobe Experience Platform con licencia de su organización. Cada producto principal tiene sus propias métricas, seguimiento de uso y vistas de obtención de detalles a nivel de zona protegida. Estos productos principales proporcionan las métricas clave para el seguimiento y todos los complementos se incluyen en estas métricas.

- **[!UICONTROL Tabla de complementos]**: Esta tabla enumera productos adicionales cuyas cantidades de licencias se combinan con las métricas admitidas por los productos principales. Los complementos no tienen métricas independientes, pero mejoran el seguimiento de uso de los productos principales con los que están asociados.

| Nombre de columna | Descripción |
|---|---|
| **[!UICONTROL Producto]** | La solución de Adobe con licencia de su organización. |
| **[!UICONTROL Métrica principal]** | La métrica principal utilizada para el seguimiento dentro de ese producto. |
| **[!UICONTROL Importe de licencia]** | El valor contratado para la cantidad máxima de la métrica principal según lo acordado en el contrato de licencia del producto. |
| **[!UICONTROL Uso]** | Cantidad de la métrica principal utilizada. Este valor proporciona el uso total de esa métrica en todas las zonas protegidas, ya sea de producción o desarrollo. |
| **[!UICONTROL Uso %]** | El porcentaje de la métrica principal utilizado según la cantidad de licencia. |
| **[!UICONTROL Uso de predicción]** | El porcentaje de uso previsto de la métrica principal según la cantidad de licencia. |

>[!NOTE]
>
>Las cantidades de licencias para complementos se incluyen en [!UICONTROL Cantidad de licencias] de los productos principales. Por ejemplo, si compra un paquete de cinco zonas protegidas como complemento, la cantidad se agrega a la del producto base. La tabla de complementos muestra un [!UICONTROL Importe de licencia] específico del complemento, pero el uso real se rastrea a través del producto base.

Las tablas indican la métrica principal de cada producto, ya que cada producto puede realizar el seguimiento de numerosas métricas.

### Uso previsto {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Uso previsto"
>abstract="Las predicciones se basan en el uso durante los últimos 6 a 7 meses y se generan el 15 de cada mes. Tenga en cuenta que las predicciones del uso de licencias son aproximaciones basadas en el uso anterior. Usted es responsable de comprender el uso real de su organización y de garantizar que el uso no vaya más allá del ámbito de la licencia de su organización con Adobe. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=es" text="Caducidades de conjuntos de datos automatizados"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Uso previsto"
>abstract="Las predicciones se basan en el uso durante los últimos 6 a 7 meses y se generan el 15 de cada mes. Tenga en cuenta que las predicciones del uso de licencias son aproximaciones basadas en el uso anterior. Usted es responsable de comprender el uso real de su organización y de garantizar que el uso no vaya más allá del ámbito de la licencia de su organización con Adobe. Para reducir el uso, puede configurar las caducidades de los datos del conjunto de datos o de perfiles seudónimos para las zonas protegidas y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=es" text="Caducidades de conjuntos de datos automatizados"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de los datos de perfiles seudónimos"

Administre y optimice de forma proactiva sus recursos de licencias en función de predicciones de uso reveladoras. La columna [!UICONTROL Uso predicho] predice con precisión el uso futuro de licencias en el nivel de zona protegida, en todas las zonas protegidas de producción y desarrollo, para todos los productos que haya comprado. Esta capacidad de alerta proporciona una previsión del uso de licencias para seis semanas en el futuro, en función de su uso hasta el 15 de este mes natural. Las predicciones se proporcionan con un límite inferior y otro superior.

>[!IMPORTANT]
>
>Las predicciones se actualizan mensualmente. La fecha de actualización se incluye en un icono de información (![Este icono de información.](../images/license-usage/info-icon.png)) sobre el título de columna.

Para ver un resumen del uso de derechos de un producto, seleccione un producto de la tabla [!UICONTROL Productos principales].

![El [!UICONTROL uso de licencias] [!UICONTROL Información general] con un producto y la columna de uso previsto resaltada.](../images/license-usage/product-predicted-usage.png)

Aparecerá la pestaña Resumen. Puede usar las predicciones detalladas disponibles en las pestañas [!UICONTROL Resumen] y [!UICONTROL Detalles] para garantizar una toma de decisiones informada y un uso eficiente de la licencia.

>[!NOTE]
>
>Tenga en cuenta que las predicciones del uso de licencias son aproximaciones basadas en el uso anterior. Usted es responsable de comprender el uso real de su organización y de garantizar que el uso no vaya más allá del ámbito de la licencia de su organización con Adobe.

![Vista de resumen de un producto de Platform con la columna de uso previsto resaltada.](../images/license-usage/summary-predicted-usage.png)

El porcentaje de uso previsto se determina de la siguiente manera:

- Si los límites inferior y superior son significativamente diferentes, se muestran como un rango (por ejemplo, 32 % - 35 %).
- Si los límites inferior y superior son casi idénticos y no son cero, se muestran como un valor aproximado (por ejemplo, ~34%).
- Si los límites inferior y superior son casi idénticos y cero, se muestran exactamente como 0%.

>[!NOTE]
>
>&quot;Casi idéntico&quot; en este contexto significa que los valores son estadísticamente significativos para dos decimales (por ejemplo, un límite inferior de 0,342 y un límite superior de 0,344 se redondean al 34 %).

La función de uso previsto admite las siguientes métricas:

- [!UICONTROL Audiencia a la que se puede dirigir]
- [!UICONTROL Calcular horas]
- [!UICONTROL Número de filas de la audiencia del Recorrido del cliente]
- [!UICONTROL Volumen total de datos]

## Pestaña [!UICONTROL Resumen] {#summary-tab}

Para ver más métricas e información detallada sobre el uso de la licencia del producto, seleccione un nombre de producto de la lista. Aparece la vista [!UICONTROL Resumen] de ese producto. Todas las métricas disponibles se muestran en la ficha [!UICONTROL Resumen]. Las métricas disponibles dependen del producto con licencia. Esta vista proporciona **una vista consolidada de todas las métricas en todos los entornos limitados de producción o desarrollo**. El mismo nivel de análisis se proporciona para los entornos limitados de producción y desarrollo.

![Vista de resumen de un producto de Platform que muestra todas las métricas disponibles para ese producto.](../images/license-usage/summary-tab.png)

En la ficha Resumen, la tabla incluye la columna [!UICONTROL Métrica]. Estas descripciones legibles en lenguaje natural indican todas las métricas utilizadas para ese tipo de zona protegida.

### Seleccionar una zona protegida {#select-sandbox}

Para cambiar la vista entre los tipos de zonas protegidas de producción y desarrollo, seleccione [!UICONTROL zonas protegidas de producción] o [!UICONTROL zonas protegidas de desarrollo]. El tipo de zona protegida seleccionado se indica con el botón de opción situado junto al nombre de la zona protegida.

Los informes de consumo para las zonas protegidas son acumulativos para todas las zonas protegidas del mismo tipo. En otras palabras, al seleccionar [!UICONTROL Producción] o [!UICONTROL Desarrollo] se proporcionan informes de consumo para todas las zonas protegidas de producción o desarrollo, respectivamente.

![Vista de resumen de un producto de Platform con las zonas protegidas de producción y las de desarrollo resaltadas.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>El permiso para ver el tablero de uso de licencias debe especificarse en el nivel de zona protegida. Añada permisos a cada zona protegida individual para verlos dentro del panel. Esta limitación se solucionará en una versión futura. Mientras tanto, está disponible la siguiente solución:
>
>1. Cree un perfil de producto en Adobe Admin Console.
>2. En Permiso en la categoría Zona protegida, agregue todas las zonas protegidas que desee ver en el panel de uso de licencias.
>3. En la categoría Permiso del tablero de usuarios, agregue el permiso &quot;Ver tablero de uso de licencias&quot;.

## Ficha [!UICONTROL Detalles] {#details-tab}

Para ver **una métrica de uso en particular de una zona protegida específica**, vaya a la pestaña [!UICONTROL Detalles]. La pestaña [!UICONTROL Detalles] muestra todas las zonas protegidas disponibles en las zonas protegidas de producción o desarrollo.

![Pestaña Detalles del tablero de uso de licencias.](../images/license-usage/details-tab.png)

Desde esta vista, puede seleccionar ![El icono de inspección.](/help/images/icons/inspect.png) junto al nombre de una zona protegida para ver la visualización de esa métrica. Se abrirá un cuadro de diálogo con una visualización para esa métrica.

### Visualizaciones {#visualizations}

Cada widget de visualización incluye los siguientes aspectos:

- Gráfico de líneas que registra el cambio de la métrica a lo largo del tiempo
- Una clave para el gráfico de líneas
- Nombre de la zona protegida
- Menú desplegable para ajustar el período de tiempo del gráfico de líneas

Los gráficos de líneas comparan los números de uso de su organización con el total disponible con las licencias de su organización y proporcionan un porcentaje del uso total.

![Visualización de una métrica.](../images/license-usage/visualization.png)

El periodo retrospectivo de análisis se puede ajustar desde el menú desplegable. El valor predeterminado de los últimos 30 días

Para seleccionar un intervalo de fecha, puede utilizar la lista desplegable de intervalo de fecha para seleccionar el período de tiempo que se mostrará en el panel. Hay varias opciones disponibles, incluido el valor predeterminado de los últimos 30 días.

![Se resaltó el cuadro de diálogo de visualización con la lista desplegable de intervalo de fechas.](../images/license-usage/date-range.png)

También puede seleccionar **[!UICONTROL Fecha personalizada]** para elegir el período de tiempo que se muestra.

![Pestaña Información general del tablero de uso de licencias con las opciones de intervalo de fechas personalizadas resaltadas.](../images/license-usage/custom-date-range.png)

## Métricas disponibles {#available-metrics}

>[!IMPORTANT]
>
>A partir del 20 de agosto, los clientes con derechos para &#39;[!UICONTROL Average Profile Richness]&#39; y &#39;[!UICONTROL Total Storage]&#39; vieron &#39;[!UICONTROL Total Data Volume]&#39; en el Tablero de uso de licencias. No se han realizado cambios en los derechos de los clientes, solo una simplificación de las métricas de seguimiento. [!UICONTROL Volumen total de datos] representa los datos disponibles en el servicio de perfil de Adobe Experience Platform para los flujos de trabajo de participación y personalización. Esta métrica simplificada mejoró la administración y la medición del uso del servicio de perfil. Se animó a los clientes a ponerse en contacto con su representante de Adobe para obtener más aclaraciones sobre este cambio.

El panel de uso de licencias informa sobre varias métricas únicas que se aplican a varios productos de la organización. Las métricas disponibles son:

| Métrica | Descripción |
|---|---|
| [!UICONTROL Tamaño Audience Activation] | El tamaño total de los perfiles activados en cualquier destino basado en archivos en un año. Nota: Esto no incluye perfiles enviados a través de destinos de flujo continuo. |
| [!UICONTROL Audiencia a la que se puede dirigir] | La suma de los derechos de audiencia empresarial y de audiencia de consumidor. Una audiencia de consumidor se define como el número de perfiles de persona identificados como una &quot;Audiencia de consumidor&quot; en el pedido de ventas. Una audiencia empresarial se define como el número de perfiles de personas de negocios identificados como la &quot;Audiencia empresarial&quot; en el pedido de ventas. |
| [!UICONTROL Paquetes de usuarios de servicio de consultas ad hoc] | Un complemento para aumentar el derecho de los usuarios autorizados del servicio de consulta simultánea en cinco usuarios adicionales del servicio de consulta simultánea y una consulta ad hoc adicional que se ejecuta simultáneamente por paquete. Se pueden adquirir licencias para varios paquetes de usuarios de Ad Hoc Query adicionales. |
| [!UICONTROL Promedio de riqueza de perfiles] | **Obsoleto**: la suma de todos los datos de producción almacenados en el servicio de perfil de concentrador en cualquier momento, dividida por cinco veces el número de perfiles de personas de negocios autorizados. [!UICONTROL Promedio de riqueza de perfiles] es una característica compartida. |
| [!UICONTROL Filas CJA disponibles] | Las filas medias diarias de datos disponibles para su análisis en Customer Journey Analytics. |
| [!UICONTROL Atributos calculados] | Recuento total de datos de comportamiento del perfil agregados. Los datos de comportamiento del perfil agregados se basan en eventos de experiencia que se convierten en un atributo de perfil y que pueden incluirse en un perfil de persona o un perfil de persona de negocios. |
| [!UICONTROL Audiencia del consumidor] | El número de perfiles de persona identificados como &quot;Audiencia del consumidor&quot; en el pedido de ventas. |
| [!UICONTROL Tamaño de exportación de datos] | Cantidad de datos enviados a través de activaciones de conjuntos de datos en un año. |
| [!UICONTROL Exportaciones de datos] | El tamaño total de los conjuntos de datos que se pueden exportar a cualquier solución que no sea de Adobe (directa o indirectamente) en un año. |
| [!UICONTROL Almacenamiento de lago de datos] | Cantidad utilizada del almacén de datos analíticos en Adobe Experience Platform. |
| [!UICONTROL Audiencia atractiva] | Esta métrica hace referencia a la audiencia de perfiles atractivos. Un perfil atractivo es un registro de información que representa a un individuo y se representa en el servicio de perfil. Estos registros son perfiles con los que ha intentado interactuar mediante las capacidades de creación, toma de decisiones, envío, experimentación u orquestación de Journey Optimizer durante los últimos 12 meses. |
| [!UICONTROL Audiencias de similitud] | Recuento de audiencias que se generan al modelar una audiencia de consumidor existente para identificar perfiles de persona similares a la audiencia de consumidor existente. |
| [!UICONTROL Número de modelos AMM] | Un recuento del modelo de aprendizaje automático (integrado en Adobe Mix Modeler) que se utiliza para medir o predecir un resultado especificado en función de sus inversiones. |
| [!UICONTROL Número de zonas protegidas] | Recuento de separaciones lógicas dentro de la instancia de cualquier servicio bajo demanda de Adobe que acceda a los datos y operaciones de aislamiento de Adobe Experience Platform. |
| [!UICONTROL Número de paquetes de riqueza de perfiles] | Un aumento en su volumen total de datos autorizado de 25 KB por perfil para cada paquete de riqueza de perfiles adicional. |
| [!UICONTROL Horas de cálculo del servicio de consultas] | Una medida de la cantidad de tiempo que los motores de servicios de consulta tardan en leer, procesar y escribir datos en el lago de datos cuando se ejecuta una consulta por lotes. |
| [!UICONTROL Nº de paquetes de segmentación de transmisión] | Los paquetes actualizan el abono de segmentos de un perfil de persona a medida que los nuevos datos entran en el servicio de segmentación a través de un flujo de streaming. La pertenencia a segmentos se evalúa en función de los atributos de perfil de la persona actual y el valor del evento actual, sin tener en cuenta el comportamiento histórico. La segmentación por secuencias es una función compartida. |
| [!UICONTROL Volumen total de datos] | Cantidad total de datos disponibles para que el servicio de perfil de Adobe Experience Platform los utilice en los flujos de trabajo de participación. Consulte las [preguntas más frecuentes acerca del volumen total de datos](../../landing/license-usage-and-guardrails/total-data-volume.md) para obtener más información. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Puede comprobar los derechos de licencia en su pedido de ventas para calcular métricas como la &quot;asignación de almacenamiento&quot;.<br>Por ejemplo,<ul><li>Asignación de Almacenamiento = El número de &quot;perfiles autorizados&quot; en su contrato X La riqueza promedio de perfiles</li></ul>

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían según la licencia que haya adquirido su organización. Para obtener definiciones detalladas de cada métrica, consulte la documentación de descripción del producto correspondiente:

| Licencia | Descripción del producto |
| --- | --- |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:ESTÁNDAR OD</li><li>ADOBE EXPERIENCE PLATFORM:PESADO OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, servicios de aplicaciones y servicios inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 10M</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) |
| <ul><li>AEP:ACTIVACIÓN OD</li><li>AEP:ACTIVACIÓN OD PRFL A 10M</li><li>AEP: PERFIL DE ACTIVACIÓN OD DE HASTA 50 M</li></ul> | [Activación de Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELIGENCIA OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>DESACTIVAR AJO PRIME STARTER:OD</li><li>DESACTIVAR AJO ULTIMATE STARTER:OD</li><li>DESACTIVAR Real-Time CDP:ORQUESTACIÓN DE PERFILES OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>El tablero de uso de licencias solo informa de la licencia más reciente aprovisionada para su organización. Si la licencia más reciente aprovisionada para su organización no aparece en la tabla anterior, es posible que el panel de uso de licencias no se muestre correctamente. La compatibilidad con licencias adicionales y múltiples licencias en una sola organización está planificada para una versión futura.

## Pasos siguientes

Después de leer este documento, puede localizar el panel de uso de licencias y ver las métricas de uso de cada producto comprado, de todas las zonas protegidas de producción o desarrollo y de una zona protegida específica. Puede encontrar más información sobre las métricas disponibles para su organización, en función de las licencias que haya adquirido su organización.

Para obtener más información acerca de otras características disponibles en la interfaz de usuario de Experience Platform, consulte la [guía de la interfaz de usuario de Platform](../../landing/ui-guide.md).
