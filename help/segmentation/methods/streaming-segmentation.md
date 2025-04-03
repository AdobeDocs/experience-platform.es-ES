---
solution: Experience Platform
title: Guía de segmentación de streaming
description: Obtenga información sobre la segmentación de flujo continuo, incluido qué es, cómo crear una audiencia evaluada mediante la segmentación de flujo y cómo ver las audiencias creadas mediante la segmentación de flujo.
exl-id: cb9b32ce-7c0f-4477-8c49-7de0fa310b97
source-git-commit: f6d700087241fb3a467934ae8e64d04f5c1d98fa
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 1%

---

# Guía de segmentación de streaming

La segmentación por streaming es la capacidad de evaluar audiencias en Adobe Experience Platform en tiempo casi real, al tiempo que se centra en la riqueza de datos.

Con la segmentación por streaming, la calificación de audiencia ahora se produce cuando los datos de streaming llegan a Experience Platform, lo que alivia la necesidad de programar y ejecutar trabajos de segmentación. Esto le permite evaluar los datos a medida que se pasan a Experience Platform, lo que permite mantener actualizada automáticamente la pertenencia a audiencias.

## Tipos de consulta aptos {#query-types}

Una consulta puede optar a la segmentación de flujo continuo si cumple cualquiera de los criterios descritos en la siguiente tabla.

>[!NOTE]
>
>Para que la segmentación de streaming funcione, deberá habilitar la segmentación programada para la organización. Para obtener más información sobre cómo habilitar la segmentación programada, consulte [la descripción general de Audience Portal](../ui/audience-portal.md#scheduled-segmentation).

| Tipo de consulta | Detalles | Consulta | Ejemplo |
| ---------- | ------- | ----- | ------- |
| Evento único en un intervalo de tiempo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante en un intervalo de tiempo inferior a 24 horas. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Se muestra un ejemplo de un solo evento dentro de una ventana de tiempo relativa.](../images/methods/streaming/single-event.png) |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. | `homeAddress.country.equals("US", false)` | ![Se muestra un ejemplo de atributo de perfil.](../images/methods/streaming/profile-attribute.png) |
| Evento único con un atributo de perfil en un intervalo de tiempo relativo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante, con uno o más atributos de perfil, y que se produzca en un intervalo de tiempo relativo inferior a 24 horas. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Se muestra un ejemplo de un solo evento con un atributo de perfil en un intervalo de tiempo relativo.](../images/methods/streaming/single-event-with-profile-attribute.png) |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se usa un segmento de segmentos, la descalificación del perfil se producirá **cada 24 horas**. | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![Se muestra un ejemplo de un segmento de segmentos.](../images/methods/streaming/segment-of-segments.png) |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tenga uno o más atributos de perfil. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("directMarketing.emailClicked", false)) WHEN(today), C1: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Se muestra un ejemplo de varios eventos con un atributo de perfil.](../images/methods/streaming/multiple-events-with-profile-attribute.png) |

Una definición de segmento **no** será elegible para la segmentación de streaming en los siguientes casos:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager (AAM).
- La definición del segmento incluye varias entidades (consultas de varias entidades).
- La definición del segmento incluye una combinación de un solo evento y un evento `inSegment`.
   - Sin embargo, si la definición del segmento contenida en el evento `inSegment` es solo de perfil, la definición del segmento **se habilitará** para la segmentación de flujo continuo.
- La definición del segmento utiliza &quot;Ignorar año&quot; como parte de sus restricciones de tiempo.

Tenga en cuenta las siguientes directrices que se aplican a las consultas de segmentación de streaming:

| Tipo de consulta | Directriz |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva está limitada a **un día**.</li><li>Debe **existir una condición de orden de tiempo estricta entre los eventos.**</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición de segmento cambiará automáticamente de &quot;Flujo&quot; a &quot;Lote&quot;.

Además, la descalificación de segmentos, de manera similar a la calificación de segmentos, se produce en tiempo real. Como resultado, si una audiencia ya no cumple los requisitos para un segmento, se elimina inmediatamente. Por ejemplo, si la definición del segmento solicita &quot;Todos los usuarios que compraron zapatos rojos en las últimas tres horas&quot;, después de tres horas, todos los perfiles que inicialmente se calificaron para la definición del segmento serán no calificados.

## Crear público {#create-audience}

Puede crear una audiencia que se evalúe mediante la segmentación de flujo continuo mediante la API del servicio de segmentación o a través de Audience Portal en la interfaz de usuario.

Una definición de segmento puede habilitarse para streaming si coincide con uno de los [tipos de consulta elegibles](#eligible-query-types).

>[!BEGINTABS]

>[!TAB API del servicio de segmentación]

**Formato de API**

```http
POST /segment/definitions
```

**Solicitud**

+++ Una solicitud de ejemplo para crear una definición de segmento habilitada para la segmentación de flujo continuo

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": false
            },
            "continuous": {
                "enabled": true
            },
            "synchronous": {
                "enabled": false
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con detalles de la definición del segmento recién creada.

+++Una respuesta de ejemplo al crear una definición de segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Encontrará más información sobre el uso de este extremo en la [guía de extremo de definición de segmento](../api/segment-definitions.md).

>[!TAB Portal de públicos]

En Audience Portal, seleccione **[!UICONTROL Crear audiencia]**.

![El botón Crear audiencia está resaltado en el Portal de audiencias.](../images/methods/streaming/select-create-audience.png)

Aparece una ventana emergente. Seleccione **[!UICONTROL Generar reglas]** para ingresar al Generador de segmentos.

![El botón Generar reglas está resaltado en la ventana emergente Crear audiencia.](../images/methods/streaming/select-build-rules.png)

En el Generador de segmentos, cree una definición de segmento que coincida con uno de los [tipos de consulta aptos](#eligible-query-types). Si la definición del segmento cumple los requisitos para la segmentación de transmisión, podrá seleccionar **[!UICONTROL Transmisión]** como **[!UICONTROL método de evaluación]**.

![Se muestra la definición del segmento. El tipo de evaluación está resaltado y muestra que la definición del segmento se puede evaluar mediante la segmentación de flujo continuo.](../images/methods/streaming/streaming-evaluation-method.png)

Para obtener más información sobre cómo crear definiciones de segmentos, lea la [guía del Generador de segmentos](../ui/segment-builder.md)

>[!ENDTABS]

## Recuperar audiencias {#retrieve-audiences}

Puede recuperar todas las audiencias que se evalúan mediante la segmentación de streaming mediante la API del servicio de segmentación o a través de Audience Portal en la interfaz de usuario.

>[!BEGINTABS]

>[!TAB API del servicio de segmentación]

Recupere una lista de todas las definiciones de segmentos que se evalúan mediante la segmentación de flujo continuo dentro de su organización realizando una petición GET al extremo `/segment/definitions`.

**Formato de API**

Debe incluir el parámetro de consulta `evaluationInfo.synchronous.enabled=true` en la ruta de solicitud para recuperar las definiciones de segmento evaluadas mediante la segmentación de flujo continuo.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Solicitud**

+++ Una solicitud de muestra para ver una lista de todas las definiciones de segmentos habilitados para streaming

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con una matriz de definiciones de segmentos en su organización que están habilitadas para la segmentación de flujo continuo.

+++Una respuesta de ejemplo que contiene una lista de todas las definiciones de segmentos habilitadas para la segmentación por streaming de su organización

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
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
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
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
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

Encontrará información más detallada sobre la definición de segmento devuelta en la [guía de extremo de definiciones de segmento](../api/segment-definitions.md).

+++

>[!TAB Portal de públicos]

Puede recuperar todas las audiencias habilitadas para la segmentación de streaming dentro de su organización mediante filtros en Audience Portal. Seleccione el icono de ![filtro](../../images/icons/filter.png) para mostrar la lista de filtros.

![El icono de filtro está resaltado en Audience Portal.](../images/methods/filter-audiences.png)

Dentro de los filtros disponibles, ve a **[!UICONTROL Actualizar frecuencia]** y selecciona &quot;[!UICONTROL Transmisión]&quot;. Uso de este filtro muestra todas las audiencias de su organización que se evalúan mediante la segmentación de flujo continuo.

![Se ha seleccionado la frecuencia Actualización de flujo continuo, que muestra todas las audiencias de la organización que se evalúan mediante la segmentación de flujo continuo.](../images/methods/streaming/filter-streaming.png)

Para obtener más información acerca de cómo ver audiencias en Experience Platform, lea la [guía de Audience Portal](../ui/audience-portal.md).

>[!ENDTABS]

## Detalles de público {#audience-details}

Puede ver los detalles de una audiencia específica evaluada mediante la segmentación de flujo continuo seleccionándola en Audience Portal.

Después de seleccionar una audiencia en Audience Portal, aparece la página de detalles de la audiencia. Muestra información sobre la audiencia, incluido un resumen de los detalles de la audiencia, la cantidad de perfiles cualificados a lo largo del tiempo, así como los destinos a los que se ha activado la audiencia.

![Se muestra la página de detalles de audiencia de una audiencia evaluada mediante la segmentación de flujo continuo.](../images/methods/streaming/audience-details.png)

Para audiencias habilitadas para streaming, se muestra la tarjeta **[!UICONTROL Perfiles a lo largo del tiempo]**, que muestra las métricas totales calificadas y actualizadas de la nueva audiencia.

La métrica **[!UICONTROL Total de audiencias calificadas]** representa el número total de audiencias calificadas, según las evaluaciones por lotes y de streaming para esta audiencia.

La métrica **[!UICONTROL Nueva audiencia actualizada]** está representada por un gráfico de líneas que muestra el cambio en el tamaño de la audiencia a través de la segmentación de flujo continuo. Puede ajustar el menú desplegable para mostrar las últimas 24 horas, la semana pasada o los últimos 30 días.

![La tarjeta Perfiles a lo largo del tiempo está resaltada.](../images/methods/streaming/profiles-over-time.png)

Para obtener más información sobre los detalles de la audiencia, lea la [descripción general del Portal de audiencias](../ui/audience-portal.md#audience-details).

## Pasos siguientes

En esta guía se explica cómo funcionan las definiciones de segmentos habilitadas para streaming en Adobe Experience Platform y cómo monitorizar las definiciones de segmentos habilitadas para streaming.

Para obtener más información acerca del uso de la interfaz de usuario de Adobe Experience Platform, lea la [Guía del usuario de segmentación](./overview.md).

Para las preguntas más frecuentes acerca de la segmentación por transmisión, lea la [sección de segmentación por transmisión de las preguntas frecuentes](../faq.md#streaming-segmentation).
