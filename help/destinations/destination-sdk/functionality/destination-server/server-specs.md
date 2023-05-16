---
description: Obtenga información sobre cómo configurar las especificaciones del servidor de destino en el Adobe Experience Platform Destination SDK mediante el extremo "/authoring/destination-servers".
title: Especificaciones del servidor para los destinos creados con el Destination SDK
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2750'
ht-degree: 3%

---


# Especificaciones del servidor para los destinos creados con el Destination SDK

Las especificaciones del servidor de destino definen el tipo de plataforma de destino que recibirá los datos de Adobe Experience Platform y los parámetros de comunicación entre Platform y su destino. Por ejemplo:

* A [streaming](#streaming-example) la especificación del servidor de destino define el extremo del servidor HTTP que recibirá los mensajes HTTP de Platform. Para aprender a configurar el formato de las llamadas HTTP al extremo, lea la [plantilla de especificaciones](templating-specs.md) página.
* Un [Amazon S3](#s3-example) la especificación del servidor de destino define [!DNL S3] nombre del contenedor y ruta donde Platform exportará los archivos.
* Un [SFTP](#sftp-example) la especificación del servidor de destino define el nombre de host, el directorio raíz, el puerto de comunicación y el tipo de cifrado del servidor SFTP donde Platform exportará los archivos.

Para comprender dónde encaja este componente en una integración creada con el Destination SDK, consulte el diagrama en la [opciones de configuración](../configuration-options.md) para ver las siguientes páginas de información general sobre la configuración de destino:

* [Usar Destination SDK para configurar un destino de flujo continuo](../../guides/configure-destination-instructions.md#create-server-template-configuratiom)
* [Usar Destination SDK para configurar un destino basado en archivos](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)

Puede configurar las especificaciones del servidor de destino mediante la variable `/authoring/destination-servers` punto final. Consulte las siguientes páginas de referencia de API para ver ejemplos detallados de llamadas de API donde puede configurar los componentes que se muestran en esta página.

* [Crear una configuración de servidor de destino](../../authoring-api/destination-server/create-destination-server.md)
* [Actualizar la configuración del servidor de destino](../../authoring-api/destination-server/update-destination-server.md)

Esta página muestra todos los tipos de servidor de destino admitidos por el Destination SDK, con todos sus parámetros de configuración. Al crear el destino, reemplace los valores de parámetro por los suyos propios.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Tipos de integración compatibles {#supported-integration-types}

Consulte la siguiente tabla para obtener más información sobre los tipos de integraciones que admiten la funcionalidad descrita en esta página.

| Tipo de integración | Admite funcionalidad |
|---|---|
| Integraciones en tiempo real (flujo continuo) | Sí |
| Integraciones basadas en archivos (por lotes) | Sí |

When [creación](../../authoring-api/destination-server/create-destination-server.md) o [actualizar](../../authoring-api/destination-server/update-destination-server.md) como servidor de destino, utilice una de las configuraciones de tipo servidor descritas en esta página. En función de los requisitos de integración, asegúrese de sustituir los valores de parámetro de ejemplo de estos ejemplos por los suyos propios.

## Campos predefinidos frente a campos con plantilla {#templatized-fields}

Al crear un servidor de destino a través de un Destination SDK, puede definir los valores de los parámetros de configuración codificándolos en la configuración o utilizando campos con plantilla. Los campos con plantilla le permiten leer valores proporcionados por el usuario desde la interfaz de usuario de Platform.

Los parámetros del servidor de destino tienen dos campos configurables. Estas opciones dictan si utiliza valores predefinidos o de plantilla.

| Parámetro | Tipo | Descripción |
|---|---|---|
| `templatingStrategy` | Cadena | *Requerido.* Define si hay un valor codificado proporcionado mediante la variable `value` o un valor configurable por el usuario en la interfaz de usuario. Valores compatibles: <ul><li>`NONE`: Utilice este valor cuando esté codificando el valor del parámetro mediante la variable `value` (consulte la fila siguiente). Ejemplo:`"value": "my-storage-bucket"`.</li><li>`PEBBLE_V1`: Utilice este valor cuando quiera que los usuarios proporcionen un valor de parámetro en la interfaz de usuario. Ejemplo: `"value": "{{customerData.bucket}}"`. </li></ul> |
| `value` | Cadena | *Requerido*. Define el valor del parámetro. Tipos de valores compatibles: <ul><li>**Valor codificado de forma rígida**: Utilizar un valor codificado (como `"value": "my-storage-bucket"`) cuando no necesita que los usuarios introduzcan un valor de parámetro en la interfaz de usuario. Cuando se codifica un valor de forma rígida, `templatingStrategy` siempre debe configurarse como `NONE`.</li><li>**Valor con plantilla**: Utilizar un valor con plantilla (por ejemplo, `"value": "{{customerData.bucket}}"`) cuando desee que los usuarios proporcionen un valor de parámetro en la interfaz de usuario. Al utilizar valores con plantillas, `templatingStrategy` siempre debe configurarse como `PEBBLE_V1`.</li></ul> |

{style="table-layout:auto"}

### Cuándo se deben utilizar los campos predefinidos y cuándo los campos con plantilla

Tanto los campos predefinidos como los plantillas tienen sus propios usos en Destination SDK, según el tipo de integración que esté creando.

**Conexión a su destino sin entrada de usuario**

Cuando los usuarios [conéctese a su destino](../../../ui/connect-destination.md) en la interfaz de usuario de Platform, es posible que desee gestionar el proceso de conexión de destino sin introducir datos.

Para ello, puede codificar los parámetros de conexión de la plataforma de destino en la especificación del servidor. Cuando se utilizan valores de parámetro codificados en la configuración del servidor de destino, la conexión entre Adobe Experience Platform y la plataforma de destino se gestiona sin que el usuario introduzca ningún dato.

En el ejemplo siguiente, un socio crea un servidor de destino de zona de aterrizaje de datos con el `path.value` campo codificado.

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

Como resultado, cuando los usuarios pasan por el [tutorial de conexión de destino](../../../ui/connect-destination.md), no verán un [paso de autenticación](../../../ui/connect-destination.md#authenticate). En su lugar, Platform gestiona la autenticación, como se muestra en la imagen siguiente.

![La imagen de la interfaz de usuario muestra la pantalla de autenticación entre Platform y un destino DLZ.](../../assets/functionality/destination-server/server-spec-hardcoded.png)

**Conexión al destino con entrada de usuario**

Cuando la conexión entre Platform y el destino debe establecerse siguiendo una entrada de usuario específica en la interfaz de usuario de Platform, como seleccionar un punto final de API o proporcionar un valor de campo, puede utilizar campos con plantilla en la especificación del servidor para leer la entrada del usuario y conectarse a la plataforma de destino.

En el ejemplo siguiente, un socio crea un [tiempo real (flujo continuo)](#streaming-example) integración y `url.value` field utiliza el parámetro de plantilla `{{customerData.region}}` para personalizar parte del extremo de la API en función de la entrada del usuario.

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

Para dar a los usuarios la opción de seleccionar un valor de la interfaz de usuario de Platform, la variable `region` también debe definirse en la variable [configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) como campo de datos del cliente, como se muestra a continuación:

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

Como resultado, cuando los usuarios pasan por el [tutorial de conexión de destino](../../../ui/connect-destination.md), deben seleccionar una región para poder conectarse a la plataforma de destino. Cuando se conectan al destino, el campo con plantilla `{{customerData.region}}` se reemplaza por el valor que el usuario ha seleccionado en la interfaz de usuario, como se muestra en la imagen siguiente.

![Imagen de interfaz de usuario que muestra la pantalla de conexión de destino con un selector de región.](../../assets/functionality/destination-server/server-spec-template-region.png)

## Servidor de destino en tiempo real (flujo continuo) {#streaming-example}

Este tipo de servidor de destino permite exportar datos de Adobe Experience Platform a su destino mediante solicitudes HTTP. La configuración del servidor contiene información sobre el servidor que recibe los mensajes (el servidor de su parte).

Este proceso envía datos de usuario como una serie de mensajes HTTP a la plataforma de destino. Los parámetros siguientes forman la plantilla de especificaciones del servidor HTTP.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino en tiempo real (flujo continuo).

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
| `name` | Cadena | *Requerido.* Representa un nombre descriptivo del servidor, visible solo para el Adobe. Este nombre no es visible para socios o clientes. Ejemplo: `Moviestar destination server`. |
| `destinationServerType` | Cadena | *Requerido.* Configure esto como `URL_BASED` para destinos de flujo continuo. |
| `templatingStrategy` | Cadena | *Requerido.* <ul><li>Uso `PEBBLE_V1` si está utilizando un campo con plantilla en lugar de un valor codificado en la variable `value` campo . Utilice esta opción si tiene un punto final como: `https://api.moviestar.com/data/{{customerData.region}}/items`, donde los usuarios deben seleccionar la región del extremo en la interfaz de usuario de Platform. </li><li> Uso `NONE` si no se necesita una transformación acelerada en el lado del Adobe, por ejemplo si tiene un punto final como: `https://api.moviestar.com/data/items` </li></ul> |
| `value` | Cadena | *Requerido.* Rellene la dirección del extremo de API al que se debe conectar el Experience Platform. |

{style="table-layout:auto"}

## [!DNL Amazon S3] servidor de destino {#s3-example}

Este servidor de destino permite exportar archivos que contengan datos de Adobe Experience Platform al almacenamiento de Amazon S3.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino de Amazon S3.

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
| `name` | Cadena | El nombre del servidor de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para exportar archivos a un [!DNL Amazon S3] bucket, establezca esto como `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `bucket.value` campo .<ul><li>Si desea que los usuarios introduzcan su propio nombre de bloque en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `value` para leer un valor de [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza un nombre de bloque codificado para la integración, como `"bucket.value":"MyBucket"`y, a continuación, establezca este valor en `NONE`.</li></ul> |
| `fileBasedS3Destination.bucket.value` | Cadena | El nombre del [!DNL Amazon S3] contenedor que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value":"MyBucket"`. |
| `fileBasedS3Destination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `path.value` campo .<ul><li>Si desea que los usuarios introduzcan su propia ruta en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `path.value` para leer un valor de [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza una ruta codificada para la integración, como `"bucket.value":"/path/to/MyBucket"`y, a continuación, establezca este valor en `NONE`.</li></ul> |
| `fileBasedS3Destination.path.value` | Cadena | La ruta al [!DNL Amazon S3] contenedor que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value":"/path/to/MyBucket"`. |

{style="table-layout:auto"}

## [!DNL SFTP] servidor de destino {#sftp-example}

Este servidor de destino le permite exportar archivos que contengan datos de Adobe Experience Platform a su [!DNL SFTP] servidor de almacenamiento.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un destino SFTP.

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
| `name` | Cadena | El nombre del servidor de destino. |
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para exportar archivos a un [!DNL SFTP] destino, configúrelo en `FILE_BASED_SFTP`. |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `rootDirectory.value` campo .<ul><li>Si desea que los usuarios introduzcan su propia ruta de directorio raíz en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `rootDirectory.value` para leer un valor proporcionado por el usuario desde la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza una ruta de directorio raíz codificada para la integración, como `"rootDirectory.value":"Storage/MyDirectory"`y, a continuación, establezca este valor en `NONE`.</li></ul> |
| `fileBasedSFTPDestination.rootDirectory.value` | Cadena | Ruta al directorio que alojará los archivos exportados. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value":"Storage/MyDirectory"` |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `hostName.value` campo .<ul><li>Si desea que los usuarios introduzcan su propio nombre de host en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `hostName.value` para leer un valor proporcionado por el usuario desde la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza un nombre de host codificado para la integración, como `"hostName.value":"my.hostname.com"`y, a continuación, establezca este valor en `NONE`.</li></ul> |
| `fileBasedSFTPDestination.hostName.value` | Cadena | El nombre de host del servidor SFTP. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"hostName.value":"my.hostname.com"`. |
| `port` | Número entero | Puerto del servidor de archivos SFTP. |
| `encryptionMode` | Cadena | Indica si se utiliza el cifrado de archivos. Valores compatibles: <ul><li>PGP</li><li>Ninguna</li></ul> |

{style="table-layout:auto"}

## [!DNL Azure Data Lake Storage] ([!DNL ADLS]) servidor de destino {#adls-example}

Este servidor de destino le permite exportar archivos que contengan datos de Adobe Experience Platform a su [!DNL Azure Data Lake Storage] cuenta.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un [!DNL Azure Data Lake Storage] destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Data Lake Storage] destinos, configúrelo en `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `path.value` campo .<ul><li>Si desea que los usuarios introduzcan sus [!DNL ADLS] ruta de carpeta en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `path.value` para leer un valor de [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza una ruta codificada para la integración, como `"abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/"`y, a continuación, establezca este valor en `NONE`.</li></ul> |
| `fileBasedAdlsGen2Destination.path.value` | Cadena | La ruta a su [!DNL ADLS] carpeta de almacenamiento. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `abfs://<file_system>@<account_name>.dfs.core.windows.net/<path>/`. |

{style="table-layout:auto"}

## [!DNL Azure Blob Storage] servidor de destino {#blob-example}

Este servidor de destino le permite exportar archivos que contengan datos de Adobe Experience Platform a su [!DNL Azure Blob Storage] contenedor.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un [!DNL Azure Blob Storage] destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Azure Blob Storage] destinos, configúrelo en `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `path.value` campo .<ul><li>Si desea que sus usuarios introduzcan sus propios datos [!DNL Azure Blob] [URI de cuenta de almacenamiento](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `path.value` para leer el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza una ruta codificada para la integración, como `"path.value": "https://myaccount.blob.core.windows.net/"`y, a continuación, establezca este valor en `NONE`. |
| `fileBasedAzureBlobDestination.path.value` | Cadena | La ruta a su [!DNL Azure Blob] almacenamiento. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `https://myaccount.blob.core.windows.net/`. |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `container.value` campo .<ul><li>Si desea que sus usuarios introduzcan sus propios datos [!DNL Azure Blob] [nombre del contenedor](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction) en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `container.value` para leer el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza un nombre de contenedor predefinido para la integración, como `"path.value: myContainer"`y, a continuación, establezca este valor en `NONE`. |
| `fileBasedAzureBlobDestination.container.value` | Cadena | Nombre del contenedor de almacenamiento del blob de Azure que se utilizará para este destino. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `myContainer`. |

{style="table-layout:auto"}

## [!DNL Data Landing Zone] ([!DNL DLZ]) servidor de destino {#dlz-example}

Este servidor de destino permite exportar archivos que contengan datos de Platform a un [[!DNL Data Landing Zone]](../../../catalog/cloud-storage/data-landing-zone.md) almacenamiento.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un [!DNL Data Landing Zone] ([!DNL DLZ]).

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Data Landing Zone] destinos, configúrelo en `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `path.value` campo .<ul><li>Si desea que sus usuarios introduzcan sus propios datos [!DNL Data Landing Zone] en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `path.value` para leer un valor de [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza una ruta codificada para la integración, como `"path.value": "https://myaccount.blob.core.windows.net/"`y, a continuación, establezca este valor en `NONE`. |
| `fileBasedDlzDestination.path.value` | Cadena | Ruta a la carpeta de destino que alojará los archivos exportados. |

{style="table-layout:auto"}

## [!DNL Google Cloud Storage] servidor de destino {#gcs-example}

Este servidor de destino le permite exportar archivos que contengan datos de Platform a su [!DNL Google Cloud Storage] cuenta.

El ejemplo siguiente muestra un ejemplo de una configuración de servidor de destino para un [!DNL Google Cloud Storage] destino.

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
| `destinationServerType` | Cadena | Establezca este valor según la plataforma de destino. Para [!DNL Google Cloud Storage] destinos, configúrelo en `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `bucket.value` campo .<ul><li>Si desea que sus usuarios introduzcan sus propios datos [!DNL Google Cloud Storage] nombre del bloque en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `bucket.value` para leer un valor de [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza un nombre de bloque codificado para la integración, como `"bucket.value": "my-bucket"`y, a continuación, establezca este valor en `NONE`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | Cadena | El nombre del [!DNL Google Cloud Storage] contenedor que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value": "my-bucket"`. |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | Cadena | *Requerido*. Establezca este valor según el tipo de valor utilizado en la variable `path.value` campo .<ul><li>Si desea que sus usuarios introduzcan sus propios datos [!DNL Google Cloud Storage] ruta de compartimento en la interfaz de usuario del Experience Platform, establezca este valor en `PEBBLE_V1`. En este caso, debe crear una plantilla de `path.value` para leer un valor de [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario. Este caso de uso se muestra en el ejemplo anterior.</li><li>Si utiliza una ruta codificada para la integración, como `"path.value": "/path/to/my-bucket"`y, a continuación, establezca este valor en `NONE`.</li></ul> |
| `fileBasedGoogleCloudStorageDestination.path.value` | Cadena | La ruta al [!DNL Google Cloud Storage] carpeta que utilizará este destino. Puede ser un campo con plantilla que leerá el valor de la variable [campos de datos del cliente](../destination-configuration/customer-data-fields.md) rellenado por el usuario (como se muestra en el ejemplo anterior) o un valor codificado, como `"value": "/path/to/my-bucket"`. |

{style="table-layout:auto"}

## Pasos siguientes {#next-steps}

Después de leer este artículo, debe comprender mejor qué es una especificación de servidor de destino y cómo puede configurarla.

Para obtener más información sobre los otros componentes del servidor de destino, consulte los siguientes artículos:

* [Plantillas de especificaciones](templating-specs.md)
* [Formato del mensaje](message-format.md)
* [Configuración de formato de archivo](file-formatting.md)
