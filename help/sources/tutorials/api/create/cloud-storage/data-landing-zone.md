---
keywords: Experience Platform;inicio;temas populares;
solution: Experience Platform
title: Conexión de la zona de aterrizaje de datos a Adobe Experience Platform mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Adobe Experience Platform a la zona de aterrizaje de datos mediante la API de Flow Service.
exl-id: bdb60ed3-7c63-4a69-975a-c6f1508f319e
source-git-commit: 0089aa0d6b765645840e6954c3957282c2ad972b
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 5%

---

# Conectar [!DNL Data Landing Zone] a Adobe Experience Platform mediante la API de Flow Service

>[!IMPORTANT]
>
>Esta página es específica para el conector [!DNL Data Landing Zone] *source* en el Experience Platform. Para obtener información sobre cómo conectarse al conector [!DNL Data Landing Zone] *destination*, consulte la [[!DNL Data Landing Zone] página de documentación de destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md).

[!DNL Data Landing Zone] es una función de almacenamiento de archivos segura y basada en la nube que permite traer archivos a Adobe Experience Platform. Los datos se eliminan automáticamente de [!DNL Data Landing Zone] pasados siete días.

Este tutorial lo guiará por los pasos para crear una conexión de origen de [!DNL Data Landing Zone] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/). Este tutorial también proporciona instrucciones sobre cómo recuperar su [!DNL Data Landing Zone], así como ver y actualizar sus credenciales.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para crear correctamente una conexión de origen de [!DNL Data Landing Zone] mediante la API [!DNL Flow Service].

Este tutorial también requiere que lea la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md) para aprender a autenticarse en las API de Platform e interpretar las llamadas de ejemplo proporcionadas en la documentación.

## Recuperación de una zona de aterrizaje utilizable

El primer paso para usar las API para obtener acceso a [!DNL Data Landing Zone] es realizar una solicitud de GET al extremo `/landingzone` de la API [!DNL Connectors] y, al mismo tiempo, proporcionar `type=user_drop_zone` como parte del encabezado de la solicitud.

**Formato de API**

```http
GET /data/foundation/connectors/landingzone?type=user_drop_zone
```

| Encabezados | Descripción |
| --- | --- |
| `user_drop_zone` | El tipo `user_drop_zone` permite a la API distinguir un contenedor de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |

**Solicitud**

La siguiente solicitud recupera una zona de aterrizaje existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' 
```

**Respuesta**

La siguiente respuesta devuelve información sobre una zona de aterrizaje, incluidos sus `containerName` y `containerTTL` correspondientes.

```json
{
    "containerName": "dlz-user-container",
    "containerTTL": "7"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | El nombre de la zona de aterrizaje que ha recuperado. |
| `containerTTL` | El tiempo de caducidad (en días) aplicado a los datos dentro de la zona de aterrizaje. Cualquier valor dentro de una zona de aterrizaje determinada se elimina después de siete días. |

## Recuperar credenciales de [!DNL Data Landing Zone]

Para recuperar las credenciales de un(a) [!DNL Data Landing Zone], realice una solicitud de GET al extremo `/credentials` de la API [!DNL Connectors].

**Formato de API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=user_drop_zone
```

**Solicitud**

El siguiente ejemplo de solicitud recupera las credenciales de una zona de aterrizaje existente.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve la información de credenciales de la zona de aterrizaje de datos, incluidos los datos actuales `SASToken`, `SASUri`, `storageAccountName` y la fecha de caducidad.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-ed86a61d-201f-4b50-b10f-a1bf173066fd&sr=c&sp=racwdlm&sig=4yTba8voU3L0wlcLAv9mZLdZ7NlMahbfYYPTMkQ6ZGU%3D",
    "expiryDate": "2024-01-06"
}
```

| Propiedad | Descripción |
| --- | --- |
| `containerName` | El nombre de su zona de aterrizaje. |
| `SASToken` | El token de firma de acceso compartido para su zona de aterrizaje. Esta cadena contiene toda la información necesaria para autorizar una solicitud. |
| `SASUri` | El URI de firma de acceso compartido para su zona de aterrizaje. Esta cadena es una combinación del URI de la zona de aterrizaje para la que se está autenticando y su token SAS correspondiente, |
| `expiryDate` | La fecha en la que caducará su token SAS. Debe actualizar el token antes de la fecha de caducidad para poder seguir utilizándolo en la aplicación para cargar datos en la zona de aterrizaje de datos. Si no actualiza manualmente el token antes de la fecha de caducidad indicada, se actualizará automáticamente y proporcionará un nuevo token cuando se realice la llamada de credenciales de GET. |


## Actualizar credenciales de [!DNL Data Landing Zone]

Puede actualizar su `SASToken` realizando una solicitud de POST al extremo `/credentials` de la API [!DNL Connectors].

**Formato de API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh
```

| Encabezados | Descripción |
| --- | --- |
| `user_drop_zone` | El tipo `user_drop_zone` permite a la API distinguir un contenedor de zona de aterrizaje de otros tipos de contenedores disponibles para usted. |
| `refresh` | La acción `refresh` le permite restablecer las credenciales de su zona de aterrizaje y generar automáticamente un nuevo `SASToken`. |

**Solicitud**

La siguiente solicitud actualiza las credenciales de la zona de aterrizaje.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=user_drop_zone&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

**Respuesta**

La siguiente respuesta devuelve valores actualizados para su `SASToken` y `SASUri`.

```json
{
    "containerName": "dlz-user-container",
    "SASToken": "sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "storageAccountName": "dlblobstore99hh25i3dflek",
    "SASUri": "https://dlblobstore99hh25i3dflek.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-9c4d03b8-a6ff-41be-9dcf-20123e717e99&sr=c&sp=racwdlm&sig=JbRMoDmFHQU4OWOpgrKdbZ1d%2BkvslO35%2FXTqBO%2FgbRA%3D",
    "expiryDate": "2024-01-06"
}
```

## Explorar la estructura y el contenido del archivo de zona de aterrizaje

Puede explorar la estructura de archivos y el contenido de su zona de aterrizaje realizando una solicitud de GET al extremo `connectionSpecs` de la API [!DNL Flow Service].

**Formato de API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | Identificador de especificación de conexión que corresponde a [!DNL Data Landing Zone]. Este identificador fijo es: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de archivos y carpetas encontrados dentro del directorio consultado. Tome nota de la propiedad `path` del archivo que desea cargar, ya que debe proporcionarla en el siguiente paso para inspeccionar su estructura.

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

## Previsualizar la estructura y el contenido del archivo de zona de aterrizaje

Para inspeccionar la estructura de un archivo en la zona de aterrizaje, realice una solicitud de GET y proporcione la ruta y el tipo del archivo como parámetro de consulta.

**Formato de API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}
```

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `{CONNECTION_SPEC_ID}` | Identificador de especificación de conexión que corresponde a [!DNL Data Landing Zone]. Este identificador fijo es: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |
| `{OBJECT_TYPE}` | El tipo de objeto al que desea acceder. | `file` |
| `{OBJECT}` | Ruta de acceso y nombre del objeto al que desea tener acceso. | `dlz-user-container/data8.csv` |
| `{FILE_TYPE}` | El tipo de archivo. | <ul><li>`delimited`</li><li>`json`</li><li>`parquet`</li></ul> |
| `{PREVIEW}` | Un valor booleano que define si se admite la vista previa del archivo. | </ul><li>`true`</li><li>`false`</li></ul> |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/data8.csv&fileType=delimited&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado, incluidos los nombres de archivo y los tipos de datos.

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

### Usar `determineProperties` para detectar automáticamente la información de propiedad de archivo de un [!DNL Data Landing Zone]

Puede usar el parámetro `determineProperties` para detectar automáticamente la información de propiedad del contenido del archivo de su [!DNL Data Landing Zone] al realizar una llamada de GET para explorar el contenido y la estructura de su origen.

#### `determineProperties` casos de uso

En la tabla siguiente se describen diferentes escenarios que se pueden encontrar al usar el parámetro de consulta `determineProperties` o al proporcionar manualmente información sobre el archivo.

| `determineProperties` | `queryParams` | Respuesta |
| --- | --- | --- |
| True | N/A | Si se proporciona `determineProperties` como parámetro de consulta, se detectarán las propiedades del archivo y la respuesta devolverá una nueva clave `properties` que incluye información sobre el tipo de archivo, el tipo de compresión y el delimitador de columna. |
| N/A | True | Si los valores de tipo de archivo, tipo de compresión y delimitador de columna se proporcionan manualmente como parte de `queryParams`, se utilizarán para generar el esquema y se devolverán las mismas propiedades como parte de la respuesta. |
| True | True | Si ambas opciones se realizan simultáneamente, se devuelve un error. |
| N/A | N/A | Si no se proporciona ninguna de las dos opciones, se devuelve un error porque no hay forma de obtener propiedades para la respuesta. |

**Formato de API**

```http
GET /connectionSpecs/{CONNECTION_SPEC_ID}/explore?objectType=file&object={OBJECT}&fileType={FILE_TYPE}&preview={PREVIEW}&determineProperties=true
```

| Parámetro | Descripción | Ejemplo |
| --- | --- | --- |
| `determineProperties` | Este parámetro de consulta permite que la API [!DNL Flow Service] detecte información relativa a las propiedades del archivo, incluida información sobre el tipo de archivo, el tipo de compresión y el delimitador de columna. | `true` |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/26f526f2-58f4-4712-961d-e41bf1ccc0e8/explore?objectType=file&object=dlz-user-container/garageWeek/file1&preview=true&determineProperties=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado, incluidos los nombres de archivo y los tipos de datos, así como una clave `properties`, que contiene información sobre `fileType`, `compressionType` y `columnDelimiter`.

+++Haga clic aquí

```json
{
    "properties": {
        "fileType": "delimited",
        "compressionType": "tarGzip",
        "columnDelimiter": "~"
    },
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "firstName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "lastName",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "email",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "birthday",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "birthday": "1313-0505-19731973",
            "firstName": "Yvonne",
            "lastName": "Thilda",
            "id": "100",
            "email": "Yvonne.Thilda@yopmail.com"
        },
        {
            "birthday": "1515-1212-19731973",
            "firstName": "Mary",
            "lastName": "Pillsbury",
            "id": "101",
            "email": "Mary.Pillsbury@yopmail.com"
        },
        {
            "birthday": "0505-1010-19751975",
            "firstName": "Corene",
            "lastName": "Joeann",
            "id": "102",
            "email": "Corene.Joeann@yopmail.com"
        },
        {
            "birthday": "2727-0303-19901990",
            "firstName": "Dari",
            "lastName": "Greenwald",
            "id": "103",
            "email": "Dari.Greenwald@yopmail.com"
        },
        {
            "birthday": "1717-0404-19651965",
            "firstName": "Lucy",
            "lastName": "Magdalen",
            "id": "199",
            "email": "Lucy.Magdalen@yopmail.com"
        }
    ]
}
```

+++

| Propiedad | Descripción |
| --- | --- |
| `properties.fileType` | El tipo de archivo correspondiente del archivo consultado. Los tipos de archivo admitidos son: `delimited`, `json` y `parquet`. |
| `properties.compressionType` | El tipo de compresión correspondiente utilizado para el archivo consultado. Los tipos de compresión admitidos son: <ul><li>`bzip2`</li><li>`gzip`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `properties.columnDelimiter` | El delimitador de columna correspondiente utilizado para el archivo consultado. Cualquier valor de carácter único es un delimitador de columna admisible. El valor predeterminado es una coma `(,)`. |


## Crear una conexión de origen

Una conexión de origen crea y administra la conexión con el origen externo desde el que se incorporan los datos. Una conexión de origen consta de información como el origen de datos, el formato de datos y el ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica de un inquilino y una organización.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | Nombre de su conexión de origen [!DNL Data Landing Zone]. |
| `data.format` | El formato de los datos que desea llevar a Platform. |
| `params.path` | La ruta al archivo que desea llevar a Platform. |
| `connectionSpec.id` | Identificador de especificación de conexión que corresponde a [!DNL Data Landing Zone]. Este identificador fijo es: `26f526f2-58f4-4712-961d-e41bf1ccc0e8`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "f5b46949-8c8d-4613-80cc-52c9c039e8b9",
    "etag": "\"1400d460-0000-0200-0000-613be3520000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha recuperado las credenciales de [!DNL Data Landing Zone], ha explorado su estructura de archivos para encontrar el archivo que desea llevar a Platform y ha creado una conexión de origen para empezar a llevar los datos a Platform. Ahora puede continuar con el siguiente tutorial, donde aprenderá a [crear un flujo de datos para llevar datos de almacenamiento en la nube a Platform mediante la [!DNL Flow Service] API](../../collect/cloud-storage.md).
