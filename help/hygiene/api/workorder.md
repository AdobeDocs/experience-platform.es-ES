---
title: Registrar Solicitudes De Eliminación (Extremo De Orden De Trabajo)
description: El extremo /workorder de la API de higiene de datos le permite administrar mediante programación las tareas de eliminación de identidades.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: d569b1d04fa76e0a0e48364a586e8a1a773b9bf2
workflow-type: tm+mt
source-wordcount: '1505'
ht-degree: 2%

---

# Registrar solicitudes de eliminación (extremo de pedido de trabajo) {#work-order-endpoint}

El extremo `/workorder` de la API de higiene de datos le permite administrar mediante programación las solicitudes de eliminación de registros en Adobe Experience Platform.

>[!IMPORTANT]
> 
>Las eliminaciones de registros están pensadas para utilizarse para limpiar, eliminar datos anónimos o minimizar datos. Son **no** para usar en solicitudes de derechos de titulares de datos (cumplimiento) relacionadas con normas de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de cumplimiento, usa [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) en su lugar.

## Introducción

El extremo utilizado en esta guía forma parte de la API de higiene de datos. Antes de continuar, revise la [descripción general](./overview.md) para ver vínculos a documentación relacionada, una guía para leer las llamadas de API de ejemplo en este documento e información importante con respecto a los encabezados necesarios para realizar correctamente llamadas a cualquier API de Experience Platform.

## Cuotas y plazos de procesamiento {#quotas}

Las solicitudes de eliminación de registros están sujetas a límites diarios y mensuales de envío de identificadores, determinados por el derecho de licencia de su organización. Estos límites se aplican a solicitudes de eliminación basadas en la interfaz de usuario y la API.

>[!NOTE]
>
>Puede enviar hasta **1.000.000 de identificadores por día**, pero solo si la cuota mensual restante lo permite. Si su límite mensual es inferior a 1 millón, sus envíos diarios no pueden exceder ese límite.

### Derecho de envío mensual por producto {#quota-limits}

En la tabla siguiente se describen los límites de envío de identificadores por producto y nivel de asignación de derechos. Para cada producto, el límite mensual es el menor de dos valores: un límite de identificador fijo o un umbral basado en porcentajes y vinculado al volumen de datos con licencia.

| Producto | Descripción del derecho | Límite mensual (el que sea menor) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o el 5 % de la audiencia direccionable |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o el 10 % de la audiencia direccionable |
| Customer Journey Analytics | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o 100 identificadores por millón de filas de CJA de derechos |
| Customer Journey Analytics | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o 200 identificadores por millón de filas de CJA de derechos |

>[!NOTE]
>
> La mayoría de las organizaciones tendrán límites mensuales más bajos en función de su audiencia direccionable real o de los derechos de fila de CJA.

Las cuotas se restablecen el primer día de cada mes calendario. La cuota no utilizada **no** se transfiere.

>[!NOTE]
>
>Las cuotas se basan en los derechos mensuales con licencia de su organización para **identificadores enviados**. Estas no se aplican mediante protecciones del sistema, pero se pueden supervisar y revisar.
>
>La eliminación de registros es un **servicio compartido**. Su límite mensual refleja el derecho más alto en Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics y cualquier complemento de Shield aplicable.

### Tiempos de procesamiento para los envíos de identificadores {#sla-processing-timelines}

Después del envío, las solicitudes de eliminación de registros se ponen en cola y se procesan según su nivel de asignación de derechos.

| Descripción del producto y los derechos | Duración de cola | Tiempo máximo de procesamiento (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Hasta 15 días | 30 días |
| Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Normalmente 24 horas | 15 días |

Si su organización requiere límites más altos, póngase en contacto con su representante de Adobe para obtener una revisión de las autorizaciones.

>[!TIP]
>
>Para comprobar el uso actual de la cuota o el nivel de derechos, consulte la [Guía de referencia de cuotas](../api/quota.md).

## Crear una solicitud de eliminación de registro {#create}

Puede eliminar una o más identidades de un único conjunto de datos o de todos ellos realizando una petición POST al extremo `/workorder`.

>[!TIP]
>
>Cada solicitud de eliminación de registro enviada a través de la API puede incluir hasta **100,000 identidades**. Para maximizar la eficacia, envíe tantas identidades por solicitud como sea posible y evite envíos de bajo volumen, como órdenes de trabajo de ID único.

**Formato de API**

```http
POST /workorder
```

>[!NOTE]
>
>Las solicitudes del Ciclo de vida de datos solo pueden modificar conjuntos de datos basados en identidades principales o en un mapa de identidad. Una solicitud debe especificar la identidad principal o proporcionar un mapa de identidad.

**Solicitud**

Según el valor de `datasetId` proporcionado en la carga útil de la solicitud, la llamada de API eliminará las identidades de todos los conjuntos de datos o de un único conjunto de datos que especifique. La siguiente solicitud elimina tres identidades de un conjunto de datos específico.

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
| `action` | Acción que se va a realizar. El valor debe establecerse en `delete_identity` para las eliminaciones de registros. |
| `datasetId` | Si está eliminando de un único conjunto de datos, este valor debe ser el ID del conjunto de datos en cuestión. Si está eliminando de todos los conjuntos de datos, establezca el valor en `ALL`.<br><br>Si está especificando un solo conjunto de datos, el esquema XDM (Experience Data Model) asociado del conjunto de datos debe tener definida una identidad principal. Si el conjunto de datos no tiene una identidad principal, debe tener un mapa de identidad para que lo modifique una solicitud del ciclo vital de datos.<br>Si existe un mapa de identidad, estará presente como un campo de nivel superior denominado `identityMap`.<br>Tenga en cuenta que una fila del conjunto de datos puede tener muchas identidades en su mapa de identidad, pero solo una se puede marcar como principal. `"primary": true` debe incluirse para forzar a `id` a coincidir con una identidad principal. |
| `displayName` | El nombre para mostrar de la solicitud de eliminación de registro. |
| `description` | Descripción de la solicitud de eliminación de registro. |
| `identities` | Matriz que contiene las identidades de al menos un usuario cuya información desea eliminar. Cada identidad consta de [área de nombres de identidad](../../identity-service/features/namespaces.md) y un valor:<ul><li>`namespace`: contiene una sola propiedad de cadena, `code`, que representa el área de nombres de identidad. </li><li>`id`: el valor de identidad.</ul>Si `datasetId` especifica un único conjunto de datos, cada entidad bajo `identities` debe usar el mismo área de nombres de identidad que la identidad principal del esquema.<br><br>Si `datasetId` está establecido en `ALL`, la matriz `identities` no está restringida a ningún área de nombres individual, ya que cada conjunto de datos puede ser diferente. Sin embargo, sus solicitudes siguen restringiendo las áreas de nombres disponibles para su organización, tal como lo informó [Identity Service](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

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

Después de [crear una solicitud de eliminación de registro](#create), puede comprobar su estado mediante una solicitud de GET.

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
| `productStatusDetails` | Una matriz que enumera el estado actual de los procesos descendentes relacionados con la solicitud. Cada objeto de matriz contiene las siguientes propiedades:<ul><li>`productName`: nombre del servicio descendente.</li><li>`productStatus`: el estado de procesamiento actual de la solicitud del servicio descendente.</li><li>`createdAt`: una marca de tiempo del momento en el que el servicio publicó el estado más reciente.</li></ul> |

## Actualizar una solicitud de eliminación de registro

Puede actualizar `displayName` y `description` para una eliminación de registro realizando una petición PUT.

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
    "workorderId": "DI-61828416-963a-463f-91c1-dbc4d0ddbd43",
    "orgId": "{ORG_ID}",
    "bundleId": "BN-aacacc09-d10c-48c5-a64c-2ced96a78fca",
    "action": "identity-delete",
    "createdAt": "2024-06-12T20:02:49.398448Z",
    "updatedAt": "2024-06-13T21:35:01.944749Z",
    "operationCount": 1,
    "status": "ingested",
    "createdBy": "{USER_ID}",
    "datasetId": "666950e6b7e2022c9e7d7a33",
    "datasetName": "Acme_Dataset_E2E_Identity_Map_Schema_5_1718178022379",
    "displayName": "Updated Display Name",
    "description": "Updated Description",
    "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
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
| `productStatusDetails` | Una matriz que enumera el estado actual de los procesos descendentes relacionados con la solicitud. Cada objeto de matriz contiene las siguientes propiedades:<ul><li>`productName`: nombre del servicio descendente.</li><li>`productStatus`: el estado de procesamiento actual de la solicitud del servicio descendente.</li><li>`createdAt`: una marca de tiempo del momento en el que el servicio publicó el estado más reciente.</li></ul> |

{style="table-layout:auto"}
