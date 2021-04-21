---
keywords: Experience Platform;inicio;temas populares;CRM;crm;servicio de flujo crm
solution: Experience Platform
title: Explorar un sistema CRM mediante la API de servicio de flujo
topic-legacy: overview
description: Este tutorial utiliza la API de servicio de flujo para explorar los sistemas CRM.
exl-id: 9a8c553a-a93d-4539-a9d2-5f76a3927d92
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---

# Explorar un sistema CRM mediante la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para explorar los sistemas CRM.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un sistema CRM mediante la API [!DNL Flow Service].

### Creación de un ID de conexión

Para explorar el sistema CRM mediante API [!DNL Platform], debe poseer un ID de conexión válido. Si todavía no tiene una conexión para el sistema CRM con el que desea trabajar, puede crear una a través de los siguientes tutoriales:

* [Microsoft Dynamics](../create/crm/ms-dynamics.md)
* [Salesforce](../create/crm/salesforce.md)

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

## Explorar las tablas de datos

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta es una matriz de tablas desde a su sistema CRM. Busque la tabla que desea introducir en [!DNL Platform] y tome nota de su propiedad `path`, ya que debe proporcionarla en el siguiente paso para inspeccionar su estructura.

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

## Inspect de la estructura de una tabla

Para inspeccionar la estructura de una tabla desde el sistema CRM, realice una solicitud de GET al especificar la ruta de una tabla como parámetro de consulta.

**Formato de API**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parámetro | Descripción |
| --- | --- |
| `{BASE_CONNECTION_ID}` | El ID de la conexión base para su sistema CRM. |
| `{TABLE_PATH}` | Ruta de una tabla. |

**Solicitud**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve la estructura de una tabla. Los detalles sobre cada una de las columnas de la tabla se encuentran dentro de los elementos de la matriz `columns`.

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

Al seguir este tutorial, ha explorado su sistema CRM, ha encontrado la ruta de la tabla a la que desea incluir [!DNL Platform] y ha obtenido información sobre su estructura. Puede utilizar esta información en el siguiente tutorial para [recopilar datos de su sistema CRM e introducirlos en Platform](../collect/crm.md).
