---
keywords: Experience Platform;inicio;temas populares;automatización de marketing
solution: Experience Platform
title: Exploración de un sistema de automatización de marketing mediante la API de Flow Service
description: Este tutorial utiliza la API de Flow Service para explorar los sistemas de automatización de marketing.
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---

# Explore un sistema de automatización de marketing con [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial utiliza el [!DNL Flow Service] API para explorar los sistemas de automatización de marketing.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema de automatización de marketing mediante [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Este tutorial requiere que tenga una conexión válida con la aplicación de automatización de marketing de terceros desde la que desee introducir datos. Una conexión válida implica el identificador de especificación de conexión y el identificador de conexión de la aplicación. Encontrará más información sobre la creación de una conexión de automatización de marketing y la recuperación de estos valores en la [conexión de una fuente de automatización de marketing a Platform](../../api/create/marketing-automation/hubspot.md) tutorial.

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los pertenecientes a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* Content-Type: `application/json`

## Exploración de las tablas de datos

Con la conexión base para el sistema de automatización de marketing, puede explorar las tablas de datos realizando solicitudes de GET. Utilice la siguiente llamada para encontrar la ruta de la tabla que desea inspeccionar o introducir en [!DNL Platform].

**Formato de API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base para el sistema de automatización de marketing. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta es una matriz de tablas desde hasta el sistema de automatización de marketing. Encuentre la tabla que desea introducir en [!DNL Platform] y tome nota de su `path` , ya que es necesario proporcionarla en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## Inspect la estructura de una tabla

Para inspeccionar la estructura de una tabla desde el sistema de automatización de marketing, realice una solicitud de GET y especifique la ruta de una tabla como parámetro de consulta.

**Formato de API**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de conexión para el sistema de automatización de marketing. |
| `{TABLE_PATH}` | La ruta de una tabla dentro del sistema de automatización de marketing. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura de una tabla. Los detalles sobre cada una de las columnas de la tabla se encuentran dentro de los elementos de la variable `columns` matriz.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Pasos siguientes

Al seguir este tutorial, ha explorado el sistema de automatización de marketing y ha encontrado la ruta de la tabla que desea incluir en [!DNL Platform]y obtuvo información sobre su estructura. Puede utilizar esta información en el siguiente tutorial para lo siguiente [recopilar datos de su sistema de automatización de marketing e introducirlos en Platform](../collect/marketing-automation.md).
