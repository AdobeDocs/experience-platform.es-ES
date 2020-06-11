---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Administrar etiquetas de uso de datos mediante API '
topic: developer guide
translation-type: tm+mt
source-git-commit: 1fce86193bc1660d0f16408ed1b9217368549f6c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 3%

---


# Administrar etiquetas de uso de datos mediante API

La API de servicio de dataset permite administrar mediante programación etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogos, que administra los metadatos del conjunto de datos.

Este documento proporciona pasos sobre cómo administrar las etiquetas de uso de datos a nivel de conjunto de datos y campo mediante la API de servicio de DataSet.

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la sección [Introducción de la guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a](../../catalog/api/getting-started.md) [!DNL Platform] las API.

Para realizar llamadas a los extremos descritos en las secciones siguientes, debe tener el valor único `id` de un conjunto de datos específico. Si no tiene este valor, consulte la guía de [listado de objetos](../../catalog/api/list-objects.md) de catálogo para encontrar los ID de los conjuntos de datos existentes.

## Buscar etiquetas para un conjunto de datos {#lookup}

Puede buscar las etiquetas de uso de datos que se han aplicado a un conjunto de datos existente haciendo una solicitud GET.

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
| `labels` | lista de las etiquetas de uso de datos que se han aplicado al conjunto de datos. |
| `optionalLabels` | lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. |

## Aplicar etiquetas a un conjunto de datos

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud POST o PUT. El uso de cualquiera de estos métodos sobrescribe las etiquetas existentes y las reemplaza por las proporcionadas en la carga útil.

**Formato API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La siguiente solicitud POST agrega una serie de etiquetas al conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud PUT.

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
| `labels` | lista de las etiquetas de uso de datos que desea agregar al conjunto de datos. |
| `optionalLabels` | lista de cualquier campo individual dentro del conjunto de datos al que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`:: Objeto que contiene los atributos del campo del Modelo de datos de experiencia (XDM). Se requieren las tres propiedades siguientes:<ul><li>id</code>: El valor de URI $id</code> del esquema asociado al campo.</li><li>contentType</code>: Tipo de contenido y número de versión del esquema. Esto debe tomar la forma de uno de los encabezados <a href="../../xdm/api/look-up-resource.md"></a> Accept válidos para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`:: lista de las etiquetas de uso de datos que desea agregar al campo. |

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

## Eliminar etiquetas para un conjunto de datos

Puede eliminar las etiquetas aplicadas a un conjunto de datos haciendo una solicitud de ELIMINACIÓN.

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos cuyas etiquetas desee eliminar. |

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

Una respuesta correcta de estado HTTP 200 (Aceptar), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas](#lookup) existentes para el conjunto de datos en una llamada separada para confirmarlo.

## Pasos siguientes

Ahora que ha agregado etiquetas de uso de datos a nivel de conjunto de datos y campo, puede empezar a ingestar datos en la plataforma de experiencia. Para obtener más información, lea la documentación [sobre la ingestión de](../../ingestion/home.md)datos para obtener inicios.

Ahora también puede definir directivas de uso de datos en función de las etiquetas que haya aplicado. Para obtener más información, consulte la descripción general [de las directivas de uso de](../policies/overview.md)datos.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la descripción general [de](../../catalog/datasets/overview.md)conjuntos de datos.