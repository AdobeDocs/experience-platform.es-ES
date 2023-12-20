---
keywords: Experience Platform;interfaz de usuario;IU;personalización;tablero de uso de licencias;tablero;uso de licencias;asignación de derechos;consumo
title: Guía del tablero de uso de licencias
description: Adobe Experience Platform proporciona un tablero a través del cual puede ver información importante acerca del uso de licencias de su organización.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: e80577cb190e77624a2dc32f8343fc4b82a24a03
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 2%

---

# Panel de uso de licencias {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Panel de uso de licencias"
>abstract="El panel de uso de licencias ofrece una perspectiva de los productos de Adobe Experience Platform que ha adquirido. La descripción general del panel muestra las métricas principales de sus productos, incluido el uso de cada una de las métricas principales y el importe de la licencia contratada. El espacio de trabajo de detalles muestra un desglose de las métricas de cada producto dentro de zonas protegidas específicas."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Panel de uso de licencias"
>abstract="El panel de uso de licencias ofrece una perspectiva de los productos de Adobe Experience Platform que ha adquirido. La descripción general del panel muestra las métricas principales de sus productos, incluido el uso de cada una de las métricas principales y el importe de la licencia contratada. El espacio de trabajo de detalles muestra un desglose de las métricas de cada producto dentro de zonas protegidas específicas.<br>Las predicciones de uso se actualizan mensualmente a fin de mes y prevén su uso para el próximo período de seis meses. Para reducir el uso, configure las caducidades de los datos de los conjuntos de datos o perfiles seudónimos para los entornos limitados y los conjuntos de datos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html" text="Caducidad de conjuntos de datos"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=es" text="Caducidad de datos de perfiles seudónimos"

Puede ver información importante sobre el uso de licencias de su organización en Adobe Experience Platform [!UICONTROL Uso de licencias] panel. La información que se muestra aquí se captura durante una captura diaria de la instancia de Platform.

Los informes de uso de licencias proporcionan un alto grado de granularidad sobre las métricas de uso de licencias. El panel proporciona métricas de uso para cada producto comprado, el uso consolidado de métricas en todas las zonas protegidas de producción o desarrollo y la métrica de uso de una zona protegida específica. Las siguientes aplicaciones de Experience Platform se pueden rastrear con métricas de uso: Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics.

Esta guía describe cómo acceder y trabajar con el tablero de uso de licencias en la interfaz de usuario y proporciona más información sobre las visualizaciones que se muestran en el tablero.

Para obtener una descripción general de la IU de Platform, consulte la [Guía de IU de Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL Uso de licencias] datos del panel

El [!UICONTROL Uso de licencias] en el tablero se muestra una lista de todos los productos de Experience Platform que ha adquirido. Desde esta lista, puede encontrar una instantánea de los datos relacionados con las licencias de su organización para Experience Platform en cualquier zona protegida asociada.

Los datos de este tablero se muestran exactamente como aparecen en el momento específico en el que se tomó la instantánea. En otras palabras, la instantánea no es una aproximación o una muestra de los datos y el panel no se actualiza en tiempo real.

>[!NOTE]
>
>Los cambios o actualizaciones realizados en los datos desde que se tomó la instantánea no se reflejarán en el tablero hasta que se tome la siguiente instantánea.

## Exploración del tablero de uso de licencias {#explore}

Para navegar al panel de uso de licencias dentro de la interfaz de usuario de Platform, seleccione **[!UICONTROL Uso de licencias]** en el carril izquierdo. El [!UICONTROL Información general] se abre la pestaña y muestra una lista de los productos disponibles.

>[!NOTE]
>
>El panel de uso de licencias no está habilitado de forma predeterminada. Los usuarios deben tener permiso para &quot;Ver tablero de uso de licencias&quot; para poder ver el tablero. Para ver los pasos sobre la concesión de permisos de acceso para ver el panel de uso de licencias, consulte la [guía de permisos del panel](../permissions.md).

![La pestaña Información general del tablero Uso de licencias, con Uso de licencias resaltado en la barra lateral de navegación izquierda.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Información general] pestaña {#overview-tab}

Este tablero muestra todos sus productos de Adobe Experience Platform con licencia, incluidos los complementos, en formato de tabla. La tabla proporciona información clave sobre el uso de la licencia en todos los perfiles disponibles.

| El nombre de la columna | Descripción |
|---|---|
| **[!UICONTROL Producto]** | La solución de Adobe con licencia de su organización. |
| **[!UICONTROL Métrica principal]** | La métrica principal utilizada para rastrear en para ese producto. |
| **[!UICONTROL Importe de licencia]** | El valor contratado para la cantidad máxima de la métrica principal según lo acordado en el contrato de licencia del producto. |
| **[!UICONTROL Uso]** | Cantidad de la métrica principal utilizada. Este valor proporciona el uso total de esa métrica en todas las zonas protegidas, ya sea de producción o desarrollo. |
| **[!UICONTROL % de uso]** | El porcentaje de la métrica principal utilizado según la cantidad de licencia. |

>[!NOTE]
>
>Adiciones a la [!UICONTROL Importe de licencia] como resultado de los complementos, se añaden encima de las [!UICONTROL Importe de licencia] para los productos base, como Real-time Customer Data Platform, Adobe Journey Optimizer y Customer Journey Analytics. El uso de esa cantidad con licencia (después de los complementos) se rastrea a través de los productos base. Por ejemplo, si compra un paquete de cinco zonas protegidas, la cantidad de cinco se agrega a la del producto base. En este caso, el complemento muestra un [!UICONTROL Importe de licencia] de uno, y el uso para ese complemento es &quot;en blanco&quot;, ya que el uso se rastrea a través del producto base.

La tabla indica la métrica principal de cada producto, ya que cada producto puede realizar el seguimiento de numerosas métricas.

## [!UICONTROL Resumen] pestaña {#summary-tab}

Para ver más métricas e información detallada sobre el uso de la licencia del producto, seleccione un nombre de producto de la lista. El [!UICONTROL Resumen] aparece la vista de ese producto. Todas las métricas disponibles se muestran en la [!UICONTROL Resumen] pestaña. Las métricas disponibles dependen del producto con licencia. Esta vista proporciona lo siguiente **una vista consolidada de todas las métricas en todos los entornos limitados de producción o desarrollo**. El mismo nivel de análisis se proporciona para los entornos limitados de producción y desarrollo.

![La vista de resumen de un producto de Platform que muestra todas las métricas disponibles para ese producto.](../images/license-usage/summary-tab.png)

En la pestaña Resumen, la tabla incluye lo siguiente [!UICONTROL Métrica] columna. Estas descripciones legibles en lenguaje natural indican todas las métricas utilizadas para ese tipo de zona protegida.

### Seleccionar una zona protegida {#select-sandbox}

Para cambiar la vista entre los tipos de zona protegida de producción y desarrollo, seleccione [!UICONTROL Zonas protegidas de producción] o [!UICONTROL Zonas protegidas de desarrollo]. El tipo de zona protegida seleccionado se indica con el botón de opción situado junto al nombre de la zona protegida.

Los informes de consumo para las zonas protegidas son acumulativos para todas las zonas protegidas del mismo tipo. En otras palabras, seleccionar [!UICONTROL Producción] o [!UICONTROL Desarrollo] proporciona informes de consumo para todas las zonas protegidas de producción o desarrollo, respectivamente.

![La vista de resumen de un producto de Platform con las zonas protegidas de producción y desarrollo resaltadas.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>El permiso para ver el tablero de uso de licencias debe especificarse en el nivel de zona protegida. Añada permisos a cada zona protegida individual para verlos dentro del panel. Esta limitación se solucionará en una versión futura. Mientras tanto, está disponible la siguiente solución:
>
>1. Cree un perfil de producto en Adobe Admin Console.
>2. En Permiso en la categoría Zona protegida, agregue todas las zonas protegidas que desee ver en el panel de uso de licencias.
>3. En la categoría Permiso del tablero de usuarios, agregue el permiso &quot;Ver tablero de uso de licencias&quot;.

## El [!UICONTROL Detalles] pestaña {#details-tab}

Para ver **una métrica de uso determinada de una zona protegida específica**, vaya al [!UICONTROL Detalles] pestaña. El [!UICONTROL Detalles] Esta pestaña muestra todas las zonas protegidas disponibles en las zonas protegidas de producción o desarrollo.

![La pestaña Detalles del panel Uso de licencias.](../images/license-usage/details-tab.png)

En esta vista, puede seleccionar ![El icono Inspeccionar.](../images/license-usage/inspect-icon.png) junto al nombre de una zona protegida para ver la visualización de esa métrica. Se abrirá un cuadro de diálogo con una visualización para esa métrica.

### Visualizaciones {#visualizations}

Cada widget de visualización incluye los siguientes aspectos:

- Gráfico de líneas que registra el cambio de la métrica a lo largo del tiempo
- Una clave para el gráfico de líneas
- Nombre de la zona protegida
- Menú desplegable para ajustar el período de tiempo del gráfico de líneas

Los gráficos de líneas comparan los números de uso de su organización con el total disponible con las licencias de su organización y proporcionan un porcentaje del uso total.

![La visualización de una métrica.](../images/license-usage/visualization.png)

El periodo retrospectivo de análisis se puede ajustar desde el menú desplegable. El valor predeterminado de los últimos 30 días

Para seleccionar un intervalo de fecha, puede utilizar la lista desplegable de intervalo de fecha para seleccionar el período de tiempo que se mostrará en el panel. Hay varias opciones disponibles, incluido el valor predeterminado de los últimos 30 días.

![Se resaltará el cuadro de diálogo de visualización con la lista desplegable de intervalo de fechas.](../images/license-usage/date-range.png)

También puede seleccionar **[!UICONTROL Fecha personalizada]** para elegir el período de tiempo que se muestra.

![La pestaña Información general del tablero de uso de licencias con las opciones de intervalo de fechas personalizadas resaltadas.](../images/license-usage/custom-date-range.png)

## Métricas disponibles {#available-metrics}

El panel de uso de licencias informa sobre varias métricas únicas que se aplican a varios productos de la organización. Las métricas disponibles son:

| Métrica | Descripción |
|---|---|
| [!UICONTROL Tamaño del Audience Activation] | El tamaño total de los perfiles activados en cualquier destino basado en archivos en un año. Nota: Esto no incluye perfiles enviados a través de destinos de flujo continuo. |
| [!UICONTROL Audiencia a la que dirigirse] | La suma de los derechos de audiencia empresarial y de audiencia de consumidor. Una audiencia de consumidor se define como el número de perfiles de persona identificados como una &quot;Audiencia de consumidor&quot; en el pedido de ventas. Una audiencia empresarial se define como el número de perfiles de personas de negocios identificados como la &quot;Audiencia empresarial&quot; en el pedido de ventas. |
| [!UICONTROL Paquetes de usuarios de servicio de consultas ad hoc] | Un complemento para aumentar el derecho de los usuarios autorizados del servicio de consulta simultánea en cinco usuarios adicionales del servicio de consulta simultánea y una consulta ad hoc adicional que se ejecuta simultáneamente por paquete. Se pueden adquirir licencias para varios paquetes de usuarios de Ad Hoc Query adicionales. |
| [!UICONTROL Promedio de riqueza de perfiles] | La suma de todos los datos de producción almacenados en el servicio de perfil de concentrador en cualquier momento, dividida por cinco veces el número de perfiles autorizados de personas de negocios. [!UICONTROL Promedio de riqueza de perfiles] es una función compartida. |
| [!UICONTROL Filas de CJA disponibles] | Las filas medias diarias de datos disponibles para su análisis dentro de Customer Journey Analytics. |
| [!UICONTROL Atributos calculados] | Recuento total de datos de comportamiento del perfil agregados. Los datos de comportamiento del perfil agregados se basan en eventos de experiencia que se convierten en un atributo de perfil y que pueden incluirse en un perfil de persona o un perfil de persona de negocios. |
| [!UICONTROL Audiencia de consumidores] | El número de perfiles de persona identificados como &quot;Audiencia del consumidor&quot; en el pedido de ventas. |
| [!UICONTROL Tamaño de exportación de datos] | Cantidad de datos enviados a través de activaciones de conjuntos de datos en un año. |
| [!UICONTROL Exportaciones de datos] | El tamaño total de los conjuntos de datos que se pueden exportar a cualquier solución que no sea de Adobe (directa o indirectamente) en un año. |
| [!UICONTROL Almacenamiento de Data Lake] | Cantidad utilizada del almacén de datos analíticos en Adobe Experience Platform. |
| [!UICONTROL Audiencia atractiva] | Esta métrica hace referencia a la audiencia de perfiles atractivos. Un perfil atractivo es un registro de información que representa a un individuo y se representa en el servicio de perfil. Estos registros son perfiles con los que ha intentado interactuar mediante las capacidades de creación, toma de decisiones, envío, experimentación u orquestación de Journey Optimizer durante los últimos 12 meses. |
| [!UICONTROL Audiencias de similitud] | Recuento de audiencias que se generan al modelar una audiencia de consumidor existente para identificar perfiles de persona similares a la audiencia de consumidor existente. |
| [!UICONTROL Número de modelos de AMM] | Recuento del modelo de aprendizaje automático (Adobe Mix Modeler integrado) que se utiliza para medir o predecir un resultado especificado en función de sus inversiones. |
| [!UICONTROL Número de zonas protegidas] | Recuento de separaciones lógicas dentro de la instancia de cualquier servicio bajo demanda de Adobe que acceda a los datos y operaciones de aislamiento de Adobe Experience Platform. |
| [!UICONTROL Riqueza de perfiles: número de paquetes] | Un aumento en su riqueza de perfiles promedio autorizada de 25 KB por perfil para cada paquete de riqueza de perfiles adicional. |
| [!UICONTROL Horario de cómputo del servicio de consultas] | Una medida de la cantidad de tiempo que los motores de servicios de consulta tardan en leer, procesar y escribir datos en el lago de datos cuando se ejecuta una consulta por lotes. |
| [!UICONTROL Nº de paquetes de segmentación de streaming] | Los paquetes actualizan el abono de segmentos de un perfil de persona a medida que los nuevos datos entran en el servicio de segmentación a través de un flujo de streaming. La pertenencia a segmentos se evalúa en función de los atributos de perfil de la persona actual y el valor del evento actual, sin tener en cuenta el comportamiento histórico. La segmentación por secuencias es una función compartida. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

La disponibilidad de estas métricas y la definición específica de cada una de ellas varían según la licencia que haya adquirido su organización. Para obtener definiciones detalladas de cada métrica, consulte la documentación de descripción del producto correspondiente:

| Licencia | Descripción del producto |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:ESTÁNDAR OD</li><li>ADOBE EXPERIENCE PLATFORM:PESADO OD</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, servicios de aplicaciones y servicios inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 10M</li><li>RT PLATAFORMA DE DATOS DEL CLIENTE:OD PRFL A 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=es) |
| <ul><li>AEP:ACTIVACIÓN DE OD</li><li>AEP:OD ACTIVATION PRFL A 10M</li><li>AEP: PERFIL DE ACTIVACIÓN DE OD DE HASTA 50 M</li></ul> | [Adobe Experience Platform Activation](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELIGENCIA OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>DESACTIVAR AJO PRIME STARTER:OD</li><li>DESACTIVAR AJO ULTIMATE STARTER:OD</li><li>DESACTIVAR Real-Time CDP:ORQUESTACIÓN DE PERFILES OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/es/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>El tablero de uso de licencias solo informa de la licencia más reciente aprovisionada para su organización. Si la licencia más reciente aprovisionada para su organización no aparece en la tabla anterior, es posible que el panel de uso de licencias no se muestre correctamente. La compatibilidad con licencias adicionales y múltiples licencias en una sola organización está planificada para una versión futura.

## Pasos siguientes

Después de leer este documento, puede localizar el panel de uso de licencias y ver las métricas de uso de cada producto comprado, de todas las zonas protegidas de producción o desarrollo y de una zona protegida específica. Puede encontrar más información sobre las métricas disponibles para su organización, en función de las licencias que haya adquirido su organización.

Para obtener más información sobre otras funciones disponibles en la interfaz de usuario de Experience Platform, consulte [Guía de IU de Platform](../../landing/ui-guide.md).
