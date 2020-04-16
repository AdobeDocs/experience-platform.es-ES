---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: 7cd9bec7336d0e1d9f3036cf862633f498002af8

---


# Explorar un sistema de almacenamiento en la nube mediante la API de servicio de flujo

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para explorar un sistema de almacenamiento en la nube de terceros.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema de almacenamiento en la nube mediante la API de servicio de flujo.

### Obtención de una conexión base

Para explorar un almacenamiento de nube de terceros mediante API de plataforma, debe tener un ID de conexión base válido. Si todavía no tiene una conexión base para el almacenamiento con el que desea trabajar, puede crear una mediante los siguientes tutoriales:

* [Amazon S3](../create/cloud-storage/s3.md)
* [Azure Blob](../create/cloud-storage/blob.md)
* [Azure Data Lake Almacenamiento Gen2](../create/cloud-storage/adls-gen2.md)
* [Tienda de Google Cloud](../create/cloud-storage/google.md)
* [SFTP](../create/cloud-storage/sftp.md)

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Explore su almacenamiento de nube

Con la conexión base para el almacenamiento de nube, puede explorar archivos y directorios realizando solicitudes GET. Al realizar solicitudes GET para explorar el almacenamiento de nube, debe incluir los parámetros de consulta que se enumeran en la tabla siguiente:

| Parámetro | Descripción |
| --------- | ----------- |
| `objectType` | El tipo de objeto que desea explorar. Establezca este valor como: <ul><li>`folder`:: Explorar un directorio específico</li><li>`root`:: Explore el directorio raíz.</li></ul> |
| `object` | Este parámetro solo es necesario cuando se visualiza un directorio específico. Su valor representa la ruta del directorio que desea explorar. |

Utilice la siguiente llamada para encontrar la ruta del archivo que desea traer a Platform:

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object={PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de una conexión base de almacenamiento de nube. |
| `{PATH}` | Ruta de un directorio. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=folder&object=/some/path/' \
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

## Inspeccionar la estructura de un archivo

Para inspeccionar la estructura del archivo de datos desde el almacenamiento de nube, realice una solicitud GET mientras proporciona la ruta del archivo como parámetro de consulta.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=file&object={FILE_PATH}&fileType={FILE_TYPE}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de una conexión base de almacenamiento de nube. |
| `{FILE_PATH}` | Ruta a un archivo. |
| `{FILE_TYPE}` | Tipo del archivo. Los tipos de archivo admitidos son:<ul><li>DELIMITADO</code>: Valor separado por delimitador. Los archivos DSV deben estar separados por comas.</li><li>JSON</code>: Notación de objetos JavaScript. Los archivos JSON deben ser compatibles con XDM</li><li>PARQUET</code>: Apache Parquet. Los archivos de parquet deben ser compatibles con XDM.</li></ul> |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=file&object=/some/path/data.csv&fileType=DELIMITED' \
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

Siguiendo este tutorial, ha explorado su sistema de almacenamiento en la nube, ha encontrado la ruta del archivo que desea traer a Platform y ha visto su estructura. Puede utilizar esta información en el siguiente tutorial para [recopilar datos de su almacenamiento en la nube y llevarlos a la plataforma](../collect/cloud-storage.md).