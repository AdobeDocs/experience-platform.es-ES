---
solution: Experience Platform
title: Segmentación de Edge mediante la API
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación de Edge con la API del servicio de segmentación de Adobe Experience Platform.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 2%

---

# Segmentación de Edge

>[!NOTE]
>
>En el siguiente documento se explica cómo realizar la segmentación de extremos mediante la API. Para obtener información sobre la segmentación de Edge mediante la interfaz de usuario, lea la [guía de la interfaz de usuario de segmentación de Edge](../ui/edge-segmentation.md).
>
>La segmentación de Edge ahora está disponible de forma general para todos los usuarios de Platform. Si ha creado definiciones de segmentos perimetrales durante la versión beta, estas definiciones de segmentos seguirán funcionando.

La segmentación de Edge es la capacidad de evaluar definiciones de segmentos en Adobe Experience Platform de forma instantánea en Edge de, lo que permite casos de uso de personalización de la misma página y de la siguiente.

>[!IMPORTANT]
>
> Los datos perimetrales se almacenarán en una ubicación de servidor perimetral más cercana a la ubicación donde se recopilaron y pueden almacenarse en una ubicación distinta a la designada como centro (o principal) del centro de datos de Adobe Experience Platform.
>
> Además, el motor de segmentación de Edge solo aceptará solicitudes en Edge donde haya **una** identidad principal marcada, lo cual es coherente con las identidades principales no basadas en Edge.

## Introducción

Esta guía para desarrolladores requiere una comprensión práctica de los distintos servicios de [!DNL Adobe Experience Platform] relacionados con la segmentación de Edge. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado en tiempo real, basado en los datos agregados de varias fuentes.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): permite crear audiencias a partir de los datos de [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Para realizar llamadas correctamente a cualquier extremo de API de Experience Platform, lea la guía de [introducción a las API de plataforma](../../landing/api-guide.md) para obtener información acerca de los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Tipos de consultas de segmentación de Edge {#query-types}

Para que se pueda evaluar un segmento mediante la segmentación de Edge, la consulta debe cumplir las siguientes directrices:

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Evento único en un intervalo de tiempo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante en un intervalo de tiempo inferior a 24 horas. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Evento único con un atributo de perfil en un intervalo de tiempo relativo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante, con uno o más atributos de perfil, y que se produzca en un intervalo de tiempo relativo inferior a 24 horas. |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se usa un segmento de segmentos, la descalificación del perfil se producirá **cada 24 horas**. |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tenga uno o más atributos de perfil. |

Además, el segmento **debe** estar vinculado a una política de combinación que esté activa en Edge. Para obtener más información acerca de las políticas de combinación, lea la [guía de políticas de combinación](../../profile/api/merge-policies.md).

Una definición de segmento **no** se habilitará para la segmentación de perímetros en los siguientes casos:

- La definición del segmento incluye una combinación de un solo evento y un evento `inSegment`.
   - Sin embargo, si el segmento contenido en el evento `inSegment` es solo de perfil, la definición del segmento **se habilitará** para la segmentación de Edge.
- La definición del segmento utiliza &quot;Ignorar año&quot; como parte de sus restricciones de tiempo.

## Recuperar todos los segmentos habilitados para la segmentación de Edge

Puede recuperar una lista de todos los segmentos habilitados para la segmentación de extremos dentro de su organización realizando una solicitud de GET al extremo `/segment/definitions`.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de segmentos en su organización que están habilitados para la segmentación de Edge. Encontrará información más detallada sobre la definición de segmento devuelta en la [guía de extremo de definiciones de segmento](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

## Cree un segmento que esté habilitado para la segmentación de Edge

Puede crear un segmento habilitado para la segmentación de Edge realizando una solicitud de POST al extremo `/segment/definitions` que coincida con uno de los tipos de consultas de segmentación de Edge [enumerados arriba](#query-types).

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

>[!NOTE]
>
>El ejemplo siguiente es una solicitud estándar para crear un segmento. Para obtener más información sobre cómo crear una definición de segmento, lea el tutorial de [creación de un segmento](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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
    }
}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición del segmento recién creada que está habilitada para la segmentación de Edge.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
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

Ahora que sabe cómo crear segmentos habilitados para la segmentación de Edge, puede utilizarlos para habilitar casos de uso de personalización de la misma página y de la siguiente.

Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [guía del usuario del Generador de segmentos](../ui/segment-builder.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de Edge:

### ¿Cuánto tiempo tarda un segmento en estar disponible en el Edge Network?

Un segmento puede tardar hasta una hora en estar disponible en el Edge Network.
