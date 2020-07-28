---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Preparación de datos para su uso en Servicios inteligentes
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 1%

---


# Preparación de datos para su uso en Servicios inteligentes

Para que los servicios inteligentes puedan descubrir perspectivas a partir de los datos de eventos de marketing, los datos deben enriquecirse y mantenerse semánticamente en una estructura estándar. Los servicios inteligentes aprovechan los esquemas del modelo de datos de experiencia (XDM) para lograr esto. Específicamente, todos los conjuntos de datos que se utilizan en Servicios inteligentes deben cumplir el esquema XDM de **Consumer ExperienceEvent (CEE)** .

Este documento proporciona una guía general sobre cómo asignar los datos de eventos de marketing de varios canales a este esquema, esbozando información sobre los campos importantes dentro del esquema para ayudarle a determinar cómo asignar los datos de manera efectiva a su estructura.

## Resumen de flujo de trabajo

El proceso de preparación varía en función de si los datos se almacenan en Adobe Experience Platform o externamente. En esta sección se resumen los pasos necesarios que debe seguir, en cualquier caso.

### Preparación de datos externos

Si los datos se almacenan fuera de [!DNL Experience Platform], siga los pasos a continuación:

1. Póngase en contacto con los servicios de consultoría de Adobe para solicitar las credenciales de acceso para un contenedor de Almacenamiento de blob de Azure dedicado.
1. Con las credenciales de acceso, cargue los datos en el contenedor Blob.
1. Trabaje con los servicios de consultoría de Adobe para obtener los datos asignados al esquema [](#cee-schema) Consumer ExperienceEvent e ingeridos en Servicios inteligentes.

### [!DNL Experience Platform] preparación de datos

Si los datos ya están almacenados en [!DNL Platform], siga los pasos a continuación:

1. Revise la estructura del esquema [](#cee-schema) Consumer ExperienceEvent y determine si los datos se pueden asignar a sus campos.
1. Póngase en contacto con los servicios de consultoría de Adobe para ayudarle a asignar sus datos al esquema y a ingerirlos en los servicios inteligentes, o [siga los pasos de esta guía](#mapping) si desea asignar los datos usted mismo.

## Explicación del esquema de CEE {#cee-schema}

El esquema Consumer ExperienceEvent describe el comportamiento de una persona en relación con eventos de marketing digital (web o móvil), así como con la actividad comercial en línea o sin conexión. El uso de este esquema es necesario para Servicios Inteligentes debido a sus campos (columnas) semánticamente bien definidos, evitando nombres desconocidos que de otra manera harían que los datos fueran menos claros.

El esquema CEE, al igual que todos los esquemas de ExperienceEvent de XDM, captura el estado del sistema basado en series temporales cuando se produjo un evento (o conjunto de eventos), incluido el momento y la identidad del sujeto involucrado. Los Eventos de experiencias son registros de hechos de lo que ocurrió, y por lo tanto son inmutables y representan lo que pasó sin agregación ni interpretación.

Los servicios inteligentes utilizan varios campos clave dentro de este esquema para generar perspectivas a partir de los datos de sus eventos de marketing, todos los cuales se pueden encontrar en el nivel raíz y se expanden para mostrar los subcampos requeridos.

![](./images/data-preparation/schema-expansion.gif)

Al igual que todos los esquemas XDM, la mezcla CEE es extensible. En otras palabras, se pueden agregar campos adicionales a la mezcla CEE y, si es necesario, se pueden incluir variaciones diferentes en varios esquemas.

Puede encontrarse un ejemplo completo de la mezcla en el repositorio [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)público y debe utilizarse como referencia para los campos clave descritos en la sección siguiente.

## Campos clave

Existen varios campos clave dentro de la mezcla CEE que deben utilizarse para que los servicios inteligentes generen perspectivas útiles. Esta sección describe el caso de uso y los datos esperados para estos campos, y proporciona vínculos a la documentación de referencia para obtener más ejemplos.

### Campos obligatorios

Aunque se recomienda encarecidamente el uso de todos los campos clave, hay dos campos **necesarios** para que los servicios inteligentes funcionen:

* [Campo de identidad principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:canal](#channel) (obligatorio solo para Attribution AI)

#### Identidad primaria {#identity}

Uno de los campos de su esquema debe configurarse como un campo de identidad principal, lo que permite a los servicios inteligentes vincular cada instancia de datos de series temporales a una persona individual.

Debe determinar el mejor campo para utilizarlo como identidad principal en función de la fuente y la naturaleza de los datos. Un campo de identidad debe incluir una Área de nombres **de** identidad que indique el tipo de datos de identidad que el campo espera como valor. Algunos valores de Área de nombres válidos son:

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (para ID de Adobe Audience Manager)
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

**esquema de ejemplo**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Para obtener información completa sobre cada uno de los subcampos obligatorios para `xdm:channel`, consulte las especificaciones del esquema [de canal de](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) experiencia. Para ver algunos ejemplos de asignaciones, consulte la [tabla siguiente](#example-channels).

##### Asignaciones de canal de ejemplo {#example-channels}

En la tabla siguiente se proporcionan algunos ejemplos de canales de marketing asignados al `xdm:channel` esquema:

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Búsqueda de pago | https:/<span>/ns.adobe.com/xdm/canal-types/search | pagado | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/canal-types/social | ganado | clicks |
| Mostrar | https:/<span>/ns.adobe.com/xdm/canal-types/display | pagado | clicks |
| Correo electrónico | https:/<span>/ns.adobe.com/xdm/canal-types/email | pagado | clicks |
| Remitente del reenvío interno | https:/<span>/ns.adobe.com/xdm/canal-types/direct | propiedad | clicks |
| Visualización de visualizaciones | https:/<span>/ns.adobe.com/xdm/canal-types/display | pagado | impresiones |
| Redirección de código QR | https:/<span>/ns.adobe.com/xdm/canal-types/direct | propiedad | clicks |
| Dispositivo móvil | https:/<span>/ns.adobe.com/xdm/canal-types/mobile | propiedad | clicks |

### Campos recomendados

El resto de los campos clave se describen en esta sección. Aunque estos campos no son necesariamente necesarios para que los servicios inteligentes funcionen, se recomienda encarecidamente que utilice tantos como sea posible para obtener perspectivas más enriquecidas.

#### xdm:productListItems

Este campo es una matriz de artículos que representan los productos seleccionados por un cliente, incluidos el SKU del producto, el nombre, el precio y la cantidad.

![](./images/data-preparation/productListItems.png)

**esquema de ejemplo**

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

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:productListItems`, consulte las especificaciones del esquema [de detalles](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) comerciales.

#### xdm:commerce

Este campo contiene información específica sobre el comercio acerca de ExperienceEvent, incluido el número de orden de compra y la información de pago.

![](./images/data-preparation/commerce.png)

**esquema de ejemplo**

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

Para obtener información completa sobre cada uno de los subcampos requeridos para `xdm:commerce`, consulte las especificaciones del esquema [de detalles](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) comerciales.

#### xdm:web

Este campo representa los detalles web relacionados con ExperienceEvent, como la interacción, los detalles de la página y el remitente del reenvío.

![](./images/data-preparation/web.png)

**esquema de ejemplo**

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

Para obtener información completa sobre cada uno de los subcampos obligatorios para `xdm:productListItems`, consulte las especificaciones del esquema [de detalles web de](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) ExperienceEvent.

#### xdm:marketing

Este campo contiene información relacionada con actividades de marketing que están activas con el touchpoint.

![](./images/data-preparation/marketing.png)

**esquema de ejemplo**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Para obtener información completa acerca de cada uno de los subcampos requeridos para `xdm:productListItems`, consulte la especificación de [chechma](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) de mercadotecnia.

## Asignación e ingesta de datos (#mapping)

Una vez que haya determinado si los datos de eventos de marketing se pueden asignar al esquema CEE, el siguiente paso es determinar qué datos se van a incluir en Servicios inteligentes. Todos los datos históricos utilizados en Servicios Inteligentes deben estar dentro del período mínimo de cuatro meses de datos, más el número de días previsto como período retroactivo.

Después de decidir el rango de datos que desea enviar, póngase en contacto con los servicios de consultoría de Adobe para ayudarle a asignar los datos al esquema y a ingerirlos al servicio.

Si tiene una [!DNL Adobe Experience Platform] suscripción y desea asignar e ingestar los datos usted mismo, siga los pasos descritos en la sección siguiente.

### Uso de Adobe Experience Platform

>[!NOTE]
>
>Los pasos a continuación requieren una suscripción al Experience Platform. Si no tiene acceso a Platform, vaya a la sección de pasos [](#next-steps) siguientes.

Esta sección describe el flujo de trabajo para asignar e ingerir datos en Experience Platform para su uso en Servicios inteligentes, incluidos vínculos a tutoriales para ver los pasos detallados.

#### Crear un esquema y un conjunto de datos de CEE

Cuando esté listo para el inicio de preparar sus datos para la ingestión, el primer paso es crear un nuevo esquema XDM que emplee la mezcla CEE. Los siguientes tutoriales explican el proceso de creación de un nuevo esquema en la interfaz de usuario o la API:

* [Creación de un esquema en la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)
* [Creación de un esquema en la API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Los tutoriales anteriores siguen un flujo de trabajo genérico para crear un esquema. Al elegir una clase para el esquema, debe utilizar la clase **ExperienceEvent de** XDM. Una vez seleccionada esta clase, puede agregar la mezcla CEE al esquema.

Después de agregar la mezcla CEE al esquema, puede agregar otras mezclas según sea necesario para campos adicionales dentro de los datos.

Una vez creado y guardado el esquema, puede crear un nuevo conjunto de datos basado en ese esquema. Los siguientes tutoriales explican el proceso de creación de un nuevo conjunto de datos en la interfaz de usuario o la API:

* [Crear un conjunto de datos en la interfaz de usuario](../catalog/datasets/user-guide.md#create) (siga el flujo de trabajo para usar un esquema existente)
* [Creación de un conjunto de datos en la API](../catalog/datasets/create.md)

Una vez creado el conjunto de datos, puede encontrarlo en la interfaz de usuario de Platform dentro del espacio de trabajo *[!UICONTROL Conjuntos]* de datos.

![](images/data-preparation/dataset-location.png)

#### Añadir una etiqueta de Área de nombres de identidad principal en el conjunto de datos

>[!NOTE]
>
>Las próximas versiones de Intelligent Services integrarán [Adobe Experience Platform Identity Service](../identity-service/home.md) en sus capacidades de identificación de clientes. Como tal, los pasos que se describen a continuación están sujetos a cambios.

Si está trayendo datos desde [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]u otra fuente externa, debe agregar una `primaryIdentityNameSpace` etiqueta al conjunto de datos. Esto se puede hacer haciendo una solicitud de PATCH a la API de servicio de catálogo.

Si va a ingerir datos de un archivo CSV local, puede pasar a la siguiente sección sobre [asignación e ingesta de datos](#ingest).

Antes de seguir el ejemplo de llamada de API que se muestra a continuación, consulte la sección [](../catalog/api/getting-started.md) Introducción en la guía para desarrolladores de catálogos para obtener información importante sobre los encabezados necesarios.

**Formato API**

```http
PATCH /dataSets/{DATASET_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | ID del conjunto de datos creado anteriormente. |

**Solicitud**

En función de la fuente desde la que ingrese datos, debe proporcionar los valores apropiados `primaryIdentityNamespace` y `sourceConnectorId` de etiqueta en la carga útil de la solicitud.

La siguiente solicitud agrega los valores de etiqueta adecuados para Audience Manager:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["mcid"],
          "sourceConnectorId": ["audiencemanager"],
        }
      }'
```

La siguiente solicitud agrega los valores de etiqueta adecuados para Analytics:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["aaid"],
          "sourceConnectorId": ["analytics"],
        }
      }'
```

>[!NOTE]
>
>Para obtener más información sobre cómo trabajar con Áreas de nombres de identidad en Platform, consulte la descripción general [de la Área de nombres de](../identity-service/namespaces.md)identidad.

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene el ID del conjunto de datos actualizado. Este ID debe coincidir con el enviado en la solicitud de PATCH.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### Asignar y transferir datos {#ingest}

Después de crear un esquema y un conjunto de datos de CEE, puede asignar en inicio las tablas de datos al esquema y transferir esos datos a Platform. Consulte el tutorial sobre la [asignación de un archivo CSV a un esquema](../ingestion/tutorials/map-a-csv-file.md) XDM para ver los pasos para realizar esto en la interfaz de usuario. Una vez que se ha rellenado un conjunto de datos, se puede utilizar el mismo conjunto de datos para ingestar archivos de datos adicionales.

Si los datos se almacenan en una aplicación de terceros admitida, también puede optar por crear un conector [de](../sources/home.md) origen para transferir los datos de eventos de marketing a Platform en tiempo real.

## Pasos siguientes {#next-steps}

Este documento proporciona una guía general sobre la preparación de los datos para su uso en Servicios inteligentes. Si necesita asesoramiento adicional en función de su caso de uso, póngase en contacto con la asistencia de consultoría de Adobe.

Una vez que haya rellenado correctamente un conjunto de datos con los datos de experiencia del cliente, puede utilizar Servicios inteligentes para generar perspectivas. Consulte los siguientes documentos para empezar:

* [Descripción general de Attribution AI](./attribution-ai/overview.md)
* [Información general sobre el AI del cliente](./customer-ai/overview.md)
