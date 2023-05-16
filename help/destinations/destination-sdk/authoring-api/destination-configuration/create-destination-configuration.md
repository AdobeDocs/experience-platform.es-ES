---
description: Aprenda a estructurar una llamada de API para crear una configuración de destino a través del Adobe Experience Platform Destination SDK.
title: Crear una configuración de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---


# Crear una configuración de destino

Esta página ejemplifica la solicitud de API y la carga útil que puede utilizar para crear su propia configuración de destino, utilizando la variable `/authoring/destinations` extremo de API.

Para obtener una descripción detallada de las capacidades que puede configurar a través de este punto final, lea los siguientes artículos:

* [Configuración de autenticación de cliente](../../functionality/destination-configuration/customer-authentication.md)
* [Autenticación OAuth2](../../functionality/destination-configuration/oauth2-authentication.md)
* [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md)
* [Atributos de interfaz de usuario](../../functionality/destination-configuration/ui-attributes.md)
* [Configuración del esquema](../../functionality/destination-configuration/schema-configuration.md)
* [Configuración del área de nombres de identidad](../../functionality/destination-configuration/identity-namespace-configuration.md)
* [Entrega de destino](../../functionality/destination-configuration/destination-delivery.md)
* [Configuración de metadatos de audiencia](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Configuración de metadatos de audiencia](../../functionality/destination-configuration/audience-metadata-configuration.md)
* [Política de agregación](../../functionality/destination-configuration/aggregation-policy.md)
* [Configuración por lotes](../../functionality/destination-configuration/batch-configuration.md)
* [Calificaciones históricas de perfil](../../functionality/destination-configuration/historical-profile-qualifications.md)

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de configuración de destino {#get-started}

Antes de continuar, revise la [guía de introducción](../../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Crear una configuración de destino {#create}

Puede crear una nueva configuración de destino realizando una solicitud de POST al `/authoring/destinations` punto final.

>[!TIP]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/destinations`

**Formato de API**

```http
POST /authoring/destinations
```

La siguiente solicitud crea un nuevo [!DNL Amazon S3] configuración de destino, configurada por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros para los destinos basados en archivos aceptados por el `/authoring/destinations` punto final.

Tenga en cuenta que no tiene que añadir todos los parámetros a la llamada de API y que la carga útil es personalizable, según los requisitos de la API.

+++Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Amazon S3 destination with predefined CSV formatting options",
   "description":"Amazon S3 destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ],
   "customerDataFields":[
      {
         "name":"bucket",
         "title":"Enter the name of your Amazon S3 bucket",
         "description":"Amazon S3 bucket name",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"path",
         "title":"Enter the path to your S3 bucket folder",
         "description":"Enter the path to your S3 bucket folder",
         "type":"string",
         "isRequired":true,
         "pattern":"^[A-Za-z]+$",
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"compression",
         "title":"Compression format",
         "description":"Select the desired file compression format.",
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
      "documentationLink":"https://www.adobe.com/go/destinations-amazon-s3-en",
      "category":"cloudStorage",
      "icon":{
         "key":"amazonS3"
      },
      "connectionType":"S3",
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
   "schemaConfig":{
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
}'
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `name` | Cadena | Indica el título del destino en el catálogo de Experience Platform. |
| `description` | Cadena | Proporcione una descripción que el Adobe utilizará en el catálogo de destinos del Experience Platform para su tarjeta de destino. Apunte a no más de 4-5 frases. ![Imagen de la interfaz de usuario de la plataforma que muestra la descripción del destino.](../../assets/authoring-api/destination-configuration/destination-description.png "Descripción del destino"){width="100" zoomable="yes"} |
| `status` | Cadena | Indica el estado del ciclo vital de la tarjeta de destino. Los valores aceptados son `TEST`, `PUBLISHED` y `DELETED`. Uso `TEST` la primera vez que configure el destino. |
| `customerAuthenticationConfigurations.authType` | Cadena | Indica la configuración utilizada para autenticar a los clientes Experience Platform en el servidor de destino. Consulte [configuración de autenticación de cliente](../../functionality/destination-configuration/customer-authentication.md) para obtener información detallada sobre los tipos de autenticación admitidos. |
| `customerDataFields.name` | Cadena | Proporcione un nombre para el campo personalizado que está introduciendo. <br/><br/> Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. ![Imagen de la interfaz de usuario de la plataforma que muestra los campos de datos del cliente.](../../assets/authoring-api/destination-configuration/customer-data-fields.png "Campo de datos del cliente"){width="100" zoomable="yes"} |
| `customerDataFields.type` | Cadena | Indica qué tipo de campo personalizado está introduciendo. Los valores aceptados son `string`, `object`, `integer`. <br/><br/> Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. |
| `customerDataFields.title` | Cadena | Indica el nombre del campo, tal como lo ven los clientes en la interfaz de usuario del Experience Platform. <br/><br/> Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. |
| `customerDataFields.description` | Cadena | Proporcione una descripción para el campo personalizado. Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. |
| `customerDataFields.isRequired` | Booleano | Indica si este campo es necesario en el flujo de trabajo de configuración de destino. <br/><br/> Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. |
| `customerDataFields.enum` | Cadena | Representa el campo personalizado como un menú desplegable y enumera las opciones disponibles para el usuario. <br/><br/> Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. |
| `customerDataFields.default` | Cadena | Define el valor predeterminado de un `enum` lista. |
| `customerDataFields.pattern` | Cadena | Aplica un patrón para el campo personalizado, si es necesario. Utilice expresiones regulares para aplicar un patrón. Por ejemplo, si los ID de cliente no incluyen números o guiones bajos, introduzca `^[A-Za-z]+$` en este campo. <br/><br/> Consulte [Campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) para obtener información detallada sobre esta configuración. |
| `uiAttributes.documentationLink` | Cadena | Se refiere a la página de documentación de la [Catálogo de destinos](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/overview.html?lang=en#catalog) para su destino. Uso `https://www.adobe.com/go/destinations-YOURDESTINATION-en`, donde `YOURDESTINATION` es el nombre de su destino. Para un destino llamado Moviestar, debe usar `https://www.adobe.com/go/destinations-moviestar-en`. Tenga en cuenta que este vínculo solo funciona después de que el Adobe establezca el destino en vivo y la documentación se publique. <br/><br/> Consulte [Atributos de interfaz de usuario](../../functionality/destination-configuration/ui-attributes.md) para obtener información detallada sobre esta configuración. ![Imagen de la interfaz de usuario de Platform que muestra el vínculo de documentación.](../../assets/authoring-api/destination-configuration/documentation-url.png "URL de documentación"){width="100" zoomable="yes"} |
| `uiAttributes.category` | Cadena | Se refiere a la categoría asignada a su destino en Adobe Experience Platform. Para obtener más información, lea [Categorías de destino](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/destinations/destination-types.html?lang=en#destination-categories). Utilice uno de los siguientes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`. <br/><br/> Consulte [Atributos de interfaz de usuario](../../functionality/destination-configuration/ui-attributes.md) para obtener información detallada sobre esta configuración. |
| `uiAttributes.connectionType` | Cadena | Tipo de conexión, según el destino. Valores compatibles: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul> |
| `uiAttributes.frequency` | Cadena | Se refiere al tipo de exportación de datos compatible con el destino. Establecer como `Streaming` para integraciones basadas en API, o `Batch` al exportar archivos a sus destinos. |
| `identityNamespaces.externalId.acceptsAttributes` | Booleano | Indica si los clientes pueden asignar atributos de perfil estándar a la identidad que está configurando. |
| `identityNamespaces.externalId.acceptsCustomNamespaces` | Booleano | Indica si los clientes pueden asignar identidades que pertenecen a [áreas de nombres personalizadas](/help/identity-service/namespaces.md#manage-namespaces) a la identidad que está configurando. |
| `identityNamespaces.externalId.transformation` | Cadena | _No se muestra en la configuración de ejemplo_. Se utiliza, por ejemplo, cuando la variable [!DNL Platform] El cliente tiene direcciones de correo electrónico simples como atributo y la plataforma solo acepta correos electrónicos con hash. Aquí es donde proporcionaría la transformación que debe aplicarse (por ejemplo, transformar el correo electrónico a minúsculas y luego a hash). |
| `identityNamespaces.externalId.acceptedGlobalNamespaces` | - | Indica qué [áreas de nombres de identidad estándar](/help/identity-service/namespaces.md#standard) (por ejemplo, IDFA) Los clientes pueden asignarse a la identidad que está configurando. <br> Cuando utilice `acceptedGlobalNamespaces`, puede usar `"requiredTransformation":"sha256(lower($))"` a direcciones de correo electrónico en minúsculas y hash o números de teléfono. |
| `destinationDelivery.authenticationRule` | Cadena | Indica cómo [!DNL Platform] los clientes se conectan a su destino. Los valores aceptados son `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>Uso `CUSTOMER_AUTHENTICATION` si los clientes de Platform inician sesión en su sistema mediante un nombre de usuario y una contraseña, un token al portador u otro método de autenticación. Por ejemplo, puede seleccionar esta opción si también selecciona `authType: OAUTH2` o `authType:BEARER` en `customerAuthenticationConfigurations`. </li><li> Uso `PLATFORM_AUTHENTICATION` si hay un sistema de autenticación global entre el Adobe y el destino y la variable [!DNL Platform] El cliente no necesita proporcionar credenciales de autenticación para conectarse al destino. En este caso, debe crear un objeto credentials utilizando la variable [API de credenciales](../../credentials-api/create-credential-configuration.md) configuración. </li><li>Uso `NONE` si no se requiere autenticación para enviar datos a la plataforma de destino. </li></ul> |
| `destinationDelivery.destinationServerId` | Cadena | La variable `instanceId` del [plantilla de servidor de destino](../destination-server/create-destination-server.md) para este destino. |
| `backfillHistoricalProfileData` | Booleano | Controla si los datos del perfil histórico se exportan cuando los segmentos se activan en el destino. Establezca siempre esto como `true`. |
| `segmentMappingConfig.mapUserInput` | Booleano | Controla si el usuario introduce el ID de asignación de segmentos en el flujo de trabajo de activación de destino. |
| `segmentMappingConfig.mapExperiencePlatformSegmentId` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el ID de segmento del Experience Platform. |
| `segmentMappingConfig.mapExperiencePlatformSegmentName` | Booleano | Controla si el ID de asignación de segmentos en el flujo de trabajo de activación de destino es el nombre del segmento del Experience Platform. |
| `segmentMappingConfig.audienceTemplateId` | Booleano | La variable `instanceId` del [plantilla de metadatos de audiencia](../../metadata-api/create-audience-template.md) para este destino. |
| `schemaConfig.profileFields` | Matriz | Al agregar una `profileFields` como se muestra en la configuración anterior, los usuarios tendrán la opción de asignar atributos de Experience Platform a los atributos predefinidos en el lado del destino. |
| `schemaConfig.profileRequired` | Booleano | Uso `true` si los usuarios deben poder asignar atributos de perfil de Experience Platform a atributos personalizados en el lado del destino, como se muestra en el ejemplo de configuración anterior. |
| `schemaConfig.segmentRequired` | Booleano | Utilice siempre `segmentRequired:true`. |
| `schemaConfig.identityRequired` | Booleano | Uso `true` si los usuarios deben poder asignar áreas de nombres de identidad desde el Experience Platform al esquema deseado. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la configuración de destino recién creada.

+++

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo crear una nueva configuración de destino a través del Destination SDK `/authoring/destinations` extremo de API.

Para obtener más información sobre lo que puede hacer con este punto final, consulte los siguientes artículos:

* [Recuperar una configuración de destino](retrieve-destination-configuration.md)
* [Actualizar una configuración de destino](update-destination-configuration.md)
* [Eliminar una configuración de destino](delete-destination-configuration.md)

Para comprender dónde encaja este punto final en el proceso de creación de destino, consulte los siguientes artículos:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)
