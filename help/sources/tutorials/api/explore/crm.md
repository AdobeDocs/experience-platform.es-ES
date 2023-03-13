---
keywords: Experience Platform;inicio;temas populares;CRM;crm;servicio de flujo de crm
solution: Experience Platform
title: Exploración de un sistema CRM mediante la API de Flow Service
description: Este tutorial utiliza la API de Flow Service para explorar los sistemas CRM.
exl-id: 9a8c553a-a93d-4539-a9d2-5f76a3927d92
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 3%

---

# Explorar un sistema CRM mediante [!DNL Flow Service] API

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Este tutorial utiliza el [!DNL Flow Service] API para explorar sistemas CRM.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema CRM mediante [!DNL Flow Service] API.

### Crear un ID de conexión

Para explorar su sistema CRM con [!DNL Platform] API, debe poseer un ID de conexión válido. Si todavía no tiene una conexión para el sistema CRM con el que desea trabajar, puede crearla mediante los siguientes tutoriales:

* [Microsoft Dynamics](../create/crm/ms-dynamics.md)
* [Salesforce](../create/crm/salesforce.md)

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los pertenecientes a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* `Content-Type: application/json`

## Exploración de las tablas de datos

Con el ID de conexión para su sistema CRM, puede explorar las tablas de datos realizando solicitudes de GET. Utilice la siguiente llamada para encontrar la ruta de la tabla que desea inspeccionar o introducir en [!DNL Platform].

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base para su sistema CRM. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta es una matriz de tablas desde al sistema CRM. Encuentre la tabla que desea introducir en [!DNL Platform] y tome nota de su `path` , ya que es necesario proporcionarla en el siguiente paso para inspeccionar su estructura.

```json
[
    {
        "type": "table",
        "name": "Solution Component Summary",
        "path": "msdyn_solutioncomponentsummary",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Quote Invoicing Product",
        "path": "msdyn_quoteinvoicingproduct",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Opportunity Relationship",
        "path": "customeropportunityrole",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect la estructura de una tabla

Para inspeccionar la estructura de una tabla desde el sistema CRM, realice una solicitud de GET y especifique la ruta de una tabla como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base para su sistema CRM. |
| `{TABLE_PATH}` | La ruta de una tabla. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}' \
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
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

## Pasos siguientes

Al seguir este tutorial, ha explorado su sistema CRM, ha encontrado la ruta de la tabla que desea introducir en [!DNL Platform]y obtuvo información sobre su estructura. Puede utilizar esta información en el siguiente tutorial para lo siguiente [recopilar datos de su sistema CRM e introducirlos en Platform](../collect/crm.md).
