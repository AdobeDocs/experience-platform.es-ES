---
title: Información general sobre personalización
description: Aprenda a utilizar la API de Adobe Experience Platform Edge Network Server para recuperar contenido personalizado de soluciones de personalización de Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: f36892103b0b202550c07a70538c97b1cc673840
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 9%

---

# Información general sobre personalización

Con la variable [!DNL Server API], puede recuperar contenido personalizado de las soluciones de personalización de Adobe, incluidas [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) y [offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=en).

Además, la variable [!DNL Server API] ofrece funciones de personalización de la misma página y de la página siguiente a través de destinos de personalización de Adobe Experience Platform, como [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) y [conexión personalizada personalizada](../destinations/catalog/personalization/custom-personalization.md). Para obtener información sobre cómo configurar Experience Platform para la personalización de la misma página y de la página siguiente, consulte la [guía dedicada](../destinations/ui/configure-personalization-destinations.md).

Al utilizar la API de servidor, debe integrar la respuesta proporcionada por el motor de personalización con la lógica utilizada para renderizar contenido en el sitio. A diferencia de [SDK web](../edge/home.md), el [!DNL Server API] no tiene un mecanismo para aplicar automáticamente el contenido devuelto por [!DNL Adobe Target] y [!DNL Offer Decisioning].

## Terminología {#terminology}

Antes de trabajar con soluciones de personalización de Adobe, asegúrese de comprender los siguientes conceptos:

* **Oferta**: una oferta es un mensaje de marketing que puede tener reglas asociadas que especifican quién puede ver la oferta.
* **Decisión**: Una decisión (anteriormente conocida como actividad de oferta) informa de la selección de una oferta.
* **Esquema**: El esquema de una decisión informa del tipo de oferta devuelta.
* **Ámbito**: El alcance de la decisión.
   * En Adobe Target, esta es la variable [!DNL mbox]. La variable [!DNL global mbox] es la variable `__view__` scope
   * Para [!DNL Offer Decisioning], son las cadenas con codificación Base64 de JSON que contienen los ID de actividad y ubicación que desea que utilice el servicio de offer decisioning para proponer ofertas.

## La variable `query` object {#query-object}

La recuperación de contenido personalizado requiere un objeto de consulta de solicitud explícita para un ejemplo de solicitud. El objeto de consulta tiene el siguiente formato:

```json
{
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "alloyStore",
            "siteWide",
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}
```

| Atributo | Tipo | Obligatorio/Opcional | Descripción |
| --- | --- | --- | ---|
| `schemas` | `String[]` | Necesario para la personalización de Target. Opcional para el Offer decisioning. | Lista de esquemas utilizados en la decisión, para seleccionar el tipo de ofertas devueltas. |
| `scopes` | `String[]` | Opcional | Lista de ámbitos de decisión. Máximo 30 por solicitud. |

## El objeto handle {#handle}

El contenido personalizado recuperado de las soluciones de personalización se presenta en un `personalization:decisions` identificador, que tiene el siguiente formato para su carga útil:

```json
{
   "type":"personalization:decisions",
   "payload":[
      {
         "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
         "scope":"__view__",
         "scopeDetails":{
            "decisionProvider":"TGT",
            "activity":{
               "id":"131010"
            },
            "experience":{
               "id":"0"
            },
            "strategies":[
               {
                  "algorithmID":"0",
                  "trafficType":"0"
               }
            ]
         },
         "items":[
            {
               "id":"0",
               "schema":"https://ns.adobe.com/personalization/dom-action",
               "meta":{
                  "offer.name":"Default Content",
                  "experience.id":"0",
                  "activity.name":"Luma target reporting",
                  "activity.id":"131010",
                  "experience.name":"Experience A",
                  "option.id":"2",
                  "offer.id":"0"
               },
               "data":{
                  "type":"setHtml",
                  "format":"application/vnd.adobe.target.dom-action",
                  "content":"Customer Service not chrome",
                  "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                  "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
               }
            }
         ]
      }
   ]
}
```

| Atributo | Tipo | Descripción |
| --- | --- | --- |
| `payload.id` | Cadena | El ID de decisión. |
| `payload.scope` | Cadena | El ámbito de decisión que dio lugar a las ofertas propuestas. |
| `payload.scopeDetails.decisionProvider` | Cadena | Establecer como `TGT` al usar Adobe Target. |
| `payload.scopeDetails.activity.id` | Cadena | ID exclusivo de la actividad de oferta. |
| `payload.scopeDetails.experience.id` | Cadena | ID exclusivo de la ubicación de la oferta. |
| `items[].id` | Cadena | ID exclusivo de la ubicación de la oferta. |
| `items[].data.id` | Cadena | El ID de la oferta propuesta. |
| `items[].data.schema` | Cadena | Esquema del contenido asociado con la oferta propuesta. |
| `items[].data.format` | Cadena | El formato del contenido asociado con la oferta propuesta. |
| `items[].data.language` | Cadena | Matriz de idiomas asociados al contenido de la oferta propuesta. |
| `items[].data.content` | Cadena | Contenido asociado con la oferta propuesta en formato de cadena. |
| `items[].data.selector` | Cadena | Selector de HTML utilizado para identificar el elemento DOM de destino para una oferta de acción DOM. |
| `items[].data.prehidingSelector` | Cadena | Selector de HTML utilizado para identificar el elemento DOM que se va a ocultar mientras se gestiona una oferta de acción DOM. |
| `items[].data.deliveryUrl` | Cadena | Contenido de imagen asociado con la oferta propuesta en formato de URL. |
| `items[].data.characteristics` | Cadena | Características asociadas con la oferta propuesta en el formato de un objeto JSON. |

## Llamada de API de ejemplo {#sample-call}

**Formato de API**

```http
POST /ee/v2/interact
```

### Solicitud {#request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event":{
      "xdm":{
         "identityMap":{
            "Email_LC_SHA256":[
               {
                  "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                  "primary":true
               }
            ]
         },
         "eventType":"web.webpagedetails.pageViews",
         "web":{
            "webPageDetails":{
               "URL":"https://alloystore.dev/",
               "name":"home-demo-Home Page"
            }
         },
         "timestamp":"2021-08-09T14:09:20.859Z"
      }
   },
   "query":{
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ"
         ]
      }
   }
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `configId` | Cadena | Sí | El ID del conjunto de datos. |
| `requestId` | Cadena | No | Proporcione un ID de seguimiento de solicitud externo. Si no se proporciona ninguno, la red perimetral generará uno por usted y lo devolverá de nuevo en el cuerpo o los encabezados de respuesta. |

### Respuesta {#response}

Devuelve un `200 OK` estado y uno o más `Handle` objetos, dependiendo de los servicios Edge que estén habilitados en la configuración del conjunto de datos.

```json
{
   "requestId":"da20d11d-adac-458c-91ac-15bf4e420a15",
   "handle":[
      {
         "payload":[
            {
               "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
               "scope":"__view__",
               "scopeDetails":{
                  "decisionProvider":"TGT",
                  "activity":{
                     "id":"131010"
                  },
                  "experience":{
                     "id":"0"
                  },
                  "strategies":[
                     {
                        "algorithmID":"0",
                        "trafficType":"0"
                     }
                  ]
               },
               "items":[
                  {
                     "id":"0",
                     "schema":"https://ns.adobe.com/personalization/dom-action",
                     "meta":{
                        "offer.name":"Default Content",
                        "experience.id":"0",
                        "activity.name":"Luma target reporting",
                        "activity.id":"131010",
                        "experience.name":"Experience A",
                        "option.id":"2",
                        "offer.id":"0"
                     },
                     "data":{
                        "type":"setHtml",
                        "format":"application/vnd.adobe.target.dom-action",
                        "content":"Customer Service not chrome",
                        "selector":"HTML > BODY > DIV.page-wrapper:eq(0) > FOOTER.page-footer:eq(0) > DIV.footer:eq(0) > DIV.links:eq(0) > DIV.widget:eq(0) > UL.footer:eq(0) > LI.nav:eq(1) > A:nth-of-type(1)",
                        "prehidingSelector":"HTML > BODY > DIV:nth-of-type(1) > FOOTER:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > DIV:nth-of-type(1) > UL:nth-of-type(1) > LI:nth-of-type(2) > A:nth-of-type(1)"
                     }
                  }
               ]
            }
         ],
         "type":"personalization:decisions"
      }
   ]
}
```

## Notificaciones {#notifications}

Las notificaciones se deben activar cuando se haya visitado o procesado un contenido o una vista previamente recuperados para el usuario final. Para que las notificaciones se desactiven para el ámbito correcto, asegúrese de realizar un seguimiento de los correspondientes `id` para cada ámbito.

Notificaciones con el derecho `id` para los ámbitos correspondientes deben activarse para que los informes se reflejen correctamente.

**Formato de API**

```http
POST /ee/v2/collect
```

### Solicitud {#notifications-request}

```shell
curl -X POST "https://server.adobedc.net/ee/v2/collect?dataStreamId={DATASTREAM_ID}" 
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "events":[
      {
         "xdm":{
            "identityMap":{
               "Email_LC_SHA256":[
                  {
                     "id":"0c7e6a405862e402eb76a70f8a26fc732d07c32931e9fae9ab1582911d2e8a3b",
                     "primary":true
                  }
               ]
            },
            "eventType":"web.webpagedetails.pageViews",
            "web":{
               "webPageDetails":{
                  "URL":"https://alloystore.dev/",
                  "name":"home-demo-Home Page"
               }
            },
            "timestamp":"2021-08-09T14:09:20.859Z",
            "_experience":{
               "decisioning":{
                  "propositions":[
                     {
                        "id":"AT:eyJhY3Rpdml0eUlkIjoiMTMxMDEwIiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                        "scope":"__view__",
                        "items":[
                           {
                              "id":"0"
                           }
                        ]
                     }
                  ]
               }
            }
         }
      }
   ]
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sí | ID del conjunto de datos utilizado por el extremo de recopilación de datos. |
| `requestId` | `String` | No | ID de seguimiento de solicitud externa externa. Si no se proporciona ninguno, la red perimetral generará uno por usted y lo devolverá de nuevo en el cuerpo o los encabezados de respuesta. |
| `silent` | `Boolean` | No | Parámetro booleano opcional que indica si la red perimetral debe devolver un `204 No Content` con una carga útil vacía. Los errores críticos se notifican utilizando el código de estado HTTP y la carga útil correspondientes. |

### Respuesta {#notifications-response}

Una respuesta correcta devuelve uno de los siguientes estados y una `requestID` si no se ha proporcionado ninguno en la solicitud.

* `202 Accepted` cuando la solicitud se haya procesado correctamente;
* `204 No Content` cuando la solicitud se procesó correctamente y la variable `silent` se ha definido como `true`;
* `400 Bad Request` cuando la solicitud no se formó correctamente (por ejemplo, no se encontró la identidad primaria obligatoria).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
