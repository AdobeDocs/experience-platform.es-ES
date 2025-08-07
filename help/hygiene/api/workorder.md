---
title: Registrar órdenes de trabajo eliminadas
description: Aprenda a utilizar el extremo /workorder en la API de higiene de datos para administrar las órdenes de trabajo de eliminación de registros en Adobe Experience Platform. Esta guía cubre las cuotas, los plazos de procesamiento y el uso de la API.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 4f4b668c2b29228499dc28b2c6c54656e98aaeab
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 2%

---

# Registrar órdenes de trabajo eliminadas {#work-order-endpoint}

Use el extremo `/workorder` en la API de higiene de datos para crear, ver y administrar órdenes de trabajo de eliminación de registros en Adobe Experience Platform. Las órdenes de trabajo le permiten controlar, monitorizar y rastrear la eliminación de datos en conjuntos de datos para ayudarle a mantener la calidad de los datos y admitir los estándares de gobernanza de datos de su organización.

>[!IMPORTANT]
>
>Las órdenes de trabajo de eliminación de registros son para limpiar, eliminar datos anónimos o minimizar datos. **No utilice órdenes de trabajo de eliminación de registros para solicitudes de derechos de titulares de datos conforme a normas de privacidad como el RGPD.** Para casos de uso de cumplimiento, use [Adobe Experience Platform Privacy Service](../../privacy-service/home.md).

## Introducción

Antes de comenzar, consulte la [descripción general](./overview.md) para obtener información sobre los encabezados necesarios, cómo leer llamadas de API de ejemplo y dónde encontrar documentación relacionada.

## Cuotas y plazos de procesamiento {#quotas}

Las órdenes de trabajo de eliminación de registros están sujetas a límites de envío de identificadores diarios y mensuales, determinados por el derecho de licencia de su organización. Estos límites se aplican a las solicitudes de eliminación de registros basadas en la IU y la API.

>[!NOTE]
>
>Puede enviar hasta **1.000.000 de identificadores por día**, pero solo si la cuota mensual restante lo permite. Si su límite mensual es inferior a 1 millón, sus envíos diarios no pueden exceder ese límite.

### Derecho de envío mensual por producto {#quota-limits}

La siguiente tabla muestra los límites de envío de identificadores por producto y nivel de asignación de derechos. Para cada producto, el límite mensual es el menor de dos valores: un límite de identificador fijo o un umbral basado en porcentajes y vinculado al volumen de datos con licencia.

| Producto | Descripción del derecho | Límite mensual (el que sea menor) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o el 5 % de la audiencia direccionable |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o el 10 % de la audiencia direccionable |
| Customer Journey Analytics | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o 100 identificadores por millón de filas de CJA de derechos |
| Customer Journey Analytics | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o 200 identificadores por millón de filas de CJA de derechos |

>[!NOTE]
>
>La mayoría de las organizaciones tendrán límites mensuales más bajos en función de su audiencia direccionable real o de los derechos de fila de CJA.

>[!NOTE]
>
>Las cuotas se restablecen el primer día de cada mes calendario. La cuota no utilizada **no** se transfiere.

>[!NOTE]
>
>El uso de la cuota se basa en las asignaciones mensuales con licencia de su organización para **identificadores enviados**. Las cuotas no se aplican mediante medidas de protección del sistema, pero pueden vigilarse y revisarse.\
>Registrar la capacidad de eliminación de órdenes de trabajo es un **servicio compartido**. Su límite mensual refleja el derecho más alto en Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics y cualquier complemento de Shield aplicable.

### Tiempos de procesamiento para los envíos de identificadores {#sla-processing-timelines}

Después del envío, las órdenes de trabajo de eliminación de registros se ponen en cola y se procesan según su nivel de asignación de derechos.

| Descripción del producto y los derechos | Duración de cola | Tiempo máximo de procesamiento (SLA) |
|------------------------------------|---------------------|-------------------------------|
| Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Hasta 15 días | 30 días |
| Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | Normalmente 24 horas | 15 días |

Si su organización requiere límites más altos, póngase en contacto con su representante de Adobe para obtener una revisión de las autorizaciones.

>[!TIP]
>
>Para comprobar el uso actual de la cuota o el nivel de derechos, consulte la [Guía de referencia de cuotas](../api/quota.md).

## Lista de órdenes de trabajo eliminadas de registro {#list}

Recupere una lista paginada de órdenes de trabajo de eliminación de registros para operaciones de higiene de datos en su organización. Filtre los resultados mediante parámetros de consulta. Cada registro de orden de trabajo incluye el tipo de acción (como `identity-delete`), el estado, el conjunto de datos relacionado, los detalles del usuario y los metadatos de auditoría.

**Formato de API**

```http
GET /workorder
```

En la tabla siguiente se describen los parámetros de consulta disponibles para enumerar las órdenes de trabajo de eliminación de registros.

| Parámetro de consulta | Descripción |
| --------------- | ------------|
| `search` | Coincidencia parcial que no distingue entre mayúsculas y minúsculas (búsqueda con comodines) en todos los campos: author, displayName, description o datasetName. También coincide con el ID de caducidad exacto. |
| `type` | Filtrar los resultados por tipo de orden de trabajo (por ejemplo, `identity-delete`). |
| `status` | Lista de estados de orden de trabajo separados por comas. Los valores de estado distinguen entre mayúsculas y minúsculas.<br>Enumeración: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | Busque a la persona que actualizó la orden de trabajo más recientemente (o al creador original). Acepta patrón SQL o literal. |
| `displayName` | Coincidencia sin distinción de mayúsculas y minúsculas en el nombre para mostrar de la orden de trabajo. |
| `description` | Coincidencia sin distinción de mayúsculas y minúsculas en la descripción de la orden de trabajo. |
| `workorderId` | Coincidencia exacta del ID de orden de trabajo. |
| `sandboxName` | Coincidencia exacta con el nombre de la zona protegida utilizado en la solicitud, o use `*` para incluir todas las zonas protegidas. |
| `fromDate` | Filtre por órdenes de trabajo creadas en esta fecha o después de ella. Requiere que se establezca `toDate`. |
| `toDate` | Filtrar por órdenes de trabajo creadas en esta fecha o antes. Requiere que se establezca `fromDate`. |
| `filterDate` | Devuelve únicamente las órdenes de trabajo creadas, actualizadas o cambiadas en esta fecha. |
| `page` | Índice de página a devolver (comienza en 0). |
| `limit` | Resultados máximos por página (1-100, predeterminado: 25). |
| `orderBy` | Orden de los resultados. Utilice el prefijo `+` o `-` para ascendente/descendente. Ejemplo: `orderBy=-datasetName`. |
| `properties` | Lista separada por comas de campos adicionales para incluir por resultado. Opcional. |


**Solicitud**

La siguiente solicitud recupera todas las órdenes de trabajo de eliminación de registros completadas, con un límite de dos por página:

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista paginada de órdenes de trabajo de eliminación de registros.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

En la tabla siguiente se describen las propiedades de la respuesta.

| Propiedad | Descripción |
| --- | --- |
| `results` | Matriz de objetos de orden de trabajo de eliminación de registros. Cada objeto contiene los campos siguientes. |
| `workorderId` | Identificador único de la orden de trabajo de eliminación de registros. |
| `orgId` | Su identificador único de organización. |
| `bundleId` | El identificador único del paquete que contiene esta orden de trabajo de eliminación de registro. El agrupamiento permite que los servicios descendentes agrupen y procesen juntas varias solicitudes de eliminación. |
| `action` | Tipo de acción solicitado en la orden de trabajo. |
| `createdAt` | La marca de tiempo cuando se creó la orden de trabajo. |
| `updatedAt` | La marca de tiempo de la última actualización de la orden de trabajo. |
| `operationCount` | Número de operaciones incluidas en la orden de trabajo. |
| `targetServices` | Lista de servicios de destino para la orden de trabajo. |
| `status` | Estado actual de la orden de trabajo. Los valores posibles son: `received`, `validated`, `submitted`, `ingested`, `completed` y `failed`. |
| `createdBy` | Correo electrónico e identificador del usuario que creó la orden de trabajo. |
| `datasetId` | El identificador único del conjunto de datos asociado con la orden de trabajo. Si la solicitud se aplica a todos los conjuntos de datos, este campo se establecerá en TODOS. |
| `datasetName` | El nombre del conjunto de datos asociado con la orden de trabajo. |
| `displayName` | Una etiqueta en lenguaje natural para la orden de trabajo. |
| `description` | Descripción del propósito de la orden de trabajo. |
| `total` | Número total de órdenes de trabajo de eliminación de registros que coinciden con la consulta. |
| `count` | Número de órdenes de trabajo de eliminación de registros en la página actual. |
| `_links` | Paginación y vínculos de navegación. |
| `next` | Objeto con `href` (cadena) y `templated` (booleano) para la página siguiente. |
| `page` | Objeto con `href` (cadena) y `templated` (booleano) para la navegación de la página. |

{style="table-layout:auto"}

## Crear una orden de trabajo de eliminación de registros {#create}

Para eliminar registros asociados con una o más identidades de un único conjunto de datos o de todos los conjuntos de datos, realice una petición POST al extremo `/workorder`.

Las órdenes de trabajo se procesan de forma asíncrona y aparecen en la lista de órdenes de trabajo después del envío.

>[!TIP]
>
>Cada orden de trabajo de eliminación de registros enviada a través de la API puede incluir hasta **100,000 identidades**. Envíe tantas identidades por solicitud como sea posible para maximizar la eficacia. Evite los envíos de bajo volumen, como las órdenes de trabajo de un solo ID.

**Formato de API**

```http
POST /workorder
```

>[!NOTE]
>
>Solo puede eliminar registros de conjuntos de datos cuyo esquema XDM asociado defina una identidad principal o un mapa de identidad.

>[!NOTE]
>
>Si intenta crear una orden de trabajo de eliminación de registros para un conjunto de datos que ya tiene una caducidad activa, la solicitud devolverá HTTP 400 (Solicitud incorrecta). Una caducidad activa es cualquier eliminación programada que aún no se haya completado.

**Solicitud**

La siguiente solicitud elimina todos los registros asociados con las direcciones de correo electrónico especificadas de un conjunto de datos concreto.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

En la tabla siguiente se describen las propiedades para crear una orden de trabajo de eliminación de registros.

| Propiedad | Descripción |
| --- | --- |
| `displayName` | Una etiqueta legible en lenguaje natural para esta orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |
| `action` | Acción solicitada para la orden de trabajo de eliminación de registros. Para eliminar registros asociados a una identidad determinada, use `delete_identity`. |
| `datasetId` | El identificador único del conjunto de datos. Use el identificador del conjunto de datos para un conjunto de datos específico o `ALL` para dirigirse a todos los conjuntos de datos. Los conjuntos de datos deben tener una identidad principal o un mapa de identidad. Si existe un mapa de identidad, estará presente como un campo de nivel superior denominado `identityMap`.<br>Tenga en cuenta que una fila del conjunto de datos puede tener muchas identidades en su mapa de identidad, pero solo una se puede marcar como principal. `"primary": true` debe incluirse para forzar a `id` a coincidir con una identidad principal. |
| `namespacesIdentities` | Una matriz de objetos, cada uno de los cuales contiene:<br><ul><li> `namespace`: un objeto con una propiedad `code` que especifica el área de nombres de identidad (por ejemplo, &quot;correo electrónico&quot;).</li><li> `IDs`: matriz de valores de identidad que se eliminarán para este espacio de nombres.</li></ul>Las áreas de nombres de identidad proporcionan contexto a los datos de identidad. Puede utilizar áreas de nombres estándar proporcionadas por Experience Platform o crear las suyas propias. Para obtener más información, consulte la [documentación del área de nombres de identidad](../../identity-service/features/namespaces.md) y la [especificación de la API del servicio de identidad](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

**Respuesta**

Una respuesta correcta devuelve los detalles de la nueva orden de trabajo de eliminación de registros.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

En la tabla siguiente se describen las propiedades de la respuesta.

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | Identificador único de la orden de trabajo de eliminación de registros. Utilice este valor para buscar el estado o los detalles de la eliminación. |
| `orgId` | Su identificador único de organización. |
| `bundleId` | El identificador único del paquete que contiene esta orden de trabajo de eliminación de registro. El agrupamiento permite que los servicios descendentes agrupen y procesen juntas varias solicitudes de eliminación. |
| `action` | El tipo de acción solicitado en la orden de trabajo de eliminación de registros. |
| `createdAt` | La marca de tiempo cuando se creó la orden de trabajo. |
| `updatedAt` | La marca de tiempo de la última actualización de la orden de trabajo. |
| `operationCount` | Número de operaciones incluidas en la orden de trabajo. |
| `targetServices` | Una lista de servicios de destino para la orden de trabajo de eliminación de registros. |
| `status` | Estado actual de la orden de trabajo de eliminación de registros. |
| `createdBy` | El correo electrónico y el identificador del usuario que creó la orden de trabajo de eliminación de registros. |
| `datasetId` | El identificador único del conjunto de datos. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. |
| `datasetName` | Nombre del conjunto de datos de la orden de trabajo de eliminación de este registro. |
| `displayName` | Una etiqueta legible en lenguaje natural para la orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |

{style="table-layout:auto"}

>[!NOTE]
>
>La propiedad action para registrar las órdenes de trabajo de eliminación es actualmente `identity-delete` en las respuestas de API. Si la API cambia para utilizar un valor diferente (como `delete_identity`), esta documentación se actualizará en consecuencia.

## Recuperar detalles de una orden de trabajo de eliminación de registros específica {#lookup}

Recupere información de una orden de trabajo de eliminación de registros específica realizando una petición GET a `/workorder/{WORKORDER_ID}`. La respuesta incluye el tipo de acción, el estado, el conjunto de datos asociado, la información de usuario y los metadatos de auditoría.

**Formato de API**

```http
GET /workorder/{WORKORDER_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | Identificador único de la orden de trabajo de eliminación de registros que está buscando. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la orden de trabajo de eliminación de registros especificada.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

En la tabla siguiente se describen las propiedades de la respuesta.

| Propiedad | Descripción |
| --- | --- |
| `workorderId` | Identificador único de la orden de trabajo de eliminación de registros. |
| `orgId` | Identificador único de su organización. |
| `bundleId` | El identificador único del paquete que contiene esta orden de trabajo de eliminación de registro. El agrupamiento permite que los servicios descendentes agrupen y procesen juntas varias solicitudes de eliminación. |
| `action` | El tipo de acción solicitado en la orden de trabajo de eliminación de registros. |
| `createdAt` | La marca de tiempo cuando se creó la orden de trabajo. |
| `updatedAt` | La marca de tiempo de la última actualización de la orden de trabajo. |
| `operationCount` | Número de operaciones incluidas en la orden de trabajo. |
| `targetServices` | Una lista de servicios de destino afectados por esta orden de trabajo de eliminación de registros. |
| `status` | Estado actual de la orden de trabajo de eliminación de registros. |
| `createdBy` | El correo electrónico y el identificador del usuario que creó la orden de trabajo de eliminación de registros. |
| `datasetId` | El identificador único del conjunto de datos asociado con la orden de trabajo. |
| `datasetName` | El nombre del conjunto de datos asociado con la orden de trabajo. |
| `displayName` | Una etiqueta legible en lenguaje natural para la orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |

## Actualizar una orden de trabajo de eliminación de registros

Actualice `name` y `description` para una orden de trabajo de eliminación de registros realizando una petición PUT al extremo `/workorder/{WORKORDER_ID}`.

**Formato de API**

```http
PUT /workorder/{WORKORDER_ID}
```

En la tabla siguiente se describe el parámetro de esta solicitud.

| Parámetro | Descripción |
| --- | --- |
| `{WORK_ORDER_ID}` | Identificador único de la orden de trabajo de eliminación de registros que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

En la tabla siguiente se describen las propiedades que se pueden actualizar.

| Propiedad | Descripción |
| --- | --- |
| `name` | La etiqueta legible en lenguaje natural actualizada para la orden de trabajo de eliminación de registros. |
| `description` | Descripción actualizada de la orden de trabajo de eliminación de registros. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve la solicitud de orden de trabajo actualizada.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
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
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | Identificador único de la orden de trabajo de eliminación de registros. |
| `orgId` | Identificador único de su organización. |
| `bundleId` | El identificador único del paquete que contiene esta orden de trabajo de eliminación de registro. El agrupamiento permite que los servicios descendentes agrupen y procesen juntas varias solicitudes de eliminación. |
| `action` | El tipo de acción solicitado en la orden de trabajo de eliminación de registros. |
| `createdAt` | La marca de tiempo cuando se creó la orden de trabajo. |
| `updatedAt` | La marca de tiempo de la última actualización de la orden de trabajo. |
| `operationCount` | Número de operaciones incluidas en la orden de trabajo. |
| `targetServices` | Una lista de servicios de destino afectados por esta orden de trabajo de eliminación de registros. |
| `status` | Estado actual de la orden de trabajo de eliminación de registros. Los valores posibles son: `received`, `validated`, `submitted`, `ingested`, `completed` y `failed`. |
| `createdBy` | El correo electrónico y el identificador del usuario que creó la orden de trabajo de eliminación de registros. |
| `datasetId` | El identificador único del conjunto de datos asociado con la orden de trabajo de eliminación de registros. |
| `datasetName` | El nombre del conjunto de datos asociado con la orden de trabajo de eliminación de registros. |
| `displayName` | Una etiqueta legible en lenguaje natural para la orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |
| `productStatusDetails` | Una matriz que enumera el estado actual de los procesos descendentes de la solicitud. Cada objeto contiene:<ul><li>`productName`: nombre del servicio descendente.</li><li>`productStatus`: el estado de procesamiento actual del servicio descendente.</li><li>`createdAt`: marca de tiempo en la que el servicio publicó el estado más reciente.</li></ul>Esta propiedad está disponible después de que la orden de trabajo se envíe a los servicios descendentes para comenzar a procesarse. |

{style="table-layout:auto"}
