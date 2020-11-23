---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api
solution: Experience Platform
title: 'Administrar etiquetas de uso de datos mediante API '
topic: developer guide
description: La API de servicio de dataset permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogos, que administra los metadatos del conjunto de datos.
translation-type: tm+mt
source-git-commit: 4b5e116d221e6689f95c8da0c54ef3af6827adc1
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 3%

---


# Administrar etiquetas de uso de datos mediante API

Este documento proporciona pasos sobre cómo administrar las etiquetas de uso de datos mediante la [!DNL Policy Service] API y la [!DNL Dataset Service] API.

El [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) proporciona varios extremos que le permiten crear y administrar etiquetas de uso de datos para su organización.

La [!DNL Dataset Service] API permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la [!DNL Catalog Service] API que administra los metadatos del conjunto de datos.

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la sección [Introducción de la guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a](../../catalog/api/getting-started.md) [!DNL Platform] las API.

Para realizar llamadas a los [!DNL Dataset Service] extremos descritos en este documento, debe tener el valor único `id` de un conjunto de datos específico. Si no tiene este valor, consulte la guía de [listado de objetos](../../catalog/api/list-objects.md) de catálogo para encontrar los ID de los conjuntos de datos existentes.

## Lista de todas las etiquetas {#list-labels}

Con la [!DNL Policy Service] API, puede realizar la lista de todas `core` o `custom` las etiquetas mediante una solicitud de GET a `/labels/core` o `/labels/custom`, respectivamente.

**Formato API**

```http
GET /labels/core
GET /labels/custom
```

**Solicitud**

La siguiente solicitud lista todas las etiquetas personalizadas creadas en la organización.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de las etiquetas personalizadas recuperadas del sistema. Dado que la solicitud de ejemplo anterior se realizó en `/labels/custom`, la respuesta siguiente solo muestra etiquetas personalizadas.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

Puede buscar una etiqueta específica incluyendo la propiedad de esa `name` etiqueta en la ruta de una solicitud de GET a la [!DNL Policy Service] API.

**Formato API**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La `name` propiedad de la etiqueta personalizada que desea buscar. |

**Solicitud**

La siguiente solicitud recupera la etiqueta personalizada `L2`, como se indica en la ruta.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

Para crear o actualizar una etiqueta personalizada, debe realizar una solicitud de PUT a la [!DNL Policy Service] API.

**Formato API**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parámetro | Descripción |
| --- | --- |
| `{LABEL_NAME}` | La `name` propiedad de una etiqueta personalizada. Si no existe una etiqueta personalizada con este nombre, se creará una nueva etiqueta. Si existe una, la etiqueta se actualizará. |

**Solicitud**

La siguiente solicitud crea una nueva etiqueta `L3`, que tiene por objeto describir los datos que contienen información relativa a los planes de pago seleccionados por los clientes.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Identificador de cadena único para la etiqueta. Este valor se utiliza para fines de búsqueda y para aplicar la etiqueta a conjuntos de datos y campos, por lo que se recomienda que sea breve y conciso. |
| `category` | La categoría de la etiqueta. Aunque puede crear sus propias categorías para las etiquetas personalizadas, se recomienda encarecidamente que las utilice `Custom` si desea que la etiqueta aparezca en la interfaz de usuario. |
| `friendlyName` | Un nombre descriptivo para la etiqueta, que se utiliza con fines de visualización. |
| `description` | (Opcional) Una descripción de la etiqueta para proporcionar contexto adicional. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la etiqueta personalizada, con el código HTTP 200 (Aceptar) si se actualizó una etiqueta existente o 201 (Creado) si se creó una nueva etiqueta.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

Puede buscar las etiquetas de uso de datos que se han aplicado a un conjunto de datos existente haciendo una solicitud de GET a la [!DNL Dataset Service] API.

**Formato API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos cuyas etiquetas desee buscar. |

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve las etiquetas de uso de datos que se han aplicado al conjunto de datos.

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `labels` | Lista de las etiquetas de uso de datos que se han aplicado al conjunto de datos. |
| `optionalLabels` | Lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. |

## Aplicar etiquetas a un conjunto de datos {#apply-dataset-labels}

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud de POST o PUT a la [!DNL Dataset Service] API. El uso de cualquiera de estos métodos sobrescribe las etiquetas existentes y las reemplaza por las proporcionadas en la carga útil.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La siguiente solicitud de POST agrega una serie de etiquetas al conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud de PUT.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `labels` | Lista de las etiquetas de uso de datos que desea agregar al conjunto de datos. |
| `optionalLabels` | Lista de cualquier campo individual dentro del conjunto de datos al que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`:: Objeto que contiene los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>id</code>: El valor de URI $id</code> del esquema asociado al campo.</li><li>contentType</code>: Tipo de contenido y número de versión del esquema. Esto debe tomar la forma de uno de los encabezados <a href="../../xdm/api/getting-started.md#accept"></a> Accept válidos para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`:: Lista de las etiquetas de uso de datos que desea agregar al campo. |

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

## Eliminar etiquetas de un conjunto de datos {#remove-dataset-labels}

Puede eliminar las etiquetas aplicadas a un conjunto de datos haciendo una solicitud de DELETE a la [!DNL Dataset Service] API.

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos cuyas etiquetas desea eliminar. |

**Solicitud**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta de estado HTTP 200 (Aceptar), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas](#look-up-dataset-labels) existentes para el conjunto de datos en una llamada separada para confirmarlo.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos mediante API.

Una vez agregadas las etiquetas de uso de datos en los niveles de conjunto de datos y campo, puede empezar a ingestar datos en [!DNL Experience Platform]. Para obtener más información, lea la documentación [sobre la ingestión de](../../ingestion/home.md)datos para obtener inicios.

Ahora también puede definir directivas de uso de datos en función de las etiquetas que haya aplicado. Para obtener más información, consulte la descripción general [de las directivas de uso de](../policies/overview.md)datos.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la descripción general [de](../../catalog/datasets/overview.md)conjuntos de datos.