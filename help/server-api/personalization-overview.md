---
title: Resumen de personalización
description: Aprenda a utilizar la API del servidor de red perimetral de Adobe Experience Platform para recuperar contenido personalizado de las soluciones de personalización de Adobe.
exl-id: 11be9178-54fe-49d0-b578-69e6a8e6ab90
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 11%

---

# Resumen de personalización

Con el [!DNL Server API], puede recuperar contenido personalizado de las soluciones de personalización de Adobe, incluyendo [Adobe Target](https://business.adobe.com/es/products/target/adobe-target.html) y [Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/starting-offer-decisioning.html?lang=es).

Además, la variable [!DNL Server API] potencia las funcionalidades de personalización de la misma página y de la siguiente página a través de destinos de personalización de Adobe Experience Platform, como [Adobe Target](../destinations/catalog/personalization/adobe-target-connection.md) y el [conexión de personalización personalizada](../destinations/catalog/personalization/custom-personalization.md). Para obtener información sobre cómo configurar Experience Platform para la personalización de la misma página y de la página siguiente, consulte la [guía especializada](../destinations/ui/activate-edge-personalization-destinations.md).

Al utilizar la API de servidor, debe integrar la respuesta proporcionada por el motor de personalización con la lógica utilizada para representar contenido en el sitio. A diferencia del [SDK web](../edge/home.md), el [!DNL Server API] no tiene un mecanismo para aplicar automáticamente el contenido devuelto por [!DNL Adobe Target] y [!DNL Offer Decisioning].

## Terminología {#terminology}

Antes de trabajar con soluciones de personalización de Adobe, asegúrese de comprender los siguientes conceptos:

* **Oferta**: una oferta es un mensaje de marketing que puede tener reglas asociadas que especifican quién puede ver la oferta.
* **Decisión**: Una decisión (anteriormente conocida como actividad de oferta) informa la selección de una oferta.
* **Esquema**: el esquema de una decisión informa el tipo de oferta devuelta.
* **Ámbito**: Ámbito de la decisión.
   * En Adobe Target, esta es la [!DNL mbox]. El [!DNL global mbox] es el `__view__` ámbito
   * Para [!DNL Offer Decisioning], son las cadenas de JSON codificadas en Base64 que contienen los ID de actividad y ubicación que desea que el servicio de offer decisioning utilice para proponer ofertas.

## El `query` objeto {#query-object}

La recuperación de contenido personalizado requiere un objeto de consulta de solicitud explícito para un ejemplo de solicitud. El objeto de consulta tiene el formato siguiente:

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
| `schemas` | `String[]` | Necesario para la personalización de Target. Opcional para Offer decisioning. | Lista de esquemas utilizados en la decisión, para seleccionar el tipo de ofertas devueltas. |
| `scopes` | `String[]` | Opcional | Lista de ámbitos de decisión. Máximo 30 por solicitud. |

## El objeto de identificador {#handle}

El contenido personalizado recuperado de las soluciones de personalización se presenta en un `personalization:decisions` controlador, que tiene el siguiente formato para su carga útil:

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
| `payload.id` | Cadena | ID de decisión. |
| `payload.scope` | Cadena | Ámbito de decisión que dio lugar a las ofertas propuestas. |
| `payload.scopeDetails.decisionProvider` | Cadena | Configure como. `TGT` al usar Adobe Target. |
| `payload.scopeDetails.activity.id` | Cadena | ID único de la actividad de oferta. |
| `payload.scopeDetails.experience.id` | Cadena | ID único de la ubicación de la oferta. |
| `items[].id` | Cadena | ID único de la ubicación de la oferta. |
| `items[].data.id` | Cadena | El ID de la oferta propuesta. |
| `items[].data.schema` | Cadena | El esquema del contenido asociado con la oferta propuesta. |
| `items[].data.format` | Cadena | El formato del contenido asociado con la oferta propuesta. |
| `items[].data.language` | Cadena | Una matriz de idiomas asociados con el contenido de la oferta propuesta. |
| `items[].data.content` | Cadena | Contenido asociado con la oferta propuesta en formato de cadena. |
| `items[].data.selector` | Cadena | Selector de HTML utilizado para identificar el elemento DOM de destino de una oferta de acción DOM. |
| `items[].data.prehidingSelector` | Cadena | Selector de HTML utilizado para identificar el elemento DOM que se va a ocultar al gestionar una oferta de acción DOM. |
| `items[].data.deliveryUrl` | Cadena | Contenido de imagen asociado con la oferta propuesta en formato de dirección URL. |
| `items[].data.characteristics` | Cadena | Características asociadas con la oferta propuesta en formato de objeto JSON. |

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
| `configId` | Cadena | Sí | ID de la secuencia de datos. |
| `requestId` | Cadena | No | Proporcione un ID de seguimiento de solicitud externa. Si no se proporciona ninguno, la red perimetral generará uno para usted y lo devolverá de nuevo en el cuerpo de respuesta/encabezados. |

### Respuesta {#response}

Devuelve un `200 OK` estado y uno o más `Handle` según los servicios perimetrales habilitados en la configuración del conjunto de datos.

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

Las notificaciones se deben activar cuando se haya visitado o procesado un contenido o una vista recuperados previamente al usuario final. Para que las notificaciones se activen en el ámbito correcto, asegúrese de realizar un seguimiento de la correspondiente `id` para cada ámbito.

Notificaciones con el derecho `id` para que los informes se reflejen correctamente, es necesario activar los ámbitos correspondientes.

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
| `dataStreamId` | `String` | Sí | ID de la secuencia de datos utilizada por el extremo de recopilación de datos. |
| `requestId` | `String` | No | ID de seguimiento de solicitud externa externa. Si no se proporciona ninguno, la red perimetral generará uno para usted y lo devolverá de nuevo en el cuerpo de respuesta/encabezados. |
| `silent` | `Boolean` | No | Parámetro booleano opcional que indica si la red perimetral debe devolver un `204 No Content` respuesta con una carga útil vacía. Los errores críticos se registran utilizando el código de estado HTTP y la carga útil correspondientes. |

### Respuesta {#notifications-response}

Una respuesta correcta devuelve uno de los siguientes estados y un `requestID` si no se proporcionó ninguno en la solicitud.

* `202 Accepted` cuando la solicitud se haya procesado correctamente;
* `204 No Content` cuando la solicitud se haya procesado correctamente y la variable `silent` el parámetro se ha establecido en `true`;
* `400 Bad Request` cuando la solicitud no se formó correctamente (por ejemplo, no se encontró la identidad principal obligatoria).

```json
{
  "requestId": "f567a988-4b3c-45a6-9ed8-f283188a445e"
}
```
