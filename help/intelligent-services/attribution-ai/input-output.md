---
keywords: Experience Platform;introducción;Attribution ai;temas populares;Attribution ai input;Attribution ai output;
solution: Experience Platform, Intelligent Services
title: Entrada y salida en Attribution AI
topic: Datos de entrada y salida para Attribution AI
description: En el siguiente documento se describen las diferentes entradas y productos utilizados en la Attribution AI.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
translation-type: tm+mt
source-git-commit: 35b3994287d4f556fab8ee75c3bf242ff2690aef
workflow-type: tm+mt
source-wordcount: '2182'
ht-degree: 3%

---

# Entrada y salida en [!DNL Attribution AI]

En el siguiente documento se describen las diferentes entradas y salidas utilizadas en [!DNL Attribution AI].

## [!DNL Attribution AI] datos de entrada

Attribution AI funciona analizando uno de los siguientes conjuntos de datos para calcular puntuaciones algorítmicas:

- Conjunto de datos de Evento de experiencia del consumidor (CEE)
- Conjuntos de datos de Adobe Analytics que utilizan el [Conector de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)

>[!IMPORTANT]
>
>El conector de origen de Adobe Analytics puede tardar hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente un conector, debe comprobar que el conjunto de datos tiene la longitud mínima de datos necesaria para la Attribution AI. Revise la sección [datos históricos](#data-requirements) para verificar que tiene datos suficientes para calcular puntuaciones algorítmicas precisas.

Para obtener más información sobre la configuración del esquema [!DNL Consumer Experience Event] (CEE), consulte la guía [Intelligent Services data preparation](../data-preparation.md) . Para obtener más información sobre la asignación de datos de Adobe Analytics, consulte la documentación [Analytics field mappings](../../sources/connectors/adobe-applications/analytics.md) .

No todas las columnas del esquema [!DNL Consumer Experience Event] (CEE) son obligatorias para la Attribution AI.

>[!NOTE]
>
> Las 9 columnas siguientes son obligatorias, las columnas adicionales son opcionales, pero se recomiendan/necesitan si desea utilizar los mismos datos para otras soluciones de Adobe como [!DNL Customer AI] y [!DNL Journey AI].

| Columnas obligatorias | Necesario para |
| --- | --- |
| Campo de identidad principal | Punto de contacto/Conversión |
| Marca de tiempo | Punto de contacto/Conversión |
| Canal._type | Touchpoint |
| Channel.mediaAction | Touchpoint |
| Channel.mediaType | Touchpoint |
| Marketing.trackingCode | Touchpoint |
| Marketing.campaignname | Touchpoint |
| Marketing.campaigngroup | Touchpoint |
| Comercio | Conversión |

Normalmente, la atribución se ejecuta en columnas de conversión como pedidos, compras y cierres de compra en &quot;comercio&quot;. Las columnas &quot;canal&quot; y &quot;marketing&quot; son muy recomendables para definir puntos de contacto para obtener buenas perspectivas. Sin embargo, puede incluir cualquier otra columna adicional junto con las columnas anteriores para configurarla como una definición de conversión o punto de contacto.

Las columnas siguientes no son obligatorias, pero se recomienda incluirlas en el esquema CEE si tiene la información disponible.

**Columnas recomendadas adicionales:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Datos históricos {#data-requirements}

>[!IMPORTANT]
>
> La cantidad mínima de datos necesaria para que la Attribution AI funcione es la siguiente:
> - Debe proporcionar al menos 3 meses (90 días) de datos para ejecutar un buen modelo.
> - Necesita al menos 1000 conversiones.


La Attribution AI requiere datos históricos como entrada para la formación de modelos. La duración de los datos requerida viene determinada principalmente por dos factores clave: ventana de formación y ventana retroactiva. Las entradas con ventanas de capacitación más cortas son más sensibles a las tendencias recientes, mientras que las ventanas de capacitación más largas ayudan a producir modelos más estables y precisos. Es importante modelar el objetivo con datos históricos que representen mejor sus objetivos comerciales.

La [configuración de la ventana de capacitación](./user-guide.md#training-window) filtra los eventos de conversión que se deben incluir para la formación del modelo en función del tiempo de incidencia. Actualmente, el período mínimo de capacitación es de 1 trimestre (90 días). La [ventana retrospectiva](./user-guide.md#lookback-window) proporciona un intervalo de tiempo que indica cuántos días antes de que se incluyan los puntos de contacto del evento de conversión relacionados con este evento de conversión. Estos dos conceptos juntos determinan la cantidad de datos de entrada (medidos por días) necesarios para una aplicación.

De forma predeterminada, Attribution AI define la ventana de formación como los últimos 2 trimestres (6 meses) y la ventana retrospectiva como 56 días. En otras palabras, el modelo tendrá en cuenta todos los eventos de conversión definidos que se hayan producido en los últimos 2 trimestres y buscará todos los puntos de contacto que se hayan producido en los 56 días anteriores a los eventos de conversión asociados.

**Fórmula**:

Longitud mínima de los datos requerida = ventana de formación + ventana retrospectiva

>[!TIP]
>
> La longitud mínima de datos necesaria para una aplicación con configuraciones predeterminadas es: 2 trimestres (180 días) + 56 días = 236 días.

Ejemplo :

- Desea atribuir eventos de conversión que se hayan producido en los últimos 90 días (3 meses) y rastrear todos los puntos de contacto que se hayan producido en las 4 semanas anteriores al evento de conversión. La duración de los datos de entrada debe abarcar los últimos 90 días + 28 días (4 semanas). La ventana de capacitación es de 90 días y la ventana retrospectiva es de 28 días, con un total de 118 días.

## datos de salida de Attribution AI

La Attribution AI genera lo siguiente:

- [Puntuaciones granulares sin procesar](#raw-granular-scores)
- [Puntuaciones agregadas](#aggregated-attribution-scores)

**Ejemplo de esquema de salida:**

![](./images/input-output/schema_output.gif)

### Puntuaciones granulares en bruto {#raw-granular-scores}

La Attribution AI genera puntuaciones de atribución en el nivel más granular posible para que pueda cortar y fragmentar las puntuaciones en cualquier columna de puntuación. Para ver estas puntuaciones en la interfaz de usuario, lea la sección [visualización de las rutas de puntuación sin procesar](#raw-score-path). Para descargar las puntuaciones con la API, visite el documento [descargar puntuaciones en Attribution AI](./download-scores.md).

>[!NOTE]
>
> Puede ver cualquier columna de informe deseada del conjunto de datos de entrada en el conjunto de datos de salida de puntuación solo si se cumple una de las siguientes condiciones:
> - La columna de informes se incluye en la página de configuración como parte de la configuración de punto de contacto o de definición de conversión.
> - La columna de informes se incluye en columnas de conjuntos de datos de puntuación adicionales.


La siguiente tabla describe los campos de esquema de la salida de ejemplo de las puntuaciones sin procesar:

| Nombre de columna (DataType) | Rellenable | Descripción |
| --- | --- | --- |
| timestamp (DateTime) | False | Hora a la que se produjo un evento de conversión o una observación. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | True | identityMap del usuario similar al formato CEE XDM. |
| eventType (String) | True | El tipo de evento principal para este registro de serie temporal. <br> **Ejemplo:** &quot;Pedido&quot;, &quot;Compra&quot;, &quot;Visita&quot; |
| eventMergeId (cadena) | True | Un ID para correlacionar o combinar varias [!DNL Experience Events] juntas que son esencialmente el mismo evento o deben combinarse. El productor de datos debe rellenarlo antes de su incorporación. <br> **Ejemplo:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (cadena) | False | Identificador único del evento de serie temporal. <br> **Ejemplo:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (objeto) | False | El contenedor de objeto de nivel superior correspondiente a su ID de tentante. <br> **Ejemplo:** _atsdsnmmsv2 |
| your_schema_name (objeto) | False | Puntee la fila con el evento de conversión en todos los eventos de punto de contacto asociados con él y sus metadatos. <br> **Ejemplo:** Puntuaciones de Attribution AI - Nombre de modelo__2020 |
| segmentación (cadena) | True | Segmento de conversión, como la segmentación geográfica con la que se basa el modelo. En caso de ausencia de segmentos, el segmento es el mismo que conversionName. <br> **Ejemplo:** ORDER_US |
| conversionName (String) | True | Nombre de la conversión que se configuró durante la configuración. <br> **Ejemplo:** pedido, posible cliente, visita |
| conversión (objeto) | False | Columnas de metadatos de conversión. |
| dataSource (String) | True | Identificación única global de una fuente de datos. <br> **Ejemplo:** Adobe Analytics |
| eventSource (String) | True | La fuente cuando se produjo el evento real. <br> **Ejemplo:** Adobe.com |
| eventType (String) | True | El tipo de evento principal para este registro de serie temporal. <br> **Ejemplo:** Pedido |
| geo (cadena) | True | Ubicación geográfica donde se entregó la conversión `placeContext.geo.countryCode`. <br> **Ejemplo:** EE. UU. |
| priceTotal (Double) | True | Ingresos obtenidos a través de la conversión <br> **Ejemplo:** 99.9 |
| product (String) | True | Identificador XDM del propio producto. <br> **Ejemplo:** RX 1080 ti |
| productType (String) | True | Nombre para mostrar del producto tal como se presenta al usuario para esta vista de producto. <br> **Ejemplo:** Gpus |
| cantidad (total) | True | Cantidad comprada durante la conversión. <br> **Ejemplo:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Se ha recibido la marca de tiempo de la conversión. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| skuId (cadena) | True | Unidad de mantenimiento de existencias (SKU), el identificador único de un producto definido por el proveedor. <br> **Ejemplo:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Marca de tiempo de la conversión. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| passThrough (objeto) | True | Columnas de conjuntos de datos de puntuación adicionales especificadas por el usuario al configurar el modelo. |
| commerce_order_purchaseCity (cadena) | True | Columna del conjunto de datos de puntuación adicional. <br> **Ejemplo:** ciudad : San José |
| customerProfile (objeto) | False | Detalles de identidad del usuario utilizado para crear el modelo. |
| identity (objeto) | False | Contiene los detalles del usuario utilizado para crear el modelo, como `id` y `namespace`. |
| id (cadena) | True | ID de identidad del usuario, como ID de cookie o AAID o MCID, etc. <br> **Ejemplo:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Área de nombres de identidad utilizada para crear las rutas y, por lo tanto, el modelo. <br> **Ejemplo:** aaid |
| touchpointsDetail (matriz de objetos) | True | La lista de detalles de puntos de contacto que llevan a la conversión ordenada por incidencia de punto de contacto o marca de tiempo. |
| touchpointName (cadena) | True | Nombre del punto de contacto que se configuró durante la configuración. <br> **Ejemplo:** PAID_SEARCH_CLICK |
| partituras (objeto) | True | Contribución de Touchpoint a esta conversión como puntuación. Para obtener más información sobre las puntuaciones producidas dentro de este objeto, consulte la sección [puntuaciones de atribución agregadas](#aggregated-attribution-scores). |
| touchPoint (objeto) | True | Metadatos de Touchpoint. Para obtener más información sobre las puntuaciones producidas dentro de este objeto, consulte la sección [puntuaciones agregadas](#aggregated-scores). |

### Visualización de rutas de puntuación sin procesar (IU) {#raw-score-path}

Puede ver la ruta a sus puntuaciones sin procesar en la interfaz de usuario de . Para empezar, seleccione **[!UICONTROL Schemas]** en la interfaz de usuario de Platform y, a continuación, busque y seleccione el esquema de puntuaciones de AI de atribución en la pestaña **[!UICONTROL Browse]** .

![Elija el esquema](./images/input-output/schemas_browse.png)

A continuación, seleccione un campo en la ventana **[!UICONTROL Structure]** de la interfaz de usuario y se abrirá la pestaña **[!UICONTROL Field properties]**. En **[!UICONTROL Field properties]** es el campo de ruta que se asigna a sus puntuaciones sin procesar.

![Elegir un esquema](./images/input-output/field_properties.png)


### Puntuaciones de atribución agregadas {#aggregated-attribution-scores}

Las puntuaciones agregadas se pueden descargar en formato CSV desde la interfaz de usuario de Platform si el intervalo de fechas es inferior a 30 días.

Attribution AI admite dos categorías de puntuaciones de atribución, las puntuaciones algorítmicas y las basadas en reglas.

Attribution AI produce dos tipos diferentes de puntuaciones algorítmicas, incrementales e influenciadas. Una puntuación con influencia es la fracción de conversión de la que es responsable cada punto de contacto de marketing. Una puntuación incremental es la cantidad de impacto marginal causado directamente por el punto de contacto de marketing. La principal diferencia entre la puntuación incremental y la puntuación influida es que la puntuación incremental tiene en cuenta el efecto basal. No supone que una conversión se deba exclusivamente a los puntos de contacto de marketing anteriores.

A continuación, se muestra un ejemplo de salida de esquema de Attribution AI de la interfaz de usuario de Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Consulte la siguiente tabla para obtener más información sobre cada una de estas puntuaciones de atribución:

| Puntuaciones de atribución | Descripción |
| ----- | ----------- |
| Influenciado (algorítmico) | La puntuación influida es la fracción de conversión de la que es responsable cada punto de contacto de marketing. |
| Incremental (algorítmico) | La puntuación incremental es la cantidad de impacto marginal causado directamente por un punto de contacto de marketing. |
| Primer contacto | Puntuación de atribución basada en reglas que asigna todos los créditos al punto de contacto inicial en una ruta de conversión. |
| Último contacto | Puntuación de atribución basada en reglas que asigna todo el crédito al punto de contacto más cercano a la conversión. |
| Lineal | Puntuación de atribución basada en reglas que asigna el mismo crédito a cada punto de contacto de una ruta de conversión. |
| Forma de U | La puntuación de atribución basada en reglas que asigna el 40 % del crédito al primer punto de contacto y el 40 % del crédito al último punto de contacto, mientras que los demás puntos de contacto dividen el 20 % restante de forma equitativa. |
| Deterioro de tiempo | La puntuación de atribución basada en reglas donde los puntos de contacto más cercanos a la conversión reciben más crédito que los puntos de contacto que están más lejos en el tiempo de la conversión. |

**Referencia de puntuación sin procesar (puntuaciones de atribución)**

La siguiente tabla asigna las puntuaciones de atribución a las puntuaciones sin procesar. Si desea descargar las puntuaciones sin procesar, visite la [descarga de puntuaciones en la documentación de Attribution AI](./download-scores.md).

| Puntuaciones de atribución | Columna de referencia de puntuación sin procesar |
| --- | --- |
| Influenciado (algorítmico) | _tenantID.your_schema_name.element.touchpoint.algorithmInfluenciado |
| Incremental (algorítmico) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmInfluenciado |
| Primer contacto | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Último contacto | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Lineal | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| Forma de U | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Deterioro de tiempo | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Puntuaciones agregadas {#aggregated-scores}

Las puntuaciones agregadas se pueden descargar en formato CSV desde la interfaz de usuario de Platform si el intervalo de fechas es inferior a 30 días. Consulte la siguiente tabla para obtener más información sobre cada una de estas columnas de agregado.

| Nombre de columna | Restricción | Rellenable | Descripción |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Formato definido por el usuario y fijo | False | Fecha de Evento del Cliente en formato AAAA-MM-DD. <br> **Ejemplo**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Formato definido por el usuario y fijo | True | Fecha de punto de contacto multimedia en formato AAAA-MM-DD <br> **Ejemplo**: 21-04-2017 |
| segment (String) | Calculado | False | Segmento de conversión como la segmentación geográfica con la que se ha creado el modelo. En caso de ausencia de segmentos, el segmento es el mismo que conversion_scope. <br> **Ejemplo**: ORDER_AMER |
| conversion_scope (cadena) | Definido por el usuario | False | Nombre de la conversión según la configuración del usuario. <br> **Ejemplo**: ORDEN |
| touchpoint_scope (cadena) | Definido por el usuario | True | Nombre del punto de contacto configurado por el usuario <br> **Ejemplo**: PAID_SEARCH_CLICK |
| product (String) | Definido por el usuario | True | Identificador XDM del producto. <br> **Ejemplo**: CC |
| product_type (String) | Definido por el usuario | True | Nombre para mostrar del producto tal como se presenta al usuario para esta vista de producto. <br> **Ejemplo**: gpus, portátiles |
| geo (cadena) | Definido por el usuario | True | Ubicación geográfica donde se entregó la conversión (placeContext.geo.countryCode) <br> **Ejemplo**: US |
| event_type (String) | Definido por el usuario | True | El tipo de evento principal para este registro de serie temporal <br> **Ejemplo**: Conversión de pago |
| media_type (String) | ENUM | False | Describe si el tipo de medio es de pago, propio o ganado. <br> **Ejemplo**: PAGO, PROPIEDAD |
| channel (String) | ENUM | False | La propiedad `channel._type` que se utiliza para proporcionar una clasificación aproximada de canales con propiedades similares en [!DNL Consumer Experience Event] XDM. <br> **Ejemplo**: BUSCAR |
| action (String) | ENUM | False | La propiedad `mediaAction` se utiliza para proporcionar un tipo de acción de medio de evento de experiencia. <br> **Ejemplo**: HAGA CLIC EN |
| campaign_group (String) | Definido por el usuario | True | Nombre del grupo de campañas en el que se agrupan varias campañas como &quot;50%_DISCOUNT&quot;. <br> **Ejemplo**: COMERCIAL |
| campaign_name (String) | Definido por el usuario | True | Nombre de la campaña utilizada para identificar la campaña de marketing como &quot;50%_DISCOUNT_USA&quot; o &quot;50%_DISCOUNT_ASIA&quot;. <br> **Ejemplo**: Venta de Acción de Gracias |

**Referencia de puntuación sin procesar (agregado)**

La tabla siguiente asigna las puntuaciones agregadas a las puntuaciones sin procesar. Si desea descargar las puntuaciones sin procesar, visite la [descarga de puntuaciones en la documentación de Attribution AI](./download-scores.md). Para ver las rutas de puntuación sin procesar desde la interfaz de usuario, visite la sección [visualización de las rutas de puntuación sin procesar](#raw-score-path) de este documento.

| Nombre de columna | Columna de referencia de la puntuación sin procesar |
| --- | --- |
| customerevents_date | timestamp |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmento | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| producto | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| canal | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| acción | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos y haya establecido todas sus credenciales y esquemas, comience por seguir la [guía del usuario de Attribution AI](./user-guide.md). Esta guía lo acompaña durante la creación de una instancia para Attribution AI.
