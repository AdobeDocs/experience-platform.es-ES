---
description: Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/Destinations`.
title: Operaciones de extremo de la API de destinos
exl-id: 96755e9d-be62-432f-b985-91330575b395
source-git-commit: 75399d2fbe111a296479f8d3404d43c6ba0d50b5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Operaciones de API de extremo de destinos {#destination-configuration}

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/destinations`

En esta página se enumeran y describen todas las operaciones de API que puede realizar mediante la `/authoring/destinations` extremo de API. Para obtener una descripción de la funcionalidad admitida por este extremo, lea [configuración de destino](./destination-configuration.md).

## Introducción a las operaciones de API de destino {#get-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Crear configuración para un destino de flujo continuo {#create}

Puede crear una nueva configuración de destino realizando una solicitud de POST al `/authoring/destinations` punto final.

**Formato de API**

```http
POST /authoring/destinations
```

**Solicitud**

La siguiente solicitud crea una nueva configuración de destino de flujo continuo, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros para los destinos de flujo continuo aceptados por el `/authoring/destinations` punto final. Tenga en cuenta que no es necesario agregar todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Indica el título del destino en el catálogo de Experience Platform |
| `description` | Cadena | Proporcione una descripción que el Adobe utilizará en el catálogo de destinos del Experience Platform para su tarjeta de destino. Apunte a no más de 4-5 frases. |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Uso `TEST` la primera vez que configure el destino. |
| `customerAuthenticationConfigurations` | Cadena | Indica la configuración utilizada para autenticar a los clientes Experience Platform en el servidor. Consulte `authType` abajo para los valores aceptados. |
| `customerAuthenticationConfigurations.authType` | Cadena | Los valores admitidos para los destinos de flujo continuo son: <ul><li>`OAUTH2`</li><li>`BEARER`</li></ul> Los valores admitidos para destinos basados en archivos son: <ul><li>`S3`</li><li>`AZURE_CONNECTION_STRING`</li><li>`AZURE_SERVICE_PRINCIPAL`</li><li>`SFTP_WITH_SSH_KEY`</li><li>`SFTP_WITH_PASSWORD`</li></ul> |
| `customerDataFields.name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. |
| `customerDataFields.type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer` |
| `customerDataFields.title` | Cadena | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario del Experience Platform |
| `customerDataFields.description` | Cadena | Proporcione una descripción para el campo personalizado. |
| `customerDataFields.isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. |
| `customerDataFields.enum` | Cadena | Representa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `customerDataFields.pattern` | Cadena | Aplica un patrón para el campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números o guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |
| `uiAttributes.documentationLink` | Cadena | Se refiere a la página de documentación de la [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Uso `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe usar `https://www.adobe.com/go/destinations-moviestar-en`. Tenga en cuenta que este vínculo solo funciona después de que el Adobe establezca el destino en vivo y la documentación se publique. |
| `uiAttributes.category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, lea [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `uiAttributes.connectionType` | Cadena | `Server-to-server` actualmente es la única opción disponible. |
| `uiAttributes.frequency` | Cadena | `Streaming` actualmente es la única opción disponible. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica si el destino acepta atributos de perfil estándar. Normalmente, estos atributos se resaltan en la documentación de nuestros socios. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica si los clientes pueden configurar áreas de nombres personalizadas en el destino. |
| `identityNamespaces.externalId.transformation` | Cadena | _No se muestra en la configuración de ejemplo_. Se utiliza, por ejemplo, cuando la variable [!DNL Platform] El cliente tiene direcciones de correo electrónico simples como atributo y la plataforma solo acepta correos electrónicos con hash. Aquí es donde proporcionaría la transformación que debe aplicarse (por ejemplo, transformar el correo electrónico a minúsculas y luego a hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Se utiliza para casos en los que la plataforma acepta [áreas de nombres de identidad estándar](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (por ejemplo, IDFA), para que pueda restringir a los usuarios de Platform a que solo seleccionen estas áreas de nombres de identidad. <br> Cuando utilice `acceptedGlobalNamespaces`, puede usar `"requiredTransformation":"sha256(lower($))"` a direcciones de correo electrónico en minúsculas y hash o números de teléfono. |
| `destinationDelivery.authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en su sistema mediante un nombre de usuario y una contraseña, un token al portador u otro método de autenticación. Por ejemplo, puede seleccionar esta opción si también selecciona `authType: OAUTH2` o `authType:BEARER` en `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable [Credenciales](./credentials-configuration-api.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | Cadena | La variable `instanceId` del [plantilla de servidor de destino](./destination-server-api.md) para este destino. |
| `backfillHistoricalProfileData` | Booleano | Controla si los datos del perfil histórico se exportan cuando los segmentos se activan en el destino. <br> <ul><li> `true`: [!DNL Platform] envía los perfiles de usuario históricos que cumplen los requisitos para el segmento antes de que se active el segmento. </li><li> `false`: [!DNL Platform] solo incluye perfiles de usuario que cumplen los requisitos para el segmento una vez activado el segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla si el usuario introduce el ID de asignación de segmentos en el flujo de trabajo de activación de destino. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el ID de segmento del Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla si el id. de asignación de segmentos en el flujo de trabajo de activación de destino es el nombre del segmento del Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | La variable `instanceId` del [plantilla de metadatos de audiencia](./audience-metadata-api.md) para este destino. |
| `schemaConfig.profileFields` | Matriz | Al agregar una `profileFields` como se muestra en la configuración anterior, los usuarios tendrán la opción de asignar atributos de Experience Platform a los atributos predefinidos en el lado del destino. |
| `schemaConfig.profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en el lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `schemaConfig.segmentRequired` | Booleano | Utilice siempre `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad desde el Experience Platform al esquema deseado. |
| `aggregation.aggregationType` | - | Seleccione `BEST_EFFORT` o `CONFIGURABLE_AGGREGATION`. La configuración de ejemplo anterior incluye `BEST_EFFORT` agregación. Para ver un ejemplo de `CONFIGURABLE_AGGREGATION`, consulte la configuración de ejemplo en la [configuración de destino](./destination-configuration.md#example-configuration) documento. Los parámetros relevantes para la agregación configurable se documentan a continuación en esta tabla. |
| `aggregation.bestEffortAggregation.maxUsersPerRequest` | Número entero | El Experience Platform puede acumular varios perfiles exportados en una sola llamada HTTP. Especifique el número máximo de perfiles que su extremo debe recibir en una sola llamada HTTP. Tenga en cuenta que esta es una agregación de mejor esfuerzo. Por ejemplo, si especifica el valor 100, Platform podría enviar cualquier número de perfiles menores que 100 en una llamada. <br> Si el servidor no acepta varios usuarios por solicitud, establezca este valor en 1. |
| `aggregation.bestEffortAggregation.splitUserById` | Booleano | Utilice este indicador si la llamada al destino debe dividirse por identidad. Establezca este indicador como `true` si el servidor solo acepta una identidad por llamada, para un área de nombres determinada. |
| `aggregation.configurableAggregation.splitUserById` | Booleano | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Utilice este indicador si la llamada al destino debe dividirse por identidad. Establezca este indicador como `true` si el servidor solo acepta una identidad por llamada, para un área de nombres determinada. |
| `aggregation.configurableAggregation.maxBatchAgeInSecs` | Número entero | <ul><li>*Valor mínimo: 1800*</li><li>*Valor máximo: 3600*</li><li>Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Configure un valor entre los valores mínimos y máximos aceptados. Junto con `maxNumEventsInBatch`, este parámetro determina cuánto tiempo debe esperar el Experience Platform hasta enviar una llamada de API al extremo. <br> Por ejemplo, si utiliza el valor máximo para ambos parámetros, el Experience Platform esperará 3600 segundos O hasta que haya 10 000 perfiles cualificados antes de realizar la llamada de API, lo que suceda primero. </li></ul> |
| `aggregation.configurableAggregation.maxNumEventsInBatch` | Número entero | <ul><li>*Valor mínimo: 1000*</li><li>*Valor máximo: 10000*</li><li>Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Configure un valor entre los valores mínimos y máximos aceptados. Para obtener una descripción de este parámetro, consulte `maxBatchAgeInSecs` justo arriba.</li></ul> |
| `aggregation.configurableAggregation.aggregationKey` | Booleano | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Permite acumular los perfiles exportados asignados al destino según los parámetros siguientes: <br> <ul><li>ID de segmento</li><li> estado del segmento </li><li> área de nombres de identidad </li></ul> |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Configure esto como `true` si desea agrupar perfiles exportados a su destino por ID de segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Debe configurar ambas `includeSegmentId:true` y `includeSegmentStatus:true` si desea agrupar perfiles exportados a su destino por ID de segmento Y estado de segmento. |
| `aggregation.configurableAggregation.aggregationKey.includeIdentity` | Booleano | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Configure esto como `true` si desea agrupar perfiles exportados al destino por el área de nombres de identidad. |
| `aggregation.configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Utilice este parámetro para especificar si desea que los perfiles exportados se agreguen en grupos de una sola identidad (GAID, IDFA, números de teléfono, correo electrónico, etc.). |
| `aggregation.configurableAggregation.aggregationKey.groups` | Cadena | Consulte parámetro en configuración de ejemplo [here](./destination-configuration.md#example-configuration). Cree listas de grupos de identidad si desea agrupar perfiles exportados a su destino por grupos de área de nombres de identidad. Por ejemplo, puede combinar perfiles que contengan los identificadores móviles IDFA y GAID en una llamada a su destino y correos electrónicos en otra utilizando la configuración del ejemplo. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de destino recién creada.

## Crear configuración para un destino basado en archivos {#create-file-based}

Puede crear una nueva configuración de destino realizando una solicitud de POST al `/authoring/destinations` punto final.

**Formato de API**

```http
POST /authoring/destinations
```

**Solicitud**

La siguiente solicitud crea un nuevo [!DNL Amazon S3] configuración de destino basada en archivos, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros para los destinos basados en archivos aceptados por el `/authoring/destinations` punto final. Tenga en cuenta que no es necesario agregar todos los parámetros en la llamada de y que la plantilla se puede personalizar, según los requisitos de la API.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
        "name": "S3 Destination with CSV Options",
        "description": "S3 Destination with CSV Options",
        "releaseNotes": "S3 Destination with CSV Options",
        "status": "TEST",
        "customerAuthenticationConfigurations": [
            {
                "authType": "S3"
            }
        ],
        "customerEncryptionConfigurations": [
            {
                "encryptionAlgo": ""
            }
        ],
        "customerDataFields": [
            {
                "name": "bucket",
                "title": "Select S3 Bucket",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "path",
                "title": "S3 path",
                "description": "Select S3 Bucket",
                "type": "string",
                "isRequired": true,
                "pattern": "^[A-Za-z]+$",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "sep",
                "title": "Select separator for each field and value",
                "description": "Select for each field and value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "encoding",
                "title": "Specify encoding (charset) of saved CSV files",
                "description": "Select encoding of csv files",
                "type": "string",
                "enum": ["UTF-8", "UTF-16"],
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quote",
                "title": "Select a single character used for escaping quoted values",
                "description": "Select single charachter for escaping quoted values",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "quoteAll",
                "title": "Quote All",
                "description": "Select flag for escaping quoted values",
                "type": "string",
                "enum" : ["true","false"],
                "default": "true",
                "isRequired": true,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "escape",
                "title": "Select a single character used for escaping quotes",
                "description": "Select a single character used for escaping quotes inside an already quoted value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "escapeQuotes",
                "title": "Escape quotes",
                "description": "A flag indicating whether values containing quotes should always be enclosed in quotes",
                "type": "string",
                "enum" : ["true","false"],
                "isRequired": false,
                "default": "true",
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "header",
                "title": "header",
                "description": "Writes the names of columns as the first line.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "ignoreLeadingWhiteSpace",
                "title": "Ignore leading white space",
                "description": "A flag indicating whether or not leading whitespaces from values being written should be skipped.",
                "type": "string",
                "isRequired": false,
                "enum" : ["true","false"],
                "readOnly": false,
                "default": "true",
                "hidden": false
            },
            {
                "name": "nullValue",
                "title": "Select the string representation of a null value",
                "description": "Sets the string representation of a null value. ",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "dateFormat",
                "title": "Date format",
                "description": "Select the string that indicates a date format. ",
                "type": "string",
                "default": "yyyy-MM-dd",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
             {
                "name": "charToEscapeQuoteEscaping",
                "title": "Char to escape quote escaping",
                "description": "Sets a single character used for escaping the escape for the quote character",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "hidden": false
            },
            {
                "name": "emptyValue",
                "title": "Select the string representation of an empty value",
                "description": "Select the string representation of an empty value",
                "type": "string",
                "isRequired": false,
                "readOnly": false,
                "default": "",
                "hidden": false
            },
            {
                "name": "compression",
                "title": "Select compression",
                "description": "Select compressiont",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "enum" : ["SNAPPY","GZIP","DEFLATE", "NONE"]
            },
            {
                "name": "fileType",
                "title": "Select a fileType",
                "description": "Select fileType",
                "type": "string",
                "isRequired": true,
                "readOnly": false,
                "hidden": false,
                "enum" :["csv", "json", "parquet"],
                "default" : "csv"
            }
        ],
        "uiAttributes": {
            "documentationLink": "https://www.adobe.io/apis/experienceplatform.html",
            "category": "S3",
            "iconUrl": "https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
            "connectionType": "S3",
            "flowRunsSupported": true,
            "monitoringSupported": true,
            "frequency": "Batch"
        },
        "destinationDelivery": [
            {
                "deliveryMatchers" : [
                    {
                        "type" : "SOURCE",
                        "value" : [
                            "batch"
                        ]
                    }
                ],
                "authenticationRule": "CUSTOMER_AUTHENTICATION",
                "destinationServerId": "{{destinationServerId}}"
            }
        ],
        "schemaConfig" : {
            "profileRequired" : true,
            "segmentRequired" : true,
            "identityRequired" : true
        },
        "batchConfig":{
            "allowMandatoryFieldSelection": true,
            "allowJoinKeyFieldSelection": true,
            "defaultExportMode": "DAILY_FULL_EXPORT",
            "allowedExportMode":[
                "DAILY_FULL_EXPORT",
                "FIRST_FULL_THEN_INCREMENTAL"
            ],
            "allowedScheduleFrequency":[
                "DAILY",
                "EVERY_3_HOURS",
                "EVERY_6_HOURS",
                "EVERY_8_HOURS",
                "EVERY_12_HOURS",
                "ONCE",
                "EVERY_HOUR"
            ],
            "defaultFrequency":"DAILY",
            "defaultStartTime":"00:00"
        },
        "backfillHistoricalProfileData": true
    }
```

Para obtener descripciones detalladas de todos los parámetros anteriores, consulte [configuración de destino basada en archivos](file-based-destination-configuration.md).

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de destino recién creada.

## Enumerar configuraciones de destino {#retrieve-list}

Puede recuperar una lista de todas las configuraciones de destino para su organización IMS realizando una solicitud de GET al `/authoring/destinations` punto final.

**Formato de API**


```http
GET /authoring/destinations
```

**Solicitud**

La siguiente solicitud recuperará la lista de configuraciones de destino a la que tiene acceso, según la configuración de la organización y el entorno limitado de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de configuraciones de destino a las que tiene acceso, según el ID de organización de IMS y el nombre del simulador de pruebas que ha utilizado. One `instanceId` corresponde a la plantilla de un destino. La respuesta se trunca para su brevedad.

```json
{
   "items":[
      {
         "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
         "createdDate":"2020-10-28T06:14:09.784471Z",
         "lastModifiedDate":"2021-06-28T06:14:09.784471Z",
         "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
         "sandboxName":"prod",
         "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
         "name":"Moviestar",
         "description":"Moviestar is a fictional destination, used for this example.",
         "status":"TEST",
         "customerAuthenticationConfigurations":[
            {
               "authType":"BEARER"
            }
         ],
         "customerDataFields":[
            {
               "name":"endpointsInstance",
               "type":"string",
               "title":"Select Endpoint",
               "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
               "isRequired":true,
               "enum":[
                  "US",
                  "EU",
                  "APAC",
                  "NZ"
               ]
            },
            {
               "name":"customerID",
               "type":"string",
               "title":"Moviestar Customer ID",
               "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
               "isRequired":true,
               "pattern":"^[A-Za-z]+$"
            }
         ],
         "uiAttributes":{
            "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
            "category":"mobile",
            "connectionType":"Server-to-server",
            "frequency":"Streaming"
         },
         "identityNamespaces":{
            "external_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true,
               "acceptedGlobalNamespaces":{
                  "Email":{
                     
                  }
               }
            },
            "another_id":{
               "acceptsAttributes":true,
               "acceptsCustomNamespaces":true
            }
         },
         "segmentMappingConfig":{
            "mapExperiencePlatformSegmentName":false,
            "mapExperiencePlatformSegmentId":false,
            "mapUserInput":false,
            "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
         },
         "schemaConfig":{
            "profileFields":[
               {
                  "name":"a_custom_attribute",
                  "title":"a_custom_attribute",
                  "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
                  "type":"string",
                  "isRequired":false,
                  "readOnly":false,
                  "hidden":false
               }
            ],
            "profileRequired":true,
            "segmentRequired":true,
            "identityRequired":true
         },
         "aggregation":{
            "aggregationType":"BEST_EFFORT",
            "bestEffortAggregation":{
               "maxUsersPerRequest":10,
               "splitUserById":false
            }
         },
         "destinationDelivery":[
            {
               "authenticationRule":"CUSTOMER_AUTHENTICATION",
               "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
            }
         ],
         "destConfigId":"410631b8-f6b3-4b7c-82da-7998aa3f327c",
         "backfillHistoricalProfileData":true
      }
   ]
}
    
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Indica el título del destino en el catálogo de Experience Platform. |
| `description` | Cadena | Proporcione una descripción que el Adobe utilizará en el catálogo de destinos del Experience Platform para su tarjeta de destino. Apunte a no más de 4-5 frases. |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Uso `TEST` la primera vez que configure el destino. |
| `customerAuthenticationConfigurations` | Cadena | Indica la configuración utilizada para autenticar a los clientes Experience Platform en el servidor. Consulte `authType` abajo para los valores aceptados. |
| `customerAuthenticationConfigurations.authType` | Cadena | Los valores aceptados son `OAUTH2, BEARER`. |
| `customerDataFields.name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. |
| `customerDataFields.type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer` |
| `customerDataFields.title` | Cadena | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario del Experience Platform |
| `customerDataFields.description` | Cadena | Proporcione una descripción para el campo personalizado. |
| `customerDataFields.isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. |
| `customerDataFields.enum` | Cadena | Representa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `customerDataFields.pattern` | Cadena | Aplica un patrón para el campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números o guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |
| `uiAttributes.documentationLink` | Cadena | Se refiere a la página de documentación de la [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Uso `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe usar `https://www.adobe.com/go/destinations-moviestar-en`. Tenga en cuenta que este vínculo solo funciona después de que el Adobe establezca el destino en vivo y la documentación se publique. |
| `uiAttributes.category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, lea [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments` |
| `uiAttributes.connectionType` | Cadena | `Server-to-server` actualmente es la única opción disponible. |
| `uiAttributes.frequency` | Cadena | `Streaming` actualmente es la única opción disponible. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica si el destino acepta atributos de perfil estándar. Normalmente, estos atributos se resaltan en la documentación de nuestros socios. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica si los clientes pueden configurar áreas de nombres personalizadas en el destino. Más información sobre [áreas de nombres personalizadas](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#manage-namespaces) en Adobe Experience Platform. |
| `identityNamespaces.externalId.transformation` | Cadena | _No se muestra en la configuración de ejemplo_. Se utiliza, por ejemplo, cuando la variable [!DNL Platform] El cliente tiene direcciones de correo electrónico simples como atributo y la plataforma solo acepta correos electrónicos con hash. Aquí es donde proporcionaría la transformación que debe aplicarse (por ejemplo, transformar el correo electrónico a minúsculas y luego a hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Se utiliza para casos en los que la plataforma acepta [áreas de nombres de identidad estándar](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#standard-namespaces) (por ejemplo, IDFA), para que pueda restringir a los usuarios de Platform a que solo seleccionen estas áreas de nombres de identidad. |
| `destinationDelivery.authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en su sistema mediante un nombre de usuario y una contraseña, un token al portador u otro método de autenticación. Por ejemplo, puede seleccionar esta opción si también selecciona `authType: OAUTH2` o `authType:BEARER` en `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable [Credenciales](./authentication-configuration.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | Cadena | La variable `instanceId` del [plantilla de servidor de destino](./destination-server-api.md) para este destino. |
| `destConfigId` | Cadena | Este campo se genera automáticamente y no requiere la introducción de datos. |
| `backfillHistoricalProfileData` | Booleano | Controla si los datos del perfil histórico se exportan cuando los segmentos se activan en el destino. <br> <ul><li> `true`: [!DNL Platform] envía los perfiles de usuario históricos que cumplen los requisitos para el segmento antes de que se active el segmento. </li><li> `false`: [!DNL Platform] solo incluye perfiles de usuario que cumplen los requisitos para el segmento una vez activado el segmento. </li></ul> |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla si el usuario introduce el ID de asignación de segmentos en el flujo de trabajo de activación de destino. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el ID de segmento del Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla si el id. de asignación de segmentos en el flujo de trabajo de activación de destino es el nombre del segmento del Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | La variable `instanceId` del [plantilla de metadatos de audiencia](./audience-metadata-management.md) para este destino. Para configurar una plantilla de metadatos de audiencia, lea la [referencia de API de metadatos de audiencia](./audience-metadata-api.md). |

{style=&quot;table-layout:auto&quot;}

## Actualizar una configuración de destino existente {#update}

Puede actualizar una configuración de destino existente realizando una solicitud de PUT al `/authoring/destinations` y proporcionando el ID de instancia de la configuración de destino que desea actualizar. En el cuerpo de la llamada a , proporcione la configuración de destino actualizada.

**Formato de API**


```http
PUT /authoring/destinations/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de destino que desea actualizar. |

**Solicitud**

La siguiente solicitud actualiza una configuración de destino existente, configurada por los parámetros proporcionados en la carga útil. En la llamada de ejemplo siguiente, se actualiza la configuración [creado anteriormente](./destination-configuration-api.md#create) para aceptar ahora identificadores de correo electrónico con hash, GAID e IDFA como áreas de nombres de identidad.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-04-28T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```

## Recuperar una configuración de destino específica {#get}

Puede recuperar información detallada sobre una configuración de destino específica realizando una solicitud de GET al `/authoring/destinations` y proporcionando el ID de instancia de la configuración de destino que desea recuperar.

**Formato de API**


```http
GET /authoring/destinations/{INSTANCE_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{INSTANCE_ID}` | El ID de la configuración de destino que desea recuperar. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la configuración de destino especificada.

```json
{
   "instanceId":"b0780cb5-2bb7-4409-bf2c-c625ca818588",
   "createdDate":"2020-10-28T06:14:09.784471Z",
   "lastModifiedDate":"2021-06-04T06:14:09.784471Z",
   "imsOrg":"AC3428435BF324E90A49402A@AdobeOrg",
   "sandboxName":"prod",
   "sandboxId":"r5g6660-c5da-11e9-93d4-6d5fc3a66a8e",
   "name":"Moviestar",
   "description":"Moviestar is a fictional destination, used for this example.",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ],
   "customerDataFields":[
      {
         "name":"endpointsInstance",
         "type":"string",
         "title":"Select Endpoint",
         "description":"Moviestar manages several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
         "isRequired":true,
         "enum":[
            "US",
            "EU",
            "APAC",
            "NZ"
         ]
      },
      {
         "name":"customerID",
         "type":"string",
         "title":"Moviestar Customer ID",
         "description":"Your customer ID in the Moviestar destination (e.g. abcdef).",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$"
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-moviestar-en",
      "category":"mobile",
      "connectionType":"Server-to-server",
      "frequency":"Streaming"
   },
   "identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
               
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "gaid":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "GAID":{
               
            }
         }
      },
      "idfa":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "IDFA":{
               
            }
         }
      },
      "email_lc_sha256":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation":"sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation":"sha256(lower($))"
            },
            "Email_LC_SHA256":{
               
            }
         }
      }
   },
   "segmentMappingConfig":{
      "mapExperiencePlatformSegmentName":false,
      "mapExperiencePlatformSegmentId":false,
      "mapUserInput":false,
      "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
   "schemaConfig":{
      "profileFields":[
         {
            "name":"a_custom_attribute",
            "title":"a_custom_attribute",
            "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the phoneNumber value in Experience Platform could be phoneNo on your side.",
            "type":"string",
            "isRequired":false,
            "readOnly":false,
            "hidden":false
         }
      ],
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "aggregation":{
      "aggregationType":"BEST_EFFORT",
      "bestEffortAggregation":{
         "maxUsersPerRequest":10,
         "splitUserById":false
      }
   },
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"9c77000a-4559-40ae-9119-a04324a3ecd4"
      }
   ],
   "backfillHistoricalProfileData":true
}
```


## Eliminar una configuración de destino específica {#delete}

Puede eliminar la configuración de destino especificada realizando una solicitud de DELETE al `/authoring/destinations` y proporcionando el ID de la configuración de destino que desea eliminar en la ruta de solicitud.

**Formato de API**

```http
DELETE /authoring/destinations/{INSTANCE_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{INSTANCE_ID}` | La variable `id` de la configuración de destino que desea eliminar. |

**Solicitud**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/destinations/b0780cb5-2bb7-4409-bf2c-c625ca818588 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con una respuesta HTTP vacía.

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo configurar su destino utilizando la variable `/authoring/destinations` extremo de API. Lectura [cómo usar Destination SDK para configurar el destino](./configure-destination-instructions.md) para comprender dónde encaja este paso en el proceso de configuración de su destino.
