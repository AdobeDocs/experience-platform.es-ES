---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 'Administrar etiquetas de uso de datos para conjuntos de datos mediante API '
topic: developer guide
translation-type: tm+mt
source-git-commit: 2f35765c0dfadbfb4782b6c3904e33ae7a330b2f
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 3%

---


# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

El [!DNL Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las capacidades del catálogo de datos de Adobe Experience Platform, pero está separado de la [!DNL Catalog Service] API que administra los metadatos del conjunto de datos.

Este documento explica cómo administrar las etiquetas para conjuntos de datos y campos mediante el uso de la variable [!DNL Dataset Service API]. Para ver los pasos sobre cómo administrar las etiquetas de uso de datos mediante llamadas de API, consulte la guía [de extremo de](../api/labels.md) etiquetas para la [!DNL Policy Service API].

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la sección [Introducción de la guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a](../../catalog/api/getting-started.md) [!DNL Platform] las API.

Para realizar llamadas a los extremos descritos en este documento, debe tener el valor único `id` de un conjunto de datos específico. Si no tiene este valor, consulte la guía de [listado de objetos](../../catalog/api/list-objects.md) de catálogo para encontrar los ID de los conjuntos de datos existentes.

## Buscar etiquetas para un conjunto de datos {#look-up}

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
| `labels` | lista de las etiquetas de uso de datos que se han aplicado al conjunto de datos. |
| `optionalLabels` | lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. |

## Aplicar etiquetas a un conjunto de datos {#apply}

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
| `labels` | lista de las etiquetas de uso de datos que desea agregar al conjunto de datos. |
| `optionalLabels` | lista de cualquier campo individual dentro del conjunto de datos al que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`:: Objeto que contiene los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>id</code>: El valor de URI $id</code> del esquema asociado al campo.</li><li>contentType</code>: Tipo de contenido y número de versión del esquema. Esto debe tomar la forma de uno de los encabezados <a href="../../xdm/api/look-up-resource.md"></a> Accept válidos para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`:: lista de las etiquetas de uso de datos que desea agregar al campo. |

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

## Eliminar etiquetas de un conjunto de datos {#remove}

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

Una respuesta correcta de estado HTTP 200 (Aceptar), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas](#look-up) existentes para el conjunto de datos en una llamada separada para confirmarlo.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos mediante la [!DNL Dataset Service] API.

Una vez agregadas las etiquetas de uso de datos en los niveles de conjunto de datos y campo, puede empezar a ingestar datos en [!DNL Experience Platform]. Para obtener más información, lea la documentación [sobre la ingestión de](../../ingestion/home.md)datos para obtener inicios.

Ahora también puede definir directivas de uso de datos en función de las etiquetas que haya aplicado. Para obtener más información, consulte la descripción general [de las directivas de uso de](../policies/overview.md)datos.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la descripción general [de](../../catalog/datasets/overview.md)conjuntos de datos.