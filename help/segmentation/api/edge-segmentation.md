---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;segmentación de Edge;segmentación de Edge;streaming edge;
solution: Experience Platform
title: Segmentación de Edge mediante la API
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación de Edge con la API del servicio de segmentación de Adobe Experience Platform.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 1%

---

# Segmentación de Edge

>[!NOTE]
>
>En el siguiente documento se explica cómo realizar la segmentación de extremos mediante la API. Para obtener información acerca de la segmentación de Edge mediante la interfaz de usuario, lea la [guía de IU de segmentación de Edge](../ui/edge-segmentation.md).
>
>La segmentación de Edge ahora está disponible de forma general para todos los usuarios de Platform. Si ha creado segmentos perimetrales durante la versión beta, estos seguirán funcionando.

La segmentación de Edge es la capacidad de evaluar segmentos en Adobe Experience Platform de forma instantánea en Edge, lo que permite casos de uso de personalización de la misma página y de la siguiente.

>[!IMPORTANT]
>
> Los datos perimetrales se almacenarán en una ubicación de servidor perimetral más cercana a la ubicación donde se recopilaron y pueden almacenarse en una ubicación distinta a la designada como centro (o principal) del centro de datos de Adobe Experience Platform.
>
> Además, el motor de segmentación de Edge solo aceptará solicitudes en el Edge donde haya **uno** identidad marcada principal, que es coherente con las identidades principales no basadas en edge.

## Primeros pasos

Esta guía para desarrolladores requiere una comprensión práctica de los distintos [!DNL Adobe Experience Platform] servicios relacionados con la segmentación de Edge. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona un perfil de consumidor unificado en tiempo real, basado en los datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md): permite crear segmentos y audiencias a partir de [!DNL Real-Time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Para realizar llamadas correctamente a cualquier extremo de API de Experience Platform, lea la guía de [introducción a las API de Platform](../../landing/api-guide.md) para obtener más información sobre los encabezados necesarios y cómo leer llamadas de API de ejemplo.

## Tipos de consulta de segmentación de Edge {#query-types}

Para que se pueda evaluar un segmento mediante la segmentación de Edge, la consulta debe cumplir las siguientes directrices:

| Tipo de consulta | Detalles | Ejemplo | Ejemplo de PQL |
| ---------- | ------- | ------- | ----------- |
| Evento único | Cualquier definición de segmento que haga referencia a un único evento entrante sin restricción horaria. | Personas que han agregado un elemento al carro de compras. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Perfil único | Cualquier definición de segmento que haga referencia a un único atributo de solo perfil | Personas que viven en los Estados Unidos. | `homeAddress.countryCode = "US"` |
| Evento único que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un único evento entrante sin restricción horaria. | Personas que viven en los EE.UU. que visitaron la página principal. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Evento único anulado con un atributo de perfil | Cualquier definición de segmento que haga referencia a un evento entrante único negado y a uno o más atributos de perfil | Personas que viven en los Estados Unidos y tienen **no** ha visitado la página principal. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Evento único dentro de una ventana de tiempo | Cualquier definición de segmento que haga referencia a un único evento entrante en un período de tiempo establecido. | Personas que visitaron la página principal en las últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| Evento único con un atributo de perfil dentro de una ventana de tiempo | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un único evento entrante en un período de tiempo establecido. | Personas que viven en Estados Unidos y que visitaron la página principal en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)])` |
| Evento único anulado con un atributo de perfil en un período de tiempo | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un evento entrante único y negado en un período de tiempo. | Personas que viven en los Estados Unidos y tienen **no** visitó la página principal en las últimas 24 horas. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "addToCart") WHEN(< 8 days before now)]))` |
| Evento de frecuencia en un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a un evento que se produce un determinado número de veces en un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frecuencia con un atributo de perfil en un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un evento que se produce un determinado número de veces en un intervalo de tiempo de 24 horas. | Personas de EE. UU. que visitaron la página principal **al menos** cinco veces en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Evento de frecuencia anulado con un perfil dentro de un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a un evento denegado que se produce un determinado número de veces en un intervalo de tiempo de 24 horas. | Personas que no han visitado la página principal **más** cinco veces en las últimas 24 horas. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Varias visitas entrantes en un perfil de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a varios eventos que se producen en un intervalo de tiempo de 24 horas. | Personas que visitaron la página principal **o** visitó la página de cierre de compra en las últimas 24 horas. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Varios eventos con un perfil en un intervalo de tiempo de 24 horas | Cualquier definición de segmento que haga referencia a uno o varios atributos de perfil y a varios eventos que se producen en un período de tiempo de 24 horas. | Personas de los EE.UU. que visitaron la página principal **y** visitó la página de cierre de compra en las últimas 24 horas. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. | Personas que viven en Estados Unidos y están en el segmento &quot;segmento existente&quot;. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Consulta que hace referencia a un mapa | Cualquier definición de segmento que haga referencia a un mapa de propiedades. | Personas que han agregado a su carro de compras en función de datos de segmentos externos. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Además, el segmento **debe** estar vinculado a una política de combinación que esté activa en edge. Para obtener más información sobre las políticas de combinación, lea la [guía de políticas de combinación](../../profile/api/merge-policies.md).

Una definición de segmento **no** Debe habilitarse la segmentación de Edge en los siguientes casos:

- La definición del segmento incluye una combinación de un solo evento y una `inSegment` evento.
   - Sin embargo, si el segmento contenido en la variable `inSegment` El evento es solo de perfil, la definición del segmento **testamento** habilitarse para la segmentación de Edge.

## Recuperar todos los segmentos habilitados para la segmentación de Edge

Puede recuperar una lista de todos los segmentos habilitados para la segmentación de Edge dentro de su organización realizando una solicitud de GET a `/segment/definitions` punto final.

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

Una respuesta correcta devuelve una matriz de segmentos en su organización que están habilitados para la segmentación de Edge. Encontrará información más detallada acerca de la definición del segmento devuelta en la [guía de extremo de definiciones de segmento](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
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
            "ttlInDays": 30,
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

Puede crear un segmento que esté habilitado para la segmentación de Edge realizando una solicitud de POST a la variable `/segment/definitions` extremo que coincide con uno de los [tipos de consulta de segmentación de Edge enumerados arriba](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
    "ttlInDays": 30,
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

Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite [Guía del usuario del Generador de segmentos](../ui/segment-builder.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de Edge:

### ¿Cuánto tiempo tarda un segmento en estar disponible en la red perimetral?

Un segmento puede tardar hasta una hora en estar disponible en la red perimetral.