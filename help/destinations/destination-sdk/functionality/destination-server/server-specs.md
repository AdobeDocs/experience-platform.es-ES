---
description: Aprenda a configurar las especificaciones del servidor de destino en el Adobe Experience Platform Destination SDK a través del punto de conexión /authoring/destination-servers.
title: Especificaciones del servidor para destinos creados con Destination SDK
exl-id: 62202edb-a954-42ff-9772-863cea37a889
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2739'
ht-degree: 2%

---

# Especificaciones del servidor para destinos creados con Destination SDK

Las especificaciones del servidor de destino definen el tipo de plataforma de destino que recibirá los datos de Adobe Experience Platform y los parámetros de comunicación entre Platform y el destino. Por ejemplo:

* Una especificación de servidor de destino [streaming](#streaming-example) define el extremo del servidor HTTP que recibirá los mensajes HTTP de Platform. Para aprender a configurar el formato de las llamadas HTTP al extremo, lea la página [especificaciones de creación de plantillas](templating-specs.md).
* Una especificación de servidor de destino [Amazon S3](#s3-example) define el nombre del contenedor [!DNL S3] y la ruta donde Platform exportará los archivos.
* Una especificación de servidor de destino [SFTP](#sftp-example) define el nombre de host, el directorio raíz, el puerto de comunicación y el tipo de cifrado del servidor SFTP donde Platform exportará los archivos.

Para saber dónde encaja este componente en una integración creada con Destination SDK, consulte el diagrama en la documentación de [opciones de configuración](../configuration-options.md) o consulte las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Puede configurar las especificaciones del servidor de destino a través del extremo `/authoring/destination-servers`. Consulte las siguientes páginas de referencia de la API para ver ejemplos detallados de llamadas de la API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Actualizar la configuración de un servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página muestra todos los tipos de servidores de destino admitidos por Destination SDK, con todos sus parámetros de configuración. Al crear el destino, reemplace los valores de parámetro por los suyos propios.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Tipos de integración admitidos {#supported-integration-types}

Consulte la tabla siguiente para obtener detalles sobre qué tipos de integraciones admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (streaming) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

Al [crear](../../authoring-api/destination-server/create-destination-server.md) o [actualizar](../../authoring-api/destination-server/update-destination-server.md) un servidor de destino, use una de las configuraciones de tipo de servidor descritas en esta página. Según los requisitos de integración, asegúrese de reemplazar los valores de parámetro de muestra de estos ejemplos por los suyos propios.

## Campos no codificados frente a campos con plantillas {#templatized-fields}

Al crear un servidor de destino a través de Destination SDK, puede definir los valores de los parámetros de configuración mediante su codificación en la configuración o utilizando campos con plantilla. Los campos con plantilla le permiten leer valores proporcionados por el usuario desde la interfaz de usuario de Platform.

Los parámetros del servidor de destino tienen dos campos configurables. Estas opciones dictan si está utilizando valores codificados o con plantillas.

| Parámetro | Tipo | Descripción |
|---|---|---|
| `templatingStrategy` | Cadena | *Requerido.* Define si hay un valor codificado mediante el campo `value` o un valor configurable por el usuario en la interfaz de usuario. Valores compatibles: <ul><li>`NONE`: utilice este valor cuando esté codificando el valor del parámetro a través del parámetro `value` (consulte la fila siguiente). Ejemplo:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: utilice este valor cuando desee que los usuarios proporcionen un valor de parámetro en la interfaz de usuario. Ejemplo: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Cadena | *Requerido*. Define el valor del parámetro. Tipos de valores admitidos: <ul><li>**Valor codificado**: use un valor codificado (como `"value": "my-storage-bucket"`) cuando no necesite que los usuarios introduzcan un valor de parámetro en la interfaz de usuario. Al codificar un valor, `templatingStrategy` siempre se debe establecer en `NONE`.</li><li>**Valor con plantilla**: use un valor con plantilla (como `"value": "{{customerData.bucket}}"`) cuando desee que los usuarios proporcionen un valor de parámetro en la interfaz de usuario. Cuando se usan valores con plantilla, `templatingStrategy` siempre se debe establecer en `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Cuándo utilizar campos con código o con plantilla

Los campos con plantilla y los campos codificados tienen sus propios usos en Destination SDK, según el tipo de integración que cree.

**Conectando con el destino sin la entrada del usuario**

Cuando los usuarios [se conectan a su destino](../../../ui/connect-destination.md) en la interfaz de usuario de Platform, es posible que desee controlar el proceso de conexión de destino sin sus datos de entrada.

Para ello, puede codificar de forma rígida los parámetros de conexión de la plataforma de destino en la especificación del servidor. Cuando se utilizan valores de parámetros codificados de forma rígida en la configuración del servidor de destino, la conexión entre Adobe Experience Platform y la plataforma de destino se gestiona sin que el usuario tenga que realizar ninguna entrada.

En el ejemplo siguiente, un socio crea un servidor de destino de zona de aterrizaje de datos con el campo `path.value` codificado.

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"NONE",
         "value":"Your/hardcoded/path/here"
      },
      "useCase": "Your use case"
   }
}
```

Como resultado, cuando los usuarios vayan a través del [tutorial de conexión de destino](../../../ui/connect-destination.md), no verán un [paso de autenticación](../../../ui/connect-destination.md#authenticate). En su lugar, Platform gestiona la autenticación, como se muestra en la siguiente imagen.

![Imagen de interfaz de usuario que muestra la pantalla de autenticación entre Platform y un destino DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Conectando con el destino mediante la entrada del usuario**

Cuando se debe establecer la conexión entre Platform y el destino después de una entrada específica del usuario en la interfaz de usuario de Platform, como seleccionar un punto final de API o proporcionar un valor de campo, puede utilizar campos con plantilla en la especificación del servidor para leer la entrada del usuario y conectarse a la plataforma de destino.

En el ejemplo siguiente, un socio crea una integración de [real-time (streaming)](#streaming-example) y el campo `url.value` usa el parámetro con plantilla `{{customerData.region}}` para personalizar parte del extremo de la API en función de la entrada del usuario.

```json
{
   "name":"Templatized API endpoint example",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.yourcompany.com/data/{{customerData.region}}/items"
      }
   }
}
```

Para dar a los usuarios la opción de seleccionar un valor en la interfaz de usuario de Platform, el parámetro `region` también debe definirse en la [configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) como campo de datos de cliente, como se muestra a continuación:

```json
"customerDataFields":[
   {
      "name":"region",
      "title":"Region",
      "description":"Select an option",
      "type":"string",
      "isRequired":true,
      "readOnly":false,
      "enum":[
         "US",
         "EU"
      ]
   }
```

Como resultado, cuando los usuarios pasan por el [tutorial de conexión de destino](../../../ui/connect-destination.md), deben seleccionar una región para poder conectarse a la plataforma de destino. Cuando se conectan al destino, el campo con plantilla `{{customerData.region}}` se reemplaza con el valor que el usuario ha seleccionado en la interfaz de usuario, como se muestra en la siguiente imagen.

![Imagen de la interfaz de usuario que muestra la pantalla de conexión de destino con un selector de región.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Servidor de destino en tiempo real (streaming) {#streaming-example}

Este tipo de servidor de destino le permite exportar datos de Adobe Experience Platform a su destino a través de solicitudes HTTP. La configuración del servidor contiene información sobre el servidor que recibe los mensajes (el servidor de su lado).

Este proceso envía datos de usuario como una serie de mensajes HTTP a la plataforma de destino. Los parámetros siguientes forman la plantilla de especificaciones del servidor HTTP.

El siguiente ejemplo muestra un ejemplo de configuración de servidor de destino para un destino de tiempo real (flujo continuo).

```json
{
   "name":"Your destination server name",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{YOUR_API_ENDPOINT}"
      }
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | *Requerido.* representa un nombre descriptivo de su servidor, visible solamente para el Adobe. Este nombre no es visible para socios o clientes. Ejemplo: `Moviestar destination server`. |
| `destinationServerType` | Cadena | *Requerido.* estableció esto en `URL_BASED` para destinos de flujo continuo. |
| `templatingStrategy` | Cadena | *Requerido.* <ul><li>Use `PEBBLE_V1` si está usando un campo con plantilla en lugar de un valor codificado en el campo `value`. Utilice esta opción si tiene un extremo como: `https://api.moviestar.com/data/{{customerData.region}}/items`, donde los usuarios deben seleccionar la región del extremo en la interfaz de usuario de Platform. </li><li> Utilice `NONE` si no se necesita ninguna transformación con plantilla en el lado del Adobe, por ejemplo, si tiene un extremo como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Cadena | *Requerido.* Rellene la dirección del extremo de API al que el Experience Platform debe conectarse. |

{style="table-layout:auto"}

## [!DNL Amazon S3] servidor de destino {#s3-example}

Este servidor de destino le permite exportar archivos que contienen datos de Adobe Experience Platform a su almacenamiento de Amazon S3.

El siguiente ejemplo muestra un ejemplo de configuración de servidor de destino para un destino de Amazon S3.

```json
{
   "name":"Amazon S3 destination",
   "destinationServerType":"FILE_BASED_S3",
   "fileBasedS3Destination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre del servidor de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para exportar archivos a un bloque de [!DNL Amazon S3], establézcalo en `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `bucket.value`.<ul><li>Si desea que los usuarios introduzcan su propio nombre de contenedor en la interfaz de usuario de Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `value` para leer un valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando un nombre de contenedor predefinido para su integración, como `"bucket.value":"MyBucket"`, establezca este valor en `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Cadena | Nombre del contenedor [!DNL Amazon S3] que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `path.value`.<ul><li>Si desea que los usuarios introduzcan su propia ruta de acceso en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `path.value` para leer un valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando una ruta de acceso codificada para su integración, como `"bucket.value":"/path/to/MyBucket"`, establezca este valor en `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Cadena | Ruta de acceso al bloque [!DNL Amazon S3] que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] servidor de destino {#sftp-example}

Este servidor de destino le permite exportar archivos que contengan datos de Adobe Experience Platform a su servidor de almacenamiento [!DNL SFTP].

El siguiente ejemplo muestra un ejemplo de configuración de servidor de destino para un destino SFTP.

```json
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      },
      "hostName":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.hostName}}"
      },
      "port":22,
      "encryptionMode":"PGP"
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre del servidor de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para exportar archivos a un destino [!DNL SFTP], establezca este valor en `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `rootDirectory.value`.<ul><li>Si desea que los usuarios introduzcan su propia ruta de acceso al directorio raíz en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `rootDirectory.value` para leer un valor proporcionado por el usuario de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando una ruta de directorio raíz codificada de forma rígida para su integración, como `"rootDirectory.value":"Storage/MyDirectory"`, establezca este valor en `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Cadena | Ruta al directorio que alojará los archivos exportados. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `hostName.value`.<ul><li>Si desea que los usuarios introduzcan su propio nombre de host en la interfaz de usuario de Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `hostName.value` para leer un valor proporcionado por el usuario de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando un nombre de host predefinido para su integración, como `"hostName.value":"my.hostname.com"`, establezca este valor en `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Cadena | El nombre de host del servidor SFTP. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"hostName.value":"my.hostname.com"`. |
| `port` | Entero | El puerto del servidor de archivos SFTP. |
| `encryptionMode` | Cadena | Indica si se debe utilizar el cifrado de archivos. Valores compatibles: <ul><li>PGP</li><li>Ninguna</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) servidor de destino {#adls-example}

Este servidor de destino le permite exportar archivos que contengan datos de Adobe Experience Platform a su cuenta de [!DNL Azure Data Lake Storage].

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino [!DNL Azure Data Lake Storage].

```json
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, establezca esto en `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `path.value`.<ul><li>Si desea que los usuarios introduzcan su ruta de acceso a la carpeta [!DNL ADLS] en la interfaz de usuario de Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `path.value` para leer un valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando una ruta de acceso codificada para su integración, como `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`, establezca este valor en `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Cadena | Ruta de acceso a la carpeta de almacenamiento [!DNL ADLS]. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] servidor de destino {#blob-example}

Este servidor de destino le permite exportar archivos que contienen datos de Adobe Experience Platform a su contenedor de [!DNL Azure Blob Storage].

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino [!DNL Azure Blob Storage].

```json
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Blob Storage] destinos, establezca esto en `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `path.value`.<ul><li>Si desea que los usuarios introduzcan su propio [!DNL Azure Blob] [URI de cuenta de almacenamiento](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `path.value` para leer el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando una ruta de acceso codificada para su integración, como `"path.value": "https://myaccount.blob.core.windows.net/"`, establezca este valor en `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Cadena | Ruta de acceso al almacenamiento de [!DNL Azure Blob]. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `container.value`.<ul><li>Si desea que los usuarios introduzcan su propio [!DNL Azure Blob] [nombre de contenedor](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `container.value` para leer el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando un nombre de contenedor predefinido para su integración, como `"path.value: myContainer"`, establezca este valor en `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Cadena | Nombre del contenedor de almacenamiento del blob de Azure que se utilizará para este destino. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) servidor de destino {#dlz-example}

Este servidor de destino le permite exportar archivos que contienen datos de Platform a un almacenamiento de [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md).

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino [!DNL Data Landing Zone] ([!DNL DLZ]).

```json
{
   "name":"Data Landing Zone destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Data Landing Zone] destinos, establezca esto en `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `path.value`.<ul><li>Si desea que los usuarios introduzcan su propia cuenta de [!DNL Data Landing Zone] en la interfaz de usuario de Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `path.value` para leer un valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando una ruta de acceso codificada para su integración, como `"path.value": "https://myaccount.blob.core.windows.net/"`, establezca este valor en `NONE`. |
| `fileBasedDlzDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] servidor de destino {#gcs-example}

Este servidor de destino le permite exportar archivos que contengan datos de Platform a su cuenta de [!DNL Google Cloud Storage].

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino [!DNL Google Cloud Storage].

```json
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   }
}
```

| Parámetro | Tipo | Descripción |
|---|---|---|
| `name` | Cadena | Nombre de la conexión de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Google Cloud Storage] destinos, establezca esto en `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `bucket.value`.<ul><li>Si desea que los usuarios introduzcan su propio nombre de contenedor de [!DNL Google Cloud Storage] en la interfaz de usuario de Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `bucket.value` para leer un valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando un nombre de contenedor predefinido para su integración, como `"bucket.value": "my-bucket"`, establezca este valor en `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Cadena | Nombre del contenedor [!DNL Google Cloud Storage] que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en el campo `path.value`.<ul><li>Si desea que los usuarios introduzcan su propia ruta de acceso del bloque [!DNL Google Cloud Storage] en la interfaz de usuario de Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla del campo `path.value` para leer un valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si está usando una ruta de acceso codificada para su integración, como `"path.value": "/path/to/my-bucket"`, establezca este valor en `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Cadena | Ruta de acceso a la carpeta [!DNL Google Cloud Storage] que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de los [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenados por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debería comprender mejor qué es una especificación de servidor de destino y cómo puede configurarla.

Para obtener más información acerca de los demás componentes del servidor de destino, consulte los siguientes artículos:

* [Especificaciones de plantilla](templating-specs.md)
* [Formato del mensaje](message-format.md)
* [Configuración de formato de archivo](file-formatting.md)
