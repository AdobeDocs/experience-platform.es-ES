---
keywords: Experience Platform;inicio;temas populares;api de conjunto de datos;administrar el uso de datos;api de uso de datos
solution: Experience Platform
title: 'Administrar etiquetas de uso de datos para conjuntos de datos mediante API '
topic: developer guide
description: La API de servicio de dataset permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogos, que administra los metadatos del conjunto de datos.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---


# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

El [[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las capacidades del catálogo de datos de Adobe Experience Platform, pero está separado de la API [!DNL Catalog Service] que administra los metadatos del conjunto de datos.

Este documento explica cómo administrar las etiquetas para conjuntos de datos y campos mediante [!DNL Dataset Service API]. Para ver los pasos sobre cómo administrar las etiquetas de uso de datos mediante llamadas de API, consulte la [guía de extremo de etiquetas](../api/labels.md) para [!DNL Policy Service API].

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la [sección de introducción](../../catalog/api/getting-started.md) de la guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a [!DNL Platform] API.

Para realizar llamadas a los extremos descritos en este documento, debe tener el valor único `id` para un conjunto de datos específico. Si no tiene este valor, consulte la guía [en la que se enumeran los objetos del catálogo](../../catalog/api/list-objects.md) para buscar los ID de los conjuntos de datos existentes.

## Buscar etiquetas para un conjunto de datos {#look-up}

Puede buscar las etiquetas de uso de datos que se han aplicado a un conjunto de datos existente haciendo una solicitud de GET a la API [!DNL Dataset Service].

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

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud de POST o PUT a la API [!DNL Dataset Service]. El uso de cualquiera de estos métodos sobrescribe las etiquetas existentes y las reemplaza por las proporcionadas en la carga útil.

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
>Se debe proporcionar un encabezado `If-Match` válido al realizar solicitudes de PUT al extremo `/datasets/{DATASET_ID}/labels`. Consulte la [sección del apéndice](#if-match) para obtener más información sobre el uso del encabezado requerido.

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
| `optionalLabels` | Lista de cualquier campo individual dentro del conjunto de datos al que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`: Objeto que contiene los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>id</code>: El valor URI $id</code> del esquema asociado al campo.</li><li>contentType</code>: Tipo de contenido y número de versión del esquema. Esto debe tomar la forma de uno de los <a href="../../xdm/api/getting-started.md#accept">encabezados Accept</a> válidos para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`:: Lista de las etiquetas de uso de datos que desea agregar al campo. |

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

## Quitar etiquetas de un conjunto de datos {#remove}

Puede eliminar las etiquetas aplicadas a un conjunto de datos haciendo una solicitud de DELETE a la API [!DNL Dataset Service].

**Formato API**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos cuyas etiquetas desee eliminar. |

**Solicitud**

La siguiente solicitud elimina las etiquetas del conjunto de datos especificado en la ruta.

>[!IMPORTANT]
>
>Se debe proporcionar un encabezado `If-Match` válido al realizar solicitudes de DELETE al extremo `/datasets/{DATASET_ID}/labels`. Consulte la [sección del apéndice](#if-match) para obtener más información sobre el uso del encabezado requerido.

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

Una respuesta correcta de estado HTTP 200 (Aceptar), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas existentes](#look-up) para el conjunto de datos en una llamada separada para confirmarlo.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos mediante la API [!DNL Dataset Service].

Una vez que haya agregado etiquetas de uso de datos en el nivel de conjunto de datos y campo, puede empezar a ingestar datos en [!DNL Experience Platform]. Para obtener más información, lea la [documentación de ingestión de datos](../../ingestion/home.md) para obtener inicio.

Ahora también puede definir directivas de uso de datos en función de las etiquetas que haya aplicado. Para obtener más información, consulte la [descripción general de las directivas de uso de datos](../policies/overview.md).

Para obtener más información sobre la administración de datasets en [!DNL Experience Platform], consulte la [información general de datasets](../../catalog/datasets/overview.md).

## Apéndice {#appendix}

La siguiente sección contiene información adicional sobre cómo trabajar con etiquetas mediante la API de servicio de Dataset.

### [!DNL If-Match] header  {#if-match}

Al realizar llamadas de API que actualizan las etiquetas existentes de un conjunto de datos (PUT y DELETE), se debe incluir un encabezado `If-Match` que indica la versión actual de la entidad de etiqueta de conjunto de datos en el servicio de conjunto de datos. Para evitar conflictos de datos, el servicio solo actualizará la entidad del conjunto de datos si la cadena `If-Match` incluida coincide con la etiqueta de versión más reciente generada por el sistema para ese conjunto de datos.

>[!NOTE]
>
>Si no existen etiquetas actualmente para el conjunto de datos en cuestión, las nuevas etiquetas solo se pueden agregar mediante una solicitud de POST, que no requiere un encabezado `If-Match`. Una vez agregadas las etiquetas a un conjunto de datos, se asigna un valor `etag` que puede utilizarse para actualizar o eliminar las etiquetas más adelante.

Para recuperar la versión más reciente de la entidad de etiqueta de conjunto de datos, haga una [solicitud de GET](#look-up) al extremo `/datasets/{DATASET_ID}/labels`. El valor actual se devuelve en la respuesta bajo un encabezado `etag`. Al actualizar las etiquetas de conjuntos de datos existentes, se recomienda realizar primero una solicitud de búsqueda para el conjunto de datos a fin de recuperar su valor más reciente `etag` antes de utilizar ese valor en el encabezado `If-Match` de la solicitud de PUT o DELETE subsiguiente.