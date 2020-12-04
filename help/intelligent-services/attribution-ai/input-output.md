---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform
title: Entrada y salida de Attribution AI
topic: Input and Output data for Attribution AI
description: En el documento siguiente se esbozan los diferentes insumos y productos utilizados en la Attribution AI.
translation-type: tm+mt
source-git-commit: 34cfcaac276bf2645a0365a0dfa71c4ead6e2ecb
workflow-type: tm+mt
source-wordcount: '2075'
ht-degree: 4%

---


# [!DNL Attribution AI] entrada y salida

El documento siguiente describe los diferentes insumos y productos utilizados en [!DNL Attribution AI].

## [!DNL Attribution AI] datos de entrada

[!DNL Attribution AI] utiliza [!DNL Consumer Experience Event] datos para calcular puntuaciones algorítmicas. Para obtener más información sobre [!DNL Consumer Experience Event], consulte la documentación [](../data-preparation.md)Preparar datos para su uso en Servicios inteligentes.

No todas las columnas del esquema [!DNL Consumer Experience Event] (CEE) son obligatorias para la Attribution AI.

>[!NOTE]
>
> Las 9 columnas siguientes son obligatorias, las columnas adicionales son opcionales pero se recomiendan/necesitan si desea utilizar los mismos datos para otras soluciones de Adobe como [!DNL Customer AI] y [!DNL Journey AI].

| Columnas obligatorias | Necesario para |
| --- | --- |
| Campo de identidad principal | Touchpoint / Conversión |
| Marca de tiempo | Touchpoint / Conversión |
| Canal._type | Touchpoint |
| Channel.mediaAction | Touchpoint |
| Channel.mediaType | Touchpoint |
| Marketing.trackingCode | Touchpoint |
| Marketing.campaignname | Touchpoint |
| Marketing.campaigngroup | Touchpoint |
| Comercio | Conversión |

Generalmente, la atribución se ejecuta en columnas de conversión como pedido, compras y cierres de compra en &quot;comercio&quot;. Las columnas &quot;canal&quot; y &quot;marketing&quot; son muy recomendadas para definir puntos de contacto para obtener buenas perspectivas. Sin embargo, puede incluir cualquier otra columna adicional junto con las columnas anteriores para configurarla como una definición de conversión o punto de contacto.

Las columnas siguientes no son obligatorias, pero se recomienda incluirlas en el esquema CEE si dispone de la información disponible.

**Columnas adicionales recomendadas:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Datos históricos

>[!IMPORTANT]
>
> La cantidad mínima de datos necesaria para que la Attribution AI funcione es la siguiente:
> - Debe proporcionar al menos 3 meses (90 días) de datos para ejecutar un buen modelo.
> - Necesita al menos 1000 conversiones.


Attribution AI requiere datos históricos como entrada para la formación de modelos. La duración de los datos requerida está determinada principalmente por dos factores clave: ventana de formación y ventana retroactiva. Las entradas con ventanas de capacitación más cortas son más sensibles a las tendencias recientes, mientras que las ventanas de capacitación más largas ayudan a producir modelos más estables y precisos. Es importante modelar el objetivo con datos históricos que representen mejor los objetivos comerciales.

Los eventos de conversión de filtros de configuración [de la ventana de](./user-guide.md#training-window) formación se configuran para la formación de modelos según el tiempo de incidencia. Actualmente, la ventana de capacitación mínima es de 1 trimestre (90 días). La ventana [](./user-guide.md#lookback-window) retrospectiva proporciona un intervalo de tiempo que indica cuántos días antes de que se incluyan los puntos de contacto del evento de conversión relacionados con este evento de conversión. Estos dos conceptos juntos determinan la cantidad de datos de entrada (medidos por días) que se requiere para una aplicación.

De forma predeterminada, Attribution AI define la ventana de formación como los últimos 2 trimestres (6 meses) y la ventana retroactiva como 56 días. Dicho de otro modo, el modelo tendrá en cuenta todos los eventos de conversión definidos que se hayan producido en los dos últimos trimestres y buscará todos los puntos de contacto que se hayan producido en los 56 días anteriores a los eventos de conversión asociados.

**Fórmula**:

Longitud mínima de los datos requerida = ventana de capacitación + ventana retrospectiva

>[!TIP]
>
> La longitud mínima de datos requerida para una aplicación con configuraciones predeterminadas es: 2 trimestres (180 días) + 56 días = 236 días.

Ejemplo :

- Desea atribuir los eventos de conversión que se han producido en los últimos 90 días (3 meses) y rastrear todos los puntos de contacto que se han producido en las 4 semanas anteriores al evento de conversión. La duración de los datos de entrada debe abarcar los últimos 90 días + 28 días (4 semanas). La ventana de formación es de 90 días y la ventana retrospectiva es de 28 días, con un total de 118 días.

## Datos de salida de Attribution AI

La Attribution AI genera lo siguiente:

- [Puntuaciones granulares sin procesar](#raw-granular-scores)
- [Puntuaciones agregadas](#aggregated-attribution-scores)

**Ejemplo de esquema de salida:**

![](./images/input-output/schema_output.gif)

### Puntuaciones granulares sin procesar {#raw-granular-scores}

La Attribution AI genera puntuaciones de atribución en el nivel más granular posible para que pueda fraccionar y fraccionar las puntuaciones según cualquier columna de puntuación. Para vista de estas puntuaciones en la interfaz de usuario, lea la sección sobre la [visualización de las rutas](#raw-score-path)de puntuación sin procesar. Para descargar las puntuaciones con la API, visite las puntuaciones de [descarga en Attribution AI](./download-scores.md) documento.

>[!NOTE]
>
> Puede ver cualquier columna de sistema de informes deseada desde el conjunto de datos de entrada en el conjunto de datos de resultados de puntuación solo si se cumple alguna de las siguientes condiciones:
> - La columna sistema de informes se incluye en la página de configuración como parte de la configuración de punto de contacto o de definición de conversión.
> - La columna sistema de informes se incluye en columnas de conjuntos de datos de puntuación adicionales.


La siguiente tabla describe los campos de esquema en la salida del ejemplo de puntuaciones sin procesar:

| Nombre de columna (DataType) | Nullable | Descripción |
| --- | --- | --- |
| timestamp (DateTime) | False | Hora en la que se produjo un evento de conversión o una observación. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap del usuario similar al formato CEE XDM. |
| eventType (String) | True | El tipo de evento principal para este registro de serie temporal. <br> **Ejemplo:** &quot;Pedido&quot;, &quot;Compra&quot;, &quot;Visita&quot; |
| eventMergeId (String) | True | ID para correlacionar o combinar varios [!DNL Experience Events] que son esencialmente el mismo evento o que se deben combinar. El productor de datos debe rellenarlo antes de la ingestión. <br> **Ejemplo:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (Cadena) | False | Un identificador único para el evento de la serie temporal. <br> **Ejemplo:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (objeto) | False | El contenedor del objeto de nivel superior correspondiente al ID de tentant. <br> **Ejemplo:** _atsdsnrmmsv2 |
| your_esquema_name (objeto) | False | Fila de puntuación con evento de conversión todos los eventos de punto de contacto asociados a ella y sus metadatos. <br> **Ejemplo:** Puntuaciones de Attribution AI - Nombre del modelo__2020 |
| segmentación (Cadena) | True | Segmento de conversión, como la segmentación geográfica, con la que se construye el modelo. En caso de ausencia de segmentos, el segmento es igual que conversionName. <br> **Ejemplo:** ORDER_US |
| conversionName (String) | True | Nombre de la conversión configurada durante la configuración. <br> **Ejemplo:** Pedido, posible cliente, visita |
| conversion (Objeto) | False | Columnas de metadatos de conversión. |
| dataSource (String) | True | Identificación única global de una fuente de datos. <br> **Ejemplo:** Adobe Analytics |
| eventSource (String) | True | La fuente cuando se produjo el evento real. <br> **Ejemplo:** Adobe.com |
| eventType (String) | True | El tipo de evento principal para este registro de serie temporal. <br> **Ejemplo:** Pedido |
| geo (cadena) | True | Ubicación geográfica en la que se entregó la conversión `placeContext.geo.countryCode`. <br> **Ejemplo:** EE.UU. |
| priceTotal (Doble) | True | Ingresos obtenidos a través de la conversión <br> **Ejemplo:** 99,9 |
| product (String) | True | Identificador XDM del producto mismo. <br> **Ejemplo:** RX 1080 ti |
| productType (String) | True | Nombre para mostrar del producto tal como se presenta al usuario para esta vista de producto. <br> **Ejemplo:** Gpus |
| cantidad (entero) | True | Cantidad comprada durante la conversión. <br> **Ejemplo:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Se recibió la marca de tiempo de la conversión. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| skuId (Cadena) | True | Unidad de mantenimiento de existencias (SKU), el identificador único de un producto definido por el proveedor. <br> **Ejemplo:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Marca de hora de la conversión. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| passThrough (objeto) | True | Columnas adicionales del conjunto de datos de puntuación especificadas por el usuario durante la configuración del modelo. |
| commerce_order_purchaseCity (String) | True | Columna adicional del conjunto de datos de puntuación. <br> **Ejemplo:** city: San José |
| customerProfile (objeto) | False | Detalles de identidad del usuario utilizado para crear el modelo. |
| identity (objeto) | False | Contiene los detalles del usuario utilizado para crear el modelo, como `id` y `namespace`. |
| id (Cadena) | True | ID de identidad del usuario, como ID de cookie o AAID o MCID, etc. <br> **Ejemplo:** 1734876272540865634468320891369597404 |
| área de nombres (Cadena) | True | Área de nombres de identidad utilizada para crear las rutas y, por lo tanto, el modelo. <br> **Ejemplo:** aaid |
| touchpointsDetail (Matriz de objetos) | True | Lista de detalles de puntos de contacto que llevan a la conversión ordenada por incidencia de punto de contacto o marca de hora. |
| touchpointName (String) | True | Nombre del punto de contacto que se configuró durante la configuración. <br> **Ejemplo:** PAID_SEARCH_CLICK |
| score (objeto) | True | Contribución de touchpoint a esta conversión como puntuación. Para obtener más información sobre las puntuaciones producidas dentro de este objeto, consulte la sección Puntuaciones [de atribución](#aggregated-attribution-scores) agregadas. |
| touchPoint (objeto) | True | Metadatos de Touchpoint. Para obtener más información sobre las puntuaciones producidas dentro de este objeto, consulte la sección puntuaciones [](#aggregated-scores) agregadas. |

### Visualización de rutas de puntuación sin procesar (IU) {#raw-score-path}

Puede realizar la vista de la ruta a sus puntuaciones sin procesar en la interfaz de usuario. Para inicio, seleccione **[!UICONTROL Esquemas]** en la interfaz de usuario de la plataforma y, a continuación, busque y seleccione el esquema de puntuaciones AI de atribución desde la ficha **[!UICONTROL Examinar]** .

![Elija su esquema](./images/input-output/schemas_browse.png)

A continuación, seleccione un campo en la ventana **[!UICONTROL Estructura]** de la interfaz de usuario y se abre la ficha Propiedades **[!UICONTROL del]** campo. En las propiedades **** Campo es el campo de ruta que se asigna a las puntuaciones sin procesar.

![Elegir un Esquema](./images/input-output/field_properties.png)


### Puntuaciones de atribución agregadas {#aggregated-attribution-scores}

Las puntuaciones agregadas se pueden descargar en formato CSV desde la interfaz de usuario de la plataforma si el intervalo de fechas es inferior a 30 días.

Attribution AI admite dos categorías de puntuaciones de atribución, las puntuaciones algorítmicas y las basadas en reglas.

La Attribution AI produce dos tipos diferentes de puntuaciones algorítmicas, incrementales e influenciadas. Una puntuación influida es la fracción de conversión de la que es responsable cada punto de contacto de marketing. Una puntuación incremental es la cantidad de impacto marginal causado directamente por el punto de contacto de marketing. La principal diferencia entre la puntuación incremental y la puntuación influida es que la puntuación incremental tiene en cuenta el efecto basal. No supone que una conversión se deba únicamente a los puntos de contacto de marketing anteriores.

A continuación se muestra un ejemplo de salida de Attribution AI esquema de la interfaz de usuario de Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Consulte la tabla siguiente para obtener más detalles sobre cada una de estas puntuaciones de atribución:

| Puntuaciones de atribución | Descripción |
| ----- | ----------- |
| Influenciado (algorítmico) | La puntuación influida es la fracción de conversión de la que es responsable cada punto de contacto de marketing. |
| Incremental (algorítmico) | La puntuación incremental es la cantidad de impacto marginal causado directamente por un punto de contacto de marketing. |
| Primer contacto | Puntuación de atribución basada en reglas que asigna todos los créditos al punto de contacto inicial en una ruta de conversión. |
| Último contacto | Puntuación de atribución basada en reglas que asigna todo el crédito al punto de contacto más cercano a la conversión. |
| Lineal | Puntuación de atribución basada en reglas que asigna el mismo crédito a cada punto de contacto de una ruta de conversión. |
| Forma de U | Puntuación de atribución basada en reglas que asigna el 40 % del crédito al primer punto de contacto y el 40 % del crédito al último punto de contacto, mientras que los demás puntos de contacto dividen el 20 % restante de forma equitativa. |
| Deterioro de tiempo | Puntuación de atribución basada en reglas donde los puntos de contacto más cercanos a la conversión reciben más crédito que los puntos de contacto más alejados en el tiempo de la conversión. |

**Referencia de puntuación sin procesar (puntuaciones de atribución)**

La siguiente tabla asigna las puntuaciones de atribución a las puntuaciones sin procesar. Si desea descargar sus puntuaciones sin procesar, visite las puntuaciones de [descarga en la documentación de Attribution AI](./download-scores.md) .

| Puntuaciones de atribución | Columna de referencia de puntuación sin procesar |
| --- | --- |
| Influenciado (algorítmico) | _tenantID.your_esquema_name.element.touchpoint.algorithmInfluenciado |
| Incremental (algorítmico) | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.algorithmInfluced |
| Primer contacto | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Último contacto | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Lineal | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.linear |
| Forma de U | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.uShape |
| Deterioro de tiempo | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Puntuaciones agregadas {#aggregated-scores}

Las puntuaciones agregadas se pueden descargar en formato CSV desde la interfaz de usuario de la plataforma si el intervalo de fechas es inferior a 30 días. Consulte la tabla siguiente para obtener más detalles sobre cada una de estas columnas acumuladas.

| Nombre de columna | Restricción | Nullable | Descripción |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Formato definido por el usuario y fijo | False | Fecha de Evento del cliente en formato AAAA-MM-DD. <br> **Ejemplo**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Formato definido por el usuario y fijo | True | Fecha de punto de contacto multimedia en formato AAAA-MM-DD <br> **Ejemplo**: 2017-04-21 |
| segment (String) | Calculado | False | Segmento de conversión, como la segmentación geográfica, con la que se construye el modelo. En caso de ausencia de segmentos, el segmento es igual que conversion_scope. <br> **Ejemplo**: ORDER_AMER |
| conversion_scope (Cadena) | Definido por el usuario | False | Nombre de la conversión según la configuración del usuario. <br> **Ejemplo**: ORDEN |
| touchpoint_scope (Cadena) | Definido por el usuario | True | Nombre del touchpoint configurado por el usuario <br> **Ejemplo**: PAID_SEARCH_CLICK |
| product (String) | Definido por el usuario | True | Identificador XDM del producto. <br> **Ejemplo**: CC |
| product_type (String) | Definido por el usuario | True | Nombre para mostrar del producto tal como se presenta al usuario para esta vista de producto. <br> **Ejemplo**: gpus, portátiles |
| geo (cadena) | Definido por el usuario | True | Ubicación geográfica en la que se entregó la conversión (placeContext.geo.countryCode) <br> **Ejemplo**: EE.UU. |
| evento_type (String) | Definido por el usuario | True | El tipo de evento principal para este registro de serie temporal <br> **Ejemplo**: Conversión paga |
| media_type (String) | ENUM | False | Describe si el tipo de medio es de pago, propiedad o ganado. <br> **Ejemplo**: PAGADO, PROPIEDAD |
| canal (Cadena) | ENUM | False | La `channel._type` propiedad que se utiliza para proporcionar una clasificación aproximada de canales con propiedades similares en [!DNL Consumer Experience Event] XDM. <br> **Ejemplo**: BUSCAR |
| action (String) | ENUM | False | La `mediaAction` propiedad se utiliza para proporcionar un tipo de acción de medios de evento de experiencias. <br> **Ejemplo**: HAGA CLIC EN |
| campaña_group (String) | Definido por el usuario | True | Nombre del grupo de campañas donde varias campañas se agrupan como &#39;50%_DISCOUNT&#39;. <br> **Ejemplo**: COMERCIAL |
| campaña_name (String) | Definido por el usuario | True | Nombre de la campaña utilizada para identificar la campaña de marketing como &#39;50%_DISCOUNT_USA&#39; o &#39;50%_DISCOUNT_ASIA&#39;. <br> **Ejemplo**: Venta de Acción de Gracias |

**Referencia de puntuación sin procesar (agregado)**

La siguiente tabla asigna las puntuaciones agregadas a las puntuaciones sin procesar. Si desea descargar sus puntuaciones sin procesar, visite las puntuaciones de [descarga en la documentación de Attribution AI](./download-scores.md) . Para vista de las rutas de puntuación sin procesar desde la interfaz de usuario, visite la sección sobre [visualización de las rutas](#raw-score-path) de puntuación sin procesar dentro de este documento.

| Nombre de columna | Columna de referencia de puntuación sin procesar |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmento | _tenantID.your_esquema_name.segmentation |
| conversion_scope | _tenantID.your_esquema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_esquema_name.touchpointsDetail.element.touchpointName |
| product | _tenantID.your_esquema_name.conversion.product |
| product_type | _tenantID.your_esquema_name.conversion.product_type |
| geo | _tenantID.your_esquema_name.conversion.geo |
| evento_type | eventType |
| media_type | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.mediaType |
| canal | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| action | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaña_grupo | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaña_nombre | _tenantID.your_esquema_name.touchpointsDetail.element.touchpoint.campaignName |


## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos y haya colocado todas las credenciales y esquemas, siga las instrucciones de inicio de la guía [del usuario de](./user-guide.md)Attribution AI. Esta guía lo acompaña durante la creación de una instancia para Attribution AI.