---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;segmentación perimetral;segmentación perimetral;borde de flujo continuo;
solution: Experience Platform
title: 'Segmentación de Edge con la API '
topic-legacy: developer guide
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación perimetral con la API del servicio de segmentación de Adobe Experience Platform.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# Segmentación de Edge (beta)

>[!NOTE]
>
>El siguiente documento indica cómo realizar la segmentación perimetral mediante la API. Para obtener información sobre cómo realizar la segmentación perimetral mediante la interfaz de usuario, lea la [guía de la interfaz de segmentación de Edge](../ui/edge-segmentation.md). Además, la segmentación de Edge se encuentra actualmente en fase beta. La documentación y las funciones están sujetas a cambios.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform instantáneamente en el perímetro, habilitando los casos de uso de personalización de la misma página y de la siguiente página.

## Primeros pasos

Esta guía para desarrolladores requiere una comprensión práctica de los diversos servicios [!DNL Adobe Experience Platform] que intervienen en la segmentación de Edge. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md): Proporciona la capacidad de crear segmentos y audiencias a partir de los  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Para realizar llamadas correctamente a [!DNL Data Prep] extremos de API, lea la guía de [introducción a las API de Platform](../../landing/api-guide.md) para obtener más información sobre los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Tipos de consulta de segmentación de Edge {#query-types}

Para que un segmento se evalúe mediante segmentación de Edge, la consulta debe cumplir las siguientes directrices:

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. |
| Consulta de frecuencia | Cualquier definición de segmento que haga referencia a un evento que se produzca al menos un determinado número de veces. |
| Consulta de frecuencia que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un evento que se produzca al menos un determinado número de veces y que tenga uno o más atributos de perfil. |

{style=&quot;table-layout:auto&quot;}

Los siguientes tipos de consulta son **no** compatibles actualmente con la segmentación de Edge:

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Ventana de tiempo relativo | Si una consulta hace referencia a un período de tiempo, no se puede evaluar mediante la segmentación perimetral. |
| Negación | Si una consulta contiene una negación o un evento `not`, no se puede evaluar mediante la segmentación perimetral. |
| Varios eventos | Si una consulta contiene más de un evento, no se puede evaluar mediante la segmentación perimetral. |

{style=&quot;table-layout:auto&quot;}

## Recuperar todos los segmentos habilitados para la segmentación de aristas

Puede recuperar una lista de todos los segmentos habilitados para la segmentación de Edge dentro de su organización IMS realizando una solicitud de GET al extremo `/segment/definitions` .

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

Una respuesta correcta devuelve una matriz de segmentos en su organización de IMS que están habilitados para la segmentación de Edge. Puede encontrar información más detallada sobre la definición de segmento devuelta en la [guía de extremo de definiciones de segmento](./segment-definitions.md).

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

Puede crear un segmento habilitado para la segmentación perimetral realizando una solicitud de POST al extremo `/segment/definitions` . Además de hacer coincidir uno de los tipos de consulta de segmentación [edge enumerados arriba](#query-types), debe establecer el indicador `evaluationInfo.synchronous.enabled` en la carga útil como verdadero.

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

>[!NOTE]
>
>El ejemplo siguiente es una solicitud estándar para crear un segmento. Para obtener más información sobre la creación de una definición de segmento, lea el tutorial sobre la [creación de un segmento](../tutorials/create-a-segment.md).

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
    },
    "evaluationInfo": {
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | El objeto `evaluationInfo` determina el tipo de evaluación que se realizará en la definición del segmento. Para utilizar la segmentación perimetral, establezca `evaluationInfo.synchronous.enabled` con un valor de `true`. |

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
```

## Pasos siguientes

Ahora que sabe cómo crear segmentos con segmentación perimetral habilitada, puede utilizarlos para habilitar casos de uso de personalización de la misma página y de la siguiente página.

Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [guía del usuario del Generador de segmentos](../ui/segment-builder.md).
