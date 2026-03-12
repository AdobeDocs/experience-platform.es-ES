---
title: Registrar órdenes de trabajo eliminadas
description: Aprenda a utilizar el extremo /workorder en la API de higiene de datos para administrar las órdenes de trabajo de eliminación de registros en Adobe Experience Platform. Esta guía cubre las cuotas, los plazos de procesamiento y el uso de la API.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: 5ca3e4feae3096e41689610ac3afac7e93047149
workflow-type: tm+mt
source-wordcount: '3316'
ht-degree: 1%

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

La siguiente tabla muestra los límites de envío de identificadores por producto y nivel de asignación de derechos. Para cada producto, el límite mensual es el menor de dos valores: un límite de identificador fijo o un umbral basado en porcentajes y vinculado al volumen de datos con licencia. En la práctica, la mayoría de las organizaciones tienen límites mensuales más bajos en función de su audiencia direccionable real o de los derechos de fila de Adobe Customer Journey Analytics.

| Producto | Descripción del derecho | Límite mensual (el que sea menor) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o el 5 % de la audiencia direccionable |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o el 10 % de la audiencia direccionable |
| Customer Journey Analytics | Sin el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 2 000 000 de identificadores o 100 identificadores por millón de filas de Customer Journey Analytics de derechos |
| Customer Journey Analytics | Con el complemento Escudo de privacidad y seguridad o Escudo de atención sanitaria | 15 000 000 de identificadores o 200 identificadores por millón de filas de Customer Journey Analytics de derechos |

>[!NOTE]
>
>- Las cuotas se restablecen el primer día de cada mes calendario. La cuota no utilizada **no** se transfiere.
>- El uso de la cuota se basa en las asignaciones mensuales con licencia de su organización para **identificadores enviados**. Las cuotas no se aplican mediante medidas de protección del sistema, pero pueden vigilarse y revisarse.
>- Registrar la capacidad de eliminación de órdenes de trabajo es un **servicio compartido**. Su límite mensual refleja el derecho más alto en Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics y cualquier complemento de Shield aplicable.

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
        "identity",
        "ajo"
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
| `targetServices` | El conjunto de servicios de destino que procesó la eliminación. El valor predeterminado depende de los derechos de su organización. Para organizaciones con Real-Time CDP o Adobe Journey Optimizer, el valor predeterminado es el conjunto completo de servicios compatibles (`["datalake", "identity", "profile", "ajo"]`). Para organizaciones solo de Customer Journey Analytics (sin un derecho de Perfil del cliente en tiempo real), el único valor válido es [&quot;datalake&quot;]. |
| `status` | Estado actual de la orden de trabajo. Los valores posibles son: `received`, `validated`, `submitted`, `ingested`, `completed` y `failed`. |
| `createdBy` | Correo electrónico e identificador del usuario que creó la orden de trabajo. |
| `datasetId` | Los conjuntos de datos a los que se dirige la orden de trabajo: un único ID de conjunto de datos, una lista separada por comas de ID de conjuntos de datos (varios conjuntos de datos) o el literal `ALL`. Cuando la solicitud utilizó el modo de solo perfil, este valor es `ALL`. |
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

Para eliminar registros asociados con una o más identidades de un único conjunto de datos, varios conjuntos de datos o todos ellos, realice una petición POST al extremo `/workorder`.

Las órdenes de trabajo se procesan de forma asíncrona y aparecen en la lista de órdenes de trabajo después del envío. Las opciones de varios conjuntos de datos y solo perfiles (servicios segmentados) generalmente están disponibles para todos los clientes a partir de la versión de Experience Platform de marzo de 2026.

>[!TIP]
>
>Cada orden de trabajo de eliminación de registros enviada a través de la API puede incluir hasta **100,000 identidades**. Envíe tantas identidades por solicitud como sea posible para maximizar la eficacia. Evite los envíos de bajo volumen, como las órdenes de trabajo de un solo ID.

**Formato de API**

```http
POST /workorder
```

>[!IMPORTANT]
>
>Registrar órdenes de trabajo de eliminación actúa exclusivamente en el campo **identidad principal**. Se aplican las siguientes limitaciones:
>
>- **El esquema del conjunto de datos debe definir una identidad principal o un mapa de identidad.** Solo puede eliminar registros de conjuntos de datos cuyo esquema XDM asociado defina una identidad principal o un mapa de identidad.
>- **Las identidades secundarias no se analizan.** Si un conjunto de datos contiene varios campos de identidad, solo se utilizará la identidad principal para la coincidencia. Los registros no se pueden segmentar ni eliminar en función de identidades no principales.
>- Se omiten **registros sin una identidad principal completada.** Si un registro no tiene rellenados los metadatos de identidad principales, no se puede eliminar.
>- **Los datos ingeridos antes de la configuración de identidad no son elegibles.** Si el campo de identidad principal se agregó a un esquema después de la ingesta de datos, los registros ingeridos anteriormente no se pueden eliminar mediante órdenes de trabajo de eliminación de registros.

>[!NOTE]
>
>Si intenta crear una orden de trabajo de eliminación de registros para un conjunto de datos que ya tiene una caducidad activa, la solicitud devolverá HTTP 400 (Solicitud incorrecta). Una caducidad activa es cualquier eliminación programada que aún no se haya completado.

### Formatos de carga útil de identidad (`namespacesIdentities` o `identities`)

El cuerpo de la solicitud debe incluir **exactamente uno** de los siguientes elementos.

| Formato | Propiedad | Forma | Cuándo usar |
|--------|----------|-------|-------------|
| **Recomendado** | `namespacesIdentities` | Matriz de objetos con `namespace` (por ejemplo, `{ "code": "email" }`) y `ids` (matriz de cadenas de identidad). | Se utiliza para todas las cargas útiles, ya sean construidas manualmente o generadas por código. Esto es especialmente eficaz para reducir el tamaño de la carga útil cuando muchas identidades comparten el mismo área de nombres. |
| **También aceptado** | `identities` | Matriz de objetos con `namespace` (por ejemplo, `{ "code": "email" }`) y un único `id` (cadena). | Aceptado para la compatibilidad con versiones anteriores. Este es el formato producido por los [scripts de conversión de csv a higiene de datos](#convert-id-lists-to-json-for-record-delete-requests). El servicio normaliza este formato internamente, por lo que el comportamiento resultante es idéntico. |

Si envía **ambas propiedades**, **ninguna propiedad** o proporciona **una matriz vacía** para la propiedad que incluye, la API devolverá **HTTP 400 (Solicitud incorrecta)** con uno de estos mensajes:

- **Se proporcionaron ambas propiedades:** `"Identities and NamespacesIdentities are not allowed at the same time"`
- **No se proporcionó ninguna lista o está vacía:** `"Identities are Empty for Delete Identity request."`

**Solicitud**

La siguiente solicitud elimina todos los registros asociados con las direcciones de correo electrónico especificadas de un conjunto de datos concreto. Utiliza el formato `namespacesIdentities` recomendado.

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
            "ids": [
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
| `datasetId` | El identificador único de los conjuntos de datos. El valor debe ser exactamente uno de: el literal `ALL`, un único ID de conjunto de datos o una lista separada por comas de dos o más ID de conjunto de datos (por ejemplo, `"id1,id2,id3"`). No puede combinar `ALL` con identificadores específicos. Las solicitudes de conjuntos de datos únicos se comportan como antes, las solicitudes de conjuntos de datos múltiples eliminan las identidades de cada conjunto de datos enumerado y `ALL` se dirige a cada conjunto de datos. Los conjuntos de datos deben tener una identidad principal o un mapa de identidad. Si existe un mapa de identidad, estará presente como un campo de nivel superior denominado `identityMap`.<br>**Nota**: una fila del conjunto de datos puede tener muchas identidades en su mapa de identidad, pero solo una se puede marcar como principal. `"primary": true` debe incluirse para forzar a `id` a coincidir con una identidad principal.<br>Cuando se usa `targetServices` para la eliminación solo de perfil, `datasetId` debe ser `ALL`. |
| `targetServices` | Opcional. Especifica los servicios que deben procesar la eliminación. El valor predeterminado depende de los derechos de su organización. Las organizaciones con Real-Time CDP o Adobe Journey Optimizer reciben el conjunto completo de servicios compatibles (`["datalake", "identity", "profile", "ajo"]`) de forma predeterminada. Las organizaciones con Customer Journey Analytics pero sin un derecho de perfil del cliente en tiempo real solo pueden usar [&quot;datalake&quot;]. Para limitar la eliminación solo a datos relacionados con perfiles y dejar el lago de datos intacto, establezca este valor en `["identity", "profile", "ajo"]` (en cualquier orden). Este modo de solo perfil requiere un derecho de Real-Time CDP o Adobe Journey Optimizer y `datasetId` debe ser `ALL`. |
| `identities` | **Use exactamente uno de `identities` o `namespacesIdentities`.** Matriz de objetos, cada uno con `namespace` (objeto con `code`, p. ej. `"email"`) y `id` (cadena de identidad única). Aceptado para la compatibilidad con versiones anteriores y producido por los scripts de conversión. El servicio normaliza este formato internamente; el comportamiento es idéntico. Consulte [Formato de carga de identidad](#identity-payload-format-identities-or-namespacesidentities) más arriba. |
| `namespacesIdentities` | **Use exactamente uno de `identities` o `namespacesIdentities`.** Matriz de objetos, cada uno con `namespace` (objeto con `code`, p. ej. `"email"`) y `ids` (matriz de cadenas de identidad). Recomendado para todas las cargas útiles. La propiedad `namespacesIdentities` es más compacta cuando muchas identidades comparten un área de nombres. Consulte [Formato de carga de identidad](#identity-payload-format-identities-or-namespacesidentities) más arriba. Áreas de nombres de identidad: [documentación del área de nombres de identidad](../../identity-service/features/namespaces.md), [API del servicio de identidad](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces). |

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
    "identity",
    "ajo"
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
| `datasetId` | El identificador único de los conjuntos de datos. Si la solicitud es para todos los conjuntos de datos, el valor se establecerá en `ALL`. Para solicitudes de varios conjuntos de datos, el valor refleja la lista separada por comas o el ID único enviado. |
| `datasetName` | Nombre del conjunto de datos de la orden de trabajo de eliminación de este registro. |
| `displayName` | Una etiqueta legible en lenguaje natural para la orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |

{style="table-layout:auto"}

El valor de la respuesta `targetServices` se hace eco de su solicitud o muestra el conjunto predeterminado completo cuando se omite (consulte la tabla de respuestas anterior).

### Conjunto de datos múltiple y solo perfil (API) {#multi-dataset-profile-only}

Las siguientes opciones están disponibles a través de la API solamente y no son compatibles con la IU de higiene de los datos. Controlan qué conjuntos de datos y qué servicios procesan la eliminación, lo que permite los envíos de conjuntos de datos múltiples y las solicitudes de servicio de destino solo de perfil.

La siguiente tabla resume cómo cambian el cuerpo y el comportamiento de la solicitud para cada opción.

| Opción | Solicitar cambio de cuerpo | Comportamiento |
|--------|---------------------|----------|
| **Conjunto de datos múltiple** | Use una lista separada por comas en `datasetId` (p. ej. `"id1,id2,id3"`). ID único o `ALL` sin cambios. | Las identidades se eliminan de los conjuntos de datos enumerados (o de un conjunto de datos, o de todos los conjuntos de datos cuando `ALL`). |
| **Solo perfil (servicios de destino)** | Agregar `targetServices` con exactamente `["identity", "profile", "ajo"]` (cualquier pedido). Requiere `datasetId`: `"ALL"`. | La eliminación solo se procesa con ID, perfil y Adobe Journey Optimizer; el lago de datos no se modifica. |

#### Solicitudes de varios conjuntos de datos

El campo `datasetId` está dividido en comas: use un solo identificador (el mismo comportamiento que antes), una lista de identificadores separados por comas o el literal `ALL`. Para eliminar identidades de varios conjuntos de datos específicos en un solo orden de trabajo, proporcione una lista separada por comas:

```json
"datasetId": "6707eb36eef4d42ab86d9fbe,6643f00c16ddf51767fcf780"
```

A continuación, las identidades se eliminan de cada uno de los conjuntos de datos enumerados. Las solicitudes de un solo conjunto de datos funcionan como siempre; use `ALL` para segmentar todos los conjuntos de datos. El valor debe ser exactamente uno de: `ALL`, un solo ID de conjunto de datos o dos o más ID de conjunto de datos separados por comas (sin combinar `ALL` con ID específicos).

#### Solo perfil (servicios segmentados)

Para quitar únicamente la identidad y los datos relacionados con el perfil sin modificar el lago de datos, incluya `targetServices` con exactamente estos tres valores en cualquier orden: `identity`, `profile` y `ajo`. Se incluyen explícitamente ID, Perfil y AJO; se excluye el lago de datos. En este modo, `datasetId` debe ser `ALL` (el caso de uso es la eliminación completa del perfil, no fragmentos por conjunto de datos).

En el siguiente ejemplo se crea una orden de trabajo de eliminación de registros de sólo perfil:

```shell
curl -X POST \
  "https://platform.adobe.io/data/core/hygiene/workorder" \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-sandbox-id: {SANDBOX_ID}' \
  -d '{
    "action": "delete_identity",
    "datasetId": "ALL",
    "displayName": "Profile-only delete for specified identity",
    "description": "Delete identity, profile, and AJO data only; datalake unchanged.",
    "targetServices": ["identity", "profile", "ajo"],
    "namespacesIdentities": [
      {
        "namespace": { "code": "email" },
        "ids": ["user@example.com"]
      }
    ]
  }'
```

Las respuestas correctas para solicitudes de varios conjuntos de datos o solo de perfil siguen la misma forma que otras respuestas de orden de trabajo. Los valores devueltos `datasetId` y `targetServices` reflejan los valores de la solicitud (o la lista predeterminada completa cuando se omite `targetServices`), para que pueda confirmar lo que se envió.

>[!NOTE]
>
>La propiedad action para registrar las órdenes de trabajo de eliminación es actualmente `identity-delete` en las respuestas de API. Si la API cambia para utilizar un valor diferente (como `delete_identity`), esta documentación se actualizará en consecuencia.

## Conversión de listas de ID a JSON para solicitudes de eliminación de registros (#convert-id-lists-to-json-for-record-delete-requests)

Use scripts de conversión para generar las cargas JSON necesarias para el extremo `/workorder` cuando los identificadores estén en archivos CSV, TSV o TXT. Este método es especialmente útil cuando se trabaja con archivos de datos existentes. Para obtener instrucciones y scripts listos para usar, consulte el [repositorio de GitHub csv para higiene de datos](https://github.com/perlmonger42/csv-to-data-hygiene).

Los scripts muestran el formato **`identities`**: un `id` por objeto con un `namespace`. La API acepta este formato tal cual; puede enviar el JSON generado directamente en el cuerpo del POST a `/workorder` sin ninguna conversión. El formato recomendado es **`namespacesIdentities`**; consulte [Crear una orden de trabajo de eliminación de registros](#create) y [Formato de carga de identidad](#identity-payload-format-identities-or-namespacesidentities).

### Generar cargas JSON

Los siguientes ejemplos de scripts de bash muestran cómo ejecutar los scripts de conversión en Python o Ruby:

>[!BEGINTABS]

>[!TAB Ejemplo para ejecutar el script de Python]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB Ejemplo para ejecutar el script Ruby]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

En la tabla siguiente se describen los parámetros de los scripts de bash.

| Parámetro | Descripción |
| ---           | ---     |
| `verbose` | Habilite la salida detallada. |
| `column` | El índice (basado en 1) o nombre del encabezado de la columna que contiene los valores de identidad que se van a eliminar. Si no se especifica nada, el valor predeterminado será la primera columna. |
| `namespace` | El código de área de nombres de identidad pasado al script (por ejemplo, `email`). El JSON generado utiliza esto en la propiedad `namespace.code` de cada objeto. |
| `dataset-id` | El identificador único de los conjuntos de datos: un identificador único, identificadores separados por comas para varios conjuntos de datos o `ALL` para todos los conjuntos de datos. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |
| `output-dir` | El directorio para escribir la carga útil JSON de salida. |

{style="table-layout:auto"}

El ejemplo siguiente muestra una carga útil JSON correcta convertida desde un archivo CSV, TSV o TXT. Contiene registros asociados al área de nombres especificada y se utiliza para eliminar registros identificados por direcciones de correo electrónico.

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

En la tabla siguiente se describen las propiedades de la carga útil JSON.

| Propiedad | Descripción |
| ---          | ---     |
| `action` | Acción solicitada para la orden de trabajo de eliminación de registros. El script de conversión establece automáticamente `delete_identity`. |
| `datasetId` | El identificador único de los conjuntos de datos: un identificador único, identificadores separados por comas o `ALL`. |
| `displayName` | Una etiqueta legible en lenguaje natural para esta orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |
| `identities` | Una matriz de objetos, cada uno de los cuales contiene:<br><ul><li> `namespace`: un objeto con una propiedad `code` que especifica el área de nombres de identidad (por ejemplo, &quot;correo electrónico&quot;).</li><li> `id`: el valor de identidad que se eliminará para este área de nombres.</li></ul> |

{style="table-layout:auto"}

### Enviar los datos JSON generados al extremo `/workorder`

La salida del script usa el formato `identities`, que la API acepta tal cual. Utilice la carga útil JSON convertida como el cuerpo de la solicitud (`-d`) cuando envíe su solicitud POST de `curl` al extremo `/workorder`. Para ver las opciones de solicitud y las reglas de validación completas, consulte [Crear una orden de trabajo de eliminación de registros](#create).

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
| `datasetId` | El identificador único de los conjuntos de datos asociados con la orden de trabajo (identificador único, identificadores separados por comas o `ALL`). |
| `datasetName` | El nombre del conjunto de datos asociado con la orden de trabajo. |
| `displayName` | Una etiqueta legible en lenguaje natural para la orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |

## Actualizar una orden de trabajo de eliminación de registros {#update}

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
| `datasetId` | El identificador único de los conjuntos de datos asociados con la orden de trabajo de eliminación de registros (identificador único, identificadores separados por comas o `ALL`). |
| `datasetName` | El nombre del conjunto de datos asociado con la orden de trabajo de eliminación de registros. |
| `displayName` | Una etiqueta legible en lenguaje natural para la orden de trabajo de eliminación de registros. |
| `description` | Descripción de la orden de trabajo de eliminación de registros. |
| `productStatusDetails` | Una matriz que enumera el estado actual de los procesos descendentes de la solicitud. Cada objeto contiene:<ul><li>`productName`: nombre del servicio descendente.</li><li>`productStatus`: el estado de procesamiento actual del servicio descendente.</li><li>`createdAt`: marca de tiempo en la que el servicio publicó el estado más reciente.</li></ul>Esta propiedad está disponible después de que la orden de trabajo se envíe a los servicios descendentes para comenzar a procesarse. |

{style="table-layout:auto"}
