---
keywords: Experience Platform;inicio;temas populares;almacenamiento en la nube;almacenamiento en la nube
title: Exploración de carpetas de almacenamiento en la nube mediante la API de Flow Service
description: Este tutorial utiliza la API de Flow Service para explorar un sistema de almacenamiento en la nube de terceros.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 9b9803b4d2aeb2a86ef980f34ee34909679ea3d9
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 4%

---

# Explorar las carpetas de almacenamiento en la nube mediante la API [!DNL Flow Service]

Este tutorial proporciona pasos sobre cómo explorar y previsualizar la estructura y el contenido de su almacenamiento en la nube mediante la API [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
>Para explorar el almacenamiento en la nube, ya debe tener un ID de conexión base válido para un origen de almacenamiento en la nube. Si no tiene este identificador, consulte la [descripción general de orígenes](../../../home.md#cloud-storage) para obtener una lista de orígenes de almacenamiento en la nube con los que puede crear una conexión base.

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../landing/api-guide.md).

## Explorar las carpetas de almacenamiento en la nube

Puede recuperar información sobre la estructura de sus carpetas de almacenamiento en la nube realizando una solicitud de GET a la API [!DNL Flow Service] y proporcionando al mismo tiempo el ID de conexión base de su origen.

Al realizar solicitudes de GET para explorar el almacenamiento en la nube, debe incluir los parámetros de consulta que se enumeran en la siguiente tabla:

| Parámetro | Descripción |
| --------- | ----------- |
| `objectType` | El tipo de objeto que desea explorar. Establezca este valor como: <ul><li>`folder`: explorar un directorio específico</li><li>`root`: explore el directorio raíz.</li></ul> |
| `object` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |


**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base del origen de almacenamiento en la nube. |
| `{PATH}` | La ruta de un directorio. |

**Solicitud**

```shell
curl -X GET \
  'http://platform.adobe.io/data/foundation/flowservice/connections/dc3c0646-5e30-47be-a1ce-d162cb8f1f07/explore?objectType=folder&object=root' \
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
        "path": "/test-connectors/testFolder-fileIngestion/account.csv",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "profileData.json",
        "path": "/test-connectors/testFolder-fileIngestion/profileData.json",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "file",
        "name": "sampleprofile--3.parquet",
        "path": "/test-connectors/testFolder-fileIngestion/sampleprofile--3.parquet",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect la estructura de un archivo

Para inspeccionar la estructura del archivo de datos desde el almacenamiento en la nube, realice una solicitud de GET y proporcione la ruta y el tipo del archivo como parámetro de consulta.

Puede inspeccionar la estructura de un archivo de datos desde su origen de almacenamiento en la nube realizando una solicitud de GET al tiempo que proporciona la ruta y el tipo del archivo. También puede inspeccionar distintos tipos de archivo, como CSV, TSV o archivos JSON comprimidos y delimitados, especificando sus tipos de archivo como parte de los parámetros de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=FILE&object={FILE_PATH}&preview=true&fileType=delimited&encoding=ISO-8859-1;
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión del conector de origen de almacenamiento en la nube. |
| `{FILE_PATH}` | La ruta al archivo que desea inspeccionar. |
| `{FILE_TYPE}` | El tipo de archivo. Los tipos de archivo admitidos son:<ul><li><code>DELIMITADO</code>: Valor separado por delimitador. Los archivos DSV deben estar separados por comas.</li><li><code>JSON</code>: Notación de objetos de JavaScript. Los archivos JSON deben ser compatibles con XDM</li><li><code>PARQUÉ</code>: Apache Parquet. Los archivos de Parquet deben ser compatibles con XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales que se pueden utilizar para filtrar los resultados. Consulte la sección sobre [parámetros de consulta](#query) para obtener más información. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura del archivo consultado, incluidos los nombres de tabla y los tipos de datos.

```json
[
    {
        "name": "Id",
        "type": "String"
    },
    {
        "name": "FirstName",
        "type": "String"
    },
    {
        "name": "LastName",
        "type": "String"
    },
    {
        "name": "Email",
        "type": "String"
    },
    {
        "name": "Phone",
        "type": "String"
    }
]
```

## Uso de parámetros de consulta {#query}

La [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) admite el uso de parámetros de consulta para obtener una vista previa e inspeccionar distintos tipos de archivos.

| Parámetro | Descripción |
| --------- | ----------- |
| `columnDelimiter` | El valor de carácter único especificado como delimitador de columna para inspeccionar los archivos CSV o TSV. Si no se proporciona el parámetro, el valor predeterminado es una coma `(,)`. |
| `compressionType` | Un parámetro de consulta necesario para previsualizar un archivo JSON o delimitado comprimido. Los archivos comprimidos admitidos son: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |
| `encoding` | Define el tipo de codificación que se utilizará al procesar la previsualización. Los tipos de codificación admitidos son: `UTF-8` y `ISO-8859-1`. **Nota**: el parámetro `encoding` solo está disponible cuando se ingieren archivos CSV delimitados. Se incorporarán otros tipos de archivo con la codificación predeterminada, `UTF-8`. |

## Pasos siguientes

Al seguir este tutorial, ha explorado el sistema de almacenamiento en la nube, ha encontrado la ruta del archivo que desea llevar a [!DNL Platform] y ha visto su estructura. Puedes usar esta información en el siguiente tutorial para [recopilar datos de tu almacenamiento en la nube e introducirlos en Platform](../collect/cloud-storage.md).
