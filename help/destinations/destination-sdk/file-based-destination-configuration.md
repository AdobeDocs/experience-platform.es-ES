---
description: Esta configuración le permite indicar información esencial para su destino basado en archivos, como el nombre de destino, categoría, descripción, etc. Los ajustes de esta configuración también determinan cómo se autentican los usuarios de Experience Platform en el destino, cómo aparece en la interfaz de usuario de Experience Platform y las identidades que se pueden exportar al destino.
title: Opciones de configuración de destino basadas en archivos para Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 74f617afe8a0f678d43fb7b949d43cef25e78b9d
workflow-type: tm+mt
source-wordcount: '2982'
ht-degree: 4%

---

# Configuración de destino basada en archivos {#destination-configuration}

## Información general {#overview}

Esta configuración le permite indicar información esencial para su destino basado en archivos, como el nombre de destino, categoría, descripción, etc. Los ajustes de esta configuración también determinan cómo se autentican los usuarios de Experience Platform en el destino, cómo aparece en la interfaz de usuario de Experience Platform y las identidades que se pueden exportar al destino. También puede utilizar esta configuración para mostrar opciones relacionadas con el tipo de archivo, el formato de archivo o la configuración de compresión de los archivos exportados.

Esta configuración también conecta las otras configuraciones necesarias para que funcione el destino (servidor de destino y metadatos de audiencia) con esta. Lea cómo puede hacer referencia a las dos configuraciones en una [más abajo](./file-based-destination-configuration.md#connecting-all-configurations).

Puede configurar la funcionalidad descrita en este documento utilizando `/authoring/destinations` Extremo de API. Leer [Operaciones de extremo de API de destinos](./destination-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en el extremo.

## Ejemplo de configuración de destino de Amazon S3 {#batch-example-configuration}

A continuación, se muestra un ejemplo de un destino de Amazon S3 privado personalizado creado a través de la variable `/destinations` extremo de configuración.

```json
{
   "name":"S3 Destination with CSV Options",
   "description":"S3 Destination with CSV Options",
   "status":"TEST",
   "maxProfileAttributes":"2000",
   "maxIdentityAttributes":"10",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerEncryptionConfigurations":[
      
   ],
   "customerDataFields":[
      {
         "name":"bucketName",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern": "^[0-9a-zA-Z\\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\\/?)+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
   ],
   "uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"S3",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ],
   "identityNamespaces":{
      "adobe_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      },
      "mobile_id":{
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
            "name":"phoneNo",
            "title":"phoneNo",
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
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
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
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Indica el título del destino en el catálogo del Experience Platform. |
| `description` | Cadena | Proporcione una descripción para la tarjeta de destino en el catálogo de destinos de Experience Platform. Apunte a no más de 4-5 oraciones. |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Uso `TEST` al configurar el destino por primera vez. |
| `maxProfileAttributes` | Cadena | Indica el número máximo de atributos de perfil que los clientes pueden exportar al destino. El valor predeterminado es `2000`. |
| `maxIdentityAttributes` | Cadena | Indica el número máximo de áreas de nombres de identidad que los clientes pueden exportar al destino. El valor predeterminado es `10`. |

{style="table-layout:auto"}

## Configuraciones de autenticación del cliente {#customer-authentication-configurations}

Esta sección de la configuración de destinos genera el [Configurar nuevo destino](/help/destinations/ui/connect-destination.md) página de la interfaz de usuario de Experience Platform, donde los usuarios se conectan con Experience Platform a las cuentas que tienen con el .

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Dependiendo del [opción de autenticación](authentication-configuration.md##supported-authentication-types) que indique en la variable `authType` , la página del Experience Platform se genera para los usuarios de la siguiente manera:

### Autenticación de Amazon S3 {#s3}

Al configurar el tipo de autenticación de Amazon S3, los usuarios deben introducir las credenciales de S3.

![Representación de la IU con autenticación S3](assets/s3-authentication-ui.png)

### Autenticación de Azure Blob  {#blob}

Al configurar el tipo de autenticación de Azure Blob, los usuarios deben introducir la cadena de conexión.

![Representación de la IU con autenticación Blob](assets/blob-authentication-ui.png)

### SFTP con autenticación de contraseña

Al configurar el SFTP con un tipo de autenticación por contraseña, los usuarios deben introducir el nombre de usuario y la contraseña del SFTP, así como el dominio y el puerto del SFTP (el puerto predeterminado es 22).

![Representación de la interfaz de usuario con SFTP con autenticación por contraseña](assets/sftp-password-authentication-ui.png)

### SFTP con autenticación de clave SSH

Al configurar el SFTP con el tipo de autenticación de clave SSH, los usuarios deben introducir el nombre de usuario y la clave SSH del SFTP, así como el dominio y el puerto del SFTP (el puerto predeterminado es 22).

![Representación de la interfaz de usuario con SFTP con autenticación de clave SSH](assets/sftp-key-authentication-ui.png)

## Campos de datos del cliente {#customer-data-fields}

Utilice esta sección para pedir a los usuarios que rellenen campos personalizados, específicos del destino, al conectarse al destino en la interfaz de usuario de Experience Platform.

En el ejemplo siguiente, `customerDataFields` requiere que los usuarios especifiquen un nombre para el destino y proporcionen un [!DNL Amazon S3] nombre del contenedor y ruta de la carpeta, así como un tipo de compresión, formato de archivo y otras opciones de formato de archivo.

Puede acceder a las entradas de datos del cliente y utilizarlas desde los campos de datos del cliente en la creación de plantillas. Uso de la macro `{{customerData.exampleName}}`. Por ejemplo, si solicita a los usuarios que introduzcan un campo de contenedor de Amazon S3, con el nombre `bucket`, puede acceder a él en la plantilla mediante la macro `{{customerData.bucket}}`. Vea un ejemplo de cómo se utiliza un campo de datos de cliente en la [configuración del servidor de destino](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example).

```json
 "customerDataFields":[
      {
         "name":"bucket",
         "title":"Amazon S3 bucket name",
         "description":"Enter your Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Amazon S3 bucket path",
         "description":"Enter your S3 bucket path",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"sep",
         "title":"Enter a separator for each field and value",
         "description":"Enter a separator character for each field and value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"encoding",
         "title":"Specify encoding (charset) of saved CSV files",
         "description":"Select encoding of csv files",
         "type":"string",
         "enum":[
            "UTF-8",
            "UTF-16"
         ],
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quote",
         "title":"Select a single character used for escaping quoted values",
         "description":"Select single charachter for escaping quoted values",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"quoteAll",
         "title":"Escape all quoted values",
         "description":"Select whether to escape all quoted values",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "default":"true",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escape",
         "title":"Select a single character used for escaping quotes",
         "description":"Select a single character used for escaping quotes inside an already quoted value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"escapeQuotes",
         "title":"Escape quotes",
         "description":"A flag indicating whether values containing quotes should always be enclosed in quotes",
         "type":"string",
         "enum":[
            "true",
            "false"
         ],
         "isRequired":false,
         "default":"true",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"header",
         "title":"header",
         "description":"Writes the names of columns as the first line.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"ignoreLeadingWhiteSpace",
         "title":"Ignore leading white space",
         "description":"A flag indicating whether or not leading whitespaces from values being written should be skipped.",
         "type":"string",
         "isRequired":false,
         "enum":[
            "true",
            "false"
         ],
         "readOnly":false,
         "default":"true",
         "hidden":false
      },
      {
         "name":"nullValue",
         "title":"Select the string representation of a null value",
         "description":"Sets the string representation of a null value. ",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"dateFormat",
         "title":"Date format",
         "description":"Select the string that indicates a date format. ",
         "type":"string",
         "default":"yyyy-MM-dd",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"charToEscapeQuoteEscaping",
         "title":"Char to escape quote escaping",
         "description":"Sets a single character used for escaping the escape for the quote character",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"emptyValue",
         "title":"Select the string representation of an empty value",
         "description":"Select the string representation of an empty value",
         "type":"string",
         "isRequired":false,
         "readOnly":false,
         "default":"",
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Select compression",
         "description":"Select compressiont",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "enum":[
            "SNAPPY",
            "GZIP",
            "DEFLATE",
            "NONE"
         ]
      },
      {
         "name":"fileType",
         "title":"Select a fileType",
         "description":"Select fileType",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false,
         "enum":[
            "csv",
            "json",
            "parquet"
         ],
         "default":"csv"
      }
```

>[!TIP]
>
>Todas las configuraciones de formato de archivo enumeradas en el ejemplo anterior se describen detalladamente en la [configuración de formato de archivo](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) sección.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. |
| `title` | Cadena | Indica el nombre del campo tal como lo ven los clientes en la interfaz de usuario del Experience Platform. |
| `description` | Cadena | Proporcione una descripción para el campo personalizado. |
| `type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer`. |
| `isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. |
| `pattern` | Cadena | Aplica un motivo al campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números ni guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |
| `enum` | Cadena | Procesa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `default` | Cadena | Define el valor predeterminado a partir de un `enum` lista. |

{style="table-layout:auto"}

## Atributos de IU {#ui-attributes}

Esta sección hace referencia a los elementos de la interfaz de usuario de la configuración anterior que el Adobe debe utilizar para su destino en la interfaz de usuario de Adobe Experience Platform.

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "iconUrl":"https://dc5tqsrhldvnl.cloudfront.net/2/90048/da276e30c730ce6cd666c8ca78360df21.png",
      "connectionType":"S3",
      "flowRunsSupported":true,
      "monitoringSupported":true,
      "frequency":"Batch"
   }
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `documentationLink` | Cadena | Hace referencia a la página de documentación de la [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Uso `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe utilizar `http://www.adobe.com/go/destinations-moviestar-en`. Tenga en cuenta que este vínculo solo funciona después de que el Adobe active el destino y se publique la documentación. |
| `category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, consulte [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Cadena | Dirección URL donde alojó el icono que se mostrará en la tarjeta del catálogo de destinos. Esto no es necesario para integraciones personalizadas privadas. Para las configuraciones de productos, debe compartir un icono con el equipo de Adobe cuando [enviar el destino para su revisión](/help/destinations/destination-sdk/submit-destination.md#logo). |
| `connectionType` | Cadena | El tipo de conexión, según el destino. Valores compatibles: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booleano | Indica si la conexión de destino se incluye en la [flujo ejecuta la IU](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Al establecer esto en `true`: <ul><li>El **[!UICONTROL Fecha de última ejecución del flujo de datos]** y **[!UICONTROL Último estado de ejecución del flujo de datos]** se muestran en la página de exploración de destino.</li><li>El **[!UICONTROL Ejecuciones de flujo de datos]** y **[!UICONTROL Datos de activación]** las pestañas se muestran en la página de vista de destino.</li></ul> |
| `monitoringSupported` | Booleano | Indica si la conexión de destino se incluye en la [IU de monitorización](../ui/destinations-workspace.md#browse). Al establecer esto en `true`, el **[!UICONTROL Ver en monitorización]** se muestra en la página de exploración de destino. |
| `frequency` | Cadena | Se refiere al tipo de exportación de datos compatible con el destino. Configure como. `Batch` para destinos basados en archivos. |

{style="table-layout:auto"}

## Envío de destino {#destination-delivery}

La sección de entrega de destino indica a dónde van exactamente los datos exportados y qué regla de autenticación se utiliza en la ubicación donde aterrizarán los datos. Debe especificar una o más `destinationServerId`Es el lugar donde se entregarán los datos y la regla de autenticación. En la mayoría de los casos, la regla de autenticación que debe utilizar es `CUSTOMER_AUTHENTICATION`.

El `deliveryMatchers` es opcional y se puede utilizar si especifica varias secciones `destinationServerId`s. Si es así, la variable `deliveryMatchers` indica cómo se deben dividir los datos exportados entre los distintos servidores de destino.

```json
 "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema mediante cualquiera de los siguientes métodos: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Uso `PLATFORM_AUTHENTICATION` si existe un sistema de autenticación global entre el Adobe y el destino y el [!DNL Platform] el cliente no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe crear un objeto de credenciales utilizando la variable [Credenciales](./credentials-configuration-api.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationServerId` | Cadena | El `instanceId` de la [configuración del servidor de destino](./server-and-file-configuration.md) que usted [created](/help/destinations/destination-sdk/destination-server-api.md#create-file-based) para este destino. |

{style="table-layout:auto"}

## Configuración de asignación de segmentos {#segment-mapping}

Esta sección de la configuración de destino se relaciona con la forma en que los metadatos de segmento, como nombres de segmento o ID, deben compartirse entre el Experience Platform y su destino.

A través de `audienceTemplateId`, esta sección también vincula esta configuración con el [configuración de metadatos de audiencia](./audience-metadata-management.md).

```json
   "segmentMappingConfig":{
       "mapExperiencePlatformSegmentName":false,
       "mapExperiencePlatformSegmentId":false,
       "mapUserInput":false,
       "audienceTemplateId":"cbf90a70-96b4-437b-86be-522fbdaabe9c"
   },
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el nombre del segmento del Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el ID de segmento del Experience Platform. |
| `mapUserInput` | Booleano | Controla si el usuario introduce el ID de asignación de segmentos en el flujo de trabajo de activación de destino. |
| `audienceTemplateId` | Booleano | El `instanceId` de la [plantilla de metadatos de audiencia](./audience-metadata-management.md) se utiliza para este destino. Para configurar una plantilla de metadatos de audiencia, lea la [referencia de API de metadatos de audiencia](./audience-metadata-api.md). |

## Configuración del esquema en el paso de asignación {#schema-configuration}

Adobe Experience Platform Destination SDK admite esquemas definidos por el socio. Un esquema definido por el socio permite a los usuarios asignar atributos de perfil e identidades a esquemas personalizados definidos por socios de destino, similares a los [destinos de streaming](destination-configuration.md#schema-configuration) flujo de trabajo.

Uso de los parámetros de `schemaConfig` para habilitar el paso de asignación del flujo de trabajo de activación de destino. Mediante los parámetros que se describen a continuación, puede determinar si los usuarios Experience Platform pueden asignar atributos de perfil o identidades al destino basado en archivos.

Puede crear campos de esquema estáticos y codificados o puede especificar un esquema dinámico al que el Experience Platform debe conectarse para recuperar y rellenar dinámicamente los campos en el esquema de destino del flujo de trabajo de asignación. El esquema de destino se muestra en la captura de pantalla siguiente.

![Captura de pantalla que resalta los campos de esquema de destino en el paso de asignación del flujo de trabajo de activación.](/help/destinations/destination-sdk/assets/target-schema-fields.png)

### Configuración del campo de esquema codificado estático

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
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
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `profileFields` | Matriz | Cuando se añaden variables predefinidas `profileFields`, los usuarios de Experience Platform tienen la opción de asignar atributos de Platform a los atributos predefinidos en el destino. |
| `profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados del lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `segmentRequired` | Booleano | Usar siempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad de Experience Platform al esquema deseado. |

{style="table-layout:auto"}

### Configuración de esquema dinámico en el paso de asignación {#dynamic-schema-configuration}

Uso de los parámetros de  `dynamicSchemaConfig` para recuperar dinámicamente su propio esquema al que se pueden asignar atributos o identidades de perfil de Platform.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"2aa8a809-c4ae-4f66-bb02-12df2e0a2279",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados del lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `segmentRequired` | Booleano | Usar siempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad de Experience Platform al esquema deseado. |
| `destinationServerId` | Cadena | El `instanceId` de la [configuración del servidor de destino](./destination-server-api.md) que ha creado para su esquema dinámico. Este servidor de destino incluye el extremo HTTP al que el Experience Platform llamará para recuperar el esquema dinámico utilizado para rellenar campos de destino. |
| `authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema mediante cualquiera de los siguientes métodos: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Uso `PLATFORM_AUTHENTICATION` si existe un sistema de autenticación global entre el Adobe y el destino y el [!DNL Platform] el cliente no necesita proporcionar credenciales de autenticación para conectarse a su destino. En este caso, debe crear un objeto de credenciales utilizando la variable [Credenciales](./credentials-configuration-api.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `value` | Cadena | Nombre del esquema que se va a mostrar en la interfaz de usuario del Experience Platform, en el paso de asignación. |
| `responseFormat` | Cadena | Siempre establecido en `SCHEMA` al definir un esquema personalizado. |

{style="table-layout:auto"}

### Asignaciones requeridas {#required-mappings}

En la configuración del esquema, tiene la opción de añadir las asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver, pero no modificar, cuando configuran una conexión con el destino. Por ejemplo, puede hacer que el campo de dirección de correo electrónico se envíe siempre al destino en los archivos exportados. Vea a continuación dos ejemplos de una configuración de esquema con asignaciones requeridas y cómo se ven en el paso de asignación de la variable [flujo de trabajo activar datos en destinos por lotes](/help/destinations/ui/activate-batch-profile-destinations.md).

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID", //if only the destination field is specified, then the user is able to select a source field to map to the destination.
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
```

![Imagen de las asignaciones requeridas en el flujo de activación de la IU.](/help/destinations/destination-sdk/assets/required-mappings-1.png)

```json
    "requiredMappingsOnly": true, // when this is selected true , users cannot map other attributes and identities in the activation flow, apart from the required mappings that you define.
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address" //when both source and destination fields are specified as required mappings, then the user can not select or edit any of the two fields and can only view the selection.
      }
    ] 
```

![Imagen de las asignaciones requeridas en el flujo de activación de la IU.](/help/destinations/destination-sdk/assets/required-mappings-2.png)

>[!NOTE]
>
>Las combinaciones admitidas actualmente de asignaciones requeridas son:
>* Puede configurar un campo de origen y un campo de destino obligatorios. En este caso, los usuarios no pueden editar ni seleccionar ninguno de los dos campos y solo pueden ver la selección.
>* Solo puede configurar un campo de destino requerido. En este caso, los usuarios podrán seleccionar un campo de origen para asignarlo al destino.
>
> Actualmente solo se puede configurar un campo de origen obligatorio *no* compatible.

Utilice los parámetros descritos en la tabla siguiente si desea añadir las asignaciones necesarias en el flujo de trabajo de activación para su destino.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `requiredMappingsOnly` | Booleano | Indica si los usuarios pueden asignar otros atributos e identidades en el flujo de activación, *aparte de* las asignaciones necesarias que defina. |
| `requiredMappings.mandatoryRequired` | Booleano | Establezca como true si este campo debe ser un atributo obligatorio que siempre debe estar presente en las exportaciones de archivos a su destino. Más información sobre [atributos obligatorios](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `requiredMappings.primaryKeyRequired` | Booleano | Establezca como true si este campo debe utilizarse como clave de anulación de duplicación en las exportaciones de archivos a su destino. Más información sobre [claves de deduplicación](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `requiredMappings.sourceType` | Cadena | Se utiliza al configurar un campo de origen según sea necesario. Uso `"text/x.schema-path"`, que indica que el campo de origen es un atributo XDM predefinido |
| `requiredMappings.source` | Cadena | Indica cuál debe ser el campo de origen requerido. |
| `requiredMappings.destination` | Cadena | Indica cuál debe ser el campo de destino requerido. |

{style="table-layout:auto"}

## Identidades y atributos {#identities-and-attributes}

Los parámetros de esta sección determinan qué identidades acepta su destino. Esta configuración también rellena las identidades y atributos de destinatario en la variable [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) de la interfaz de usuario de Experience Platform, donde los usuarios asignan identidades y atributos de sus esquemas XDM al esquema de destino.


```json
"identityNamespaces": {
        "crm_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        },
        "mobile_id": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": true
        }
    },
```

Debe indicar qué [!DNL Platform] identidades que los clientes pueden exportar a su destino. Algunos ejemplos son [!DNL Experience Cloud ID], correo electrónico con hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Estos valores son [!DNL Platform] áreas de nombres de identidad que los clientes pueden asignar a áreas de nombres de identidad desde el destino. También puede indicar si los clientes pueden asignar áreas de nombres personalizadas a identidades admitidas en el destino (`acceptsCustomNamespaces: true`) y si los clientes pueden asignar atributos XDM estándar a identidades admitidas por el destino (`acceptsAttributes: true`).

Las áreas de nombres de identidad no requieren una correspondencia de 1 a 1 entre [!DNL Platform] y su destino.
Por ejemplo, los clientes podrían asignar un [!DNL Platform] [!DNL IDFA] área de nombres a [!DNL IDFA] Área de nombres de su destino o pueden asignar lo mismo [!DNL Platform] [!DNL IDFA] área de nombres a [!DNL Customer ID] área de nombres en su destino.

Obtenga más información sobre las identidades en [Resumen de área de nombres de identidad](/help/identity-service/namespaces.md).


## Configuración por lotes: asignación de nombres de archivo y programación de exportación {#batch-configuration}

Esta sección hace referencia a la configuración de nomenclatura de archivos y programación de exportación que se mostrará para su destino en la interfaz de usuario de Adobe Experience Platform. Los valores que configure aquí aparecen en la variable [Programar exportación de segmentos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) paso del flujo de trabajo de activación de destinos basados en archivos.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
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
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   }
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Booleano | Configure como. `true` para permitir a los clientes especificar qué atributos de perfil son obligatorios. El valor predeterminado es `false`. Consulte [Atributos obligatorios](../ui/activate-batch-profile-destinations.md#mandatory-attributes) para obtener más información. |
| `allowDedupeKeyFieldSelection` | Booleano | Configure como. `true` para permitir a los clientes especificar claves de deduplicación. El valor predeterminado es `false`.  Consulte [Claves de deduplicación](../ui/activate-batch-profile-destinations.md#deduplication-keys) para obtener más información. |
| `defaultExportMode` | Enumeración | Define el modo de exportación de archivos predeterminado. Valores compatibles:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> El valor predeterminado es `DAILY_FULL_EXPORT`. Consulte la [documentación de activación por lotes](../ui/activate-batch-profile-destinations.md#scheduling) para obtener más información sobre la programación de exportaciones de archivos. |
| `allowedExportModes` | Lista | Define los modos de exportación de archivos disponibles para los clientes de. Valores compatibles:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define la frecuencia de exportación de archivos disponible para los clientes. Valores compatibles:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enumeración | Define la frecuencia predeterminada de exportación de archivos. Valores compatibles:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> El valor predeterminado es `DAILY`. |
| `defaultStartTime` | Cadena | Define la hora de inicio predeterminada para la exportación de archivos. Utiliza el formato de archivo de 24 horas. El valor predeterminado es 00:00. |
| `filenameConfig.allowedFilenameAppendOptions` | Cadena | *Requerido*. Lista de macros de nombre de archivo disponibles para que los usuarios elijan. Esto determina qué elementos se anexan a los nombres de archivo exportados (ID de segmento, nombre de organización, fecha y hora de exportación, etc.). Al configurar `defaultFilename`, asegúrese de evitar la duplicación de macros. <br><br>Valores compatibles: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independientemente del orden en el que defina las macros, la interfaz de usuario de Experience Platform siempre las mostrará en el orden presentado aquí. <br><br> If `defaultFilename` está vacío, la variable `allowedFilenameAppendOptions` La lista debe contener al menos una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Cadena | *Requerido*. Macros de nombre de archivo predeterminado preseleccionadas que los usuarios pueden desmarcar.<br><br> Las macros de esta lista son un subconjunto de las definidas en `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Cadena | *Opcional*. Define las macros de nombre de archivo predeterminadas para los archivos exportados. Los usuarios no pueden sobrescribirlos. <br><br>Cualquier macro definida por `allowedFilenameAppendOptions` se adjuntará después de `defaultFilename` macros. <br><br>If `defaultFilename` está vacío, debe definir al menos una macro en `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

### Configuración del nombre de archivo {#file-name-configuration}

Utilice macros de configuración de nombres de archivo para definir qué nombres de archivo exportados deben incluir. Las macros de la tabla siguiente describen los elementos que se encuentran en la interfaz de usuario de [configuración de nombre de archivo](../ui/activate-batch-profile-destinations.md#file-names) pantalla.


>[!TIP]
> 
>Como práctica recomendada, siempre debe incluir la variable `SEGMENT_ID` macro en los nombres de archivo exportados. Los ID de segmento son únicos, por lo que incluirlos en el nombre de archivo es la mejor manera de asegurarse de que los nombres de archivo también sean únicos.

| Macro | Etiqueta de IU | Descripción | Ejemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nombre del destino en la interfaz de usuario. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID del segmento] | ID de segmento único generado por Platform | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nombre del segmento] | Nombre del segmento definido por el usuario | VIP suscriptor del servicio de asistencia |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de destino] | ID único y generado por Platform de la instancia de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nombre del destino] | Nombre definido por el usuario de la instancia de destino. | Mi destino publicitario de 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nombre de la organización] | Nombre de la organización del cliente en Adobe Experience Platform. | Nombre de mi organización |
| `SANDBOX_NAME` | [!UICONTROL Nombre de zona protegida] | Nombre de la zona protegida utilizada por el cliente. | picar |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Fecha y hora] | `DATETIME` y `TIMESTAMP` ambos definen cuándo se generó el archivo, pero en formatos diferentes. <br><br><ul><li>`DATETIME` utiliza el siguiente formato: AAAAMMDD_HHMMSS.</li><li>`TIMESTAMP` utiliza el formato Unix de 10 dígitos. </li></ul> `DATETIME` y `TIMESTAMP` son mutuamente excluyentes y no pueden utilizarse simultáneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido por el usuario que se incluirá en el nombre del archivo. No se puede usar en `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Fecha y hora] | Marca de tiempo de 10 dígitos de la hora en la que se generó el archivo, en formato Unix. | 1652131584 |

{style="table-layout:auto"}

![Imagen de la interfaz de usuario que muestra la pantalla de configuración del nombre de archivo con macros preseleccionadas](assets/file-name-configuration.png)

El ejemplo que se muestra en la imagen anterior utiliza la siguiente configuración de macro de nombre de archivo:

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```


## Cualificaciones históricas del perfil {#profile-backfill}

Puede usar el complemento `backfillHistoricalProfileData` en la configuración de destinos para determinar si las cualificaciones de perfil históricas deben exportarse a su destino.

```json
   "backfillHistoricalProfileData":true
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla si los datos de perfil históricos se exportan cuando los segmentos se activan en el destino. <br> <ul><li> `true`: [!DNL Platform] envía los perfiles de usuario históricos aptos para el segmento antes de activarlo. </li><li> `false`: [!DNL Platform] solo incluye perfiles de usuario que cumplen los requisitos para el segmento después de activarlo. </li></ul> |

{style="table-layout:auto"}

## Cómo esta configuración conecta toda la información necesaria para su destino {#connecting-all-configurations}

Algunos de los ajustes de destino deben configurarse a través del [servidor de destino](./server-and-file-configuration.md) o el [configuración de metadatos de audiencia](./audience-metadata-management.md) puntos finales. La configuración de destino que se describe aquí conecta todas estas configuraciones haciendo referencia a las otras dos configuraciones de la siguiente manera:

* Utilice el `destinationServerId` para hacer referencia al servidor de destino y a la configuración de la plantilla de archivos establecida para el destino.
* Utilice el `audienceMetadataId` para hacer referencia a la configuración de metadatos de audiencia configurada para su destino.
