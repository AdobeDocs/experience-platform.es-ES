---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;segmentación perimetral;segmentación perimetral;borde de flujo continuo;
solution: Experience Platform
title: 'Segmentación de Edge con la API '
topic-legacy: developer guide
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación perimetral con la API del servicio de segmentación de Adobe Experience Platform.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: 0173fbd36791f837e0d0336f9fa7bcc84e64909f
workflow-type: tm+mt
source-wordcount: '1014'
ht-degree: 1%

---

# Segmentación de Edge

>[!NOTE]
>
>El siguiente documento indica cómo realizar la segmentación perimetral mediante la API. Para obtener información sobre la realización de segmentación de Edge mediante la interfaz de usuario, lea la [guía de la interfaz de usuario de segmentación de Edge](../ui/edge-segmentation.md).
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

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md): Proporciona la capacidad de crear segmentos y audiencias a partir de [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Para realizar llamadas correctamente a cualquier extremo de API de Experience Platform, lea la guía de [introducción a las API de Platform](../../landing/api-guide.md) para obtener más información sobre los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Tipos de consultas de segmentación de Edge {#query-types}

Para que un segmento se evalúe mediante segmentación de Edge, la consulta debe cumplir las siguientes directrices:

| Tipo de consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Un solo evento | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | Personas que han agregado un elemento al carro de compras. |
| Un solo evento que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un solo evento entrante sin restricciones de tiempo. | Personas que viven en Estados Unidos que visitaron la página principal. |
| Se ha anulado un evento único con un atributo de perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante denegado y a uno o más atributos de perfil | Personas que viven en Estados Unidos y que tienen **not** visité la página principal. |
| Un solo evento dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un solo evento entrante en un plazo de 24 horas. | Personas que visitaron la página principal en las últimas 24 horas. |
| Evento único con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un solo evento entrante en un plazo de 24 horas. | Personas que viven en Estados Unidos que visitaron la página principal en las últimas 24 horas. |
| Se ha anulado un evento único con un atributo de perfil en un periodo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento entrante único denegado en un plazo de 24 horas. | Personas que viven en Estados Unidos y que tienen **not** visité la página principal en las últimas 24 horas. |
| Evento de frecuencia dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. |
| Evento de frecuencia con un atributo de perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento que se produce un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. |
| Evento de frecuencia anulado con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a un evento rechazado que tenga lugar un determinado número de veces dentro de un intervalo de tiempo de 24 horas. | Personas que no han visitado la página principal **more** más de cinco veces en las últimas 24 horas. |
| Varias visitas entrantes dentro de un perfil de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a varios eventos que se producen dentro de un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **o** visité la página de cierre de compra en las últimas 24 horas. |
| Varios eventos con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o más atributos de perfil y a varios eventos que se producen en un periodo de tiempo de 24 horas. | Personas de los Estados Unidos que visitaron la página principal **y** visité la página de cierre de compra en las últimas 24 horas. |

Además, el segmento **must** esté vinculado a una política de combinación activa en edge. Para obtener más información sobre las directivas de combinación, lea la [guía de políticas de combinación](../../profile/api/merge-policies.md).

## Recuperar todos los segmentos habilitados para la segmentación de aristas

Puede recuperar una lista de todos los segmentos habilitados para la segmentación de Edge dentro de su organización de IMS realizando una solicitud de GET al `/segment/definitions` punto final.

**Formato de API**

Para recuperar segmentos habilitados para la segmentación de Edge, debe incluir el parámetro de consulta `evaluationInfo.synchronous.enabled=true` en la ruta de solicitud.

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

Una respuesta correcta devuelve una matriz de segmentos en su organización de IMS que están habilitados para la segmentación de Edge. Encontrará información más detallada sobre la definición de segmento devuelta en la [guía de extremo de definiciones de segmentos](./segment-definitions.md).

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

Puede crear un segmento que esté habilitado para la segmentación perimetral realizando una solicitud de POST al `/segment/definitions` punto final que coincida con uno de los [tipos de consulta de segmentación de aristas enumerados arriba](#query-types).

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

>[!NOTE]
>
>El ejemplo siguiente es una solicitud estándar para crear un segmento. Para obtener más información sobre la creación de una definición de segmento, lea el tutorial sobre [creación de segmentos](../tutorials/create-a-segment.md).

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

Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [Guía del usuario del Generador de segmentos](../ui/segment-builder.md).
