---
title: Punto final de la API del pedido de trabajo
description: El extremo /workorder de la API de higiene de datos permite administrar mediante programación las tareas de eliminación para las identidades de los consumidores.
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
hide: true
hidefromtoc: true
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 5%

---

# Punto final del pedido de trabajo

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido el Escudo de la salud.

La variable `/workorder` en la API de higiene de datos le permite administrar mediante programación tareas de eliminación para identidades de consumidores en Adobe Experience Platform.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [información general](./overview.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante sobre los encabezados necesarios para realizar llamadas correctamente a cualquier API de Experience Platform.

## Eliminar identidades {#delete-identities}

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
| `action` | La acción que se va a realizar. El valor debe establecerse en `delete_identity` al eliminar identidades. |
| `datasetId` | Si va a eliminar de un único conjunto de datos, este valor debe ser el ID del conjunto de datos en cuestión. Si va a eliminar de todos los conjuntos de datos, establezca el valor en `ALL`.<br><br>Si especifica un único conjunto de datos, el esquema del Modelo de datos de experiencia (XDM) asociado al conjunto de datos debe tener definida una identidad principal. |
| `identities` | Matriz que contiene las identidades de al menos un usuario cuya información desea eliminar. Cada identidad consta de un [área de nombres de identidad](../../identity-service/namespaces.md) y un valor:<ul><li>`namespace`: Contiene una propiedad de cadena única, `code`, que representa el área de nombres de identidad. </li><li>`id`: El valor de identidad.</ul>If `datasetId` especifica un conjunto de datos único, cada entidad de `identities` debe utilizar el mismo área de nombres de identidad que la identidad principal del esquema.<br><br>If `datasetId` está configurado como `ALL`, el `identities` matriz no está restringida a un solo espacio de nombres, ya que cada conjunto de datos puede ser diferente. Sin embargo, las solicitudes siguen restringiendo los espacios de nombres disponibles para su organización, tal y como informa [Servicio de identidad](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la eliminación de identidad.

```json
{
  "workorderId": "a15345b8-a2d6-4d6f-b33c-5b593e86439a",
  "orgId": "{ORG_ID}",
  "batchId": "fc0cf8af-a176-4107-a31a-381d6af38cbe",
  "bundleOrdinal": 1,
  "payloadByteSize": 362,
  "operationCount": 3,
  "createdAt": 1652122493242,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | El ID del orden de eliminación. Se puede utilizar para buscar el estado de la eliminación más adelante. |
| `orgId` | El ID de su organización. |
| `batchId` | El ID del lote al que está asociada esta orden de eliminación, utilizado para la depuración. Los múltiples pedidos de eliminación se agrupan en un lote para que los servicios descendentes los procesen. |
| `bundleOrdinal` | El orden en el que se recibió este pedido de eliminación cuando se agrupó en un lote para el procesamiento descendente. Se utiliza con fines de depuración. |
| `payloadByteSize` | El tamaño, en bytes, de la lista de identidades proporcionadas en la carga útil de solicitud que creó esta orden de eliminación. |
| `operationCount` | Número de identidades a las que se aplica esta orden de eliminación. |
| `createdAt` | Marca de tiempo del momento en que se creó el pedido de eliminación. |
| `responseMessage` | La respuesta más reciente devuelta por el sistema. Si se produce un error durante el procesamiento, este valor es una cadena JSON que contiene información detallada del error para ayudarle a comprender qué puede haber salido mal. |
| `status` | Estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |

{style=&quot;table-layout:auto&quot;}

## Enumerar los estados de todas las eliminaciones de identidad {#list}

Puede enumerar los estados de todas las eliminaciones de identidad realizando una solicitud de GET.

**Formato de API**

```http
GET /workorder?{QUERY_PARAMS}
```

| Parámetro | Descripción |
| --- | --- |
| `{QUERY_PARAMS}` | Una lista de parámetros de consulta opcionales para la llamada de lista, con varios parámetros separados por `&` caracteres. Los parámetros de consulta aceptados son los siguientes:<ul><li>`data` - Un valor booleano que, cuando se establece en `true`, incluye todos los datos de solicitud y respuesta adicionales recibidos para la solicitud de eliminación. El valor predeterminado es `false`.</li><li>`start` - Marca de fecha y hora del principio del periodo para buscar solicitudes de eliminación.</li><li>`end` : marca de tiempo del final del periodo para buscar solicitudes de eliminación.</li><li>`page` - La página de respuesta específica que se va a devolver.</li><li>`limit` - El número de registros que se mostrarán por página.</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de todas las operaciones de eliminación, incluido su estado actual. La respuesta de ejemplo siguiente se ha truncado para el espacio.

```json
{
  "results": [
    {
      "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
      "orgId": "{ORG_ID}",
      "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650929265295,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    },
    {
      "workorderId": "e4a662e8-a5f3-497d-8d6a-d26970d8732b",
      "orgId": "{ORG_ID}",
      "batchId": "74fe4e38-ed42-4ca5-8bee-88bdc03ae786",
      "bundleOrdinal": 1,
      "payloadByteSize": 164,
      "operationCount": 1,
      "createdAt": 1650931057899,
      "responseMessage": "received",
      "status": "received",
      "createdBy": "{USER_ID}"
    }
  ],
  "total": 200,
  "count": 50,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=50",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `results` | Contiene la lista de pedidos de eliminación y sus detalles. Para obtener más información sobre las propiedades de una orden de eliminación, consulte la respuesta de ejemplo en la sección de [búsqueda de una orden de eliminación](#lookup). |
| `total` | Número total de pedidos de eliminación encontrados según los filtros actuales. |
| `count` | Número total de pedidos de eliminación encontrados en cada página de la respuesta. |
| `_links` | Contiene información de paginación para ayudarle a explorar el resto de la respuesta:<ul><li>`next`: Contiene una dirección URL para la página siguiente de la respuesta.</li><li>`page`: Contiene una plantilla de dirección URL para acceder a otra página de la respuesta o ajustar el número de elementos devueltos en cada página.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Recuperar el estado de una eliminación de identidad (#lookup)

Después de enviar una solicitud a [eliminar una identidad](#delete-identities), puede comprobar su estado mediante una solicitud de GET.

**Formato de API**

```http
GET /workorder/{WORK_ORDER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | La variable `workorderId` de la eliminación de identidad que está buscando. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/ID6c28e2d2d2b54079aadf7be94568f6d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la operación de eliminación, incluido su estado actual.

```json
{
  "workorderId": "4fe4be4f-47f3-477a-927e-f908452513f6",
  "orgId": "{ORG_ID}",
  "batchId": "e62cd6b6-ce3e-49e0-9221-ba1f286a851c",
  "bundleOrdinal": 1,
  "payloadByteSize": 164,
  "operationCount": 1,
  "createdAt": 1650929265295,
  "responseMessage": "received",
  "status": "received",
  "createdBy": "{USER_ID}"
}
```

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | El ID del orden de eliminación. Se puede utilizar para buscar el estado de la eliminación más adelante. |
| `orgId` | El ID de su organización. |
| `batchId` | El ID del lote al que está asociada esta orden de eliminación, utilizado para la depuración. Los múltiples pedidos de eliminación se agrupan en un lote para que los servicios descendentes los procesen. |
| `bundleOrdinal` | El orden en el que se recibió este pedido de eliminación cuando se agrupó en un lote para el procesamiento descendente. Se utiliza con fines de depuración. |
| `payloadByteSize` | El tamaño, en bytes, de la lista de identidades proporcionadas en la carga útil de solicitud que creó esta orden de eliminación. |
| `operationCount` | Número de identidades a las que se aplica esta orden de eliminación. |
| `createdAt` | Marca de tiempo del momento en que se creó el pedido de eliminación. |
| `responseMessage` | La respuesta más reciente devuelta por el sistema. Si se produce un error durante el procesamiento, este valor es una cadena JSON que contiene información detallada del error para ayudarle a comprender qué puede haber salido mal. |
| `status` | Estado actual del orden de eliminación. |
| `createdBy` | El usuario que creó el orden de eliminación. |
