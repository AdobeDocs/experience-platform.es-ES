---
keywords: Experience Platform;inicio;temas populares;
solution: Experience Platform
title: Conexión de la zona de aterrizaje de datos a Adobe Experience Platform mediante la API del servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a la zona de aterrizaje de datos mediante la API de servicio de flujo.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 57089cc9aa9c586f5fae70e2a7154d48ebd62447
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 4%

---

# Conectar [!DNL Data Landing Zone] a Adobe Experience Platform mediante la API de servicio de flujo

[!DNL Data Landing Zone] es una funcionalidad de almacenamiento de datos basada en la nube para el almacenamiento temporal de archivos aprovisionado con Adobe Experience Platform. Los datos se eliminan automáticamente del [!DNL Data Landing Zone] después de siete días.

Este tutorial le explica cómo crear una conexión de origen [!DNL Data Landing Zone] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Este tutorial también proporciona instrucciones sobre cómo recuperar su [!DNL Data Landing Zone], así como la forma de ver y actualizar sus credenciales.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para crear correctamente una conexión de origen [!DNL Data Landing Zone] mediante la API [!DNL Flow Service].

Este tutorial también requiere que lea la guía de [introducción a las API de plataforma](../../../../../landing/api-guide.md) para aprender a autenticarse en las API de plataforma e interpretar las llamadas de ejemplo proporcionadas en la documentación.

## Recuperar una zona de aterrizaje utilizable

El primer paso para utilizar API para acceder a [!DNL Data Landing Zone] es realizar una solicitud de GET al extremo `/landingzone` de la API [!DNL Connectors] mientras proporciona `type=user_drop_zone` como parte del encabezado de la solicitud.

**Formato de API**

```http
GET /connectors/landingzone?type=user_drop_zone
```

| Encabezados | Descripción |
| --- | --- |
| `user_drop_zone` | El tipo `user_drop_zone` permite que la API distinga un contenedor de zona de aterrizaje de los demás tipos de contenedores disponibles. |

**Solicitud**

La siguiente solicitud recupera una zona de aterrizaje existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Respuesta**

La siguiente respuesta devuelve información sobre una zona de aterrizaje, incluidas sus correspondientes `containerName` y `containerTTL`.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | Nombre de la zona de aterrizaje que recuperó. |
| `containerTTL` | La configuración de tiempo de vida aplicada a sus datos dentro de la zona de aterrizaje. Cualquier valor de una zona de aterrizaje determinada se elimina al cabo de siete días. |

## Recuperar [!DNL Data Landing Zone] credenciales

Para recuperar las credenciales para un [!DNL Data Landing Zone], realice una solicitud de GET al extremo `/credentials` de la API [!DNL Connectors].

**Formato de API**

```http
GET /connectors/landingzone/credentials?type=user_drop_zone
```

**Solicitud**

El siguiente ejemplo de solicitud recupera las credenciales de una zona de aterrizaje existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve la información de credenciales para su zona de aterrizaje, incluidos los `SASToken` y `SASUri` actuales, así como el `storageAccountName` que corresponde al contenedor de su zona de aterrizaje.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | Nombre de la zona de aterrizaje. |
| `SASToken` | Token de firma de acceso compartido para su zona de aterrizaje. Esta cadena contiene toda la información necesaria para autorizar una solicitud. |
| `SASUri` | El URI de firma de acceso compartido para su zona de aterrizaje. Esta cadena es una combinación de la URI con la zona de aterrizaje a la que se está autenticando y su token SAS correspondiente, |


## Actualizar [!DNL Data Landing Zone] credenciales

Puede actualizar su `SASToken` realizando una solicitud de POST al extremo `/credentials` de la API [!DNL Connectors].

**Formato de API**

```http
POST /connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Encabezados | Descripción |
| --- | --- |
| `user_drop_zone` | El tipo `user_drop_zone` permite que la API distinga un contenedor de zona de aterrizaje de los demás tipos de contenedores disponibles. |
| `refresh` | La acción `refresh` le permite restablecer sus credenciales de zona de aterrizaje y generar automáticamente un nuevo `SASToken`. |

**Solicitud**

La siguiente solicitud actualiza las credenciales de la zona de aterrizaje.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve valores actualizados para sus `SASToken` y `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D"
}
```

## Explorar la estructura y el contenido del archivo de la zona de aterrizaje

Puede explorar la estructura de archivos y el contenido de su zona de aterrizaje realizando una solicitud de GET al extremo `connectionSpecs` de la API [!DNL Flow Service].

**Formato de API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | El ID de especificación de conexión que corresponde a [!DNL Data Landing Zone]. Este ID fijo es: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de archivos y carpetas que se encuentran en el directorio consultado. Tenga en cuenta la propiedad `path` del archivo que desea cargar, ya que debe proporcionarla en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "file",
        "name": "account.csv",
        "path": "dlz-user-container/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "data8.csv",
        "path": "dlz-user-container/data8.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "folder",
        "name": "userdata1",
        "path": "dlz-user-container/userdata1/",
        "canPreview": false,
        "canFetchSchema": false
    }
]
```

## Vista previa de la estructura y el contenido del archivo de la zona de aterrizaje

Para inspeccionar la estructura de un archivo en la zona de aterrizaje, realice una solicitud de GET y proporcione la ruta del archivo y escriba como parámetro de consulta.

**Formato de API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | El ID de especificación de conexión que corresponde a [!DNL Data Landing Zone]. Este ID fijo es: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | Tipo del objeto al que desea acceder. | `file` |
| `{OBJECT}` | Ruta y nombre del objeto al que desea acceder. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | Tipo de archivo. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Un valor booleano que define si se admite la previsualización de archivos. | </ul><li>`true`</li><li>`false`</li></ul> |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado, incluidos los nombres de tabla y los tipos de datos.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "FirstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "LastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Email": "rsmith@abc.com",
            "FirstName": "Richard",
            "Phone": "111111111",
            "Id": "12345",
            "LastName": "Smith"
        },
        {
            "Email": "morgan@bac.com",
            "FirstName": "Morgan",
            "Phone": "22222222222",
            "Id": "67890",
            "LastName": "Hart"
        }
    ]
}
```

## Crear una conexión de origen

Una conexión de origen crea y administra la conexión con el origen externo desde el que se introducen los datos. Una conexión de origen consiste en información como el origen de datos, el formato de datos y el ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica para un inquilino y una organización IMS.

Para crear una conexión de origen, realice una solicitud de POST al extremo `/sourceConnections` de la API [!DNL Flow Service].


**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Data Landing Zone source connection",
        "data": {
            "format": "delimited"
        },
        "params": {
            "path": "dlz-user-container/data8.csv"
        },
        "connectionSpec": {
            "id": "26f526f2-58f4-4712-961d-e41bf1ccc0e8",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | El nombre de la conexión de origen [!DNL Data Landing Zone]. |
| `data.format` | El formato de los datos que desea traer a Platform. |
| `params.path` | La ruta al archivo que desea traer a Platform. |
| `connectionSpec.id` | El ID de especificación de conexión que corresponde a [!DNL Data Landing Zone]. Este ID fijo es: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha recuperado sus credenciales [!DNL Data Landing Zone], ha explorado su estructura de archivos para encontrar el archivo que desea traer a Platform y ha creado una conexión de origen para empezar a llevar los datos a Platform. Ahora puede continuar con el siguiente tutorial, en el que aprenderá a [crear un flujo de datos para traer datos de almacenamiento en la nube a Platform mediante la  [!DNL Flow Service] API](../../collect/cloud-storage.md).
