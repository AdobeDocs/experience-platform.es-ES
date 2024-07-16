---
keywords: Experience Platform;inicio;temas populares;api de conjuntos de datos;administrar uso de datos;api de uso de datos
solution: Experience Platform
title: Administrar etiquetas de uso de datos para conjuntos de datos mediante API
description: La API del servicio de conjuntos de datos permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente de la API del servicio de catálogo que administra los metadatos del conjunto de datos.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 2%

---

# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente de la API [!DNL Catalog Service] que administra los metadatos del conjunto de datos.

>[!IMPORTANT]
>
>La aplicación de etiquetas en el nivel de conjunto de datos solo es compatible con casos de uso de gobernanza de datos. Si está intentando crear directivas de acceso para los datos, debe [aplicar etiquetas al esquema](../../xdm/tutorials/labels.md) en el que se basa el conjunto de datos. Consulte la descripción general de [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener más información.

Este documento explica cómo administrar etiquetas para conjuntos de datos y campos mediante [!DNL Dataset Service API]. Para ver los pasos sobre cómo administrar las propias etiquetas de uso de datos mediante llamadas API, consulte la [guía de extremo de etiquetas](../api/labels.md) para [!DNL Policy Service API].

## Introducción

Antes de leer esta guía, siga los pasos descritos en la [sección de introducción](../../catalog/api/getting-started.md) en la guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a las API de [!DNL Platform].

Para realizar llamadas a los extremos descritos en este documento, debe tener el valor `id` único para un conjunto de datos específico. Si no tiene este valor, consulte la guía en [listar objetos de catálogo](../../catalog/api/list-objects.md) para encontrar los ID de los conjuntos de datos existentes.

## Búsqueda de etiquetas para un conjunto de datos {#look-up}

Puede buscar las GET de uso de datos que se han aplicado a un conjunto de datos existente realizando una solicitud a la API [!DNL Dataset Service].

**Formato de API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor `id` único del conjunto de datos cuyas etiquetas desea buscar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las etiquetas de uso de datos aplicadas al conjunto de datos.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `labels` | Una lista de etiquetas de uso de datos que se han aplicado al conjunto de datos. |
| `optionalLabels` | Una lista de campos individuales dentro del conjunto de datos a los que se les han aplicado etiquetas de uso de datos. |

## Aplicar etiquetas a un conjunto de datos {#apply}

Puede aplicar un conjunto de etiquetas para un conjunto de datos completo proporcionándolas en la carga útil de una solicitud de POST o PUT a la API [!DNL Dataset Service]. El cuerpo de la solicitud es el mismo para ambas llamadas. No puede agregar etiquetas a campos de conjuntos de datos individuales.

**Formato de API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor `id` único del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La siguiente solicitud de POST de ejemplo actualiza todo el conjunto de datos con la etiqueta `C1`. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud de PUT.

Cuando se realizan llamadas de API que actualizan las etiquetas existentes de un conjunto de datos (PUT), se debe incluir un encabezado `If-Match` que indique la versión actual de la entidad dataset-label en el servicio Dataset. Para evitar conflictos de datos, el servicio solo actualizará la entidad del conjunto de datos si la cadena `If-Match` incluida coincide con la última etiqueta de versión generada por el sistema para ese conjunto de datos.

>[!NOTE]
>
>Si existen etiquetas para el conjunto de datos en cuestión, solo se pueden agregar nuevas mediante una solicitud de PUT, que requiere un encabezado `If-Match`. Una vez agregadas las etiquetas a un conjunto de datos, se requiere el valor `etag` más reciente para actualizar o quitar las etiquetas más adelante<br>Antes de ejecutar el método PUT, debe realizar una solicitud de GET en las etiquetas del conjunto de datos. Asegúrese de actualizar únicamente los campos específicos que se van a modificar en la solicitud, dejando el resto sin cambiar. Además, asegúrese de que la llamada al PUT mantiene las mismas entidades principales que la llamada al GET. Cualquier discrepancia produciría un error para el cliente.

Para recuperar la versión más reciente de la entidad dataset-label, realice una [solicitud de GET](#look-up) al extremo `/datasets/{DATASET_ID}/labels`. El valor actual se devuelve en la respuesta bajo un encabezado `etag`. Al actualizar las etiquetas de conjuntos de datos existentes, se recomienda realizar primero una solicitud de búsqueda para el conjunto de datos a fin de recuperar su último valor `etag` antes de utilizar ese valor en el encabezado `If-Match` de la solicitud de PUT posterior.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| Propiedad | Descripción |
| --- | --- |
| `entityId` | Esto identifica la entidad del conjunto de datos específica que se va a actualizar. |
| `entityId.namespace` | Se utiliza para evitar conflictos de ID. `namespace` es `AEP`. |
| `entityId.id` | El ID del recurso que se actualiza. Hace referencia a `datasetId`. |
| `entityId.type` | El tipo de recurso que se actualiza. Siempre será `dataset`. |
| `labels` | Una lista de etiquetas de uso de datos que desee agregar a todo el conjunto de datos. |
| `parents` | La matriz `parents` contiene una lista de `entityId` de los que heredará este conjunto de datos. Los conjuntos de datos pueden heredar etiquetas de esquemas o conjuntos de datos. |

**Respuesta**

Una respuesta correcta devuelve el conjunto actualizado de etiquetas para el conjunto de datos.

>[!IMPORTANT]
>
>La propiedad `optionalLabels` ha quedado obsoleta para su uso con solicitudes de POST. Ya no es posible añadir etiquetas de datos a los campos de conjuntos de datos. Una operación del POST generará un error si hay un valor `optionalLabel`. Sin embargo, puede eliminar las etiquetas de campos individuales mediante una solicitud de PUT y la propiedad `optionalLabels`. Para obtener más información, consulte la sección sobre [quitar etiquetas de un conjunto de datos](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## Eliminación de etiquetas de un conjunto de datos {#remove}

Puede quitar cualquier etiqueta de campo aplicada anteriormente actualizando los valores de `optionalLabels` existentes con un subconjunto de las etiquetas de campo existentes o con una lista vacía para quitarlos por completo. Realice una solicitud de PUT a la API [!DNL Dataset Service] para actualizar o quitar las etiquetas aplicadas anteriormente.

**Formato de API**

```http
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor `id` único del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

El siguiente conjunto de datos en el que se aplica la operación de PUT tenía el campo C1 optionalLabel en properties/person/properties/address y el campo C1, C2 optionalLabels en /properties/person/properties/name/properties/fullName. Después de la operación de colocación, el primer campo no tendrá etiqueta (se eliminó la etiqueta C1) y el segundo campo solo tendrá etiqueta C1 (se eliminó la etiqueta C2)

En el siguiente escenario de ejemplo, se utiliza una solicitud de PUT para eliminar las etiquetas agregadas a campos individuales. Antes de realizar la solicitud, el campo `fullName` tenía aplicadas las etiquetas `C1` y `C2`, y el campo `address` ya tenía aplicada una etiqueta `C1`. La solicitud de PUT reemplaza las etiquetas existentes `C1, C2` del campo `fullName` con una etiqueta `C1` que usa el parámetro `optionalLabels.labels`. La solicitud también invalida la etiqueta `C1` del campo `address` con un conjunto vacío de etiquetas de campo.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| Parámetro | Descripción |
| --- | --- |
| `entityId` | Esto identifica la entidad del conjunto de datos específica que se va a actualizar. `entityId` debe incluir los tres valores siguientes:<br/><br/>`namespace`: Se usa para evitar conflictos de ID. `namespace` es `AEP`.<br/>`id`: ID del recurso que se está actualizando. Hace referencia a `datasetId`.<br/>`type`: tipo de recurso que se está actualizando. Siempre será `dataset`. |
| `labels` | Una lista de etiquetas de uso de datos que desee agregar a todo el conjunto de datos. |
| `parents` | La matriz `parents` contiene una lista de `entityId` de los que heredará este conjunto de datos. Los conjuntos de datos pueden heredar etiquetas de esquemas o conjuntos de datos. |
| `optionalLabels` | Este parámetro se utiliza para eliminar etiquetas aplicadas anteriormente a un campo de conjunto de datos. Una lista de cualquier campo individual dentro del conjunto de datos del que desee quitar las etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`: Un objeto que contenga los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li><code>id</code>: URI <code>$id</code> valor del esquema asociado al campo.</li><li><code>contentType</code>: el tipo de contenido y el número de versión del esquema. Debe adoptar la forma de uno de los <a href="../../xdm/api/getting-started.md#accept">encabezados Aceptar</a> válidos para una solicitud de búsqueda XDM.</li><li><code>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`: este valor debe contener un subconjunto de las etiquetas de campo existentes aplicadas o estar vacío para quitar todas las etiquetas de campo existentes. Los métodos PUT o POST ahora devuelven un error si el campo `optionalLabels` tiene etiquetas nuevas o modificadas. |

**Respuesta**

Una respuesta correcta devuelve el conjunto actualizado de etiquetas para el conjunto de datos.

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos mediante la API [!DNL Dataset Service]. Ahora puede definir [políticas de uso de datos](../policies/overview.md) y [políticas de control de acceso](../../access-control/abac/ui/policies.md) en función de las etiquetas que haya aplicado.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], vea la [descripción general de conjuntos de datos](../../catalog/datasets/overview.md).
