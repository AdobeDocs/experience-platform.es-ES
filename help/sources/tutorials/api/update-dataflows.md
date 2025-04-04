---
title: Actualización de flujos de datos mediante la API de Flow Service
description: Obtenga información sobre cómo crear un flujo de datos, incluido su nombre, descripción y programación, mediante la API de Flow Service.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 3%

---

# Actualización de flujos de datos mediante la API de Flow Service

Este tutorial describe los pasos para actualizar un flujo de datos, incluida su información básica, programación y conjuntos de asignaciones mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!TIP]
>
>La conexión de origen y la conexión de destino deben asignarse a un solo flujo de datos. No debe actualizar las conexiones de origen y destino por separado, ya que los cambios no se reflejarán en su flujo de datos correspondiente. Si su caso de uso requiere una actualización de las conexiones de origen y destino, debe crear un nuevo par de conexiones de origen y destino, así como un nuevo flujo de datos.

## Introducción

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un identificador de flujo válido, seleccione el conector que prefiera en la [descripción general de orígenes](../../home.md) y siga los pasos descritos antes de intentar realizar este tutorial.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../landing/api-guide.md).

## Búsqueda de detalles de flujo de datos

El primer paso para actualizar el flujo de datos es recuperar los detalles del flujo de datos con el ID de flujo. Puede ver los detalles actuales de un flujo de datos existente realizando una petición GET al extremo `/flows`.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El valor `id` único del flujo de datos que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información actualizada sobre el ID de flujo.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales del flujo de datos, incluida su versión, programación e identificador único (`id`).

```json
{
    "items": [
        {
            "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
            "createdAt": 1612310475905,
            "updatedAt": 1614122324830,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "imsOrgId": "{ORG_ID}",
            "name": "Database dataflow using BigQuery",
            "description": "collecting test1.Mytable from Google BigQuery",
            "flowSpec": {
                "id": "14518937-270c-4525-bdec-c2ba7cce3860",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "etag": "\"5400d99c-0000-0200-0000-60358d540000\"",
            "sourceConnectionIds": [
                "b7581b59-c603-4df1-a689-d23d7ac440f3"
            ],
            "targetConnectionIds": [
                "320f119a-5ac1-4ab1-88ea-eb19e674ea2e"
            ],
            "inheritedAttributes": {
                "sourceConnections": [
                    {
                        "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
                        "connectionSpec": {
                            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
                            "connectionSpec": {
                                "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "320f119a-5ac1-4ab1-88ea-eb19e674ea2e",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "scheduleParams": {
                "startTime": "1612310466",
                "frequency": "week",
                "interval": "15",
                "backfill": "true"
            },
            "transformations": [
                {
                    "name": "Copy",
                    "params": {
                        "deltaColumn": {
                            "name": "Datefield",
                            "dateFormat": "YYYY-MM-DD",
                            "timezone": "UTC"
                        }
                    }
                },
                {
                    "name": "Mapping",
                    "params": {
                        "mappingId": "0b090130b58b4819afc78b6dc98b484d",
                        "mappingVersion": "0"
                    }
                }
            ],
            "runs": "/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c/runs",
            "lastOperation": {
                "started": 1614122316652,
                "updated": 1614122324830,
                "percentCompleted": 100.0,
                "status": {
                    "value": "completed",
                    "errors": []
                },
                "ops": [
                    {
                        "op": "replace",
                        "path": "/scheduleParams/frequency",
                        "value": "week"
                    }
                ],
                "operation": "update"
            },
            "lastRunDetails": {
                "id": "a10cc80b-fbea-4c6b-873e-d7fd32f4d12d",
                "state": "success",
                "startedAtUTC": 1613079975512,
                "completedAtUTC": 1613080027511
            }
        }
    ]
}
```

## Actualizar flujo de datos

Para actualizar la programación de ejecución, el nombre y la descripción del flujo de datos, realice una petición PATCH a la API [!DNL Flow Service] y proporcione al mismo tiempo el ID de flujo, la versión y la nueva programación que desee utilizar.

>[!IMPORTANT]
>
>Se requiere el encabezado `If-Match` al realizar una petición PATCH. El valor de este encabezado es la versión única de la conexión que desea actualizar. El valor de la etiqueta se actualiza con cada actualización correcta de un flujo de datos.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud actualiza la programación de ejecución del flujo, así como el nombre y la descripción del flujo de datos.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
            {
                "op": "replace",
                "path": "/scheduleParams/frequency",
                "value": "day"
            },
            {
                "op": "replace",
                "path": "/name",
                "value": "Database Dataflow Feb2021"
            },
            {
                "op": "replace",
                "path": "/description",
                "value": "Database dataflow for testing update API"
            }
        ]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una petición GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Actualizar asignación

Puede actualizar el conjunto de asignaciones de un flujo de datos existente realizando una petición PATCH a la API [!DNL Flow Service] y proporcionando valores actualizados para `mappingId` y `mappingVersion`.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud actualiza el conjunto de asignaciones del flujo de datos.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/flows/2edc08ac-4df5-4fe6-936f-81a19ce92f5c' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "50014cc8-0000-0200-0000-6036eb720000"' \
    -d '[
        {
            "op": "replace",
            "path": "/transformations/0",
            "value": {
                "name": "Mapping",
                "params": {
                    "mappingId": "c5f22f04e09f44498e528901546a83b1",
                    "mappingVersion": 2
                }
            }
        }
    ]'
```

| Propiedad | Descripción |
| --- | --- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. En este ejemplo, `transformations` se está actualizando. |
| `value.name` | Nombre de la propiedad que se va a actualizar. |
| `value.params.mappingId` | El nuevo ID de asignación que se utilizará para actualizar el conjunto de asignación del flujo de datos. |
| `value.params.mappingVersion` | La nueva versión de asignación asociada con el ID de asignación actualizado. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una petición GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha actualizado la información básica, la programación y los conjuntos de asignaciones del flujo de datos mediante la API [!DNL Flow Service]. Para obtener más información sobre el uso de conectores de origen, vea la [descripción general de orígenes](../../home.md).
