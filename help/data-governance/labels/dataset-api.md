---
keywords: Experience Platform;home;popular topics;dataset api;manage data usage;data usage api
solution: Experience Platform
title: 'Administrar etiquetas de uso de datos para conjuntos de datos mediante API '
topic: developer guide
description: La API de servicio de dataset permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogos, que administra los metadatos del conjunto de datos.
translation-type: tm+mt
source-git-commit: 4b5e116d221e6689f95c8da0c54ef3af6827adc1
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 2%

---


# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

La [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la [!DNL Catalog Service] API que administra los metadatos del conjunto de datos.

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
| `labels` | Lista de las etiquetas de uso de datos que se han aplicado al conjunto de datos. |
| `optionalLabels` | Lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. |

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

La siguiente solicitud de PUT actualiza las etiquetas existentes para un conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud de POST.

>[!IMPORTANT]
>
>Se debe proporcionar un `If-Match` encabezado válido al realizar solicitudes de PUT al `/datasets/{DATASET_ID}/labels` extremo. Consulte la sección [del](#if-match) apéndice para obtener más información sobre el uso del encabezado requerido.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
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

La siguiente solicitud elimina las etiquetas del conjunto de datos especificado en la ruta.

>[!IMPORTANT]
>
>Se debe proporcionar un `If-Match` encabezado válido al realizar solicitudes de DELETE al `/datasets/{DATASET_ID}/labels` extremo. Consulte la sección [del](#if-match) apéndice para obtener más información sobre el uso del encabezado requerido.

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**Respuesta**

Una respuesta correcta de estado HTTP 200 (Aceptar), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas](#look-up) existentes para el conjunto de datos en una llamada separada para confirmarlo.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos mediante la [!DNL Dataset Service] API.

Una vez agregadas las etiquetas de uso de datos en los niveles de conjunto de datos y campo, puede empezar a ingestar datos en [!DNL Experience Platform]. Para obtener más información, lea la documentación [sobre la ingestión de](../../ingestion/home.md)datos para obtener inicios.

Ahora también puede definir directivas de uso de datos en función de las etiquetas que haya aplicado. Para obtener más información, consulte la descripción general [de las directivas de uso de](../policies/overview.md)datos.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la descripción general [de](../../catalog/datasets/overview.md)conjuntos de datos.

## Apéndice {#appendix}

La siguiente sección contiene información adicional sobre cómo trabajar con etiquetas mediante la API de servicio de Dataset.

### [!DNL If-Match] header {#if-match}

Al realizar llamadas de API que actualizan las etiquetas existentes de un conjunto de datos (PUT y DELETE), se debe incluir un `If-Match` encabezado que indique la versión actual de la entidad de etiqueta de conjunto de datos en el servicio de conjunto de datos. Para evitar conflictos de datos, el servicio solo actualizará la entidad del conjunto de datos si la cadena incluida coincide con la etiqueta de versión más reciente generada por el sistema para ese conjunto de datos. `If-Match`

>[!NOTE]
>
>Si no existen etiquetas actualmente para el conjunto de datos en cuestión, las nuevas etiquetas solo se pueden agregar mediante una solicitud de POST, lo que no requiere un `If-Match` encabezado. Una vez agregadas las etiquetas a un conjunto de datos, se asigna un `etag` valor que puede utilizarse para actualizar o quitar las etiquetas más adelante.

Para recuperar la versión más reciente de la entidad de etiqueta de conjunto de datos, realice una solicitud [de](#look-up) GET al `/datasets/{DATASET_ID}/labels` extremo. El valor actual se devuelve en la respuesta bajo un `etag` encabezado. Al actualizar las etiquetas de conjuntos de datos existentes, lo mejor es realizar primero una solicitud de búsqueda para el conjunto de datos a fin de recuperar su último `etag` valor antes de utilizar ese valor en el `If-Match` encabezado de la solicitud de PUT o DELETE subsiguiente.