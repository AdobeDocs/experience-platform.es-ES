---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Explorar un sistema de éxito del cliente mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: fc5cdaa661c47e14ed5412868f3a54fd7bd2b451
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---


# Explorar un sistema de éxito del cliente mediante la [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes distintas dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la [!DNL Flow Service] API para explorar los sistemas de éxito del cliente (CS).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema CS mediante la [!DNL Flow Service] API.

### Obtención de una conexión base

Para explorar el sistema CS mediante [!DNL Platform] API, debe disponer de un ID de conexión base válido. Si todavía no dispone de una conexión de base para el sistema CS con el que desea trabajar, puede crear una mediante los siguientes tutoriales:

* [Salesforce Service Cloud](../create/customer-success/salesforce-service-cloud.md)
* [ServiceNow](../create/customer-success/servicenow.md)

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Explorar las tablas de datos

Con la conexión base del sistema CS, puede explorar las tablas de datos realizando solicitudes de GET. Utilice la siguiente llamada para encontrar la ruta de la tabla que desea inspeccionar o en la que desea realizar la ingesta [!DNL Platform].

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de una conexión base CS. |

**Solicitud**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de tablas del sistema CS. Encuentre la tabla que desea traer [!DNL Platform] y tome nota de su `path` propiedad, ya que se le pedirá que la proporcione en el próximo paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "Accepted Event Relation",
        "path": "AcceptedEventRelation",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account",
        "path": "Account",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Change Event",
        "path": "AccountChangeEvent",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Clean Info",
        "path": "AccountCleanInfo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect de la estructura de una tabla

Para inspeccionar la estructura de una tabla desde el sistema CS, realice una solicitud de GET mientras especifica la ruta de una tabla como parámetro de consulta.

**Formato API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | ID de una conexión base CS. |
| `{TABLE_PATH}` | Ruta de una tabla. |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura de la tabla especificada. Los detalles relativos a cada una de las columnas de la tabla se encuentran dentro de los elementos de la `columns` matriz.

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
                "name": "Name",
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
            },
        ]
    }
}
```

## Pasos siguientes

Siguiendo este tutorial, ha explorado su sistema CS, ha encontrado la ruta de la tabla en la que desea realizar la ingesta [!DNL Platform]y ha obtenido información sobre su estructura. Puede utilizar esta información en el siguiente tutorial para [recopilar datos de su sistema CS e incluirlos en Platform](../collect/customer-success.md).