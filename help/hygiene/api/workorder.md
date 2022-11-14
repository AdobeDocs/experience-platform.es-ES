---
title: Punto final de la API del pedido de trabajo
description: El extremo /workorder de la API de higiene de datos permite administrar mediante programación las tareas de eliminación para las identidades de los consumidores.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: b76e1bc6d5b346c32ea09612e24b68c6636f7deb
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 5%

---

# Punto final del pedido de trabajo

La variable `/workorder` en la API de higiene de datos le permite administrar mediante programación las solicitudes de eliminación de consumidores en Adobe Experience Platform.

>[!IMPORTANT]
>
>Las solicitudes de eliminación de consumidores solo están disponibles para las organizaciones que han comprado **Adobe Escudo Sanitario**.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [información general](./overview.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Crear una solicitud de eliminación de consumidor {#delete-consumers}

Puede eliminar una o más identidades de consumidores de un único conjunto de datos o de todos los conjuntos de datos realizando una solicitud de POST al `/workorder` punto final.

**Formato de API**

```http
POST /workorder
```

**Solicitud**

Según el valor de la variable `datasetId` proporcionado en la carga útil de la solicitud, la llamada de API eliminará las identidades de consumidor de todos los conjuntos de datos o de un único conjunto de datos que especifique. La siguiente solicitud elimina tres identidades de consumidor de un conjunto de datos específico.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "action": "delete_identity",
        "datasetId": "c48b51623ec641a2949d339bad69cb15",
        "displayName": "Example Consumer Delete Request",
        "description": "Cleanup identities required by Jira request 12345.",
        "identities": [
          {
            "namespace": {
              "code": "email"
            },
            "id": "poul.anderson@example.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cordwainer.smith@gmail.com"
          },
          {
            "namespace": {
              "code": "email"
            },
            "id": "cyril.kornbluth@yahoo.com"
          }
        ]
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `action` | La acción que se va a realizar. El valor debe establecerse en `delete_identity` para eliminaciones de consumidores. |
| `datasetId` | Si va a eliminar de un único conjunto de datos, este valor debe ser el ID del conjunto de datos en cuestión. Si va a eliminar de todos los conjuntos de datos, establezca el valor en `ALL`.<br><br>Si especifica un único conjunto de datos, el esquema del Modelo de datos de experiencia (XDM) asociado al conjunto de datos debe tener definida una identidad principal. |
| `displayName` | Nombre para mostrar de la solicitud de eliminación de consumidor. |
| `description` | Descripción de la solicitud de eliminación de consumidor. |
| `identities` | Matriz que contiene las identidades de al menos un usuario cuya información desea eliminar. Cada identidad consta de un [área de nombres de identidad](../../identity-service/namespaces.md) y un valor:<ul><li>`namespace`: Contiene una propiedad de cadena única, `code`, que representa el área de nombres de identidad. </li><li>`id`: El valor de identidad.</ul>If `datasetId` especifica un conjunto de datos único, cada entidad de `identities` debe utilizar el mismo área de nombres de identidad que la identidad principal del esquema.<br><br>If `datasetId` está configurado como `ALL`, el `identities` matriz no está restringida a un solo espacio de nombres, ya que cada conjunto de datos puede ser diferente. Sin embargo, las solicitudes siguen restringiendo los espacios de nombres disponibles para su organización, tal y como informa [Servicio de identidad](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la eliminación del consumidor.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | El ID del orden de eliminación. Se puede utilizar para buscar el estado de la eliminación más adelante. |
| `orgId` | Su ID de organización. |
| `bundleId` | El ID del paquete al que está asociada esta orden de eliminación, utilizado para la depuración. Los servicios descendentes agrupan varios pedidos de eliminación para procesarlos. |
| `action` | Acción que realiza la orden de trabajo. Para las eliminaciones de consumidores, el valor es `identity-delete`. |
| `createdAt` | Marca de tiempo del momento en que se creó el pedido de eliminación. |
| `updatedAt` | Marca de fecha y hora de la última actualización del pedido de eliminación. |
| `status` | Estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
| `datasetId` | El ID del conjunto de datos que está sujeto a la solicitud. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |

{style=&quot;table-layout:auto&quot;}

## Recuperar el estado de una eliminación de consumidor (#lookup)

Después [creación de una solicitud de eliminación de consumidor](#delete-consumers), puede comprobar su estado mediante una solicitud de GET.

**Formato de API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | La variable `workorderId` del cliente elimine que está buscando. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la operación de eliminación, incluido su estado actual.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName": "Example Consumer Delete Request",
  "description": "Cleanup identities required by Jira request 12345.",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | El ID del orden de eliminación. Se puede utilizar para buscar el estado de la eliminación más adelante. |
| `orgId` | Su ID de organización. |
| `bundleId` | El ID del paquete al que está asociada esta orden de eliminación, utilizado para la depuración. Los servicios descendentes agrupan varios pedidos de eliminación para procesarlos. |
| `action` | Acción que realiza la orden de trabajo. Para las eliminaciones de consumidores, el valor es `identity-delete`. |
| `createdAt` | Marca de tiempo del momento en que se creó el pedido de eliminación. |
| `updatedAt` | Marca de fecha y hora de la última actualización del pedido de eliminación. |
| `status` | Estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
| `datasetId` | El ID del conjunto de datos que está sujeto a la solicitud. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |
| `productStatusDetails` | Matriz que enumera el estado actual de los procesos descendentes relacionados con la solicitud. Cada objeto de matriz contiene las siguientes propiedades:<ul><li>`productName`: Nombre del servicio descendente.</li><li>`productStatus`: Estado de procesamiento actual de la solicitud desde el servicio descendente.</li><li>`createdAt`: Marca de fecha y hora en la que el servicio anunció el estado más reciente.</li></ul> |

## Actualizar una solicitud de eliminación de consumidor

Puede actualizar el `displayName` y `description` para eliminar un cliente realizando una solicitud de PUT.

**Formato de API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | La variable `workorderId` del cliente elimine que está buscando. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName" : "Update - displayName",
        "description" : "Update - description"
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `displayName` | Un nombre para mostrar actualizado para la solicitud de eliminación de consumidor. |
| `description` | Una descripción actualizada de la solicitud de eliminación de consumidor. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la eliminación del consumidor.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "bundleId": "BN-35c1676c-3b4f-4195-8d6c-7cf5aa21efdd",
  "action": "identity-delete",
  "createdAt": "2022-07-21T18:05:28.316029Z",
  "updatedAt": "2022-07-21T17:59:43.217801Z",
  "status": "received",
  "createdBy": "{USER_ID}",
  "datasetId": "c48b51623ec641a2949d339bad69cb15",
  "displayName" : "Update - displayName",
  "description" : "Update - description",
  "productStatusDetails": [
    {
        "productName": "Data Management",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:51:31.535872Z"
    },
    {
        "productName": "Identity Service",
        "productStatus": "success",
        "createdAt": "2022-08-08T16:43:46.331150Z"
    },
    {
        "productName": "Profile Service",
        "productStatus": "waiting",
        "createdAt": "2022-08-08T16:37:13.443481Z"
    }
  ]
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | El ID del orden de eliminación. Se puede utilizar para buscar el estado de la eliminación más adelante. |
| `orgId` | Su ID de organización. |
| `bundleId` | El ID del paquete al que está asociada esta orden de eliminación, utilizado para la depuración. Los servicios descendentes agrupan varios pedidos de eliminación para procesarlos. |
| `action` | Acción que realiza la orden de trabajo. Para las eliminaciones de consumidores, el valor es `identity-delete`. |
| `createdAt` | Marca de tiempo del momento en que se creó el pedido de eliminación. |
| `updatedAt` | Marca de fecha y hora de la última actualización del pedido de eliminación. |
| `status` | Estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
| `datasetId` | El ID del conjunto de datos que está sujeto a la solicitud. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |
| `productStatusDetails` | Matriz que enumera el estado actual de los procesos descendentes relacionados con la solicitud. Cada objeto de matriz contiene las siguientes propiedades:<ul><li>`productName`: Nombre del servicio descendente.</li><li>`productStatus`: Estado de procesamiento actual de la solicitud desde el servicio descendente.</li><li>`createdAt`: Marca de fecha y hora en la que el servicio anunció el estado más reciente.</li></ul> |

{style=&quot;table-layout:auto&quot;}
