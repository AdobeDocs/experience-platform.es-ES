---
keywords: Experience Platform;inicio;temas populares;api de conjunto de datos;administrar uso de datos;api de uso de datos
solution: Experience Platform
title: 'Administrar etiquetas de uso de datos para conjuntos de datos mediante API '
topic-legacy: developer guide
description: La API del servicio de conjunto de datos le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funcionalidades del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogo que administra los metadatos del conjunto de datos.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 2%

---

# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

El [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las capacidades del catálogo de datos de Adobe Experience Platform, pero está separado de la API [!DNL Catalog Service] que administra los metadatos del conjunto de datos.

Este documento explica cómo administrar etiquetas para conjuntos de datos y campos mediante [!DNL Dataset Service API]. Para ver los pasos sobre cómo administrar las etiquetas de uso de datos por sí mismas mediante llamadas API, consulte la [guía de extremo de etiquetas](../api/labels.md) para [!DNL Policy Service API].

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la [sección de introducción](../../catalog/api/getting-started.md) en la guía para desarrolladores del catálogo para recopilar las credenciales necesarias para realizar llamadas a las API [!DNL Platform] .

Para realizar llamadas a los extremos descritos en este documento, debe tener el valor único `id` para un conjunto de datos específico. Si no tiene este valor, consulte la guía de [listar objetos de catálogo](../../catalog/api/list-objects.md) para encontrar los ID de sus conjuntos de datos existentes.

## Buscar etiquetas para un conjunto de datos {#look-up}

Puede buscar las etiquetas de uso de datos que se han aplicado a un conjunto de datos existente realizando una solicitud de GET a la API [!DNL Dataset Service].

**Formato de API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos cuyas etiquetas desea buscar. |

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
| `labels` | Una lista de etiquetas de uso de datos que se han aplicado al conjunto de datos. |
| `optionalLabels` | Una lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. |

## Aplicar etiquetas a un conjunto de datos {#apply}

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud de POST o PUT a la API [!DNL Dataset Service]. El uso de cualquiera de estos métodos sobrescribe cualquier etiqueta existente y la sustituye por las que se proporcionan en la carga útil.

**Formato de API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | El valor único `id` del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La siguiente solicitud de PUT actualiza las etiquetas existentes para un conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud del POST.

>[!IMPORTANT]
>
>Se debe proporcionar un encabezado `If-Match` válido al realizar solicitudes de PUT al extremo `/datasets/{DATASET_ID}/labels` . Consulte la [sección del apéndice](#if-match) para obtener más información sobre el uso del encabezado requerido.

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
| `labels` | Una lista de etiquetas de uso de datos que desea agregar al conjunto de datos. |
| `optionalLabels` | Una lista de los campos individuales dentro del conjunto de datos a los que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`: Un objeto que contiene los atributos [!DNL Experience Data Model] (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>id</code>: El valor URI $id</code> del esquema asociado al campo.</li><li>contentType</code>: Tipo de contenido y número de versión del esquema. Esto debe tomar la forma de uno de los <a href="../../xdm/api/getting-started.md#accept">Accept headers</a> válidos para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`: Una lista de etiquetas de uso de datos que desea agregar al campo. |

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

## Eliminación de etiquetas de un conjunto de datos {#remove}

Puede eliminar las etiquetas aplicadas a un conjunto de datos realizando una solicitud de DELETE a la API [!DNL Dataset Service].

**Formato de API**

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
>Se debe proporcionar un encabezado `If-Match` válido al realizar solicitudes de DELETE al extremo `/datasets/{DATASET_ID}/labels` . Consulte la [sección del apéndice](#if-match) para obtener más información sobre el uso del encabezado requerido.

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

Respuesta correcta Estado HTTP 200 (OK), que indica que se han eliminado las etiquetas. Puede [buscar las etiquetas existentes](#look-up) para el conjunto de datos en una llamada separada para confirmar esto.

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos mediante la API [!DNL Dataset Service].

Una vez que haya agregado etiquetas de uso de datos en los niveles de conjunto de datos y campo, puede empezar a introducir datos en [!DNL Experience Platform]. Para obtener más información, comience leyendo la [documentación sobre ingesta de datos](../../ingestion/home.md).

Ahora también puede definir políticas de uso de datos basadas en las etiquetas aplicadas. Para obtener más información, consulte la [descripción general de las políticas de uso de datos](../policies/overview.md).

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la [información general de conjuntos de datos](../../catalog/datasets/overview.md).

## Apéndice {#appendix}

La siguiente sección contiene información adicional sobre cómo trabajar con etiquetas mediante la API del servicio de conjuntos de datos.

### [!DNL If-Match] header {#if-match}

Al realizar llamadas de API que actualizan las etiquetas existentes de un conjunto de datos (PUT y DELETE), se debe incluir un encabezado `If-Match` que indica la versión actual de la entidad de etiqueta del conjunto de datos en el servicio de conjunto de datos. Para evitar conflictos de datos, el servicio solo actualizará la entidad del conjunto de datos si la cadena `If-Match` incluida coincide con la última etiqueta de versión generada por el sistema para ese conjunto de datos.

>[!NOTE]
>
>Si actualmente no existen etiquetas para el conjunto de datos en cuestión, solo se pueden agregar nuevas etiquetas a través de una solicitud de POST, que no requiere un encabezado `If-Match`. Una vez agregadas las etiquetas a un conjunto de datos, se asigna un valor `etag` que puede utilizarse para actualizar o eliminar las etiquetas más adelante.

Para recuperar la versión más reciente de la entidad de etiqueta del conjunto de datos, realice una [solicitud de GET](#look-up) al extremo `/datasets/{DATASET_ID}/labels` . El valor actual se devuelve en la respuesta bajo un encabezado `etag`. Al actualizar las etiquetas de conjuntos de datos existentes, se recomienda realizar primero una solicitud de consulta para el conjunto de datos a fin de recuperar su valor `etag` más reciente antes de utilizar ese valor en el encabezado `If-Match` de la solicitud de PUT o DELETE posterior.
