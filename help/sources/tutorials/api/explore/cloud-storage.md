---
keywords: Experience Platform;inicio;temas populares;almacenamiento en la nube;almacenamiento en la nube
solution: Experience Platform
title: Explorar un sistema de almacenamiento en voz alta mediante la API de servicio de flujo
topic: sobre validación
description: Este tutorial utiliza la API de servicio de flujo para explorar un sistema de almacenamiento en la nube de terceros.
translation-type: tm+mt
source-git-commit: 457fc9e1b0c445233f0f574fefd31bc1fc3bafc8
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---


# Explorar un sistema de almacenamiento en la nube mediante la API [!DNL Flow Service]

Este tutorial utiliza la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para explorar un sistema de almacenamiento en la nube de terceros.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema de almacenamiento en la nube mediante la API [!DNL Flow Service].

### Obtención de un ID de conexión

Para explorar un almacenamiento en la nube de terceros mediante API [!DNL Platform], debe poseer un ID de conexión válido. Si todavía no tiene una conexión para el almacenamiento con el que desea trabajar, puede crear una a través de los siguientes tutoriales:

* [[!DNL Amazon S3]](../create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../create/cloud-storage/azure-file-storage.md)
* [[!DNL FTP]](../create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../create/cloud-storage/sftp.md)

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Explorar el almacenamiento en la nube

Con el ID de conexión para el almacenamiento en la nube, puede explorar archivos y directorios realizando solicitudes de GET. Al realizar solicitudes de GET para explorar el almacenamiento en la nube, debe incluir los parámetros de consulta que se enumeran en la siguiente tabla:

| Parámetro | Descripción |
| --------- | ----------- |
| `objectType` | Tipo de objeto que desea explorar. Establezca este valor como: <ul><li>`folder`: Explorar un directorio específico</li><li>`root`: Explore el directorio raíz.</li></ul> |
| `object` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |

Utilice la siguiente llamada para encontrar la ruta del archivo que desea introducir en [!DNL Platform]:

**Formato de API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONNECTION_ID}` | El ID de conexión para el conector de origen de almacenamiento en la nube. |
| `{PATH}` | Ruta de un directorio. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
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
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&{QUERY_PARAMS}&preview=true
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&columnDelimiter=\t
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&preview=true&fileType=delimited&compressionType=gzip;
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El ID de conexión del conector de origen de almacenamiento en la nube. |
| `{FILE_PATH}` | Ruta al archivo que desea inspeccionar. |
| `{FILE_TYPE}` | Tipo de archivo. Los tipos de archivo admitidos son:<ul><li>DELIMITADO</code>: Valor separado por delimitadores. Los archivos DSV deben separarse con comas.</li><li>JSON</code>: Notación de objeto JavaScript. Los archivos JSON deben ser compatibles con XDM</li><li>PARQUET</code>: Apache Parquet. Los archivos de parqué deben ser compatibles con XDM.</li></ul> |
| `{QUERY_PARAMS}` | Parámetros de consulta opcionales que se pueden usar para filtrar los resultados. Consulte la sección sobre [parámetros de consulta](#query) para obtener más información. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/aep-bootcamp/Adobe%20Pets%20Customer%2020190801%20EXP.json&fileType=json&preview=true' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

La [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) admite el uso de parámetros de consulta para previsualizar e inspeccionar diferentes tipos de archivos.

| Parámetro | Descripción |
| --------- | ----------- |
| `columnDelimiter` | El valor de un solo carácter especificado como delimitador de columna para inspeccionar archivos CSV o TSV. Si no se proporciona el parámetro, el valor predeterminado es una coma `(,)`. |
| `compressionType` | Parámetro de consulta requerido para obtener una vista previa de un archivo delimitado o JSON comprimido. Los archivos comprimidos admitidos son: <ul><li>`bzip2`</li><li>`gzip`</li><li>`deflate`</li><li>`zipDeflate`</li><li>`tarGzip`</li><li>`tar`</li></ul> |

## Pasos siguientes

Al seguir este tutorial, ha explorado su sistema de almacenamiento en la nube, ha encontrado la ruta del archivo que desea traer a [!DNL Platform] y ha visto su estructura. Puede utilizar esta información en el siguiente tutorial para [recopilar datos del almacenamiento en la nube e introducirlos en Platform](../collect/cloud-storage.md).