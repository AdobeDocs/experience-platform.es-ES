---
keywords: Experience Platform;home;popular topics;cloud storage;Cloud storage
solution: Experience Platform
title: Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo
topic: overview
description: Este tutorial utiliza la API de servicio de flujo para explorar un sistema de almacenamiento en la nube de terceros.
translation-type: tm+mt
source-git-commit: 026007e5f80217f66795b2b53001b6cf5e6d2344
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 2%

---


# Explorar un sistema de almacenamiento en la nube mediante la [!DNL Flow Service] API

Este tutorial utiliza la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para explorar un sistema de almacenamiento en la nube de terceros.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema de almacenamiento en la nube mediante la [!DNL Flow Service] API.

### Obtención de un ID de conexión

Para explorar un almacenamiento de nube de terceros mediante [!DNL Platform] API, debe disponer de un ID de conexión válido. Si todavía no tiene una conexión para el almacenamiento con el que desea trabajar, puede crear una mediante los siguientes tutoriales:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Almacenamiento Gen2](../create/cloud-storage/adls-gen2.md)
* [Almacenamiento de archivos de Azure](../create/cloud-storage/azure-file-storage.md)
* [Tienda de Google Cloud](../create/cloud-storage/google.md)
* [HDFS](../create/cloud-storage/hdfs.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Explore su almacenamiento de nube

Con el ID de conexión del almacenamiento de nube, puede explorar archivos y directorios realizando solicitudes de GET. Al realizar solicitudes de GET para explorar el almacenamiento de nube, debe incluir los parámetros de consulta que se enumeran en la tabla siguiente:

| Parámetro | Descripción |
| --------- | ----------- |
| `objectType` | El tipo de objeto que desea explorar. Establezca este valor como: <ul><li>`folder`:: Explorar un directorio específico</li><li>`root`:: Explore el directorio raíz.</li></ul> |
| `object` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |

Utilice la siguiente llamada para encontrar la ruta del archivo en el que desea [!DNL Platform]:

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
GET /connections/{CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{CONNECTION_ID}` | ID de conexión del conector de origen del almacenamiento de nube. |
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

Una respuesta correcta devuelve una matriz de archivos y carpetas que se encuentran en el directorio consultado. Tenga en cuenta la `path` propiedad del archivo que desea cargar, ya que debe proporcionarlo en el paso siguiente para inspeccionar su estructura.

```json
[
    {
        "type": "File",
        "name": "data.csv",
        "path": "/some/path/data.csv"
    },
    {
        "type": "Folder",
        "name": "foobar",
        "path": "/some/path/foobar"
    }
]
```

## Inspect: la estructura de un archivo

Para inspeccionar la estructura del archivo de datos desde el almacenamiento de la nube, realice una solicitud de GET mientras proporciona la ruta del archivo y escriba como parámetro de consulta.

Puede inspeccionar la estructura de un archivo CSV o TSV especificando un delimitador personalizado como perímetro de consulta. Cualquier valor de carácter único es un delimitador de columna permitido. Si no se proporciona, se `(,)` utiliza una coma como valor predeterminado.

**Formato API**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=;
GET /connections/{CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}&preview=true&fileType=delimited&columnDelimiter=\t
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | ID de conexión del conector de origen del almacenamiento de nube. |
| `{FILE_PATH}` | Ruta al archivo que desea inspeccionar. |
| `{FILE_TYPE}` | Tipo del archivo. Los tipos de archivo admitidos son:<ul><li>DELIMITADO</code>: Valor separado por delimitador. Los archivos DSV deben estar separados por comas.</li><li>JSON</code>: Notación de objetos JavaScript. Los archivos JSON deben ser compatibles con XDM</li><li>PARQUET</code>: Apache Parquet. Los archivos de parquet deben ser compatibles con XDM.</li></ul> |
| `columnDelimiter` | El valor de un solo carácter especificado como delimitador de columna para inspeccionar archivos CSV o TSV. Si no se proporciona el parámetro, el valor predeterminado es una coma `(,)`. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

## Pasos siguientes

Siguiendo este tutorial, ha explorado su sistema de almacenamiento en la nube, ha encontrado la ruta del archivo al que desea acceder [!DNL Platform]y ha visto su estructura. Puede utilizar esta información en el siguiente tutorial para [recopilar datos de su almacenamiento en la nube y llevarlos a la plataforma](../collect/cloud-storage.md).