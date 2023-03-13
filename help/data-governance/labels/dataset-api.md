---
keywords: Experience Platform;inicio;temas populares;api de conjuntos de datos;administrar uso de datos;api de uso de datos
solution: Experience Platform
title: Administrar etiquetas de uso de datos para conjuntos de datos mediante API
description: La API del servicio de conjuntos de datos permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente de la API del servicio de catálogo que administra los metadatos del conjunto de datos.
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 2%

---

# Administrar etiquetas de uso de datos para conjuntos de datos mediante API

El [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) permite aplicar y editar etiquetas de uso para conjuntos de datos. Forma parte de las funciones del catálogo de datos de Adobe Experience Platform, pero es independiente del [!DNL Catalog Service] API que administra los metadatos del conjunto de datos.

>[!IMPORTANT]
>
>La aplicación de etiquetas en el nivel de conjunto de datos solo es compatible con casos de uso de gobernanza de datos. Si intenta crear directivas de acceso para los datos, debe [aplicar etiquetas al esquema](../../xdm/tutorials/labels.md) en el que se basa el conjunto de datos. Consulte la información general sobre [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener más información.

Este documento explica cómo administrar etiquetas para conjuntos de datos y campos mediante [!DNL Dataset Service API]. Para ver los pasos sobre cómo administrar las propias etiquetas de uso de datos mediante llamadas a la API, consulte la [guía de extremo de etiquetas](../api/labels.md) para el [!DNL Policy Service API].

## Primeros pasos

Antes de leer esta guía, siga los pasos descritos en la [sección de introducción](../../catalog/api/getting-started.md) en la Guía para desarrolladores de catálogos para recopilar las credenciales necesarias para realizar llamadas a [!DNL Platform] API.

Para realizar llamadas a los extremos descritos en este documento, debe tener el `id` para un conjunto de datos específico. Si no tiene este valor, consulte la guía de [enumeración de objetos de catálogo](../../catalog/api/list-objects.md) para buscar los ID de los conjuntos de datos existentes.

## Búsqueda de etiquetas para un conjunto de datos {#look-up}

Puede buscar las etiquetas de uso de datos que se han aplicado a un conjunto de datos existente realizando una solicitud de GET al [!DNL Dataset Service] API.

**Formato de API**

```http
GET /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | La exclusiva `id` valor del conjunto de datos cuyas etiquetas desea buscar. |

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

Puede crear un conjunto de etiquetas para un conjunto de datos proporcionándolas en la carga útil de una solicitud de POST o PUT a [!DNL Dataset Service] API. El uso de cualquiera de estos métodos sobrescribe las etiquetas existentes y las reemplaza por las proporcionadas en la carga útil.

**Formato de API**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| Parámetro | Descripción |
| --- | --- |
| `{DATASET_ID}` | La exclusiva `id` valor del conjunto de datos para el que está creando etiquetas. |

**Solicitud**

La solicitud del PUT de ejemplo siguiente actualiza las etiquetas existentes para un conjunto de datos, así como un campo específico dentro de ese conjunto de datos. Los campos proporcionados en la carga útil son los mismos que se requerirían para una solicitud de POST.

Cuando se realizan llamadas de API que actualizan las etiquetas existentes de un conjunto de datos (PUT), una `If-Match` que indica la versión actual de la entidad dataset-label en el servicio Dataset debe estar incluido. Para evitar conflictos de datos, el servicio solo actualizará la entidad del conjunto de datos si el incluye `If-Match` cadena coincide con la última etiqueta de versión generada por el sistema para ese conjunto de datos.

>[!NOTE]
>
>Si actualmente no existen etiquetas para el conjunto de datos en cuestión, solo se pueden añadir nuevas etiquetas mediante una solicitud de POST, que no requiere un `If-Match` encabezado. Una vez añadidas las etiquetas a un conjunto de datos, se puede `etag` se asigna un valor que puede utilizarse para actualizar o quitar las etiquetas más adelante.

Para recuperar la versión más reciente de la entidad dataset-label, cree un [petición de GET](#look-up) a la `/datasets/{DATASET_ID}/labels` punto final. El valor actual se devuelve en la respuesta en un `etag` encabezado. Al actualizar las etiquetas de conjuntos de datos existentes, la práctica recomendada es realizar primero una solicitud de búsqueda para el conjunto de datos para recuperar su última versión `etag` antes de usar ese valor en `If-Match` encabezado de la solicitud de PUT posterior.

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
| `labels` | Una lista de etiquetas de uso de datos que desee agregar al conjunto de datos. |
| `optionalLabels` | Una lista de cualquier campo individual dentro del conjunto de datos al que desee agregar etiquetas. Cada elemento de esta matriz debe tener las siguientes propiedades: <br/><br/>`option`: Un objeto que contiene la variable [!DNL Experience Data Model] Atributos (XDM) del campo. Se requieren las tres propiedades siguientes:<ul><li>id</code>: URI $id</code> valor del esquema asociado al campo.</li><li>contentType</code>: el tipo de contenido y el número de versión del esquema. Debe adoptar la forma de una de las <a href="../../xdm/api/getting-started.md#accept">Aceptar encabezados</a> para una solicitud de búsqueda XDM.</li><li>schemaPath</code>: Ruta al campo dentro del esquema del conjunto de datos.</li></ul>`labels`: una lista de etiquetas de uso de datos que desea agregar al campo. |

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

Al leer este documento, ha aprendido a administrar las etiquetas de uso de datos para conjuntos de datos y campos mediante [!DNL Dataset Service] API. Ahora puede definir [políticas de uso de datos](../policies/overview.md) y [directivas de control de acceso](../../access-control/abac/ui/policies.md) en función de las etiquetas aplicadas.

Para obtener más información sobre la administración de conjuntos de datos en [!DNL Experience Platform], consulte la [información general sobre conjuntos de datos](../../catalog/datasets/overview.md).
