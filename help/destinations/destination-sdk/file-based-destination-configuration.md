---
description: Esta configuración le permite indicar información esencial para su destino basado en archivos, como el nombre de destino, la categoría, la descripción y mucho más. Los ajustes de esta configuración también determinan cómo se autentican los usuarios Experience Platform en el destino, cómo aparece en la interfaz de usuario del Experience Platform y las identidades que se pueden exportar al destino.
title: Opciones de configuración de destino basadas en archivos para Destination SDK
exl-id: 6b0a0398-6392-470a-bb27-5b34b0062793
source-git-commit: 21278b39a2dc12771449b9a471ea4182c6b999a3
workflow-type: tm+mt
source-wordcount: '3012'
ht-degree: 5%

---

# Configuración de destino basada en archivos {#destination-configuration}

## Información general {#overview}

Esta configuración le permite indicar información esencial para su destino basado en archivos, como el nombre de destino, la categoría, la descripción y mucho más. Los ajustes de esta configuración también determinan cómo se autentican los usuarios Experience Platform en el destino, cómo aparece en la interfaz de usuario del Experience Platform y las identidades que se pueden exportar al destino. También puede utilizar esta configuración para mostrar las opciones relacionadas con el tipo de archivo, el formato de archivo o la configuración de compresión de los archivos exportados.

Esta configuración también conecta a esta las demás configuraciones necesarias para que funcione su destino (servidor de destino y metadatos de audiencia). Lea cómo puede hacer referencia a las dos configuraciones en una [sección siguiente](./file-based-destination-configuration.md#connecting-all-configurations).

Puede configurar la funcionalidad descrita en este documento utilizando la variable `/authoring/destinations` extremo de API. Lectura [Operaciones de extremo de la API de destinos](./destination-configuration-api.md) para obtener una lista completa de las operaciones que puede realizar en el punto final.

## Ejemplo de configuración de destino de Amazon S3 {#batch-example-configuration}

A continuación, se muestra un ejemplo de un destino Amazon S3 personalizado privado creado mediante la variable `/destinations` punto final de configuración.

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
| `name` | Cadena | Indica el título del destino en el catálogo de Experience Platform. |
| `description` | Cadena | Proporcione una descripción para su tarjeta de destino en el catálogo de destinos de Experience Platform. Apunte a no más de 4-5 frases. |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Uso `TEST` la primera vez que configure el destino. |
| `maxProfileAttributes` | Cadena | Indica el número máximo de atributos de perfil que los clientes pueden exportar al destino. El valor predeterminado es `2000`. |
| `maxIdentityAttributes` | Cadena | Indica el número máximo de áreas de nombres de identidad que los clientes pueden exportar al destino. El valor predeterminado es `10`. |

{style=&quot;table-layout:auto&quot;}

## Configuraciones de autenticación de clientes {#customer-authentication-configurations}

Esta sección en la configuración de destinos genera la variable [Configurar nuevo destino](/help/destinations/ui/connect-destination.md) en la interfaz de usuario del Experience Platform, donde los usuarios se conectan Experience Platform a las cuentas que tienen con el destino.

```json
"customerAuthenticationConfigurations": [
        {
            "authType": "S3"
        }
    ],
```

Dependiendo de qué [opción de autenticación](authentication-configuration.md##supported-authentication-types) usted indica en el `authType` , la página Experience Platform se genera para los usuarios de la siguiente manera:

### Autenticación de Amazon S3 {#s3}

Al configurar el tipo de autenticación de Amazon S3, los usuarios deben introducir las credenciales de S3.

![Renderización de la interfaz de usuario con autenticación S3](assets/s3-authentication-ui.png)

### Autenticación de Azure Blob  {#blob}

Al configurar el tipo de autenticación de Azure Blob, los usuarios deben introducir la cadena de conexión.

![Renderización de la interfaz de usuario con autenticación Blob](assets/blob-authentication-ui.png)

### SFTP con autenticación de contraseña

Al configurar el SFTP con un tipo de autenticación de contraseña, los usuarios deben introducir el nombre de usuario y la contraseña del SFTP, así como el dominio y el puerto del SFTP (el puerto predeterminado es 22).

![Renderización de la interfaz de usuario con SFTP con autenticación de contraseña](assets/sftp-password-authentication-ui.png)

### SFTP con autenticación de clave SSH

Al configurar el SFTP con el tipo de autenticación de clave SSH, los usuarios deben introducir el nombre de usuario y la clave SSH del SFTP, así como el dominio y el puerto SFTP (el puerto predeterminado es 22).

![Renderización de la interfaz de usuario con SFTP con autenticación de clave SSH](assets/sftp-key-authentication-ui.png)

## Campos de datos del cliente {#customer-data-fields}

Utilice esta sección para solicitar a los usuarios que rellenen campos personalizados, específicos de su destino, al conectarse al destino en la interfaz de usuario del Experience Platform.

En el ejemplo siguiente, `customerDataFields` requiere que los usuarios introduzcan un nombre para su destino y que proporcionen un [!DNL Amazon S3] nombre del contenedor y ruta de carpeta, así como un tipo de compresión, formato de archivo y otras opciones de formato de archivo.

Puede acceder y utilizar las entradas de cliente de los campos de datos del cliente en la plantilla. Utilice la macro `{{customerData.exampleName}}`. Por ejemplo, si pide a los usuarios que introduzcan un campo de compartimento de Amazon S3, con el nombre `bucket`, puede acceder a ella en la plantilla mediante la macro `{{customerData.bucket}}`. Ver un ejemplo de cómo se utiliza un campo de datos de cliente en la variable [configuración del servidor de destino](/help/destinations/destination-sdk/server-and-file-configuration.md#s3-example).

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
>Todas las configuraciones de formato de archivo enumeradas en el ejemplo anterior se describen en detalle en la variable [configuración de formato de archivo](/help/destinations/destination-sdk/server-and-file-configuration.md#file-configuration) para obtener más información.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. |
| `title` | Cadena | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario del Experience Platform. |
| `description` | Cadena | Proporcione una descripción para el campo personalizado. |
| `type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer`. |
| `isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. |
| `pattern` | Cadena | Aplica un patrón para el campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números o guiones bajos, introduzca `^[A-Za-z]+$` en este campo. |
| `enum` | Cadena | Representa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. |
| `default` | Cadena | Define el valor predeterminado de un `enum` lista. |

{style=&quot;table-layout:auto&quot;}

## Atributos de interfaz de usuario {#ui-attributes}

Esta sección se refiere a los elementos de IU de la configuración anterior que el Adobe debe utilizar para el destino en la interfaz de usuario de Adobe Experience Platform.

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
| `documentationLink` | Cadena | Se refiere a la página de documentación de la [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Uso `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe usar `http://www.adobe.com/go/destinations-moviestar-en`. Tenga en cuenta que este vínculo solo funciona después de que el Adobe establezca el destino en vivo y la documentación se publique. |
| `category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, lea [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. |
| `iconUrl` | Cadena | Dirección URL donde alojó el icono para que se muestre en la tarjeta de catálogo de destinos. Para integraciones personalizadas privadas, esto no es necesario. Para las configuraciones de producto, debe compartir un icono con el equipo de Adobe cuando [enviar el destino para su revisión](/help/destinations/destination-sdk/submit-destination.md#logo). |
| `connectionType` | Cadena | Tipo de conexión, según el destino. Valores compatibles: <ul><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li></ul> |
| `flowRunsSupported` | Booleano | Indica si la conexión de destino está incluida en la variable [flujo ejecuta la interfaz de usuario](../../dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard). Al configurar esto `true`: <ul><li>La variable **[!UICONTROL Última fecha de ejecución del flujo de datos]** y **[!UICONTROL Último estado de ejecución de flujo de datos]** se muestran en la página de búsqueda de destino.</li><li>La variable **[!UICONTROL Ejecuciones de flujo de datos]** y **[!UICONTROL Datos de activación]** se muestran en la página de vista de destino.</li></ul> |
| `monitoringSupported` | Booleano | Indica si la conexión de destino está incluida en la variable [IU de monitorización](../ui/destinations-workspace.md#browse). Al configurar esto `true`, el **[!UICONTROL Ver en monitorización]** se muestra en la página de búsqueda de destino. |
| `frequency` | Cadena | Se refiere al tipo de exportación de datos compatible con el destino. Establecer como `Batch` para destinos basados en archivos. |

{style=&quot;table-layout:auto&quot;}

## Entrega de destino {#destination-delivery}

La sección de entrega de destino indica dónde se dirigen exactamente los datos exportados y qué regla de autenticación se utiliza en la ubicación a la que llegan los datos. Debe especificar uno o más `destinationServerId`s dónde se enviarán los datos y la regla de autenticación. En la mayoría de los casos, la regla de autenticación que debe utilizar es `CUSTOMER_AUTHENTICATION`.

La variable `deliveryMatchers` es opcional y puede utilizarse si especifica varias `destinationServerId`s. Si ese es el caso, la variable `deliveryMatchers` indica cómo se deben dividir los datos exportados entre los distintos servidores de destino.

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
| `authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema mediante cualquiera de los métodos siguientes: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Uso `PLATFORM_AUTHENTICATION` si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable [Credenciales](./credentials-configuration-api.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationServerId` | Cadena | La variable `instanceId` del [configuración del servidor de destino](./server-and-file-configuration.md) que [created](/help/destinations/destination-sdk/destination-server-api.md#create-file-based) para este destino. |

{style=&quot;table-layout:auto&quot;}

## Configuración de asignación de segmentos {#segment-mapping}

Esta sección de la configuración de destino se relaciona con la forma en que los metadatos de segmento, como los nombres o ID de segmentos, deben compartirse entre el Experience Platform y el destino.

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
| `mapExperiencePlatformSegmentName` | Booleano | Controla si el id. de asignación de segmentos en el flujo de trabajo de activación de destino es el nombre del segmento del Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el ID de segmento del Experience Platform. |
| `mapUserInput` | Booleano | Controla si el usuario introduce el ID de asignación de segmentos en el flujo de trabajo de activación de destino. |
| `audienceTemplateId` | Booleano | La variable `instanceId` del [plantilla de metadatos de audiencia](./audience-metadata-management.md) para este destino. Para configurar una plantilla de metadatos de audiencia, lea la [referencia de API de metadatos de audiencia](./audience-metadata-api.md). |

## Configuración del esquema en el paso de asignación {#schema-configuration}

El Adobe Experience Platform Destination SDK admite esquemas definidos por el socio. Un esquema definido por el socio permite a los usuarios asignar atributos e identidades de perfil a esquemas personalizados definidos por los socios de destino, de forma similar a la variable [destinos de flujo continuo](destination-configuration.md#schema-configuration) flujo de trabajo.

Utilice los parámetros de `schemaConfig` para habilitar el paso de asignación del flujo de trabajo de activación de destino. Mediante los parámetros que se describen a continuación, puede determinar si los usuarios Experience Platform pueden asignar atributos de perfil o identidades a su destino basado en archivos.

Puede crear campos de esquema estáticos y codificados o especificar un esquema dinámico al que el Experience Platform debe conectarse para recuperar y rellenar dinámicamente los campos en el esquema de destino del flujo de trabajo de asignación. El esquema de destino se muestra en la captura de pantalla siguiente.

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
| `profileFields` | Matriz | Al agregar una `profileFields`, los usuarios Experience Platform tienen la opción de asignar atributos de Platform a los atributos predefinidos en el destino. |
| `profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en el lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `segmentRequired` | Booleano | Utilice siempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad desde el Experience Platform al esquema deseado. |

{style=&quot;table-layout:auto&quot;}

### Configuración de esquema dinámico en el paso de asignación {#dynamic-schema-configuration}

Utilice los parámetros de  `dynamicSchemaConfig` para recuperar dinámicamente su propio esquema al que se pueden asignar los atributos o identidades de perfil de Platform.

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
| `profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en el lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `segmentRequired` | Booleano | Utilice siempre `segmentRequired:true`. |
| `identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad desde el Experience Platform al esquema deseado. |
| `destinationServerId` | Cadena | La variable `instanceId` del [configuración del servidor de destino](./destination-server-api.md) que ha creado para el esquema dinámico. Este servidor de destino incluye el extremo HTTP al que llama el Experience Platform para recuperar el esquema dinámico utilizado para rellenar los campos de destino. |
| `authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en el sistema mediante cualquiera de los métodos siguientes: <ul><li>`"authType": "S3"`</li><li>`"authType":"AZURE_CONNECTION_STRING"`</li><li>`"authType":"AZURE_SERVICE_PRINCIPAL"`</li><li>`"authType":"SFTP_WITH_SSH_KEY"`</li><li>`"authType":"SFTP_WITH_PASSWORD"`</li></ul> </li><li> Uso `PLATFORM_AUTHENTICATION` si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable [Credenciales](./credentials-configuration-api.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `value` | Cadena | Nombre del esquema que se va a mostrar en la interfaz de usuario del Experience Platform, en el paso de asignación. |
| `responseFormat` | Cadena | Siempre se configura como `SCHEMA` al definir un esquema personalizado. |

{style=&quot;table-layout:auto&quot;}

### Asignaciones necesarias {#required-mappings}

Dentro de la configuración de esquema, tiene la opción de añadir asignaciones necesarias (o predefinidas). Son asignaciones que los usuarios pueden ver pero no modificar cuando configuran una conexión con su destino. Por ejemplo, puede aplicar el campo de dirección de correo electrónico para que siempre se envíe al destino en los archivos exportados. Consulte a continuación dos ejemplos de una configuración de esquema con asignaciones necesarias y su aspecto en el paso de asignación de la variable [flujo de trabajo de activación de datos en destinos por lotes](/help/destinations/ui/activate-batch-profile-destinations.md).

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

![Imagen de las asignaciones necesarias en el flujo de activación de la interfaz de usuario.](/help/destinations/destination-sdk/assets/required-mappings-1.png)

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

![Imagen de las asignaciones necesarias en el flujo de activación de la interfaz de usuario.](/help/destinations/destination-sdk/assets/required-mappings-2.png)

>[!NOTE]
>
>Actualmente, las combinaciones admitidas de las asignaciones requeridas son:
>* Puede configurar un campo de origen requerido y un campo de destino requerido. En este caso, los usuarios no pueden editar ni seleccionar ninguno de los dos campos y solo pueden ver la selección.
>* Solo puede configurar un campo de destino requerido. En este caso, los usuarios podrán seleccionar un campo de origen para asignarlo al destino.
>
> Actualmente, la configuración de un campo de origen requerido solo está *not* compatible.

Utilice los parámetros descritos en la tabla siguiente si desea añadir las asignaciones necesarias en el flujo de trabajo de activación para el destino.

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `requiredMappingsOnly` | Booleano | Indica si los usuarios pueden asignar otros atributos e identidades en el flujo de activación, *apart* las asignaciones necesarias que defina. |
| `requiredMappings.mandatoryRequired` | Booleano | Se establece en true si este campo debe ser un atributo obligatorio que siempre esté presente en las exportaciones de archivos al destino. Más información sobre [atributos obligatorios](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `requiredMappings.primaryKeyRequired` | Booleano | Se establece en true si este campo debe utilizarse como clave de deduplicación en las exportaciones de archivos al destino. Más información sobre [claves de deduplicación](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `requiredMappings.sourceType` | Cadena | Se utiliza cuando se configura un campo de origen como necesario. Uso `"text/x.schema-path"`, que indica que el campo de origen es un atributo XDM predefinido |
| `requiredMappings.source` | Cadena | Indica cuál debe ser el campo de origen requerido. |
| `requiredMappings.destination` | Cadena | Indica cuál debe ser el campo de destino requerido. |

{style=&quot;table-layout:auto&quot;}

## Identidades y atributos {#identities-and-attributes}

Los parámetros de esta sección determinan qué identidades acepta el destino. Esta configuración también rellena las identidades y atributos de destino en la variable [paso de asignación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) de la interfaz de usuario del Experience Platform, donde los usuarios asignan identidades y atributos de sus esquemas XDM al esquema en el destino.


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

Debe indicar qué [!DNL Platform] identidades que los clientes pueden exportar a su destino. Algunos ejemplos son [!DNL Experience Cloud ID], correo electrónico con hash, ID de dispositivo ([!DNL IDFA], [!DNL GAID]). Estos valores son [!DNL Platform] áreas de nombres de identidad que los clientes pueden asignar a áreas de nombres de identidad desde su destino. También puede indicar si los clientes pueden asignar áreas de nombres personalizadas a identidades compatibles con el destino (`acceptsCustomNamespaces: true`) y si los clientes pueden asignar atributos XDM estándar a identidades compatibles con el destino (`acceptsAttributes: true`).

Las áreas de nombres de identidad no requieren una correspondencia de 1 a 1 entre [!DNL Platform] y su destino.
Por ejemplo, los clientes podrían asignar un [!DNL Platform] [!DNL IDFA] espacio de nombres a un [!DNL IDFA] del destino o pueden asignar el mismo [!DNL Platform] [!DNL IDFA] espacio de nombres a [!DNL Customer ID] en el destino.

Obtenga más información sobre las identidades en la [Información general sobre el área de nombres de identidad](/help/identity-service/namespaces.md).


## Configuración de lotes: asignación de nombres a archivos y programación de exportaciones {#batch-configuration}

Esta sección hace referencia a la configuración de asignación de nombres a archivos y de programación de exportación que se mostrará para el destino en la interfaz de usuario de Adobe Experience Platform. Los valores que configure aquí aparecen en la [Programar exportación de segmentos](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling) paso del flujo de trabajo de activación de destinos basados en archivos.

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
| `allowMandatoryFieldSelection` | Booleano | Establecer como `true` para permitir a los clientes especificar qué atributos de perfil son obligatorios. El valor predeterminado es `false`. Consulte [Atributos obligatorios](../ui/activate-batch-profile-destinations.md#mandatory-attributes) para obtener más información. |
| `allowDedupeKeyFieldSelection` | Booleano | Establecer como `true` para permitir a los clientes especificar claves de deduplicación. El valor predeterminado es `false`.  Consulte [Claves de deduplicación](../ui/activate-batch-profile-destinations.md#deduplication-keys) para obtener más información. |
| `defaultExportMode` | Enum | Define el modo predeterminado de exportación de archivos. Valores compatibles:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> El valor predeterminado es `DAILY_FULL_EXPORT`. Consulte la [documentación de activación por lotes](../ui/activate-batch-profile-destinations.md#scheduling) para obtener más información sobre la programación de exportaciones de archivos. |
| `allowedExportModes` | Lista | Define los modos de exportación de archivos disponibles para los clientes. Valores compatibles:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Lista | Define la frecuencia de exportación de archivos disponible para los clientes. Valores compatibles:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Define la frecuencia de exportación de archivos predeterminada. Valores compatibles:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> El valor predeterminado es `DAILY`. |
| `defaultStartTime` | Cadena | Define la hora de inicio predeterminada para la exportación de archivos. Utiliza el formato de archivo de 24 horas. El valor predeterminado es &quot;00:00&quot;. |
| `filenameConfig.allowedFilenameAppendOptions` | Cadena | *Requerido*. Lista de macros de nombres de archivo disponibles para que los usuarios puedan elegir. Esto determina qué elementos se adjuntan a los nombres de archivo exportados (ID de segmento, nombre de organización, fecha y hora de exportación, etc.). Al configurar `defaultFilename`, asegúrese de evitar la duplicación de macros. <br><br>Valores compatibles: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Independientemente del orden en que defina las macros, la interfaz de usuario del Experience Platform siempre las mostrará en el orden presentado aquí. <br><br> If `defaultFilename` está vacío, la variable `allowedFilenameAppendOptions` La lista debe contener al menos una macro. |
| `filenameConfig.defaultFilenameAppendOptions` | Cadena | *Requerido*. Macros de nombres de archivo predeterminados preseleccionados que los usuarios pueden desmarcar.<br><br> Las macros de esta lista son un subconjunto de las definidas en `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Cadena | *Opcional*. Define las macros de nombre de archivo predeterminadas para los archivos exportados. Los usuarios no pueden sobrescribirlos. <br><br>Cualquier macro definida por `allowedFilenameAppendOptions` se añadirá después de `defaultFilename` macros. <br><br>If `defaultFilename` está vacío, debe definir al menos una macro en `allowedFilenameAppendOptions`. |

{style=&quot;table-layout:auto&quot;}

### Configuración de nombre de archivo {#file-name-configuration}

Utilice las macros de configuración de nombre de archivo para definir qué deben incluir los nombres de archivo exportados. Las macros de la tabla siguiente describen los elementos que se encuentran en la interfaz de usuario de [configuración de nombre de archivo](../ui/activate-batch-profile-destinations.md#file-names) en el Navegador.


>[!TIP]
> 
>Como práctica recomendada, debe incluir siempre la variable `SEGMENT_ID` en los nombres de archivo exportados. Los ID de segmento son únicos, por lo que incluirlos en el nombre de archivo es la mejor manera de garantizar que los nombres de archivo también sean únicos.

| Macro | Etiqueta de la interfaz de usuario | Descripción | Ejemplo |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Destino] | Nombre de destino en la interfaz de usuario. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL ID de segmento] | ID de segmento único generado por la plataforma | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Nombre del segmento] | Nombre de segmento definido por el usuario | VIP suscriptor |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL ID de destino] | ID único, generado por la plataforma de la instancia de destino | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Nombre de destino] | Nombre definido por el usuario de la instancia de destino. | Mi destino publicitario de 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Nombre de la organización] | Nombre de la organización de clientes en Adobe Experience Platform. | Mi nombre de organización |
| `SANDBOX_NAME` | [!UICONTROL Nombre del Simulador para pruebas] | Nombre del simulador de pruebas utilizado por el cliente. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Fecha y hora] | `DATETIME` y `TIMESTAMP` ambos definen cuándo se generó el archivo, pero en diferentes formatos. <br><br><ul><li>`DATETIME` utiliza el siguiente formato: AAAAMMDD_HHMMSS.</li><li>`TIMESTAMP` utiliza el formato Unix de 10 dígitos. </li></ul> `DATETIME` y `TIMESTAMP` son mutuamente excluyentes y no se pueden usar simultáneamente. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Texto personalizado] | Texto personalizado definido por el usuario que se incluirá en el nombre del archivo. No se puede usar en `defaultFilename`. | My_Custom_Text |
| `TIMESTAMP` | [!UICONTROL Fecha y hora] | Marca de fecha y hora de 10 dígitos del momento en que se generó el archivo, en formato Unix. | 1652131584 |

{style=&quot;table-layout:auto&quot;}

![Imagen de interfaz de usuario que muestra la pantalla de configuración del nombre de archivo con macros preseleccionadas](assets/file-name-configuration.png)

El ejemplo mostrado en la imagen anterior utiliza la siguiente configuración de macro de nombre de archivo:

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


## Calificaciones históricas de perfil {#profile-backfill}

Puede usar la variable `backfillHistoricalProfileData` en la configuración de destinos para determinar si se deben exportar a su destino las cualificaciones históricas de perfil.

```json
   "backfillHistoricalProfileData":true
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `backfillHistoricalProfileData` | Booleano | Controla si los datos del perfil histórico se exportan cuando los segmentos se activan en el destino. <br> <ul><li> `true`: [!DNL Platform] envía los perfiles de usuario históricos que cumplen los requisitos para el segmento antes de que se active el segmento. </li><li> `false`: [!DNL Platform] solo incluye perfiles de usuario que cumplen los requisitos para el segmento una vez activado el segmento. </li></ul> |

{style=&quot;table-layout:auto&quot;}

## Conexión de esta configuración a toda la información necesaria para el destino {#connecting-all-configurations}

Algunos de los ajustes de destino deben configurarse mediante el [servidor de destino](./server-and-file-configuration.md) o [configuración de metadatos de audiencia](./audience-metadata-management.md) extremos. La configuración de destino descrita conecta todos estos ajustes haciendo referencia a las otras dos configuraciones de la siguiente manera:

* Utilice la variable `destinationServerId` para hacer referencia a la configuración del servidor de destino y la plantilla de archivo configurada para el destino.
* Utilice la variable `audienceMetadataId` para hacer referencia a la configuración de metadatos de audiencia configurada para el destino.
