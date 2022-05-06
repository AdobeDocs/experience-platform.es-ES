---
keywords: Experience Platform;inicio;temas populares;almacenamiento en la nube;almacenamiento en la nube
title: Explorar carpetas de almacenamiento en la nube mediante la API de servicio de flujo
description: Este tutorial utiliza la API de servicio de flujo para explorar un sistema de almacenamiento en la nube de terceros.
exl-id: ba1a9bff-43a6-44fb-a4e7-e6a45b7eeebd
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 3%

---

# Explorar las carpetas de almacenamiento en la nube mediante [!DNL Flow Service] API

Este tutorial proporciona pasos sobre cómo explorar y previsualizar la estructura y el contenido del almacenamiento en la nube mediante el uso de [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API.

>[!NOTE]
>
>Para explorar el almacenamiento en la nube, ya debe tener un ID de conexión base válido para un origen de almacenamiento en la nube. Si no tiene este ID, consulte la [información general sobre fuentes](../../../home.md#cloud-storage) para obtener una lista de los orígenes de almacenamiento en la nube con los que puede crear una conexión base.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../landing/api-guide.md).

## Explorar las carpetas de almacenamiento en la nube

Puede recuperar información sobre la estructura de las carpetas de almacenamiento en la nube realizando una solicitud de GET al [!DNL Flow Service] al proporcionar el ID de conexión base de su origen.

Al realizar solicitudes de GET para explorar el almacenamiento en la nube, debe incluir los parámetros de consulta que se enumeran en la siguiente tabla:

| Parámetro | Descripción |
| --------- | ----------- |
| `objectType` | Tipo de objeto que desea explorar. Establezca este valor como: <ul><li>`folder`: Explorar un directorio específico</li><li>`root`: Explore el directorio raíz.</li></ul> |
| `object` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |


**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de conexión base del origen de almacenamiento en la nube. |
| `{PATH}` | Ruta de un directorio. |

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

Una respuesta correcta devuelve una matriz de archivos y carpetas que se encuentran en el directorio consultado. Tome nota de la `path` del archivo que desea cargar, ya que debe proporcionarlo en el siguiente paso para inspeccionar su estructura.

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

## Inspect: estructura de un archivo

Para inspeccionar la estructura del archivo de datos desde el almacenamiento en la nube, realice una solicitud de GET mientras proporciona la ruta del archivo y escriba como parámetro de consulta.

Puede inspeccionar la estructura de un archivo de datos desde el origen de almacenamiento en la nube realizando una solicitud de GET mientras proporciona la ruta y el tipo del archivo. También puede inspeccionar diferentes tipos de archivos, como CSV, TSV o JSON comprimido y archivos delimitados especificando sus tipos de archivo como parte de los parámetros de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | El ID de conexión del conector de origen de almacenamiento en la nube. |
| `{FILE_PATH}` | Ruta al archivo que desea inspeccionar. |
| `{FILE_TYPE}` | Tipo de archivo. Los tipos de archivo admitidos son:<ul><li>DELIMITADO</code>: Valor separado por delimitadores. Los archivos DSV deben separarse con comas.</li><li>JSON</code>: Notación de objeto JavaScript. Los archivos JSON deben ser compatibles con XDM</li><li>PARQUET</code>: Apache Parquet. Los archivos de parqué deben ser compatibles con XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales que se pueden usar para filtrar los resultados. Consulte la sección sobre [parámetros de consulta](#query) para obtener más información. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
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

La variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) admite el uso de parámetros de consulta para previsualizar e inspeccionar diferentes tipos de archivos.

| Parámetro | Descripción |
| --------- | ----------- |
| `columnDelimiter` | El valor de un solo carácter especificado como delimitador de columna para inspeccionar archivos CSV o TSV. Si no se proporciona el parámetro, el valor predeterminado es una coma `(,)`. |
| `compressionType` | Parámetro de consulta requerido para obtener una vista previa de un archivo delimitado o JSON comprimido. Los archivos comprimidos admitidos son: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Pasos siguientes

Al seguir este tutorial, ha explorado su sistema de almacenamiento en la nube y ha encontrado la ruta del archivo que desea traer [!DNL Platform]y vio su estructura. Puede utilizar esta información en el siguiente tutorial para [recopile datos de su almacenamiento en la nube y agréguelos a Platform](../collect/cloud-storage.md).
