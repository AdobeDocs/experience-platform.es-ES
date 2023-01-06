---
keywords: Experience Platform;inicio;temas populares;control de datos;api de etiquetas de uso de datos;api de servicio de políticas
solution: Experience Platform
title: Administrar etiquetas de uso de datos mediante API
description: La API del servicio de conjunto de datos le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funcionalidades del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogo que administra los metadatos del conjunto de datos.
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 3%

---


# Administrar etiquetas de uso de datos mediante API

Este documento proporciona los pasos sobre cómo administrar las etiquetas de uso de datos mediante el [!DNL Policy Service] API y [!DNL Dataset Service] API.

La variable [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) proporciona varios extremos que le permiten crear y administrar etiquetas de uso de datos para su organización.

La variable [!DNL Dataset Service] La API le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la función [!DNL Catalog Service] API que administra metadatos de conjuntos de datos.

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la sección [sección introducción](../../catalog/api/getting-started.md) en la guía para desarrolladores de Catálogo para recopilar las credenciales necesarias para realizar llamadas a [!DNL Platform] API.

Para realizar llamadas al [!DNL Dataset Service] extremos descritos en este documento, debe tener la variable `id` para un conjunto de datos específico. Si no tiene este valor, consulte la guía de [listado de objetos del catálogo](../../catalog/api/list-objects.md) para buscar los ID de sus conjuntos de datos existentes.

## Enumerar todas las etiquetas {#list-labels}

Al usar la variable [!DNL Policy Service] API, puede enumerar todo `core` o `custom` etiquetas realizando una solicitud de GET a `/labels/core` o `/labels/custom`, respectivamente.

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

Una respuesta correcta devuelve una lista de etiquetas personalizadas recuperadas del sistema. Dado que la solicitud de ejemplo anterior se realizó en `/labels/custom`, la respuesta a continuación solo muestra etiquetas personalizadas.

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

## Buscar una etiqueta {#look-up-label}

Puede buscar una etiqueta específica incluyendo la etiqueta `name` en la ruta de una solicitud de GET al [!DNL Policy Service] API.

**Formato de API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La variable `name` de la etiqueta personalizada que desea buscar. |

**Solicitud**

La siguiente solicitud recupera la etiqueta personalizada `L2`, tal como se indica en la ruta.

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

Para crear o actualizar una etiqueta personalizada, debe realizar una solicitud de PUT al [!DNL Policy Service] API.

**Formato de API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La variable `name` propiedad de una etiqueta personalizada. Si no existe una etiqueta personalizada con este nombre, se creará una etiqueta nueva. Si existe una, se actualizará esa etiqueta. |

**Solicitud**

La siguiente solicitud crea una etiqueta nueva, `L3`, que tiene por objeto describir los datos que contienen información relacionada con los planes de pago seleccionados por los clientes.

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
| `name` | Identificador de cadena único para la etiqueta. Este valor se utiliza con fines de búsqueda y de aplicación de la etiqueta a conjuntos de datos y campos, por lo que se recomienda que sea corto y conciso. |
| `category` | La categoría de la etiqueta. Aunque puede crear sus propias categorías para etiquetas personalizadas, es muy recomendable que utilice `Custom` si desea que la etiqueta aparezca en la interfaz de usuario. |
| `friendlyName` | Un nombre descriptivo para la etiqueta, que se utiliza para la visualización. |
| `description` | (Opcional) Descripción de la etiqueta para proporcionar más contexto. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada, con el código HTTP 200 (OK) si se actualizó una etiqueta existente o 201 (Creado) si se creó una etiqueta nueva.

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

## Buscar etiquetas para un conjunto de datos {#look-up-dataset-labels}

Puede consultar las etiquetas de uso de datos que se han aplicado a un conjunto de datos existente realizando una solicitud de GET al [!DNL Dataset Service] API.

**Formato de API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El único `id` del conjunto de datos cuyas etiquetas desea buscar. |

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

Una respuesta correcta devuelve las etiquetas de uso de datos que se han aplicado al conjunto de datos.

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
| `optionalLabels` | Una lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. Se requieren las siguientes subpropiedades:<br/><br/>`option`: Un objeto que contiene la variable [!DNL Experience Data Model] (XDM) atributos del campo. Se requieren las tres propiedades siguientes:<ul><li>`id`: El URI `$id` del esquema asociado al campo.</li><li>`contentType`: Indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de la API XDM para obtener más información.</li><li>`schemaPath`: La ruta a la propiedad de esquema en cuestión, escrita en [Puntero JSON](../../landing/api-fundamentals.md#json-pointer) sintaxis.</li></ul>`labels`: Una lista de etiquetas de uso de datos que desea agregar al campo. |

- id: El valor URI $id del esquema XDM en el que se basa el conjunto de datos.
- contentType: Indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de la API XDM para obtener más información.
- schemaPath: La ruta a la propiedad de esquema en cuestión, escrita en [Puntero JSON](../../landing/api-fundamentals.md#json-pointer) sintaxis.

## Aplicar etiquetas a un conjunto de datos {#apply-dataset-labels}

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud de POST o PUT al [!DNL Dataset Service] API. El uso de cualquiera de estos métodos sobrescribe cualquier etiqueta existente y la sustituye por las que se proporcionan en la carga útil.

**Formato de API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El único `id` del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La siguiente solicitud de POST agrega una serie de etiquetas al conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud del PUT.

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
| `labels` | Una lista de etiquetas de uso de datos que desea agregar al conjunto de datos. |
| `optionalLabels` | Una lista de los campos individuales dentro del conjunto de datos a los que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades:<br/><br/>`option`: Un objeto que contiene la variable [!DNL Experience Data Model] (XDM) atributos del campo. Se requieren las tres propiedades siguientes:<ul><li>`id`: El URI `$id` del esquema asociado al campo.</li><li>`contentType`: Indica el formato y la versión del esquema. Consulte la sección sobre [versiones de esquema](../../xdm/api/getting-started.md#versioning) en la guía de la API XDM para obtener más información.</li><li>`schemaPath`: La ruta a la propiedad de esquema en cuestión, escrita en [Puntero JSON](../../landing/api-fundamentals.md#json-pointer) sintaxis.</li></ul>`labels`: Una lista de etiquetas de uso de datos que desea agregar al campo. |

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

Puede eliminar las etiquetas aplicadas a un conjunto de datos realizando una solicitud de DELETE al [!DNL Dataset Service] API.

**Formato de API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El único `id` del conjunto de datos cuyas etiquetas desea eliminar. |

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

Respuesta correcta Estado HTTP 200 (OK), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas existentes](#look-up-dataset-labels) para el conjunto de datos en una llamada separada para confirmar esto.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos mediante API.

Una vez que haya agregado etiquetas de uso de datos en los niveles de conjunto de datos y campo, puede empezar a introducir datos en [!DNL Experience Platform]. Para obtener más información, comience leyendo el [documentación de ingesta de datos](../../ingestion/home.md).

Ahora también puede definir políticas de uso de datos basadas en las etiquetas aplicadas. Para obtener más información, consulte la [información general sobre las políticas de uso de datos](../policies/overview.md).

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la [información general sobre conjuntos de datos](../../catalog/datasets/overview.md).