---
keywords: Experience Platform;home;popular topics; flow service; update connections
solution: Experience Platform
title: Actualización de la información de conexión mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: En este tutorial se explican los pasos para actualizar la información de conexión, incluido su nombre, descripción y credenciales mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 2%

---


# Actualización de la información de conexión mediante la API de servicio de flujo

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

En este tutorial se explican los pasos para actualizar la información de conexión, incluido el nombre, la descripción y las credenciales, mediante la [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Este tutorial requiere que tenga un ID de conexión válido. Si no tiene un ID de conexión válido, seleccione el conector que desee en la información general [de](../../home.md) orígenes y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga conocimientos prácticos sobre los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para actualizar correctamente la información de la conexión mediante la API [!DNL Flow Service] .

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Buscar detalles de conexión

>[!NOTE]
>Este tutorial utiliza el conector [de origen de](../../connectors/crm/salesforce.md) Salesforce como ejemplo, pero los pasos descritos se aplican a cualquiera de los conectores [de origen](../../home.md)disponibles.

El primer paso para actualizar la información de conexión es recuperar los detalles de conexión con su ID de conexión.

**Formato API**

```http
GET /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor único `id` de la conexión que desea recuperar. |

**Solicitud**

A continuación, se recupera información relativa a su ID de conexión.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales de la conexión, incluidas sus credenciales, identificador único (`id`) y versión.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1597973312000,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "E2E_SF Base_Connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "my-salesforce-account",
                    "environmentUrl": "login.salesforce.com"
                }
            },
            "version": "\"1400dd53-0000-0200-0000-5f3f23450000\"",
            "etag": "\"1400dd53-0000-0200-0000-5f3f23450000\""
        }
    ]
}
```

## Actualizar conexión

Una vez que tenga un ID de conexión existente, realice una solicitud de PATCH a la [!DNL Flow Service] API.

>[!IMPORTANT]
>Una solicitud de PATCH requiere el uso del `If-Match` encabezado. El valor de este encabezado es la versión única de la conexión.

**Formato API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor único `id` de la conexión que desea actualizar. |

**Solicitud**

La siguiente solicitud proporciona nueva información para actualizar la conexión.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: 1400dd53-0000-0200-0000-5f3f23450000' \
    -d '[
        {
            "op": "replace",
            "path": "/auth/params",
            "value": {
                "username": "salesforce-connector-username",
                "password": "{NEW_PASSWORD}",
                "securityToken": "{NEW_SECURITY_TOKEN}"
            }
        },
        {
            "op": "replace",
            "path": "/name",
            "value": "Test salesforce connection"
        },
        {
            "op": "add",
            "path": "/description",
            "value": "A test salesforce connection"
        }
    ]'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la conexión. Las operaciones incluyen: `add`, `replace`, y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión y una etiqueta actualizada.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Buscar detalles de conexión actualizados

Puede recuperar el mismo ID de conexión que ha actualizado para ver los cambios realizados mediante una solicitud de GET a la [!DNL Flow Service] API.

**Formato API**

```http
GET /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor único `id` de la conexión que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información actualizada sobre su ID de conexión.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actualizados de su ID de conexión, incluido su nuevo nombre, descripción y versión.

```json
{
    "items": [
        {
            "createdAt": 1597973312000,
            "updatedAt": 1598038319627,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxName": "{SANDBOX_NAME}",
            "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
            "name": "Test salesforce connection",
            "description": "A test salesforce connection",
            "connectionSpec": {
                "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Basic Authentication",
                "params": {
                    "securityToken": "{NEW_SECURITY_TOKEN}",
                    "password": "{PASSWORD}",
                    "username": "salesforce-connector-username"
                }
            },
            "version": "\"3600e378-0000-0200-0000-5f40212f0000\"",
            "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
        }
    ]
}
```

## Pasos siguientes

Siguiendo este tutorial, ha actualizado las credenciales y la información asociada con la conexión mediante la [!DNL Flow Service] API. Para obtener más información sobre el uso de los conectores de origen, consulte la descripción general [de](../../home.md)las fuentes.
