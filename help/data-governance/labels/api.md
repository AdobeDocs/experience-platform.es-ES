---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas
solution: Experience Platform
title: Administración de etiquetas de uso de datos mediante API
description: La API del servicio de conjuntos de datos permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente de la API del servicio de catálogo que administra los metadatos del conjunto de datos.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 3%

---


# Administración de etiquetas de uso de datos mediante API

Este documento proporciona pasos sobre cómo administrar las etiquetas de uso de datos mediante la API [!DNL Policy Service] y la API [!DNL Dataset Service].

[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) proporciona varios extremos que le permiten crear y administrar etiquetas de uso de datos para su organización.

La API [!DNL Dataset Service] le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente de la API [!DNL Catalog Service] que administra los metadatos del conjunto de datos.

## Introducción

Antes de leer esta guía, siga los pasos descritos en la [sección de introducción](../../catalog/api/getting-started.md) en la guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a las API de [!DNL Platform].

Para realizar llamadas a los extremos [!DNL Dataset Service] descritos en este documento, debe tener el valor `id` único para un conjunto de datos específico. Si no tiene este valor, consulte la guía en [listar objetos de catálogo](../../catalog/api/list-objects.md) para encontrar los ID de los conjuntos de datos existentes.

## Enumerar todas las etiquetas {#list-labels}

Con la API [!DNL Policy Service], puede enumerar todas las etiquetas `core` o `custom` realizando una solicitud de GET a `/labels/core` o `/labels/custom`, respectivamente.

**Formato de API**

```http
GET /labels/core
GET /labels/custom
```

**Solicitud**

La siguiente solicitud enumera todas las etiquetas personalizadas creadas en su organización.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de etiquetas personalizadas recuperadas del sistema. Dado que la solicitud de ejemplo anterior se realizó a `/labels/custom`, la respuesta siguiente solo muestra etiquetas personalizadas.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Búsqueda de una etiqueta {#look-up-label}

Puede buscar una etiqueta específica incluyendo la propiedad `name` de esa etiqueta en la ruta de una solicitud de GET a la API [!DNL Policy Service].

**Formato de API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La propiedad `name` de la etiqueta personalizada que desea buscar. |

**Solicitud**

La siguiente solicitud recupera la etiqueta personalizada `L2`, tal como se indica en la ruta de acceso.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Crear o actualizar una etiqueta personalizada {#create-update-label}

Para crear o actualizar una etiqueta personalizada, debe realizar una solicitud de PUT a la API [!DNL Policy Service].

**Formato de API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La propiedad `name` de una etiqueta personalizada. Si no existe una etiqueta personalizada con este nombre, se creará una nueva. Si existe una, se actualizará esa etiqueta. |

**Solicitud**

La siguiente solicitud crea una etiqueta nueva, `L3`, que tiene como objetivo describir los datos que contienen información relacionada con los planes de pago seleccionados de los clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Un identificador de cadena único para la etiqueta. Este valor se utiliza con fines de búsqueda y para aplicar la etiqueta a conjuntos de datos y campos, por lo que se recomienda que sea corto y conciso. |
| `category` | La categoría de la etiqueta. Aunque puede crear sus propias categorías para etiquetas personalizadas, se recomienda encarecidamente que utilice `Custom` si desea que la etiqueta aparezca en la interfaz de usuario. |
| `friendlyName` | Un nombre descriptivo para la etiqueta, que se utiliza con fines de visualización. |
| `description` | (Opcional) Una descripción de la etiqueta para proporcionar más contexto. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada, con código HTTP 200 (OK) si se actualizó una etiqueta existente o 201 (Created) si se creó una etiqueta nueva.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Búsqueda de etiquetas para un conjunto de datos {#look-up-dataset-labels}

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
| `optionalLabels` | Una lista de campos individuales dentro del conjunto de datos a los que se les han aplicado etiquetas de uso de datos. Se requieren las siguientes subpropiedades:<br/><br/>`option`: Un objeto que contiene los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>`id`: el valor del URI `$id` del esquema asociado con el campo.</li><li>`contentType`: indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de API de XDM para obtener más información.</li><li>`schemaPath`: ruta a la propiedad de esquema en cuestión, escrita con sintaxis de [puntero JSON](../../landing/api-fundamentals.md#json-pointer).</li></ul>`labels`: una lista de etiquetas de uso de datos que desea agregar al campo. |

- id: el valor $id de URI para el esquema XDM en el que se basa el conjunto de datos.
- contentType: indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de API de XDM para obtener más información.
- schemaPath: ruta a la propiedad de esquema en cuestión, escrita con sintaxis [JSON Pointer](../../landing/api-fundamentals.md#json-pointer).

## Aplicar etiquetas a un conjunto de datos {#apply-dataset-labels}

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud de POST o PUT a la API [!DNL Dataset Service]. El uso de cualquiera de estos métodos sobrescribe las etiquetas existentes y las reemplaza por las proporcionadas en la carga útil.

**Formato de API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor `id` único del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La siguiente solicitud del POST agrega una serie de etiquetas al conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud de PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
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
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `labels` | Una lista de etiquetas de uso de datos que desee agregar al conjunto de datos. |
| `optionalLabels` | Una lista de cualquier campo individual dentro del conjunto de datos al que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades:<br/><br/>`option`: Un objeto que contenga los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>`id`: el valor del URI `$id` del esquema asociado con el campo.</li><li>`contentType`: indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de API de XDM para obtener más información.</li><li>`schemaPath`: ruta a la propiedad de esquema en cuestión, escrita con sintaxis de [puntero JSON](../../landing/api-fundamentals.md#json-pointer).</li></ul>`labels`: una lista de etiquetas de uso de datos que desea agregar al campo. |

**Respuesta**

Una respuesta correcta devuelve las etiquetas que se han agregado al conjunto de datos.

```json
{
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
```

## Eliminación de etiquetas de un conjunto de datos {#remove-dataset-labels}

Puede quitar las etiquetas aplicadas a un conjunto de datos realizando una solicitud de DELETE a la API [!DNL Dataset Service].

**Formato de API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor `id` único del conjunto de datos cuyas etiquetas desea quitar. |

**Solicitud**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta HTTP de estado 200 (OK) correcta, que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas existentes](#look-up-dataset-labels) para el conjunto de datos en una llamada independiente para confirmarlo.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos mediante API.

Una vez que haya agregado etiquetas de uso de datos en el conjunto de datos y en el nivel de campo, puede empezar a introducir datos en [!DNL Experience Platform]. Para obtener más información, comience por leer la [documentación de ingesta de datos](../../ingestion/home.md).

Ahora también puede definir políticas de uso de datos basadas en las etiquetas aplicadas. Para obtener más información, consulte la [descripción general de las directivas de uso de datos](../policies/overview.md).

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], vea la [descripción general de conjuntos de datos](../../catalog/datasets/overview.md).