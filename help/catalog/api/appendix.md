---
keywords: Experience Platform;inicio;temas populares;servicio de catálogo;api de catálogo;apéndice
solution: Experience Platform
title: Apéndice de la guía de API del servicio de catálogo
description: Este documento contiene información adicional para ayudarle a trabajar con la API de catálogo en Adobe Experience Platform.
exl-id: fafc8187-a95b-4592-9736-cfd9d32fd135
source-git-commit: 24db94b959d1bad925af1e8e9cbd49f20d9a46dc
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# Apéndice de guía de API [!DNL Catalog Service]

Este documento contiene información adicional para ayudarle a trabajar con la API [!DNL Catalog].

## Ver objetos interrelacionados {#view-interrelated-objects}

Algunos objetos [!DNL Catalog] se pueden interrelacionar con otros objetos [!DNL Catalog]. Cualquier campo con el prefijo `@` en las cargas de respuesta denotan objetos relacionados. Los valores de estos campos toman la forma de un URI, que se puede utilizar en una solicitud de GET independiente para recuperar los objetos relacionados que representan.

El conjunto de datos de ejemplo devuelto en el documento el [al buscar un conjunto de datos específico](look-up-object.md) contiene un campo `files` con el siguiente valor de URI: `"@/datasetFiles?datasetId={DATASET_ID}"`. El contenido del campo `files` se puede ver usando este URI como ruta para una nueva solicitud de GET.

**Formato de API**

```http
GET {OBJECT_URI}
```

| Parámetro | Descripción |
| --- | --- |
| `{OBJECT_URI}` | URI proporcionado por el campo de objeto interrelacionado (excluyendo el símbolo `@`). |

**Solicitud**

La siguiente solicitud utiliza el URI proporcionado por la propiedad `files` del conjunto de datos de ejemplo para recuperar una lista de los archivos asociados del conjunto de datos.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/datasetFiles?datasetId={DATASET_ID}' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una lista de objetos relacionados. En este ejemplo, se devuelve una lista de archivos de conjuntos de datos.

```json
{
    "7d501090-0280-11ea-a6bb-f18323b7005c-1": {
        "id": "7d501090-0280-11ea-a6bb-f18323b7005c-1",
        "batchId": "7d501090-0280-11ea-a6bb-f18323b7005c",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573256315368,
        "updated": 1573256315368
    },
    "148ac690-0280-11ea-8d23-8571a35dce49-1": {
        "id": "148ac690-0280-11ea-8d23-8571a35dce49-1",
        "batchId": "148ac690-0280-11ea-8d23-8571a35dce49",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1573255982433,
        "updated": 1573255982433
    },
    "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1": {
        "id": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb-1",
        "batchId": "64dd5e19-8ea4-4ddd-acd1-f43cccd8eddb",
        "dataSetViewId": "5ba9452f7de80400007fc52b",
        "imsOrg": "{ORG_ID}",
        "createdUser": "{USER_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1569499425037,
        "updated": 1569499425037
    }
}
```

## Encabezados de solicitud adicionales

[!DNL Catalog] proporciona varias convenciones de encabezado para ayudarle a mantener la integridad de los datos durante las actualizaciones.

### Si-Coincidencia

Se recomienda utilizar el control de versiones de objetos para evitar el tipo de corrupción de datos que se produce cuando varios usuarios guardan un objeto casi simultáneamente.

La práctica recomendada al actualizar un objeto implica realizar primero una llamada de API para ver (o GET) el objeto que se va a actualizar. Incluido en la respuesta (y en cualquier llamada en la que la respuesta contenga un solo objeto) hay un encabezado `E-Tag` que contiene la versión del objeto. Si agrega la versión del objeto como un encabezado de solicitud denominado `If-Match` en las llamadas de actualización (PUT o PATCH), la actualización solo se realizará correctamente si la versión sigue siendo la misma, lo que ayudará a evitar el conflicto de datos.

Si las versiones no coinciden (el objeto fue modificado por otro proceso desde que lo recuperó), recibirá el estado HTTP 412 (Error de condición previa) que indica que se ha denegado el acceso al recurso de destino.

### Pragma

En ocasiones, es posible que desee validar un objeto sin guardar la información. El uso del encabezado `Pragma` con un valor de `validate-only` le permite enviar solicitudes de POST o PUT únicamente con fines de validación, lo que evita que se mantengan los cambios en los datos.

## Compactación de datos

La compactación es un servicio de [!DNL Experience Platform] que combina datos de archivos pequeños en archivos más grandes sin cambiar ningún dato. Por motivos de rendimiento, a veces resulta beneficioso combinar un conjunto de archivos pequeños en archivos más grandes para proporcionar un acceso más rápido a los datos cuando se realizan consultas.

Cuando se compactan los archivos de un lote ingerido, su objeto [!DNL Catalog] asociado se actualiza con fines de supervisión.
