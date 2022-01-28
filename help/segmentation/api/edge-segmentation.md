---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;segmentación perimetral;segmentación perimetral;borde de flujo continuo;
solution: Experience Platform
title: 'Segmentación de Edge con la API '
topic-legacy: developer guide
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación perimetral con la API del servicio de segmentación de Adobe Experience Platform.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: e52aa55adde532d838d5417feba36913ed03ce29
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---

# Segmentación de Edge

>[!NOTE]
>
>The following document states how to perform edge segmentation using the API. Para obtener información sobre la realización de segmentación de Edge mediante la interfaz de usuario, lea la [guía de la interfaz de usuario de segmentación de Edge](../ui/edge-segmentation.md).
>
>La segmentación perimetral ahora está disponible para todos los usuarios de Platform. Si ha creado segmentos Edge durante la versión beta, estos segmentos seguirán funcionando.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.

>[!IMPORTANT]
>
> Los datos perimetrales se almacenarán en una ubicación de servidor perimetral más cercana a donde se recopilaron y pueden almacenarse en una ubicación distinta a la designada como centro de datos de Adobe Experience Platform hub (o principal).
>
> Además, el motor de segmentación de aristas solo aceptará solicitudes en el perímetro donde haya **one** identidad marcada principal, que es coherente con las identidades principales no basadas en periferia.

## Primeros pasos

Esta guía para desarrolladores requiere una comprensión práctica de las distintas [!DNL Adobe Experience Platform] servicios relacionados con la segmentación de Edge. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Provides a unified consumer profile in real-time, based on aggregated data from multiple sources.
- [[!DNL Segmentation]](../home.md): Provides the ability to create segments and audiences from your [!DNL Real-time Customer Profile] data.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

In order to successfully make calls to any Experience Platform API endpoints, please read the guide on [getting started with Platform APIs](../../landing/api-guide.md) to learn about required headers and how to read sample API calls.

## Edge segmentation query types {#query-types}

In order for a segment to be evaluated using edge segmentation, the query must conform to the following guidelines:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Un solo evento | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | Personas que han agregado un elemento al carro de compras. |
| Single event that refers to a profile | Any segment definition that refers to one or more profile attributes and a single incoming event with no time restriction. | Personas que viven en Estados Unidos que visitaron la página principal. |
| Se ha anulado un evento único con un atributo de perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante denegado y a uno o más atributos de perfil | Personas que viven en Estados Unidos y que tienen **not** visité la página principal. |
| Un solo evento dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un solo evento entrante en un plazo de 24 horas. | Personas que visitaron la página principal en las últimas 24 horas. |
| Evento único con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento entrante único denegado en un plazo de 24 horas. | Personas que viven en Estados Unidos que visitaron la página principal en las últimas 24 horas. |
| Se ha anulado un evento único con un atributo de perfil en un periodo de tiempo de 24 horas | Any segment definition that refers to one or more profile attributes and a negated single incoming event within 24 hours. | Personas que viven en Estados Unidos y que tienen **not** visité la página principal en las últimas 24 horas. |
| Frequency event within a 24-hour time window | Cualquier definición de segmento que haga referencia a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. |
| Evento de frecuencia con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | People from the USA who visited the homepage **at least** five times in the last 24 hours. |
| Evento de frecuencia anulado con un perfil dentro de un intervalo de tiempo de 24 horas | Any segment definition that refers to one or more profile attributes and a negated event that takes place a certain number of times within a time window of 24 hours. | Personas que no han visitado la página principal **more** más de cinco veces en las últimas 24 horas. |
| Varias visitas entrantes dentro de un perfil de tiempo de 24 horas | Any segment definition that refers to multiple events that occur within a time window of 24 hours. | Personas que visitaron la página principal **o** visité la página de cierre de compra en las últimas 24 horas. |
| Multiple events with a profile within a 24-hour time window | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a varios eventos que se producen en un periodo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **y** visité la página de cierre de compra en las últimas 24 horas. |

Additionally, the segment **must** be tied to a merge policy that is active on edge. Para obtener más información sobre las directivas de combinación, lea la [guía de políticas de combinación](../../profile/api/merge-policies.md).

## Retrieve all segments enabled for edge segmentation

Puede recuperar una lista de todos los segmentos habilitados para la segmentación de Edge dentro de su organización de IMS realizando una solicitud de GET al `/segment/definitions` punto final.

**Formato de API**

To retrieve segments enabled for edge segmentation, you must include the query parameter `evaluationInfo.synchronous.enabled=true` in the request path.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de segmentos en su organización de IMS que están habilitados para la segmentación de Edge. More detailed information about the segment definition returned can be found in the [segment definitions endpoint guide](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Crear un segmento que esté habilitado para la segmentación perimetral

You can create a segment that is enabled for edge segmentation by making a POST request to the `/segment/definitions` endpoint that matches one of the [edge segmentation query types listed above](#query-types).

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

>[!NOTE]
>
>El ejemplo siguiente es una solicitud estándar para crear un segmento. For more information about creating a segment definition, please read the tutorial on [creating a segment](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición de segmento recién creada que está habilitada para la segmentación de Edge.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Pasos siguientes

Ahora que sabe cómo crear segmentos con segmentación perimetral habilitada, puede utilizarlos para habilitar casos de uso de personalización de la misma página y de la siguiente página.

To learn how to perform similar actions and work with segments using the Adobe Experience Platform user interface, please visit the [Segment Builder user guide](../ui/segment-builder.md).
