---
keywords: Experience Platform;inicio;Servicios inteligentes;temas populares;servicio inteligente;Servicio inteligente
solution: Experience Platform
title: Preparación de datos para utilizarlos en servicios inteligentes
description: Para que los servicios inteligentes descubran datos de sus eventos de marketing, los datos deben enriquecerse semánticamente y mantenerse en una estructura estándar. Los servicios inteligentes utilizan esquemas XDM (Experience Data Model) para conseguirlo.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2951'
ht-degree: 0%

---

# Preparar datos para usarlos en [!DNL Intelligent Services]

Para que [!DNL Intelligent Services] descubra datos de sus eventos de marketing, los datos deben estar semánticamente enriquecidos y mantenerse en una estructura estándar. [!DNL Intelligent Services] aprovechan [!DNL Experience Data Model] esquemas (XDM) para lograrlo. Específicamente, todos los conjuntos de datos que se utilizan en [!DNL Intelligent Services] deben cumplir con el esquema XDM de Consumer ExperienceEvent (CEE) o utilizar el conector de Adobe Analytics. Además, la inteligencia artificial aplicada al cliente admite el conector de Adobe Audience Manager.

Este documento proporciona orientación general sobre la asignación de los datos de eventos de marketing de varios canales al esquema CEE, y describe información sobre campos importantes dentro del esquema para ayudarle a determinar cómo asignar de forma eficaz los datos a su estructura. Si planea usar datos de Adobe Analytics, consulte la sección para [preparación de datos de Adobe Analytics](#analytics-data). Si planea usar datos de Adobe Audience Manager (solo inteligencia artificial aplicada al cliente), consulte la sección correspondiente a [Preparación de datos de Adobe Audience Manager](#AAM-data).

## Requisitos de datos

[!DNL Intelligent Services] requiere diferentes cantidades de datos históricos según el objetivo que cree. Independientemente, los datos que prepare para **todos** [!DNL Intelligent Services] deben incluir eventos o recorridos de clientes positivos y negativos. Tener eventos negativos y positivos mejora la precisión y la precisión del modelo.

Por ejemplo, si utiliza la inteligencia artificial aplicada al cliente para predecir la tendencia a comprar un producto, el modelo para la inteligencia artificial aplicada al cliente necesita tanto ejemplos de rutas de compra exitosas como ejemplos de rutas fallidas. Esto se debe a que durante la formación del modelo, la inteligencia artificial aplicada al cliente busca comprender qué eventos y recorridos conducen a una compra. Esto también incluye las acciones realizadas por los clientes que no realizaron ninguna compra, como por ejemplo una persona que detuvo su recorrido al agregar un artículo al carro de compras. Estos clientes pueden mostrar comportamientos similares; sin embargo, la inteligencia artificial aplicada al cliente puede proporcionar perspectivas y explorar en profundidad las principales diferencias y factores que conducen a una puntuación de tendencia más alta. Del mismo modo, Inteligencia artificial aplicada a la atribución requiere ambos tipos de eventos y recorridos para mostrar métricas como la efectividad de los puntos de contacto, las rutas de conversión principales y los desgloses por posición de punto de contacto.

Para obtener más ejemplos e información sobre los requisitos de datos históricos, visite la sección de requisitos de datos históricos de [inteligencia artificial aplicada al cliente](./customer-ai/data-requirements.md#data-requirements) o [inteligencia artificial aplicada a la atribución](./attribution-ai/input-output.md#data-requirements) en la documentación de entrada y salida.

### Directrices para vincular datos

Se recomienda vincular los eventos de un usuario a un ID común siempre que sea posible. Por ejemplo: es posible que tenga datos de usuario con &quot;id1&quot; en 10 eventos. Posteriormente, el mismo usuario eliminó el ID de cookie y se registró como &quot;id2&quot; en los 20 eventos siguientes. Si sabe que id1 e id2 corresponden al mismo usuario, se recomienda unir los 30 eventos con un ID común.

Si esto no es posible, debe tratar cada conjunto de eventos como un usuario diferente al crear los datos de entrada del modelo. Esto garantiza los mejores resultados durante la formación y la puntuación del modelo.

## Resumen del flujo de trabajo

El proceso de preparación varía en función de si los datos se almacenan en Adobe Experience Platform o externamente. Esta sección resume los pasos necesarios que debe seguir, en cualquiera de los casos.

### Preparación de datos externos

Si los datos se almacenan fuera de Experience Platform, debe asignarlos a los campos obligatorios y relevantes en un [esquema de Consumer ExperienceEvent](#cee-schema). Este esquema se puede ampliar con grupos de campos personalizados para capturar mejor los datos de los clientes. Una vez asignado, puede crear un conjunto de datos con el esquema Consumer ExperienceEvent e [introducir los datos en Experience Platform](../ingestion/home.md). El conjunto de datos CEE se puede seleccionar al configurar un [!DNL Intelligent Service].

Según el(la) [!DNL Intelligent Service] que desee utilizar, es posible que se requieran diferentes campos. Tenga en cuenta que es recomendable agregar datos a un campo si tiene los datos disponibles. Para obtener más información sobre los campos obligatorios, visita la guía de requisitos de datos de [inteligencia artificial aplicada a la atribución](./attribution-ai/input-output.md) o la [inteligencia artificial aplicada al cliente](./customer-ai/data-requirements.md).

### Preparación de datos de Adobe Analytics {#analytics-data}

La inteligencia artificial aplicada al cliente y la inteligencia artificial aplicada a la atribución admiten datos de Adobe Analytics de forma nativa. Para usar datos de Adobe Analytics, sigue los pasos descritos en la documentación para configurar un [conector de origen de Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Una vez que el conector de origen transmite los datos a Experience Platform, puede seleccionar Adobe Analytics como fuente de datos seguida de un conjunto de datos durante la configuración de la instancia. Todos los grupos de campos de esquema requeridos y los campos individuales se crean automáticamente durante la configuración de la conexión. No es necesario extraer, transformar o cargar los conjuntos de datos en el formato CEE.

Si compara los datos volados a través del conector de origen de Adobe Analytics en Adobe Experience Platform con los datos de Adobe Analytics, puede observar algunas discrepancias. El conector Source de Analytics podría soltar filas durante la transformación a un esquema Experience Data Model (XDM). Puede haber varias razones para que toda la fila no sea apta para la transformación, como marcas de tiempo que faltan, personID que faltan, ID de persona no válidos o grandes, valores de análisis no válidos y más.

Para obtener más información y ejemplos, visite la documentación de [comparación de datos de Adobe Analytics y Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Este artículo se ha diseñado para ayudarle a diagnosticar y resolver esas diferencias, de modo que usted y su equipo puedan utilizar los datos de Adobe Experience Platform para servicios inteligentes sin impedimentos por motivos de integridad de los datos.

En Adobe Experience Platform Query Services, ejecute la siguiente consulta Registros totales entre la marca de tiempo de inicio y de fin por channel.typeAtSource para buscar el recuento por canales de marketing.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>El conector de Adobe Analytics tarda hasta cuatro semanas en rellenar los datos. Si ha configurado recientemente una conexión, debe verificar que el conjunto de datos tenga la longitud mínima de datos necesaria para la inteligencia artificial aplicada a la atribución o el cliente. Revise las secciones de datos históricos en [inteligencia artificial aplicada al cliente](./customer-ai/data-requirements.md#data-requirements) o [inteligencia artificial aplicada a la atribución](./attribution-ai/input-output.md#data-requirements), y verifique que tenga datos suficientes para el objetivo de predicción.

### Preparación de datos de Adobe Audience Manager (solo inteligencia artificial aplicada al cliente) {#AAM-data}

La inteligencia artificial aplicada al cliente admite datos de Adobe Audience Manager de forma nativa. Para usar datos de Audience Manager, sigue los pasos descritos en la documentación para configurar un [conector de origen de Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Una vez que el conector de origen transmite los datos a Experience Platform, puede seleccionar Adobe Audience Manager como fuente de datos seguida de un conjunto de datos durante la configuración de la inteligencia artificial aplicada al cliente. Todos los grupos de campos de esquema y los campos individuales se crean automáticamente durante la configuración de la conexión. No es necesario extraer, transformar o cargar los conjuntos de datos en el formato CEE.

>[!IMPORTANT]
>
>Si ha configurado recientemente un conector, debe verificar que el conjunto de datos tenga la longitud mínima de datos requerida. Revise la sección de datos históricos de la [documentación de entrada y salida](./customer-ai/data-requirements.md) para la inteligencia artificial aplicada al cliente y compruebe que dispone de datos suficientes para el objetivo de predicción.

### [!DNL Experience Platform] preparación de datos

Si sus datos ya están almacenados en [!DNL Experience Platform] y no se transmiten a través de los conectores de origen de Adobe Analytics o Adobe Audience Manager (solo inteligencia artificial aplicada al cliente), siga los pasos a continuación. Se recomienda que entienda el esquema de CEE.

1. Revise la estructura del esquema [Consumer ExperienceEvent](#cee-schema) y determine si los datos se pueden asignar a sus campos.
2. Póngase en contacto con los servicios de Adobe Consulting para que le ayuden a asignar los datos al esquema e ingerirlos en [!DNL Intelligent Services], o [siga los pasos de esta guía](#mapping) si desea asignar los datos usted mismo.

## Explicación del esquema CEE {#cee-schema}

El esquema Consumer ExperienceEvent describe el comportamiento de una persona en relación con los eventos de marketing digital (web o móvil), así como la actividad de comercio en línea o sin conexión. Se requiere el uso de este esquema para [!DNL Intelligent Services] debido a sus campos semánticamente bien definidos (columnas), lo que evita nombres desconocidos que, de otro modo, harían que los datos fueran menos claros.

El esquema CEE, como todos los esquemas XDM ExperienceEvent, captura el estado basado en series temporales del sistema cuando se produjo un evento (o conjunto de eventos), incluido el momento y la identidad del sujeto involucrado. Los eventos de experiencia son registros de hechos de lo que ha ocurrido y, por lo tanto, son inmutables y representan lo que ha sucedido sin agregación ni interpretación.

[!DNL Intelligent Services] utiliza varios campos clave dentro de este esquema para generar perspectivas a partir de los datos de eventos de marketing, los cuales se pueden encontrar en el nivel raíz y expandir para mostrar sus subcampos obligatorios.

![Demostración de la expansión de esquemas en la interfaz de usuario de Adobe Experience Platform, que muestra detalles de navegación y subcampos.](./images/data-preparation/schema-expansion.gif)

Al igual que todos los esquemas XDM, el grupo de campos de esquema CEE es extensible. En otras palabras, se pueden añadir campos adicionales al grupo de campos CEE, y se pueden incluir diferentes variaciones en varios esquemas si es necesario.

Se puede encontrar un ejemplo completo del grupo de campos en el [repositorio XDM público](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Además, puede ver y copiar el siguiente [archivo JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para ver un ejemplo de cómo se pueden estructurar los datos para cumplir con el esquema CEE. Consulte ambos ejemplos a medida que aprenda sobre los campos clave descritos en la sección siguiente para determinar cómo puede asignar sus propios datos al esquema.

## Campos clave

Hay varios campos clave dentro del grupo de campos CEE que deben usarse para que [!DNL Intelligent Services] genere perspectivas útiles. En esta sección se describe el caso de uso y los datos esperados para estos campos, y se proporcionan vínculos a documentación de referencia para ver más ejemplos.

### Campos obligatorios

Aunque se recomienda encarecidamente el uso de todos los campos clave, hay dos campos que son **obligatorios** para que [!DNL Intelligent Services] funcione:

* [Un campo de identidad principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obligatorio solo para inteligencia artificial aplicada a la atribución)

#### Identidad principal {#identity}

Uno de los campos del esquema debe establecerse como campo de identidad principal, lo que permite a [!DNL Intelligent Services] vincular cada instancia de datos de series temporales a una persona individual.

Debe determinar el mejor campo para utilizarlo como identidad principal en función del origen y la naturaleza de los datos. Un campo de identidad debe incluir un **área de nombres de identidad** que indique el tipo de datos de identidad que el campo espera como valor. Algunos valores de área de nombres válidos incluyen:

>[!NOTE]
>
>El Experience Cloud ID (ECID) también se conoce como MCID y sigue utilizándose en áreas de nombres.

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (para Adobe Audience Manager ID)
* &quot;aaid&quot; (para Adobe Analytics ID)

Si no está seguro de qué campo debe utilizar como identidad principal, póngase en contacto con los servicios de Adobe Consulting para determinar la mejor solución. Si no se define una identidad principal, la aplicación Servicio inteligente utilizará el siguiente comportamiento predeterminado:

| Predeterminado | Inteligencia artificial aplicada a la atribución | Inteligencia artificial aplicada al cliente |
| --- | --- | --- |
| Columna de identidad | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Área de nombres | AAID | ECID |

Para establecer una identidad principal, vaya al esquema desde la ficha **[!UICONTROL Esquemas]** y seleccione el hipervínculo del nombre del esquema para abrir **[!DNL Schema Editor]**.

![Navegación al esquema en la interfaz de usuario de Adobe Experience Platform.](./images/data-preparation/navigate_schema.png)

A continuación, vaya al campo que desee utilizar como identidad principal y selecciónelo. Se abre el menú **[!UICONTROL Propiedades del campo]** para ese campo.

![Proceso de selección del campo deseado en la interfaz de usuario de Adobe Experience Platform.](./images/data-preparation/find_field.png)

En el menú **[!UICONTROL Propiedades del campo]**, desplácese hacia abajo hasta que encuentre la casilla de verificación **[!UICONTROL Identidad]**. Después de marcar la casilla, aparecerá la opción para establecer la identidad seleccionada como **[!UICONTROL identidad principal]**. Seleccione también esta casilla.

![Casilla de verificación para establecer la identidad principal en la interfaz de usuario de Adobe Experience Platform.](./images/data-preparation/set_primary_identity.png)

A continuación, debe proporcionar un **[!UICONTROL área de nombres de identidad]** de la lista de áreas de nombres predefinidas en el menú desplegable. En este ejemplo, el área de nombres ECID está seleccionada porque se está utilizando un Adobe Audience Manager ID `mcid.id`. Seleccione **[!UICONTROL Aplicar]** para confirmar las actualizaciones y, a continuación, seleccione **[!UICONTROL Guardar]** en la esquina superior derecha para guardar los cambios en el esquema.

Menú desplegable ![que muestra la selección del área de nombres ECID en la interfaz de usuario de Adobe Experience Platform.](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Este campo representa la fecha y hora a la que se produjo el evento. Este valor debe proporcionarse como una cadena, según la norma ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Este campo solo es obligatorio cuando se utiliza Attribution AI.

Este campo representa el canal de marketing relacionado con ExperienceEvent. El campo incluye información sobre el tipo de canal, el tipo de medios y el tipo de ubicación.

![Diagrama que muestra la estructura del campo xdm:channel, incluidos subcampos como type, mediaType y mediaAction.](./images/data-preparation/channel.png)

**Esquema de ejemplo**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:channel`, consulte la especificación [esquema del canal de experiencia](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Para ver algunas asignaciones de ejemplo, consulte la [tabla siguiente](#example-channels).

#### Ejemplo de asignaciones de canales {#example-channels}

En la tabla siguiente se proporcionan algunos ejemplos de canales de marketing asignados al esquema `xdm:channel`:

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Búsqueda de pago | https:/<span>/ns.adobe.com/xdm/channel-types/search | pagado | clics |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | merecido | clics |
| Mostrar | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagado | clics |
| Correo electrónico | https:/<span>/ns.adobe.com/xdm/channel-types/email | pagado | clics |
| Referente interno | https:/<span>/ns.adobe.com/xdm/channel-types/direct | de propiedad | clics |
| Mostrar vista completa | https:/<span>/ns.adobe.com/xdm/channel-types/display | pagado | impresiones |
| Redirección de código QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | de propiedad | clics |
| Dispositivo móvil | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | de propiedad | clics |

### Campos recomendados

El resto de los campos clave se describen en esta sección. Aunque estos campos no son necesariamente necesarios para que [!DNL Intelligent Services] funcione, se recomienda encarecidamente que utilice tantos como sea posible para obtener información más completa.

#### xdm:productListItems

Este campo es una matriz de artículos que representan los productos seleccionados por un cliente, incluido el SKU del producto, el nombre, el precio y la cantidad.

![El campo xdm:productListItems, que incluye subcampos como SKU, nombre, currencyCode, cantidad y priceTotal.](./images/data-preparation/productListItems.png)

**Esquema de ejemplo**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación [esquema de detalles de comercio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Este campo contiene información específica de comercio sobre ExperienceEvent, incluido el número de orden de compra y la información de pago.

![Estructura del campo xdm:commerce, incluidos subcampos como pedidos, compras y pagos.](./images/data-preparation/commerce.png)

**Esquema de ejemplo**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:commerce`, consulte la especificación [esquema de detalles de comercio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Este campo representa los detalles web relacionados con el ExperienceEvent, como la interacción, los detalles de página y el referente.

![Campo xdm:web, incluidos subcampos como webPageDetails y webReferrer.](./images/data-preparation/web.png)

**Esquema de ejemplo**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación [esquema de detalles web de ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md).

#### xdm:marketing

Este campo contiene información relacionada con las actividades de marketing que están activas con el punto de contacto.

![Estructura del campo xdm:marketing, incluidos subcampos como trackingCode, campaignGroup y campaignName.](./images/data-preparation/marketing.png)

**Esquema de ejemplo**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación de [esquema de marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Asignación e ingesta de datos {#mapping}

Una vez que haya determinado si los datos de los eventos de marketing se pueden asignar al esquema de CEE, el siguiente paso es determinar qué datos desea introducir en [!DNL Intelligent Services]. Todos los datos históricos utilizados en [!DNL Intelligent Services] deben encontrarse dentro del período de tiempo mínimo de cuatro meses de datos, más el número de días que se pretende que sean un período retroactivo.

Después de decidir el rango de datos que desea enviar, póngase en contacto con los servicios de Adobe Consulting para que le ayuden a asignar los datos al esquema e ingerirlos en el servicio.

Si tiene una suscripción de [!DNL Adobe Experience Platform] y desea asignar e ingerir los datos usted mismo, siga los pasos descritos en la sección siguiente.

### Uso de Adobe Experience Platform

>[!NOTE]
>
>Los pasos siguientes requieren una suscripción a Experience Platform. Si no tiene acceso a Experience Platform, vaya a la sección [pasos siguientes](#next-steps).

En esta sección se describe el flujo de trabajo para asignar e ingerir datos en Experience Platform para usarlos en [!DNL Intelligent Services], incluidos los vínculos a tutoriales para ver los pasos detallados.

#### Crear un esquema y un conjunto de datos de CEE

Cuando esté listo para empezar a preparar los datos para la ingesta, el primer paso es crear un nuevo esquema XDM que emplee el grupo de campos CEE. Los siguientes tutoriales explican el proceso de creación de un nuevo esquema en la IU o API de:

* [Creación de un esquema en la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)
* [Creación de un esquema en la API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Los tutoriales anteriores siguen un flujo de trabajo genérico para crear un esquema. Al elegir una clase para el esquema, debe utilizar la **clase XDM ExperienceEvent**. Una vez elegida esta clase, puede añadir el grupo de campos CEE al esquema.

Después de agregar el grupo de campos CEE al esquema, puede agregar otros grupos de campos según sea necesario para campos adicionales dentro de los datos.

Una vez creado y guardado el esquema, puede crear un nuevo conjunto de datos basado en ese esquema. Los siguientes tutoriales explican el proceso de creación de un nuevo conjunto de datos en la IU o API de:

* [Crear un conjunto de datos en la interfaz de usuario](../catalog/datasets/user-guide.md#create) (siga el flujo de trabajo para usar un esquema existente)
* [Cree un conjunto de datos en la API](../catalog/datasets/create.md)

Una vez creado el conjunto de datos, puede encontrarlo en la interfaz de usuario de Experience Platform dentro del área de trabajo **[!UICONTROL Conjuntos de datos]**.

![](images/data-preparation/dataset-location.png)

#### Añadir campos de identidad al conjunto de datos

Si va a traer datos de [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] u otro origen externo, tiene la opción de establecer un campo de esquema como campo de identidad. Para establecer un campo de esquema como campo de identidad, consulte la sección sobre la configuración de campos de identidad en el [tutorial de interfaz de usuario](../xdm/tutorials/create-schema-ui.md#identity-field) o en el [tutorial de API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) para crear un esquema.

Si está ingiriendo datos de un archivo CSV local, puede pasar a la siguiente sección sobre [asignación e ingesta de datos](#ingest).

#### Asignación e ingesta de datos {#ingest}

Después de crear un esquema y un conjunto de datos de CEE, puede empezar a asignar las tablas de datos al esquema e introducir esos datos en Experience Platform. Consulte el tutorial sobre [asignación de un archivo CSV a un esquema XDM](../ingestion/tutorials/map-csv/overview.md) para ver los pasos sobre cómo hacerlo en la interfaz de usuario. Puede usar el siguiente [archivo JSON de muestra](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para probar el proceso de ingesta antes de usar sus propios datos.

Una vez que se ha rellenado un conjunto de datos, se puede utilizar el mismo conjunto de datos para introducir archivos de datos adicionales.

Si los datos están almacenados en una aplicación de terceros compatible, también puede optar por crear un [conector de origen](../sources/home.md) para introducir los datos de eventos de marketing en [!DNL Experience Platform] en tiempo real.

## Pasos siguientes {#next-steps}

En este documento se proporcionan instrucciones generales sobre cómo preparar los datos para usarlos en [!DNL Intelligent Services]. Si necesita asesoramiento adicional basado en su caso de uso, póngase en contacto con el soporte de Adobe Consulting.

Una vez que haya rellenado correctamente un conjunto de datos con los datos de experiencia del cliente, puede usar [!DNL Intelligent Services] para generar perspectivas. Consulte los siguientes documentos para empezar:

* [Descripción general de Attribution AI](./attribution-ai/overview.md)
* [Información general sobre Customer AI ](./customer-ai/overview.md)
