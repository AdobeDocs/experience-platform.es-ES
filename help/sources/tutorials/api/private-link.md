---
title: Compatibilidad con vínculos privados para fuentes en la API
description: Obtenga información sobre cómo crear y utilizar vínculos privados para fuentes de Adobe Experience Platform
exl-id: 9b7fc1be-5f42-4e29-b552-0b0423a40aa1
source-git-commit: 4d82b0a7f5ae9e0a7607fe7cb75261e4d3489eff
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 4%

---

# Compatibilidad con vínculos privados para fuentes en la API

>[!AVAILABILITY]
>
>Las siguientes fuentes admiten esta función:
>
>* [[!DNL Azure Blob Storage]](../../connectors/cloud-storage/blob.md)
>* [[!DNL ADLS Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>
>Actualmente, la compatibilidad con enlaces privados solo está disponible para las organizaciones que han adquirido Adobe Healthcare Shield o Adobe Privacy &amp; Security Shield.

Puede utilizar la función Vínculo privado para crear extremos privados a los que se conectarán los orígenes de Adobe Experience Platform. Conecte sus fuentes de forma segura a una red virtual mediante direcciones IP privadas, lo que elimina la necesidad de direcciones IP públicas y reduce la superficie de ataque. Simplifique la configuración de la red eliminando la necesidad de configuraciones complejas de firewall o traducción de direcciones de red, a la vez que garantiza que el tráfico de datos solo llegue a los servicios aprobados.

Lea esta guía para aprender a utilizar las API para crear y utilizar un extremo privado.

>[!BEGINSHADEBOX]

## Derecho de uso de licencias para compatibilidad con vínculos privados

Las métricas de asignación de derechos de uso de licencias para la compatibilidad con vínculos privados en fuentes de son las siguientes:

* Los clientes tienen derecho a hasta 2 TB por año de transferencia de datos a través de fuentes compatibles ([!DNL Azure Blob Storage], [!DNL ADLS Gen2] y [!DNL Azure File Storage]), en todas las zonas protegidas y organizaciones.
* Cada organización puede tener un máximo de 10 extremos para todas las zonas protegidas de producción.
* Cada organización puede tener un máximo de 1 extremo para todas las zonas protegidas de desarrollo.

>[!ENDSHADEBOX]

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../landing/api-guide.md).

## Crear un extremo privado {#create-private-endpoint}

Para crear un extremo privado, realice una petición POST a `/privateEndpoints`.

**Formato de API**

```http
POST /privateEndpoints
```

**Solicitud**

La siguiente solicitud crea un extremo privado:

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de su extremo privado. |
| `subscriptionId` | El identificador asociado con su suscripción a [!DNL Azure]. Para obtener más información, lea la guía de [!DNL Azure] sobre [recuperación de los ID de suscripción e inquilino de [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Nombre de su grupo de recursos en [!DNL Azure]. Un grupo de recursos contiene recursos relacionados para una solución [!DNL Azure]. Para obtener más información, lea la guía [!DNL Azure] sobre [administración de grupos de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | El nombre del recurso. En [!DNL Azure], un recurso hace referencia a instancias como máquinas virtuales, aplicaciones web y bases de datos. Para obtener más información, lea la guía de [!DNL Azure] sobre [cómo entender al [!DNL Azure] administrador de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `connectionSpec.id` | El ID de especificación de conexión del origen que está utilizando. |
| `connectionSpec.version` | La versión del ID de especificación de conexión que está utilizando. |

+++

**Respuesta**

Una respuesta correcta devuelve lo siguiente:

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| Propiedad | Descripción |
| --- | --- |
| `id` | El ID del extremo privado recién creado. |
| `name` | Nombre de su extremo privado. |
| `subscriptionId` | El identificador asociado con su suscripción a [!DNL Azure]. Para obtener más información, lea la guía de [!DNL Azure] sobre [recuperación de los ID de suscripción e inquilino de [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id). |
| `resourceGroupName` | Nombre de su grupo de recursos en [!DNL Azure]. Un grupo de recursos contiene recursos relacionados para una solución [!DNL Azure]. Para obtener más información, lea la guía [!DNL Azure] sobre [administración de grupos de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal). |
| `resourceName` | El nombre del recurso. En [!DNL Azure], un recurso hace referencia a instancias como máquinas virtuales, aplicaciones web y bases de datos. Para obtener más información, lea la guía de [!DNL Azure] sobre [cómo entender al [!DNL Azure] administrador de recursos](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview). |
| `connectionSpec.id` | El ID de especificación de conexión del origen que está utilizando. |
| `connectionSpec.version` | La versión del ID de especificación de conexión que está utilizando. |
| `state` | Estado actual del extremo privado. Los estados válidos incluyen: <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## Recuperar una lista de extremos privados {#retrieve-private-endpoints}

Para recuperar una lista de extremos privados de una zona protegida determinada de su organización, realice una petición GET a `/privateEndpoints`.

**Formato de API**

```http
GET /privateEndpoints
```

**Solicitud**

La siguiente solicitud recupera una lista de todos los extremos privados que existen en su organización.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve una lista de extremos privados de su organización.

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Recuperar una lista de extremos privados para un origen determinado {#retrieve-private-endpoints-by-source}

Para recuperar una lista de extremos privados que corresponden a un origen específico, realice una petición GET al extremo `/privateEndpoints` y proporcione el `connectionSpec.id` del origen.

**Formato de API**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | El ID de especificación de conexión del origen en el que desea buscar los extremos privados. |

**Solicitud**

La siguiente solicitud recupera una lista de todos los extremos privados que corresponden al origen con el id. de especificación de conexión: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve una lista de todos los extremos privados que corresponden al origen con el id. de especificación de conexión: `4c10e202-c428-4796-9208-5f1f5732b1cf`.

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## Recuperar un extremo privado {#retrieve-specific-private-endpoint}

Para recuperar un extremo privado específico, realice una petición GET a `/privateEndpoints` y proporcione el identificador del extremo privado que desea recuperar.

**Formato de API**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | El ID del extremo privado que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera el extremo privado con el identificador:`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el extremo privado con el identificador: `2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## Resolver un extremo privado {#resolve-private-endpoint}

**Formato de API**

```http
GET /privateEndpoints?op=autoResolve
```

**Solicitud**

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**Respuesta**

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## Habilitar [!DNL Interactive Authoring] {#enable-interactive-authoring}

>[!IMPORTANT]
>
>Debe habilitar [!DNL Interactive Authoring] antes de crear o actualizar un flujo y antes de crear, actualizar o explorar una conexión.

[!DNL Interactive Authoring] se usa para funcionalidades como explorar una conexión o cuenta y obtener una vista previa de los datos. Para habilitar [!DNL Interactive Authoring], realice una petición POST a `/privateEndpoints/interactiveAuthoring` y especifique `enable` como operador en los parámetros de consulta.

**Formato de API**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `op` | La operación que desea realizar. Para habilitar [!DNL Interactive Authoring], establezca el valor `op` en `enable`. |

**Solicitud**

La siguiente solicitud habilita [!DNL Interactive Authoring] para el extremo privado y establece el TTL en 60 minutos.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `autoTerminationMinutes` | El TTL [!DNL Interactive Authoring] (tiempo de vida) en minutos. [!DNL Interactive Authoring] se usa para funcionalidades como explorar una conexión o cuenta y obtener una vista previa de los datos. Puede establecer un TTL máximo de 120 minutos. El TTL predeterminado es de 60 minutos. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 202 (Aceptado).

## Recuperar estado de [!DNL Interactive Authoring] {#retrieve-interactive-authoring-status}

Para ver el estado actual de [!DNL Interactive Authoring] para su extremo privado, realice una petición GET a `/privateEndpoints/interactiveAuthoring`.

**Formato de API**

```http
GET /privateEndpoints/interactiveAuthoring
```

**Solicitud**

La siguiente solicitud recupera el estado de [!DNL Interactive Authoring]:

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

+++Seleccionar para ver el ejemplo de respuesta

```json
{
    "status": "Disabled"
}
```

| Propiedad | Descripción |
| --- | --- |
| `status` | El estado de [!DNL Interactive Authoring]. Los valores válidos incluyen: `disabled`, `enabling`, `enabled`. |

+++

## Eliminar punto final privado {#delete-private-endpoint}

Para eliminar su extremo privado, realice una petición DELETE a `/privateEndpoints` y proporcione el identificador del extremo que desea eliminar.

**Formato de API**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| Parámetros de consulta | Descripción |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | El ID del extremo privado que desea eliminar. |

**Solicitud**

La siguiente solicitud elimina el extremo privado con el identificador: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 (Correcto). Para comprobar la eliminación, realice una petición GET y `/privateEndpoints` y proporcione el ID eliminado como parámetro de consulta.

## Flow Service {#flow-service}

Lea las secciones siguientes para obtener información sobre cómo usar extremos privados junto con la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

### Crear una conexión con un extremo privado {#create-base-connection}

Para crear una conexión con un extremo privado en Experience Platform, realice una petición POST al extremo `/connections` de la API [!DNL Flow Service].

**Formato de API**

```http
POST /connections/
```

**Solicitud**

La siguiente solicitud crea una conexión base autenticada para [!DNL Azure Blob Storage], a la vez que utiliza un extremo privado.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Azure Blob Storage base connection",
      "description": "A base connection for a Azure Blob Storage source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión base. |
| `description` | (Opcional) Descripción que proporciona información adicional sobre la conexión. |
| `auth.specName` | La autenticación que se está utilizando para conectar su origen a Experience Platform. |
| `auth.params.connectionString` | La cadena de conexión [!DNL Azure Blob Storage]. Para obtener más información, lea la [[!DNL Azure Blob Storage] guía de autenticación de API](../api/create/cloud-storage/blob.md). |
| `auth.params.usePrivateLink` | Un valor booleano que determina si está utilizando o no un extremo privado. Establezca este valor en `true` si está usando un extremo privado. |
| `connectionSpec.id` | Identificador de especificación de conexión de [!DNL Azure Blob Storage]. |
| `connectionSpec.version` | La versión de su ID de especificación de conexión [!DNL Azure Blob Storage]. |

+++

**Respuesta**

Una respuesta correcta devuelve el ID de la conexión base y la etiqueta generados recientemente.

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### Recuperar conexiones vinculadas a un extremo privado determinado {#retrieve-connections-by-endpoint}

Para recuperar conexiones vinculadas a un extremo privado concreto, realice una petición GET al extremo `/connections` y proporcione el ID del extremo privado como parámetro de consulta.

**Formato de API**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| Parámetros de consulta | Descripción |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | El ID del extremo privado vinculado a las conexiones que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera las conexiones existentes vinculadas al extremo privado con el identificador: `02a74b31-a566-4a86-9cea-309b101a7f24`.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve una lista de conexiones vinculadas al extremo privado consultado.

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### Recuperar conexiones asociadas a cualquier extremo privado {#retrieve-connections}

Para recuperar conexiones asociadas a cualquier extremo privado, realice una petición GET al extremo `/connections` y proporcione `property=auth.params.usePrivateLink==true` como parámetro de consulta.

**Formato de API**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**Solicitud**

La siguiente solicitud recupera todas las conexiones de su organización que utilizan extremos privados.

+++Seleccionar para ver ejemplo de solicitud

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Respuesta**

Una respuesta correcta devuelve todas las conexiones vinculadas a extremos privados.

+++Seleccionar para ver el ejemplo de respuesta

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

## Apéndice

Lea esta sección para obtener más información sobre el uso de [!DNL Azure] vínculos privados en la API.

### Aprobar un extremo privado para [!DNL Azure Blob] y [!DNL Azure Data Lake Gen2]

Para aprobar una solicitud de extremo privado para los orígenes [!DNL Azure Blob] y [!DNL Azure Data Lake Gen2], inicie sesión en [!DNL Azure Portal]. En el panel de navegación izquierdo, seleccione **[!DNL Data storage]**, luego vaya a la ficha **[!DNL Security + networking]** y elija **[!DNL Networking]**. A continuación, seleccione **[!DNL Private endpoints]** para ver una lista de los extremos privados asociados a su cuenta y sus estados de conexión actuales. Para aprobar una solicitud pendiente, seleccione el extremo deseado y haga clic en **[!DNL Approve]**.

![El portal de Azure con una lista de extremos privados pendientes.](../../images/tutorials/private-links/azure.png)

<!--

### Configure your [!DNL Snowflake] account to connect to private links

You must complete the following prerequisite steps in order to use the [!DNL Snowflake] source with private links.

First, you must raise a support ticket in [!DNL Snowflake] and request for the **endpoint service resource ID** of the [!DNL Azure] region of your [!DNL Snowflake] account. Follow the steps below to raise a [!DNL Snowflake] ticket:

1. Navigate to the [[!DNL Snowflake] UI](https://app.snowflake.com) and sign in with your email account. During this step, you must ensure that your email is verified in profile settings.
2. Select your **user menu** and then select **support** to access [!DNL Snowflake] support.
3. To create a support case, select **[!DNL + Support Case]**. Then, fill out the form with relevant details and attach any necessary files.
4. When finished, submit the case.

The endpoint resource ID is formatted as follows:

```shell
subscriptions/{SUBSCRIPTION_ID}/resourceGroups/az{REGION}-privatelink/providers/microsoft.network/privatelinkservices/sf-pvlinksvc-az{REGION}
```

+++Select to view example

```shell
/subscriptions/4575fb04-6859-4781-8948-7f3a92dc06a3/resourceGroups/azwestus2-privatelink/providers/microsoft.network/privatelinkservices/sf-pvlinksvc-azwestus2
```

+++

| Parameter | Description | Example |
| --- | --- | --- |
| `{SUBSCRIPTION_ID}` | The unique ID that identifies your [!DNL Azure] subscription. | `a1b2c3d4-5678-90ab-cdef-1234567890ab` |
| `{REGION}` | The [!DNL Azure] region of your [!DNL Snowflake] account. | `azwestus2` |

### Retrieve your private link configuration details

To retrieve your private link configuration details, you must run the following command in [!DNL Snowflake]:

```sql
USE ROLE accountadmin;
SELECT key, value::varchar
FROM TABLE(FLATTEN(input => PARSE_JSON(SYSTEM$GET_PRIVATELINK_CONFIG())));
```

Next, retrieve values for the following properties:

* `privatelink-account-url`
* `regionless-privatelink-account-url`
* `privatelink_ocsp-url`

Once you have retrieved the values, you can make the following call to create a private link for [!DNL Snowflake].

**Request**

The following request creates a private endpoint for [!DNL Snowflake]:

>[!BEGINTABS]

>[!TAB Template]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "{ENDPOINT_NAME}",
    "subscriptionId": "{AZURE_SUBSCRIPTION_ID}",
    "resourceGroupName": "{RESOURCE_GROUP_NAME}",
    "resourceName": "{SNOWFLAKE_ENDPOINT_SERVICE_NAME}",
    "fqdns": [
      "{PRIVATELINK_ACCOUNT_URL}",
      "{REGIONLESS_PRIVATELINK_ACCOUNT_URL}",
      "{PRIVATELINK_OCSP_URL}"
    ],
    "connectionSpec": {
      "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
      "version": "1.0"
    }
  }'
```

>[!TAB Example]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "TEST_Snowflake_PE",
    "subscriptionId": "4575fb04-6859-4781-8948-7f3a92dc06a3",
    "resourceGroupName": "azwestus2-privatelink",
    "resourceName": "sf-pvlinksvc-azwestus2",
    "fqdns": [
      "hf06619.west-us-2.privatelink.snowflakecomputing.com",
      "adobe-segmentationdbint.privatelink.snowflakecomputing.com",
      "ocsp.hf06619.west-us-2.privatelink.snowflakecomputing.com"
    ],
    "connectionSpec": {
      "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
      "version": "1.0"
    }
  }'
```

>[!ENDTABS]

-->