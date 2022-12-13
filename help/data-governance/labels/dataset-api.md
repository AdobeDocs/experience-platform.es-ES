---
keywords: Experience Platform;inicio;temas populares;api de conjunto de datos;administrar uso de datos;api de uso de datos
solution: Experience Platform
title: Administrar etiquetas de uso de datos para conjuntos de datos mediante API
topic-legacy: developer guide
description: La API del servicio de conjunto de datos le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funcionalidades del catálogo de datos de Adobe Experience Platform, pero está separado de la API del servicio de catálogo que administra los metadatos del conjunto de datos.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 2%

---

# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

La variable [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) le permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero está separado de la función [!DNL Catalog Service] API que administra metadatos de conjuntos de datos.

>[!IMPORTANT]
>
>La aplicación de etiquetas en el nivel de conjunto de datos solo se admite para casos de uso de control de datos. Si intenta crear directivas de acceso para los datos, debe [aplicar etiquetas al esquema](../../xdm/tutorials/labels.md) en el que se basa el conjunto de datos. Consulte la descripción general sobre [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener más información.

Este documento explica cómo administrar etiquetas para conjuntos de datos y campos mediante el uso de [!DNL Dataset Service API]. Para ver los pasos sobre cómo administrar las etiquetas de uso de datos mediante llamadas a la API, consulte la [guía de extremo de etiquetas](../api/labels.md) para el [!DNL Policy Service API].

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la sección [sección introducción](../../catalog/api/getting-started.md) en la guía para desarrolladores de Catálogo para recopilar las credenciales necesarias para realizar llamadas a [!DNL Platform] API.

Para realizar llamadas a los extremos descritos en este documento, debe tener la variable `id` para un conjunto de datos específico. Si no tiene este valor, consulte la guía de [listado de objetos del catálogo](../../catalog/api/list-objects.md) para buscar los ID de sus conjuntos de datos existentes.

## Buscar etiquetas para un conjunto de datos {#look-up}

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
| `optionalLabels` | Una lista de campos individuales dentro del conjunto de datos que tienen etiquetas de uso de datos aplicadas a ellos. |

## Aplicar etiquetas a un conjunto de datos {#apply}

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

La solicitud de PUT de ejemplo siguiente actualiza las etiquetas existentes para un conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud del POST.

Al realizar llamadas de API que actualizan las etiquetas existentes de un conjunto de datos (PUT), una variable `If-Match` que indica la versión actual de la entidad de etiqueta de conjunto de datos en el servicio de conjunto de datos debe estar incluida. Para evitar conflictos de datos, el servicio solo actualizará la entidad del conjunto de datos si se incluye el `If-Match` coincide con la última etiqueta de versión generada por el sistema para ese conjunto de datos.

>[!NOTE]
>
>Si actualmente no existen etiquetas para el conjunto de datos en cuestión, solo se pueden agregar nuevas etiquetas a través de una solicitud del POST, que no requiere una `If-Match` encabezado. Una vez que las etiquetas se han agregado a un conjunto de datos, una `etag` se asigna el valor que puede utilizarse para actualizar o eliminar las etiquetas más adelante.

Para recuperar la versión más reciente de la entidad de etiqueta del conjunto de datos, realice una [solicitud de GET](#look-up) a `/datasets/{DATASET_ID}/labels` punto final. El valor actual se devuelve en la respuesta en una `etag` encabezado. Al actualizar las etiquetas de conjuntos de datos existentes, se recomienda realizar primero una solicitud de consulta para el conjunto de datos con el fin de obtener la última `etag` antes de usar ese valor en la variable `If-Match` encabezado de la solicitud de PUT posterior.

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
| `optionalLabels` | Una lista de los campos individuales dentro del conjunto de datos a los que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`: Un objeto que contiene la variable [!DNL Experience Data Model] (XDM) atributos del campo. Se requieren las tres propiedades siguientes:<ul><li>id</code>: El URI $id</code> del esquema asociado al campo.</li><li>contentType</code>: Tipo de contenido y número de versión del esquema. Esto debería adoptar la forma de uno de los <a href="../../xdm/api/getting-started.md#accept">Aceptar encabezados</a> para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`: Una lista de etiquetas de uso de datos que desea agregar al campo. |

**Respuesta**

Una respuesta correcta devuelve el conjunto actualizado de etiquetas para el conjunto de datos.

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

## Pasos siguientes

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos usando la variable [!DNL Dataset Service] API. Ahora puede definir [políticas de uso de datos](../policies/overview.md) y [directivas de control de acceso](../../access-control/abac/ui/policies.md) en función de las etiquetas aplicadas.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la [información general sobre conjuntos de datos](../../catalog/datasets/overview.md).
