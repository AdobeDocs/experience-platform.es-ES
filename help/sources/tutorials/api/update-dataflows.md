---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;actualizar flujos de datos
solution: Experience Platform
title: Actualización de flujos de datos mediante la API del servicio de flujo
type: Tutorial
description: Este tutorial trata los pasos para actualizar un flujo de datos, incluido su nombre, descripción y programación, mediante la API de servicio de flujo.
exl-id: 367a3a9e-0980-4144-a669-e4cfa7a9c722
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---

# Actualización de flujos de datos mediante la API del servicio de flujo

Este tutorial trata los pasos para actualizar un flujo de datos, incluida su información básica, programación y conjuntos de asignación mediante el uso de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Este tutorial requiere que tenga un ID de flujo válido. Si no tiene un ID de flujo válido, seleccione el conector que desee en el [información general sobre fuentes](../../home.md) y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Buscar detalles de flujo de datos

El primer paso para actualizar el flujo de datos es recuperar los detalles del flujo de datos mediante su ID de flujo. Puede ver los detalles actuales de un flujo de datos existente realizando una solicitud de GET al `/flows` punto final.

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El único `id` para el flujo de datos que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información actualizada sobre su ID de flujo.

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

Para actualizar la programación, el nombre y la descripción de ejecución del flujo de datos, realice una solicitud de PATCH al [!DNL Flow Service] mientras proporciona su ID de flujo, versión y la nueva programación que desea utilizar.

>[!IMPORTANT]
>
>La variable `If-Match` es obligatorio cuando se realiza una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión que desea actualizar. El valor de etiqueta se actualiza con cada actualización correcta de un flujo de datos.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud actualiza la programación de la ejecución del flujo, así como el nombre y la descripción del flujo de datos.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

## Actualizar asignación

Puede actualizar el conjunto de asignaciones de un flujo de datos existente realizando una solicitud de PATCH al [!DNL Flow Service] API y proporcionar valores actualizados para su `mappingId` y `mappingVersion`.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

La siguiente solicitud actualiza el conjunto de asignaciones de su flujo de datos.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. En este ejemplo, `transformations` se está actualizando. |
| `value.name` | Nombre de la propiedad que se va a actualizar. |
| `value.params.mappingId` | El nuevo ID de asignación que se utilizará para actualizar el conjunto de asignación del flujo de datos. |
| `value.params.mappingVersion` | La nueva versión de asignación asociada con el ID de asignación actualizado. |

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de flujo.

```json
{
    "id": "2edc08ac-4df5-4fe6-936f-81a19ce92f5c",
    "etag": "\"2c000802-0000-0200-0000-613976440000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha actualizado los conjuntos básicos de información, programación y asignación del flujo de datos mediante la variable [!DNL Flow Service] API. Para obtener más información sobre el uso de conectores de origen, consulte la [información general sobre fuentes](../../home.md).
