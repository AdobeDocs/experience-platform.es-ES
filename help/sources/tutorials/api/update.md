---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;actualizar cuentas
solution: Experience Platform
title: Actualización de cuentas mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Este tutorial trata los pasos para actualizar los detalles y las credenciales de una cuenta mediante la API de servicio de flujo.
exl-id: a93385fd-ed36-457f-8882-41e37f6f209d
source-git-commit: 95f455bd03b7baefe0133a9818c9d048f36f9d38
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 3%

---

# Actualizar cuentas mediante la API de servicio de flujo

En algunas circunstancias, puede ser necesario actualizar los detalles de una conexión de origen existente. [!DNL Flow Service] permite agregar, editar y eliminar detalles de un lote o conexión de flujo continuo existente, como su nombre, descripción y credenciales.

Este tutorial trata los pasos para actualizar los detalles y las credenciales de una conexión mediante el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Este tutorial requiere que tenga una conexión existente y un ID de conexión válido. Si no tiene una conexión existente, seleccione el origen que desee en el [información general sobre fuentes](../../home.md) y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Buscar detalles de conexión

El primer paso para actualizar la conexión es recuperar sus detalles con su ID de conexión. Para recuperar los detalles actuales de la conexión, realice una solicitud de GET al [!DNL Flow Service] al proporcionar el ID de conexión, de la conexión que desea actualizar.

**Formato de API**

```http
GET /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El único `id` para la conexión que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información relacionada con su conexión.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales de la conexión, incluidas sus credenciales, el identificador único (`id`) y la versión. Se requiere el valor de la versión para actualizar la conexión.

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

Para actualizar el nombre, la descripción y las credenciales de la conexión, realice una solicitud de PATCH al [!DNL Flow Service] al proporcionar su ID de conexión, versión y la nueva información que desea utilizar.

>[!IMPORTANT]
>
>La variable `If-Match` es obligatorio cuando se realiza una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión que desea actualizar.

**Formato de API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El único `id` para la conexión que desea actualizar. |

**Solicitud**

La siguiente solicitud proporciona un nuevo nombre y descripción, así como un nuevo conjunto de credenciales, para actualizar la conexión con.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la conexión. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha actualizado las credenciales y la información asociada a su conexión mediante el uso de [!DNL Flow Service] API. Para obtener más información sobre el uso de conectores de origen, consulte la [información general sobre fuentes](../../home.md).
