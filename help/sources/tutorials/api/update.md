---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;conexiones de actualización
solution: Experience Platform
title: Actualización de conexiones mediante la API de servicio de flujo
topic: sobre validación
type: Tutorial
description: Este tutorial trata los pasos para actualizar los detalles y las credenciales de una conexión mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: 5187647dfcf82a476bc776bf2b606db228ca70a4
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 2%

---


# Actualización de conexiones mediante la API de servicio de flujo

En algunas circunstancias, puede ser necesario actualizar los detalles de una conexión de origen existente. [!DNL Flow Service] le permite agregar, editar y eliminar detalles de un lote o una conexión de flujo existente, incluido su nombre, descripción y credenciales.

Este tutorial trata los pasos para actualizar los detalles y las credenciales de una conexión mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Este tutorial requiere que tenga una conexión existente y un ID de conexión válido. Si no tiene una conexión existente, seleccione el origen de su elección en la [información general de fuentes](../../home.md) y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga conocimientos prácticos sobre los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos desde diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para actualizar correctamente una conexión mediante la API [!DNL Flow Service].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos del Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Buscar detalles de conexión

El primer paso en la actualización de la conexión es recuperar los detalles con su ID de conexión. Para recuperar los detalles actuales de la conexión, realice una solicitud de GET a la API [!DNL Flow Service] mientras proporciona el ID de conexión de la conexión que desea actualizar.

**Formato API**

```http
GET /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor único `id` de la conexión que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información relativa a su conexión.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/139f6a5f-a78b-4744-9f6a-5fa78bd74431' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales de la conexión, incluidas sus credenciales, identificador único (`id`) y versión. Se requiere el valor de la versión para actualizar la conexión.

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

Para actualizar el nombre, la descripción y las credenciales de la conexión, realice una solicitud de PATCH a la API [!DNL Flow Service] mientras proporciona el ID de conexión, la versión y la nueva información que desee utilizar.

>[!IMPORTANT]
>
>Se requiere el encabezado `If-Match` al realizar una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión que desea actualizar.

**Formato API**

```http
PATCH /connections/{CONNECTION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{CONNECTION_ID}` | El valor único `id` de la conexión que desea actualizar. |

**Solicitud**

La siguiente solicitud proporciona un nuevo nombre y descripción, así como un nuevo conjunto de credenciales, para actualizar la conexión.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar la conexión. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Ruta del parámetro que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], mientras proporciona su ID de conexión.

```json
{
    "id": "139f6a5f-a78b-4744-9f6a-5fa78bd74431",
    "etag": "\"3600e378-0000-0200-0000-5f40212f0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha actualizado las credenciales y la información asociada con la conexión mediante la API [!DNL Flow Service]. Para obtener más información sobre el uso de los conectores de origen, consulte la [información general de las fuentes](../../home.md).
