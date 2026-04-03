---
title: Extremo de carpetas
description: Obtenga información sobre cómo crear, actualizar, administrar y eliminar carpetas mediante las API de Adobe Experience Platform.
role: Developer
exl-id: ee43d699-725d-4ffd-a71b-049eeb3b4d7c
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 5%

---

# Extremo de carpetas

>[!IMPORTANT]
>
>La dirección URL de extremo para este conjunto de extremos es `https://experience.adobe.io`.

Las carpetas son una capacidad que permite organizar mejor los objetos de negocio para facilitar la navegación y la categorización.

Esta guía proporciona información para ayudarle a comprender mejor las carpetas e incluye llamadas de API de ejemplo para realizar acciones básicas mediante la API.

## Introducción

Antes de continuar, revisa la [guía de introducción](./getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluidos los encabezados requeridos y cómo leer llamadas de API de ejemplo.

## Recuperación de una lista de carpetas {#list}

Puede recuperar una lista de carpetas que pertenecen a su organización realizando una petición GET al extremo `/folder` y especificando el tipo de carpeta y el ID de carpeta principal.

**Formato de API**

```http
GET /folders/{FOLDER_TYPE}/{PARENT_FOLDER_ID}/subfolders
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FOLDER_TYPE}` | El tipo de objetos contenidos en la carpeta. Los valores admitidos son `segment` y `dataset`. |
| `{PARENT_FOLDER_ID}` | El ID de la carpeta principal desde la que recupera la lista de carpetas. Para ver una lista de todas las carpetas principales, use el identificador de carpeta `root`. |

**Solicitud**

+++Una solicitud de ejemplo para enumerar todas las carpetas de conjuntos de datos de nivel superior

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/root/subfolders
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una lista de todas las carpetas de nivel superior para el conjunto de datos de su organización.

+++Una respuesta de ejemplo que contiene una lista de todas las carpetas de nivel superior del conjunto de datos de su organización.

```json
{
    "id": "c626b4f7-223b-4486-8900-00c266e31dd1",
    "name": "ParentFolder",
    "noun": "Dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": null,
    "createdAt": "2023-01-12T03:31:00.118+00:00",
    "modifiedBy": null,
    "modifiedAt": "2023-01-13T05:47:06.718+00:00",
    "_links": null,
    "children": [
        {
            "id": "09d86b23-4819-471b-8a2a-05774ed268de",
            "name": "ChildFolder.1",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-12T12:51:39.284+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-12T12:51:39.284+00:00",
            "_links": null,
            "children": []
        },
        {
            "id": "fd2f6a68-ef65-470d-ab31-b02b7b2241ca",
            "name": "ChildFolder.2",
            "noun": "dataset",
            "parentId": "c626b4f7-223b-4486-8900-00c266e31dd1",
            "imsOrg": "{ORG_ID}",
            "sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
            "sandboxName": null,
            "createdBy": "{USER_ID}",
            "createdAt": "2023-01-13T03:38:40.006+00:00",
            "modifiedBy": "{USER_ID}",
            "modifiedAt": "2023-01-13T03:38:40.006+00:00",
            "_links": null,
            "children": []
        }
    ]
}
```

+++

## Creación de una nueva carpeta {#create}

Puede crear una carpeta nueva realizando una petición POST al extremo `/folder` y especificando el tipo de carpeta.

**Formato de API**

```http
POST /folders/{FOLDER_TYPE}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FOLDER_TYPE}` | El tipo de objetos contenidos en la carpeta. Los valores admitidos son `segment` y `dataset`. |

**Solicitud**

+++Una solicitud de ejemplo para crear una carpeta nueva.

```shell
curl -X POST https://experience.adobe.io/unifiedfolders/folders/dataset
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
    "name": "SampleFolder",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5"
 }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | El nombre de la carpeta que desea crear. |
| `parentId` | El ID de la carpeta principal. |

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la carpeta recién creada.

+++Una respuesta de ejemplo que contiene detalles de la carpeta recién creada.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "6a5e0927-1527-4abc-9993-376fd7067ca5",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": null
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El ID de la carpeta recién creada. |
| `createdBy` | El ID del usuario que creó la carpeta. |
| `createdAt` | La marca de tiempo del momento en el que se creó la carpeta. |
| `modifiedBy` | El ID del usuario que modificó la carpeta por última vez. |
| `modifiedAt` | La marca de tiempo de la última actualización de la carpeta. |

+++

## Recuperar una carpeta específica {#get}

Puede recuperar una carpeta específica que pertenezca a su organización realizando una petición GET al extremo `/folder` y especificando el tipo de carpeta y el ID de la carpeta.

**Formato de API**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FOLDER_TYPE}` | El tipo de objetos contenidos en la carpeta. Los valores admitidos son `segment` y `dataset`. |
| `{FOLDER_ID}` | El ID de la carpeta que está recuperando. |

**Solicitud**

+++Una solicitud de ejemplo para recuperar una carpeta específica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la carpeta solicitada.

+++Una respuesta de ejemplo que contiene detalles de la carpeta solicitada.

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | El ID de la carpeta solicitada. |
| `name` | Nombre de la carpeta solicitada. |
| `parentId` | El ID de la carpeta principal. |
| `createdBy` | El ID del usuario que creó la carpeta. |
| `createdAt` | La marca de tiempo del momento en el que se creó la carpeta. |
| `modifiedBy` | El ID del usuario que actualizó la carpeta por última vez. |
| `modifiedAt` | La marca de tiempo de la última actualización de la carpeta. |
| `status` | El estado de la carpeta solicitada. Los valores admitidos son `IN_USE` y `ARCHIVED`. |

+++

## Validar una carpeta especificada {#validate}

Puede validar si una carpeta cumple los requisitos para tener objetos en ella realizando una petición GET al extremo `/folder/{FOLDER_TYPE}/{FOLDER_ID}/validate` y proporcionando el tipo de carpeta y el identificador.

**Formato de API**

```http
GET /folders/{FOLDER_TYPE}/{FOLDER_ID}/validate
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FOLDER_TYPE}` | El tipo de objetos contenidos en la carpeta. Los valores admitidos son `segment` y `dataset`. |
| `{FOLDER_ID}` | El ID de la carpeta que está validando. |

**Solicitud**

+++Una solicitud de ejemplo para validar una carpeta específica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e/validate
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Un estado correcto devuelve el estado HTTP 200 con detalles de la carpeta que está validando.

+++Una respuesta de ejemplo contiene detalles de la carpeta validada

```json
{
    "id": "83f8287c-767b-4106-b271-257282fd170e",
    "name": "SampleFolder",
    "noun": "dataset",
    "parentId": "{PARENT_ID}",
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "{USER_ID}",
    "createdAt": "2023-10-01T08:47:06.192+00:00",
    "status": "IN_USE",
    "modifiedBy": "{USER_ID}",
    "modifiedAt": "2023-10-01T08:47:06.192+00:00",
    "_links": {
        "self": {
            "href": "/folders/dataset/83f8287c-767b-4106-b271-257282fd170e"
        }
    }
}
```

+++

## Actualizar una carpeta específica {#update}

Puede actualizar los detalles de una carpeta específica que pertenezca a su organización realizando una petición PATCH al extremo `/folder` y especificando el tipo de carpeta y el ID de la carpeta.

**Formato de API**

```http
PATCH /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FOLDER_TYPE}` | El tipo de objetos contenidos en la carpeta. Los valores admitidos son `segment` y `dataset`. |
| `{FOLDER_ID}` | El ID de la carpeta que está actualizando. |

**Solicitud**

+++Una solicitud de ejemplo para actualizar una carpeta específica

```shell
curl -X GET https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '[{
    "op": "replace",
    "path": "/name",
    "value": "RenamedSampleFolder"
 }]'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información sobre la carpeta recién actualizada.

```json
{
    "id": "eafab5bf-3457-4b7f-b366-3c5399bd98f1",
    "name": "RenamedSampleFolder",
    "noun": "dataset",
    "parentFolderId": null,
    "imsOrg": "{ORG_ID}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "createdBy": "183807A65A0F5D180A494004@AdobeID",
    "createdAt": "2024-03-05T01:42:36.910+00:00",
    "modifiedBy": "183807A65A0F5D180A494004@AdobeID",
    "modifiedAt": "2024-03-05T01:45:54.740+00:00",
    "status": "IN_USE",
    "_links": {
        "self": {
            "href": "/folders/dataset/eafab5bf-3457-4b7f-b366-3c5399bd98f1"
        }
    },
    "namespace": null
}
```

## Eliminar una carpeta específica {#delete}

Puede eliminar una carpeta específica que pertenezca a su organización realizando una petición DELETE a `/folder` y especificando el tipo de carpeta y el identificador de la carpeta.

***Formato de API**

```http
DELETE /folders/{FOLDER_TYPE}/{FOLDER_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FOLDER_TYPE}` | El tipo de objetos contenidos en la carpeta. Los valores admitidos son `segment` y `dataset`. |
| `{FOLDER_ID}` | El ID de la carpeta que está eliminando. |

**Solicitud**

+++Una solicitud de ejemplo para eliminar una carpeta específica

```shell
curl -X DELETE https://experience.adobe.io/unifiedfolders/folders/dataset/83f8287c-767b-4106-b271-257282fd170e
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con un cuerpo de mensaje que le informa de la eliminación de la carpeta.

```json
{
    "message": "delete request accepted successfully"
}
```

## Próximos pasos

Después de leer esta guía, ahora comprende mejor cómo crear, administrar y eliminar carpetas mediante la API de Adobe Experience Platform.
