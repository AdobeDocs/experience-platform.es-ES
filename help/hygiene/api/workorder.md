---
title: Punto final de API de orden de trabajo
description: El extremo /workorder de la API de higiene de datos le permite administrar mediante programación las tareas de eliminación de identidades.
badgeBeta: label="Beta" type="Informative"
role: Developer
badge: Beta
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 2259bf70e1503cf468f72a73345592ace0f58f63
workflow-type: tm+mt
source-wordcount: '1278'
ht-degree: 2%

---

# Punto final de orden de trabajo {#work-order-endpoint}

El `/workorder` Este extremo de la API de higiene de datos le permite administrar mediante programación las solicitudes de eliminación de registros en Adobe Experience Platform.

>[!IMPORTANT]
> 
>La función de eliminación de registros está actualmente en versión beta y solo está disponible en un **versión limitada**. No está disponible para todos los clientes. Las solicitudes de eliminación de registros solo están disponibles para organizaciones en la versión limitada.
>
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Lo son **no** para su uso en solicitudes de derechos de titulares de los datos (cumplimiento) relacionadas con regulaciones de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de conformidad, utilice [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, consulte la [descripción general](./overview.md) para obtener vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Crear una solicitud de eliminación de registro {#create}

Puede eliminar una o más identidades de un único conjunto de datos o de todos ellos realizando una solicitud del POST a `/workorder` punto final.

>[!IMPORTANT]
> 
>Existen diferentes límites para el número total de eliminaciones de registros de identidad únicos que se pueden enviar cada mes. Estos límites se basan en el acuerdo de licencia. Las organizaciones que han comprado todas las ediciones de Adobe Real-time Customer Data Platform y Adobe Journey Optimizer pueden enviar hasta 100 000 eliminaciones de registros de identidad cada mes. Organizaciones que han realizado compras **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad** puede enviar hasta 600 000 eliminaciones de registros de identidad cada mes.<br>Un solo [registrar la solicitud de eliminación a través de la IU](../ui/record-delete.md) le permite enviar 10 000 ID al mismo tiempo. El método API para eliminar registros permite enviar 100 000 ID al mismo tiempo.<br>Se recomienda enviar tantos ID por solicitud como sea posible, hasta el límite de su ID. Cuando tenga intención de eliminar un gran volumen de ID, debe evitar enviar un bajo volumen o una sola solicitud de eliminación de ID por registro.

**Formato de API**

```http
POST /workorder
```

>[!NOTE]
>
>Las solicitudes del Ciclo de vida de datos solo pueden modificar conjuntos de datos basados en identidades principales o en un mapa de identidad. Una solicitud debe especificar la identidad principal o proporcionar un mapa de identidad.

**Solicitud**

Según el valor de la variable `datasetId` proporcionada en la carga útil de la solicitud, la llamada de API eliminará las identidades de todos los conjuntos de datos o de un único conjunto de datos que especifique. La siguiente solicitud elimina tres identidades de un conjunto de datos específico.

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
        "displayName": "Example Record Delete Request",
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
| `action` | Acción que se va a realizar. El valor debe establecerse en `delete_identity` para eliminaciones de registros. |
| `datasetId` | Si está eliminando de un único conjunto de datos, este valor debe ser el ID del conjunto de datos en cuestión. Si está eliminando de todos los conjuntos de datos, establezca el valor en `ALL`.<br><br>Si especifica un único conjunto de datos, el esquema del modelo de datos de experiencia (XDM) asociado al conjunto de datos debe tener definida una identidad principal. Si el conjunto de datos no tiene una identidad principal, debe tener un mapa de identidad para que lo modifique una solicitud del ciclo vital de datos.<br>Si existe un mapa de identidad, estará presente como un campo de nivel superior denominado `identityMap`.<br>Tenga en cuenta que una fila del conjunto de datos puede tener muchas identidades en su mapa de identidad, pero solo una se puede marcar como principal. `"primary": true` se debe incluir para forzar la `id` para que coincida con una identidad principal. |
| `displayName` | El nombre para mostrar de la solicitud de eliminación de registro. |
| `description` | Descripción de la solicitud de eliminación de registro. |
| `identities` | Matriz que contiene las identidades de al menos un usuario cuya información desea eliminar. Cada identidad consta de un [área de nombres de identidad](../../identity-service/features/namespaces.md) y un valor:<ul><li>`namespace`: contiene una sola propiedad de cadena, `code`, que representa el área de nombres de identidad. </li><li>`id`: El valor de identidad.</ul>If `datasetId` especifica un único conjunto de datos, cada entidad en `identities` debe utilizar el mismo área de nombres de identidad que la identidad principal del esquema.<br><br>If `datasetId` se establece en `ALL`, el `identities` La matriz no está restringida a un área de nombres única, ya que cada conjunto de datos puede ser diferente. Sin embargo, las solicitudes siguen restringiendo las áreas de nombres disponibles para su organización, tal como indica [Servicio de identidad](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la eliminación del registro.

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
  "displayName": "Example Record Delete Request",
  "description": "Cleanup identities required by Jira request 12345."
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | El ID del orden de eliminación. Se puede utilizar para buscar el estado de la eliminación más adelante. |
| `orgId` | Su ID de organización. |
| `bundleId` | El ID del paquete al que está asociado este orden de eliminación, que se utiliza con fines de depuración. Los servicios descendentes agrupan varios pedidos de eliminación para procesarlos. |
| `action` | Acción que está realizando la orden de trabajo. Para eliminaciones de registros, el valor es `identity-delete`. |
| `createdAt` | Una marca de tiempo del momento en el que se creó el pedido de eliminación. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó el orden de eliminación. |
| `status` | El estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
| `datasetId` | El ID del conjunto de datos sujeto a la solicitud. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |

{style="table-layout:auto"}

## Recuperar el estado de una eliminación de registro {#lookup}

Después de usted [crear una solicitud de eliminación de registro](#create), puede comprobar su estado mediante una solicitud de GET.

**Formato de API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | El `workorderId` de la eliminación de registro que está buscando. |

{style="table-layout:auto"}

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
  "displayName": "Example Record Delete Request",
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
| `bundleId` | El ID del paquete al que está asociado este orden de eliminación, que se utiliza con fines de depuración. Los servicios descendentes agrupan varios pedidos de eliminación para procesarlos. |
| `action` | Acción que está realizando la orden de trabajo. Para eliminaciones de registros, el valor es `identity-delete`. |
| `createdAt` | Una marca de tiempo del momento en el que se creó el pedido de eliminación. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó el orden de eliminación. |
| `status` | El estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
| `datasetId` | El ID del conjunto de datos sujeto a la solicitud. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |
| `productStatusDetails` | Una matriz que enumera el estado actual de los procesos descendentes relacionados con la solicitud. Cada objeto de matriz contiene las siguientes propiedades:<ul><li>`productName`: Nombre del servicio descendente.</li><li>`productStatus`: el estado de procesamiento actual de la solicitud del servicio descendente.</li><li>`createdAt`: Una marca de tiempo del momento en el que el servicio publicó el estado más reciente.</li></ul> |

## Actualizar una solicitud de eliminación de registro

Puede actualizar el `displayName` y `description` para eliminar un registro realizando una solicitud al PUT.

**Formato de API**

```http
PUT /workorder{WORK_ORDER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | El `workorderId` de la eliminación de registro que está buscando. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X PUT \
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
| `displayName` | Un nombre para mostrar actualizado para la solicitud de eliminación de registro. |
| `description` | Una descripción actualizada para la solicitud de eliminación de registro. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la eliminación del registro.

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
| `bundleId` | El ID del paquete al que está asociado este orden de eliminación, que se utiliza con fines de depuración. Los servicios descendentes agrupan varios pedidos de eliminación para procesarlos. |
| `action` | Acción que está realizando la orden de trabajo. Para eliminaciones de registros, el valor es `identity-delete`. |
| `createdAt` | Una marca de tiempo del momento en el que se creó el pedido de eliminación. |
| `updatedAt` | Una marca de tiempo de la última vez que se actualizó el orden de eliminación. |
| `status` | El estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
| `datasetId` | El ID del conjunto de datos sujeto a la solicitud. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |
| `productStatusDetails` | Una matriz que enumera el estado actual de los procesos descendentes relacionados con la solicitud. Cada objeto de matriz contiene las siguientes propiedades:<ul><li>`productName`: Nombre del servicio descendente.</li><li>`productStatus`: el estado de procesamiento actual de la solicitud del servicio descendente.</li><li>`createdAt`: Una marca de tiempo del momento en el que el servicio publicó el estado más reciente.</li></ul> |

{style="table-layout:auto"}
