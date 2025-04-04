---
keywords: Experience Platform;introducción;inteligencia artificial aplicada a la atribución;temas populares;entrada de inteligencia artificial aplicada a la atribución;salida de inteligencia artificial aplicada a la atribución;
feature: Attribution AI
title: Entrada y salida en Attribution AI
description: En el siguiente documento se describen los diferentes insumos y productos utilizados en la inteligencia artificial aplicada a la atribución.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2474'
ht-degree: 3%

---

# Entrada y salida en [!DNL Attribution AI]

El siguiente documento describe las diferentes entradas y salidas utilizadas en [!DNL Attribution AI].

## [!DNL Attribution AI] datos de entrada

Attribution AI funciona analizando los siguientes conjuntos de datos para calcular puntuaciones algorítmicas:

- Conjuntos de datos de Adobe Analytics que usan el [conector de origen de Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Conjuntos de datos de Evento de experiencia (EE) en general desde el esquema de Adobe Experience Platform
- Conjuntos de datos de Evento de experiencia del consumidor (CEE)

Ahora puede agregar varios conjuntos de datos de diferentes fuentes en función del **mapa de identidad** (campo) si cada uno de los conjuntos de datos comparte el mismo tipo de identidad (área de nombres), como un ECID. Después de seleccionar una identidad y un área de nombres, aparecen las métricas de integridad de la columna de ID que indican el volumen de datos que se están vinculando. Para obtener más información sobre cómo agregar varios conjuntos de datos, visite la [guía del usuario de inteligencia artificial aplicada a la atribución](./user-guide.md#identity).

La información del canal no siempre está asignada de forma predeterminada. En algunos casos, si mediaChannel (campo) está en blanco, no podrá &quot;continuar&quot; hasta que asigne un campo a mediaChannel, ya que es una columna obligatoria. Si el canal se detecta en el conjunto de datos, se asigna a mediaChannel de forma predeterminada. Las otras columnas, como **tipo de medios** y **acción de medios**, siguen siendo opcionales.

Después de asignar el campo de canal, continúe con el paso Definir eventos, donde puede seleccionar los eventos de conversión, los eventos de punto de contacto y elegir campos específicos de conjuntos de datos individuales.

>[!IMPORTANT]
>
>El conector de origen de Adobe Analytics puede tardar hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente un conector, debe comprobar que el conjunto de datos tiene la longitud mínima de datos necesaria para la inteligencia artificial aplicada a la atribución. Revise la sección [datos históricos](#data-requirements) para verificar que tiene datos suficientes para calcular puntuaciones algorítmicas precisas.

Para obtener más información sobre la configuración del esquema [!DNL Consumer Experience Event] (CEE), consulte la guía de [preparación de datos de servicios inteligentes](../data-preparation.md). Para obtener más información sobre la asignación de datos de Adobe Analytics, visite la [documentación de asignaciones de campos de Analytics](../../sources/connectors/adobe-applications/analytics.md).

No todas las columnas del esquema [!DNL Consumer Experience Event] (CEE) son obligatorias para Inteligencia artificial aplicada a la atribución.

Puede configurar los puntos de contacto mediante cualquier campo recomendado a continuación en el esquema o el conjunto de datos seleccionado.

| Columnas recomendadas | Necesario para |
| --- | --- |
| Campo de identidad principal | Touchpoint / Conversión |
| Marca de tiempo | Touchpoint / Conversión |
| Canal._type | Touchpoint |
| Channel.mediaAction | Touchpoint |
| Channel.mediaType | Touchpoint |
| Marketing.trackingCode | Touchpoint |
| Marketing.campaignname | Touchpoint |
| Marketing.campaigngroup | Touchpoint |
| Commerce | Conversión |

Normalmente, la atribución se ejecuta en columnas de conversión como pedidos, compras y cierres de compra en comercio. Las columnas &quot;canal&quot; y &quot;marketing&quot; se utilizan para definir puntos de contacto para la inteligencia artificial aplicada a la atribución (por ejemplo, `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Para obtener resultados y perspectivas óptimos, se recomienda incluir tantas columnas de conversión y punto de contacto como sea posible. Además, no está limitado solo a las columnas anteriores. Puede incluir cualquier otra columna recomendada o personalizada como conversión o definición de punto de contacto.

Los conjuntos de datos de evento de experiencia (EE) no necesitan tener explícitamente mezclas de canal y marketing, siempre que la información de canal o campaña relevante para configurar un punto de contacto esté presente en uno de los campos de mezcla o paso a través.

>[!TIP]
>
>Si utiliza datos de Adobe Analytics en su esquema de CEE, la información del punto de contacto para Analytics se almacena generalmente en `channel.typeAtSource` (por ejemplo, `channel.typeAtSource = 'email'`).

## Datos históricos {#data-requirements}

>[!IMPORTANT]
>
> La cantidad mínima de datos necesaria para que la inteligencia artificial aplicada a la atribución funcione es la siguiente:
> - Debe proporcionar datos durante al menos 3 meses (90 días) para ejecutar un buen modelo.
> - Necesita al menos 1000 conversiones.

Inteligencia artificial aplicada a la atribución requiere datos históricos como entrada para la formación de modelos. La duración de los datos requerida viene determinada principalmente por dos factores clave: ventana de formación y ventana retrospectiva. La entrada con ventanas de formación más cortas es más sensible a las tendencias recientes, mientras que las ventanas de formación más largas ayudan a producir modelos más estables y precisos. Es importante modelar el objetivo con datos históricos que mejor representen los objetivos de su negocio.

La [configuración de la ventana de aprendizaje](./user-guide.md#training-window) filtra los eventos de conversión establecidos para que se incluyan en la formación de modelos en función del tiempo de ocurrencia. Actualmente, la ventana de formación mínima es de 1 trimestre (90 días). La [ventana retrospectiva](./user-guide.md#lookback-window) proporciona un intervalo de tiempo que indica cuántos días antes del evento de conversión se deben incluir los puntos de contacto relacionados con este evento de conversión. Estos dos conceptos determinan juntos la cantidad de datos de entrada (medidos por días) necesarios para una aplicación.

De forma predeterminada, Inteligencia artificial aplicada a la atribución define la ventana de formación como los dos trimestres (6 meses) más recientes y la ventana retrospectiva como 56 días. En otras palabras, el modelo tendrá en cuenta todos los eventos de conversión definidos que se han producido en los últimos 2 trimestres y buscará todos los puntos de contacto que se han producido en los 56 días anteriores a los eventos de conversión asociados.

**fórmula**:

Longitud mínima de datos necesaria = ventana de formación + ventana retrospectiva

>[!TIP]
>
> La longitud mínima de datos requerida para una aplicación con configuraciones predeterminadas es: 2 trimestres (180 días) + 56 días = 236 días.

Por ejemplo:

- Desea atribuir eventos de conversión que se hayan producido en los últimos 90 días (3 meses) y rastrear todos los puntos de contacto que se han producido en las 4 semanas anteriores al evento de conversión. La duración de los datos de entrada debe ser de 90 días + 28 días (4 semanas). La ventana de formación es de 90 días y la ventana retrospectiva es de 28 días, con un total de 118 días.

## Datos de salida de Attribution AI

Inteligencia artificial aplicada a la atribución genera lo siguiente:

- [Puntuaciones granulares sin procesar](#raw-granular-scores)
- [Puntuaciones agregadas](#aggregated-attribution-scores)

**Ejemplo de esquema de salida:**

![](./images/input-output/schema_output.gif)

### Puntuaciones granulares sin procesar {#raw-granular-scores}

Inteligencia artificial aplicada a la atribución genera puntuaciones de atribución en el nivel más granular posible, de modo que puede cortar y fragmentar las puntuaciones por cualquier columna de puntuación. Para ver estas puntuaciones en la interfaz de usuario, lea la sección de [visualización de las rutas de puntuación sin procesar](#raw-score-path). Para descargar las puntuaciones mediante la API, visite el documento [descargar puntuaciones en Attribution AI](./download-scores.md).

>[!NOTE]
>
> Puede ver cualquier columna de creación de informes que desee del conjunto de datos de entrada en el conjunto de datos de salida de puntuación solo si alguna de las siguientes opciones es verdadera:
> - La columna de creación de informes se incluye en la página de configuración como parte de la configuración de punto de contacto o de definición de conversión.
> - La columna de creación de informes se incluye en columnas de conjuntos de datos de puntuación adicionales.

La siguiente tabla describe los campos de esquema en la salida de ejemplo de puntuaciones sin procesar:

| Nombre de columna (DataType) | Nullable | Descripción |
| --- | --- | --- |
| timestamp (DateTime) | False | El momento en que se produjo un evento de conversión o una observación. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| identityMap (mapa) | True | identityMap del usuario similar al formato XDM de CEE. |
| eventType (String) | True | El tipo de evento principal para este registro de serie temporal. <br> **Ejemplo:** &quot;Pedido&quot;, &quot;Compra&quot;, &quot;Visita&quot; |
| eventMergeId (String) | True | Identificador para correlacionar o combinar varios(as) [!DNL Experience Events] que son, en esencia, el mismo evento o que deben combinarse. Está previsto que el productor de datos lo rellene antes de la ingesta. <br> **Ejemplo:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (cadena) | False | Un identificador único del evento de la serie temporal. <br> **Ejemplo:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId, objeto | False | El contenedor de objeto de nivel superior correspondiente a su ID de tienda de campaña. <br> **Ejemplo:** _atsdsnrmmsv2 |
| your_schema_name, objeto | False | Fila de puntuación con evento de conversión: todos los eventos de punto de contacto asociados a él y sus metadatos. <br> **Ejemplo:** puntuaciones de inteligencia artificial aplicada a la atribución - Nombre de modelo__2020 |
| segmentation (String) | True | Segmento de conversión, como la segmentación geográfica con el que se crea el modelo. En caso de ausencia de segmentos, el segmento es el mismo que conversionName. <br> **Ejemplo:** ORDER_US |
| conversionName (String) | True | Nombre de la conversión que se configuró durante la configuración. <br> **Ejemplo:** pedido, posible cliente, visita |
| conversion, objeto | False | Columnas de metadatos de conversión. |
| dataSource (String) | True | Identificación global única de una fuente de datos. <br> **Ejemplo:** Adobe Analytics |
| eventSource (String) | True | Origen cuando se produjo el evento real. <br> **Ejemplo:** Adobe.com |
| eventType (String) | True | El tipo de evento principal para este registro de serie temporal. <br> **Ejemplo:** Pedido |
| geo (cadena) | True | Ubicación geográfica donde se entregó la conversión `placeContext.geo.countryCode`. <br> **Ejemplo:** EE. UU. |
| priceTotal (doble) | True | Ingresos obtenidos mediante la conversión <br> **Ejemplo:** 99.9 |
| product (String) | True | El identificador de XDM del producto en sí. <br> **Ejemplo:** RX 1080 ti |
| productType (String) | True | El nombre para mostrar del producto tal como se presenta al usuario en esta vista de producto. <br> **Ejemplo:** Gpus |
| cantidad (total) | True | Cantidad comprada durante la conversión. <br> **Ejemplo:** 1 1080 ti |
| receivedTimestamp (DateTime) | True | Marca de tiempo recibida de la conversión. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| skuId (cadena) | True | SKU (código de referencia), el identificador único de un producto definido por el proveedor. <br> **Ejemplo:** MJ-03-XS-Black |
| timestamp (DateTime) | True | Marca de tiempo de la conversión. <br> **Ejemplo:** 2020-06-09T00:01:51.000Z |
| passThrough, objeto | True | Conjunto de datos de puntuación adicional Columnas especificadas por el usuario al configurar el modelo. |
| commerce_order_purchaseCity (cadena) | True | Columna del conjunto de datos de puntuación adicional. <br> **Ejemplo:** ciudad: San José |
| customerProfile, objeto | False | Detalles de identidad del usuario utilizado para crear el modelo. |
| identity, objeto | False | Contiene los detalles del usuario utilizado para generar el modelo como `id` y `namespace`. |
| id (cadena) | True | ID de identidad del usuario, como ID de cookie, ID de Adobe Analytics (AAID) o ID de Experience Cloud (ECID, también conocido como MCID o como ID de visitante), etc. <br> **Ejemplo:** 17348762725408656344688320891369597404 |
| namespace (String) | True | Área de nombres de identidad utilizada para crear las rutas y, por lo tanto, el modelo. <br> **Ejemplo:** aaid |
| touchpointsDetail (matriz de objetos) | True | La lista de detalles del punto de contacto que llevan a la conversión ordenada por | incidencia de punto de contacto o marca de tiempo. |
| touchpointName (String) | True | Nombre del punto de contacto que se configuró durante la configuración. <br> **Ejemplo:** PAID_SEARCH_CLICK |
| score, objeto | True | Contribución de punto de contacto a esta conversión como puntuación. Para obtener más información sobre las puntuaciones producidas dentro de este objeto, consulte la sección [puntuaciones de atribución agregadas](#aggregated-attribution-scores). |
| touchPoint, objeto | True | Metadatos de Touchpoint. Para obtener más información sobre las puntuaciones generadas dentro de este objeto, consulte la sección [puntuaciones agregadas](#aggregated-scores). |

### Visualización de rutas de puntuación sin procesar (IU) {#raw-score-path}

Puede ver la ruta a las puntuaciones sin procesar en la interfaz de usuario. Comience por seleccionar **[!UICONTROL Esquemas]** en la interfaz de usuario de Experience Platform, luego busque y seleccione su esquema de puntuaciones de inteligencia artificial aplicada a la atribución en la pestaña **[!UICONTROL Examinar]**.

![Elija su esquema](./images/input-output/schemas_browse.png)

A continuación, seleccione un campo en la ventana **[!UICONTROL Structure]** de la interfaz de usuario, y se abrirá la pestaña **[!UICONTROL Field properties]**. Dentro de **[!UICONTROL Propiedades del campo]** está el campo de ruta que se asigna a las puntuaciones sin procesar.

![Elegir un esquema](./images/input-output/field_properties.png)

### Puntuaciones de atribución agregadas {#aggregated-attribution-scores}

Las puntuaciones agregadas se pueden descargar en formato CSV desde la interfaz de usuario de Experience Platform si el intervalo de fecha es inferior a 30 días.

Inteligencia artificial aplicada a la atribución admite dos categorías de puntuaciones de atribución, puntuaciones algorítmicas y basadas en reglas.

Attribution AI produce dos tipos diferentes de puntuaciones algorítmicas, incrementales e influenciadas. Una puntuación influenciada es la fracción de la conversión de la que es responsable cada punto de contacto de marketing. Una puntuación incremental es la cantidad de impacto marginal causado directamente por el punto de contacto de marketing. La principal diferencia entre la puntuación incremental y la puntuación influenciada es que la puntuación incremental tiene en cuenta el efecto de línea de base. No supone que una conversión se deba únicamente a los puntos de contacto de marketing anteriores.

A continuación, se muestra un ejemplo de salida de esquema de inteligencia artificial aplicada a la atribución desde la interfaz de usuario de Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Consulte la tabla siguiente para obtener más detalles sobre cada una de estas puntuaciones de atribución:

| Puntuaciones de atribución | Descripción |
| ----- | ----------- |
| Influenciado (algorítmico) | La puntuación influenciada es la fracción de la conversión de la que es responsable cada punto de contacto de marketing. |
| Incremental (algorítmico) | La puntuación incremental es la cantidad de impacto marginal causado directamente por un punto de contacto de marketing. |
| Primer contacto | Puntuación de atribución basada en reglas que asigna todos los créditos al punto de contacto inicial de una ruta de conversión. |
| Último contacto | Puntuación de atribución basada en reglas que asigna todo el crédito al punto de contacto más cercano a la conversión. |
| Lineal | Puntuación de atribución basada en reglas que asigna crédito igual a cada punto de contacto en una ruta de conversión. |
| Forma de U | Puntuación de atribución basada en reglas que asigna el 40 % del crédito al primer punto de contacto y el 40 % del crédito al último punto de contacto, mientras que los demás puntos de contacto dividen el 20 % restante de forma equitativa. |
| Deterioro de tiempo | Puntuación de atribución basada en reglas en la que los puntos de contacto más cercanos a la conversión reciben más crédito que los puntos de contacto que están más lejos en el tiempo de la conversión. |

**Referencia de puntuación sin procesar (puntuaciones de atribución)**

La siguiente tabla asigna las puntuaciones de atribución a las puntuaciones sin procesar. Si desea descargar sus puntuaciones sin procesar, visite la documentación de [descarga de puntuaciones en Attribution AI](./download-scores.md).

| Puntuaciones de atribución | Columna de referencia de puntuación sin procesar |
| --- | --- |
| Influenciado (algorítmico) | _tenantID.your_schema_name.element.touchpoint.algorítmicoInfluencing |
| Incremental (algorítmico) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorítmicoInfluencing |
| Primer contacto | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Último contacto | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Lineal | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| Forma de U | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Deterioro de tiempo | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Puntuaciones agregadas {#aggregated-scores}

Las puntuaciones agregadas se pueden descargar en formato CSV desde la interfaz de usuario de Experience Platform si el intervalo de fecha es inferior a 30 días. Consulte la tabla siguiente para obtener más detalles sobre cada una de estas columnas agregadas.

| Nombre de columna | Restricción | Nullable | Descripción |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Formato fijo y definido por el usuario | False | Fecha del evento del cliente en formato AAAA-MM-DD. <br> **Ejemplo**: 02-05-2016 |
| mediatouchpoints_date (DateTime) | Formato fijo y definido por el usuario | True | Fecha de punto de contacto de medios en formato AAAA-MM-DD <br> **Ejemplo**: 2017-04-21 |
| segment (String) | Calculado | False | Segmento de conversión, como la segmentación geográfica con la que se crea el modelo. En caso de ausencia de segmentos, el segmento es el mismo que conversion_scope. <br> **Ejemplo**: ORDER_AMER |
| conversion_scope (String) | Definido por el usuario | False | Nombre de la conversión según la configuración del usuario. <br> **Ejemplo**: ORDER |
| touchpoint_scope (cadena) | Definido por el usuario | True | Nombre del punto de contacto configurado por el usuario <br> **Ejemplo**: PAID_SEARCH_CLICK |
| product (String) | Definido por el usuario | True | El identificador de XDM del producto. <br> **Ejemplo**: CC |
| product_type (String) | Definido por el usuario | True | El nombre para mostrar del producto tal como se presenta al usuario en esta vista de producto. <br> **Ejemplo**: gpus, portátiles |
| geo (cadena) | Definido por el usuario | True | Ubicación geográfica donde se entregó la conversión (placeContext.geo.countryCode) <br> **Ejemplo**: EE. UU. |
| event_type (String) | Definido por el usuario | True | El tipo de evento principal para este registro de serie temporal <br> **Ejemplo**: Conversión de pago |
| media_type (String) | ENUM | False | Describe si el tipo de medios es de pago, se posee o se obtiene. <br> **Ejemplo**: DE PAGO, DE PROPIEDAD |
| channel (String) | ENUM | False | La propiedad `channel._type` que se usa para proporcionar una clasificación aproximada de canales con propiedades similares en el XDM [!DNL Consumer Experience Event]. <br> **Ejemplo**: SEARCH |
| action (String) | ENUM | False | La propiedad `mediaAction` se usa para proporcionar un tipo de acción multimedia de evento de experiencia. <br> **Ejemplo**: CLIC |
| campaign_group (String) | Definido por el usuario | True | Nombre del grupo de campañas donde se agrupan varias campañas como 50%_DESCUENTO. <br> **Ejemplo**: COMERCIAL |
| campaign_name (String) | Definido por el usuario | True | Nombre de la campaña utilizada para identificar la campaña de marketing como 50%_DESCUENTO_USA o 50%_DESCUENTO_ASIA. <br> **Ejemplo**: Venta de Acción de Gracias |

**Referencia de puntuación sin procesar (agregada)**

La siguiente tabla asigna las puntuaciones agregadas a las puntuaciones sin procesar. Si desea descargar sus puntuaciones sin procesar, visite la documentación de [descarga de puntuaciones en Attribution AI](./download-scores.md). Para ver las rutas de puntuación sin procesar desde la interfaz de usuario, visite la sección de [visualización de rutas de puntuación sin procesar](#raw-score-path) dentro de este documento.

| Nombre de columna | Columna de referencia de puntuación sin procesar |
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

>[!IMPORTANT]
>
> - Inteligencia artificial aplicada a la atribución solo utiliza datos actualizados para un aprendizaje y una puntuación adicionales. Del mismo modo, cuando solicita eliminar datos, la inteligencia artificial aplicada al cliente se abstiene de utilizar los datos eliminados.
> - Inteligencia artificial aplicada a la atribución aprovecha los conjuntos de datos de Experience Platform. Para admitir solicitudes de derechos de consumidor que una marca pueda recibir, las marcas deben utilizar Experience Platform Privacy Service para enviar solicitudes de acceso y eliminación de consumidores con el fin de eliminar sus datos en el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real.
> - Todos los conjuntos de datos que utilizamos para la entrada/salida de modelos seguirán las directrices de Experience Platform. El cifrado de datos de Experience Platform se aplica a los datos en reposo y en tránsito. Consulte la documentación para obtener más información sobre el [cifrado de datos](../../../help/landing/governance-privacy-security/encryption.md)

## Pasos siguientes {#next-steps}

Una vez que haya preparado los datos y haya establecido todas sus credenciales y esquemas, comience por seguir la [guía del usuario de inteligencia artificial aplicada a la atribución](./user-guide.md). Esta guía le explica cómo crear una instancia para la inteligencia artificial aplicada a la atribución.
