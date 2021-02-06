---
keywords: Experience Platform;hogar;Servicios inteligentes;temas populares;servicio inteligente;Servicio inteligente
solution: Experience Platform, Intelligent Services
title: Preparación de datos para su uso en Servicios inteligentes
topic: Intelligent Services
description: 'Para que los servicios inteligentes puedan descubrir perspectivas a partir de los datos de eventos de marketing, los datos deben enriquecirse y mantenerse semánticamente en una estructura estándar. Los servicios inteligentes aprovechan los esquemas del modelo de datos de experiencia (XDM) para lograr esto. Específicamente, todos los datasets que se utilizan en Servicios inteligentes] deben cumplir con el esquema XDM de Consumer ExperienceEvent (CEE). '
translation-type: tm+mt
source-git-commit: eb163949f91b0d1e9cc23180bb372b6f94fc951f
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 1%

---


# Preparar datos para su uso en [!DNL Intelligent Services]

Para que [!DNL Intelligent Services] detecte perspectivas a partir de los datos de eventos de mercadotecnia, los datos deben enriquecirse semánticamente y mantenerse en una estructura estándar. [!DNL Intelligent Services] aproveche los esquemas  [!DNL Experience Data Model] (XDM) para lograrlo. Específicamente, todos los datasets que se utilizan en [!DNL Intelligent Services] deben cumplir con el esquema XDM de Consumer ExperienceEvent (CEE).

Este documento proporciona una guía general sobre cómo asignar los datos de eventos de marketing de varios canales a este esquema, esbozando información sobre los campos importantes dentro del esquema para ayudarle a determinar cómo asignar los datos de manera efectiva a su estructura.

## Resumen de flujo de trabajo

El proceso de preparación varía en función de si los datos se almacenan en Adobe Experience Platform o externamente. En esta sección se resumen los pasos necesarios que debe seguir, en cualquier caso.

### Preparación de datos externos

Si los datos se almacenan fuera de [!DNL Experience Platform], siga los pasos a continuación:

1. Póngase en contacto con los servicios de consultoría de Adobe para solicitar las credenciales de acceso para un contenedor de Almacenamiento de blob de Azure dedicado.
1. Con las credenciales de acceso, cargue los datos en el contenedor Blob.
1. Trabaje con los servicios de consultoría de Adobe para obtener los datos asignados al esquema [Consumer ExperienceEvent](#cee-schema) e ingeridos en [!DNL Intelligent Services].

### [!DNL Experience Platform] preparación de datos

Si los datos ya están almacenados en [!DNL Platform], siga los pasos a continuación:

1. Revise la estructura del [esquema de Consumer ExperienceEvent](#cee-schema) y determine si los datos se pueden asignar a sus campos.
1. Póngase en contacto con los servicios de consultoría de Adobe para ayudarle a asignar los datos al esquema e ingerirlos en [!DNL Intelligent Services] o [siga los pasos de esta guía](#mapping) si desea asignar los datos usted mismo.

## Explicación del esquema CEE {#cee-schema}

El esquema Consumer ExperienceEvent describe el comportamiento de una persona en relación con eventos de marketing digital (web o móvil), así como con la actividad comercial en línea o sin conexión. Se requiere el uso de este esquema para [!DNL Intelligent Services] debido a sus campos (columnas) semánticamente bien definidos, evitando nombres desconocidos que de otra manera harían que los datos fueran menos claros.

El esquema CEE, al igual que todos los esquemas de ExperienceEvent de XDM, captura el estado del sistema basado en series temporales cuando se produjo un evento (o conjunto de eventos), incluido el momento y la identidad del sujeto involucrado. Los Eventos de experiencias son registros de hechos de lo que ocurrió, y por lo tanto son inmutables y representan lo que pasó sin agregación ni interpretación.

[!DNL Intelligent Services] utilice varios campos clave dentro de este esquema para generar perspectivas a partir de los datos de eventos de marketing, todos los cuales se pueden encontrar en el nivel raíz y expandirse para mostrar los subcampos requeridos.

![](./images/data-preparation/schema-expansion.gif)

Al igual que todos los esquemas XDM, la mezcla CEE es extensible. En otras palabras, se pueden agregar campos adicionales a la mezcla CEE y, si es necesario, se pueden incluir variaciones diferentes en varios esquemas.

Encontrará un ejemplo completo de la mezcla en el [repositorio XDM público](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Además, puede crear vistas y copiar el siguiente [archivo JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para ver un ejemplo de cómo se pueden estructurar los datos para cumplir con el esquema CEE. Consulte estos dos ejemplos cuando conozca los campos clave descritos en la sección siguiente para determinar cómo puede asignar sus propios datos al esquema.

## Campos clave

Existen varios campos clave dentro de la mezcla CEE que deben utilizarse para que [!DNL Intelligent Services] genere perspectivas útiles. Esta sección describe el caso de uso y los datos esperados para estos campos, y proporciona vínculos a la documentación de referencia para obtener más ejemplos.

### Campos obligatorios

Aunque se recomienda enfáticamente el uso de todos los campos clave, hay dos campos **requeridos** para que [!DNL Intelligent Services] funcione:

* [Campo de identidad principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:canal](#channel)  (obligatorio solo para Attribution AI)

#### Identidad principal {#identity}

Uno de los campos del esquema debe configurarse como un campo de identidad principal, que permite a [!DNL Intelligent Services] vincular cada instancia de datos de series temporales a una persona individual.

Debe determinar el mejor campo para utilizarlo como identidad principal en función de la fuente y la naturaleza de los datos. Un campo de identidad debe incluir una **Área de nombres de identidad** que indique el tipo de datos de identidad que el campo espera como valor. Algunos valores de Área de nombres válidos son:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (para Adobe Audience Manager ID)
* &quot;aaid&quot; (para Adobe Analytics ID)

Si no está seguro de qué campo debe utilizar como identidad principal, póngase en contacto con los servicios de consultoría de Adobe para determinar cuál es la mejor solución.

#### xdm:timestamp {#timestamp}

Este campo representa la fecha y hora en que se produjo el evento. Este valor debe proporcionarse como una cadena, según la norma ISO 8601.

#### xdm:canal {#channel}

>[!NOTE]
>
>Este campo solo es obligatorio cuando se utiliza Attribution AI.

Este campo representa el canal de marketing relacionado con ExperienceEvent. El campo incluye información sobre el tipo de canal, el tipo de medio y el tipo de ubicación.

![](./images/data-preparation/channel.png)

**Esquema de ejemplo**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Para obtener información completa acerca de cada uno de los subcampos requeridos para `xdm:channel`, consulte la especificación del [esquema de canal de experiencias](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Para ver algunos ejemplos de asignaciones, consulte la tabla [a continuación](#example-channels).

##### Ejemplos de asignaciones de canal {#example-channels}

La siguiente tabla proporciona algunos ejemplos de canales de mercadotecnia asignados al esquema `xdm:channel`:

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Búsqueda de pago | https:/<span>/ns.adobe.com/xdm/canal-types/search | pagado | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/canal-types/social | ganado | clics |
| Mostrar | https:/<span>/ns.adobe.com/xdm/canal-types/display | pagado | clics |
| Correo electrónico | https:/<span>/ns.adobe.com/xdm/canal-types/email | pagado | clics |
| Remitente del reenvío interno | https:/<span>/ns.adobe.com/xdm/canal-types/direct | propiedad | clics |
| Visualización de visualizaciones | https:/<span>/ns.adobe.com/xdm/canal-types/display | pagado | impresiones |
| Redirección de código QR | https:/<span>/ns.adobe.com/xdm/canal-types/direct | propiedad | clics |
| Dispositivo móvil | https:/<span>/ns.adobe.com/xdm/canal-types/mobile | propiedad | clics |

### Campos recomendados

El resto de los campos clave se describen en esta sección. Aunque estos campos no son necesariamente necesarios para que [!DNL Intelligent Services] funcione, se recomienda usar tantos como sea posible para obtener perspectivas más enriquecidas.

#### xdm:productListItems

Este campo es una matriz de artículos que representan los productos seleccionados por un cliente, incluidos el SKU del producto, el nombre, el precio y la cantidad.

![](./images/data-preparation/productListItems.png)

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

Para obtener información completa acerca de cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación [esquema de detalles comerciales](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Este campo contiene información específica sobre el comercio acerca de ExperienceEvent, incluido el número de orden de compra y la información de pago.

![](./images/data-preparation/commerce.png)

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

Para obtener información completa acerca de cada uno de los subcampos requeridos para `xdm:commerce`, consulte la especificación [esquema de detalles comerciales](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Este campo representa los detalles web relacionados con ExperienceEvent, como la interacción, los detalles de la página y el remitente del reenvío.

![](./images/data-preparation/web.png)

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

Para obtener información completa acerca de cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación del [esquema de detalles web de ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md).

#### xdm:marketing

Este campo contiene información relacionada con actividades de marketing que están activas con el touchpoint.

![](./images/data-preparation/marketing.png)

**Esquema de ejemplo**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación [chechma de mercadotecnia](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Asignación e ingesta de datos {#mapping}

Una vez que haya determinado si los datos de eventos de mercadotecnia se pueden asignar al esquema de CEE, el siguiente paso es determinar qué datos se van a importar a [!DNL Intelligent Services]. Todos los datos históricos utilizados en [!DNL Intelligent Services] deben estar dentro del intervalo de tiempo mínimo de cuatro meses de datos, más el número de días previsto como período retroactivo.

Después de decidir el rango de datos que desea enviar, póngase en contacto con los servicios de consultoría de Adobe para ayudarle a asignar los datos al esquema y a ingerirlos al servicio.

Si tiene una suscripción [!DNL Adobe Experience Platform] y desea asignar e ingestar los datos usted mismo, siga los pasos descritos en la sección a continuación.

### Uso de Adobe Experience Platform

>[!NOTE]
>
>Los pasos a continuación requieren una suscripción al Experience Platform. Si no tiene acceso a Platform, vaya a la sección [siguientes pasos](#next-steps).

Esta sección describe el flujo de trabajo para asignar e ingerir datos en Experience Platform para utilizarlos en [!DNL Intelligent Services], incluidos vínculos a tutoriales para obtener pasos detallados.

#### Crear un esquema y un conjunto de datos de CEE

Cuando esté listo para el inicio de preparar sus datos para la ingestión, el primer paso es crear un nuevo esquema XDM que emplee la mezcla CEE. Los siguientes tutoriales explican el proceso de creación de un nuevo esquema en la interfaz de usuario o la API:

* [Creación de un esquema en la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)
* [Creación de un esquema en la API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Los tutoriales anteriores siguen un flujo de trabajo genérico para crear un esquema. Al elegir una clase para el esquema, debe utilizar la clase **XDM ExperienceEvent**. Una vez seleccionada esta clase, puede agregar la mezcla CEE al esquema.

Después de agregar la mezcla CEE al esquema, puede agregar otras mezclas según sea necesario para campos adicionales dentro de los datos.

Una vez creado y guardado el esquema, puede crear un nuevo conjunto de datos basado en ese esquema. Los siguientes tutoriales explican el proceso de creación de un nuevo conjunto de datos en la interfaz de usuario o la API:

* [Crear un conjunto de datos en la interfaz de usuario](../catalog/datasets/user-guide.md#create)  (siga el flujo de trabajo para usar un esquema existente)
* [Creación de un conjunto de datos en la API](../catalog/datasets/create.md)

Una vez creado el conjunto de datos, puede encontrarlo en la interfaz de usuario de la plataforma dentro del espacio de trabajo **[!UICONTROL Datasets]**.

![](images/data-preparation/dataset-location.png)

#### Añadir campos de identidad al conjunto de datos

Si está trayendo datos de [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] u otra fuente externa, tiene la opción de configurar un campo de esquema como campo de identidad. Para definir un campo de esquema como un campo de identidad, vista la sección sobre la configuración de campos de identidad dentro del [tutorial de interfaz de usuario](../xdm/tutorials/create-schema-ui.md#identity-field) o [tutorial de API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) para crear un esquema.

Si va a ingerir datos de un archivo CSV local, puede pasar a la siguiente sección sobre [asignación e ingesta de datos](#ingest).

#### Asignar y transferir datos {#ingest}

Después de crear un esquema y un conjunto de datos de CEE, puede asignar inicios a las tablas de datos en el esquema e ingerirlos en la plataforma. Consulte el tutorial sobre [asignación de un archivo CSV a un esquema XDM](../ingestion/tutorials/map-a-csv-file.md) para ver los pasos para realizar esto en la interfaz de usuario. Puede utilizar el siguiente [archivo JSON de muestra](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para probar el proceso de ingestión antes de utilizar sus propios datos.

Una vez que se ha rellenado un conjunto de datos, se puede utilizar el mismo conjunto de datos para ingestar archivos de datos adicionales.

Si los datos se almacenan en una aplicación de terceros admitida, también puede crear un [conector de origen](../sources/home.md) para ingerir los datos de eventos de mercadotecnia en [!DNL Platform] en tiempo real.

## Pasos siguientes {#next-steps}

Este documento proporciona una guía general sobre cómo preparar sus datos para su uso en [!DNL Intelligent Services]. Si necesita asesoramiento adicional en función de su caso de uso, póngase en contacto con la asistencia de consultoría de Adobe.

Una vez que haya completado correctamente un conjunto de datos con los datos de experiencia del cliente, puede utilizar [!DNL Intelligent Services] para generar perspectivas. Consulte los siguientes documentos para empezar:

* [Descripción general de Attribution AI](./attribution-ai/overview.md)
* [Información general sobre Customer AI ](./customer-ai/overview.md)
