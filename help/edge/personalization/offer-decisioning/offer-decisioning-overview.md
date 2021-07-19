---
title: Uso del Offer decisioning con el SDK web de Platform
description: El SDK web de Adobe Experience Platform puede entregar y procesar ofertas personalizadas administradas en Offer decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario o la API de Offer decisioning.
keywords: offer decisioning;toma de decisiones;SDK web;SDK web de plataforma;ofertas personalizadas;entrega de ofertas;entrega de ofertas;personalización de ofertas;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 3%

---

# Uso del Offer decisioning con el SDK web de Platform

>[!NOTE]
>
>El uso de Offer decisioning en el SDK web de Adobe Experience Platform está disponible actualmente en acceso anticipado para determinados usuarios. Esta funcionalidad no está disponible para todas las organizaciones de IMS.

Adobe Experience Platform [!DNL Web SDK] puede entregar y procesar ofertas personalizadas que se administran en Offer decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario (IU) o las API de Offer decisioning.

## Requisitos previos

* La organización IMS está habilitada para la toma de decisiones de Edge
* Ofertas, actividades creadas
* Datastream se publica

## Terminología

Es importante comprender la siguiente terminología al trabajar con Offer decisioning. Para obtener más información y ver términos adicionales, visite el [glosario del Offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contenedor:** un contenedor es un mecanismo de aislamiento para mantener separadas diferentes preocupaciones. El ID de contenedor es el primer elemento de ruta para todas las API de repositorio. Todos los objetos de decisión residen dentro de un contenedor.

* **Ámbitos de decisión:** Para Offer decisioning, estas son las cadenas codificadas Base64 de JSON que contienen los ID de actividad y ubicación que desea que utilice el servicio de offer decisioning para proponer ofertas.

   *Ámbito de la decisión JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Alcance de la decisión Cadena codificada Base64:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Puede copiar el valor del ámbito de decisión de la página **Información general de actividad** en la interfaz de usuario.

   ![](assets/decision-scope-copy.png)

* **Datastreams:** Para obtener más información, lea la documentación de  [](../../fundamentals/datastreams.md) datastreamsdocumentation.

* **Identidad**: Para obtener más información, consulte esta documentación que describe cómo el SDK web de  [Platform aprovecha el servicio](../../identity/overview.md) de identidad.

## Activación del Offer decisioning

Para habilitar el Offer decisioning, debe realizar los siguientes pasos:

1. Adobe Experience Platform habilitado en su [almacén de datos](../../fundamentals/datastreams.md) y marque la casilla &quot;Offer decisioning&quot;

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Siga las instrucciones para [instalar el SDK](../../fundamentals/installing-the-sdk.md) (El SDK puede instalarse de forma independiente o a través de [Adobe Experience Platform Launch](http://launch.adobe.com/es). Esta es una [guía de inicio rápido para Platform launch](../../../tags/quick-start/quick-start.md)).
1. [Configure el ](../../fundamentals/configuring-the-sdk.md) SDK para el Offer decisioning. A continuación se proporcionan pasos adicionales específicos del Offer decisioning.

   * SDK instalado de forma independiente

      1. Configure la acción &quot;sendEvent&quot; con su `decisionScopes`

         ```javascript
          alloy("sendEvent", {
             ...
             "decisionScopes": [
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIwOWMxM2JkZDIyNCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMDZhODRkMDViMTEifQ==",
                 "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIxYWIyNWI5NTUwNWIxZiIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMWFiMjFmOTQzMDE0MmIifQ=="
             ]
          })
         ```
   * SDK instalado de platform launch

      1. [Crear una propiedad de Platform launch](../../../tags/ui/administration/companies-and-properties.md)
      1. [Añadir el código incrustado de Platform launch](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Instale y configure la extensión del SDK web de Platform con el Datastream que acaba de crear seleccionando la configuración en la lista desplegable &quot;Datastream&quot;. Consulte la documentación sobre [extensiones](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Cree los [Elementos de datos](../../../tags/ui/managing-resources/data-elements.md) necesarios. Como mínimo, debe crear un mapa de identidad del SDK web de plataforma y un elemento de datos de objeto XDM del SDK web de plataforma .

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Cree sus [Reglas](../../../tags/ui/managing-resources/rules.md).

         * Añada una acción de Platform Web SDK Send Event y añada el `decisionScopes` correspondiente a la configuración de esa acción

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [Cree y publique una ](../../../tags/ui/publishing/libraries.md) biblioteca que contenga todas las reglas, elementos de datos y extensiones relevantes que haya configurado



## Solicitudes y respuestas de ejemplo

### Un valor `decisionScopes`

**Solicitud**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
          ]
        }
      }
    }
  ]
}
```

| Propiedad | Requerido | Descripción | Límites | Ejemplo |
|---|---|---|---|---|
| `identityMap` | Sí | Consulte esta [documentación del servicio de identidad](../../identity/overview.md). | Una identidad por solicitud. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sí | Matriz de cadenas codificadas Base64 de JSON que contienen los ID de actividad y ubicación. | Máximo 30 `decisionScopes` por solicitud. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

**Respuesta**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "2862bb89-5df2-4bc6-85c2-d8f7e1a091de",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:124cc332095cfa74",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-html",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:124cc332095cfa74",
                "format": "text/html",
                "language": [
                  "en-US"
                ],
                "content": "<p>20% Off on shipping</p>",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Propiedad | Descripción | Ejemplo |
|---|---|---|
| `scope` | El ámbito de decisión que dio lugar a las ofertas propuestas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID exclusivo de la actividad de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID exclusivo de la ubicación de la oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Esquema del contenido asociado con la oferta propuesta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | El formato del contenido asociado con la oferta propuesta. | `"format": "text/html"` |
| `language` | Matriz de idiomas asociados al contenido de la oferta propuesta. | `"language": [ "en-US" ]` |
| `content` | Contenido asociado con la oferta propuesta en formato de cadena. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenido de imagen asociado con la oferta propuesta en formato de URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características asociadas con la oferta propuesta en el formato de un objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Varios valores `decisionScopes`

**Solicitud**

```json
{
  "events": [
    {
      "xdm": {
        "identityMap": {
          "ECID": [
            {
              "id": "91133425615229052182584359620783097099"
            }
          ]
        }
      },
      "query": {
        "personalization": {
          "decisionScopes": [
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ==",
            "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyYzkxMzg1Mjc2MDE4YyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMzMxZjU2MTYyYWEyZjcifQ=="
          ]
        }
      }
    }
  ]
}
```

| Propiedad | Requerido | Descripción | Límites | Ejemplo |
|---|---|---|---|---|
| `identityMap` | Sí | Consulte esta [documentación del servicio de identidad](../../identity/overview.md). | Una identidad por solicitud. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }` |
| `decisionScopes` | Sí | Matriz de cadenas codificadas Base64 de JSON que contienen los ID de actividad y ubicación. | Máximo 30 `decisionScopes` por solicitud. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

**Respuesta**

```json
{
  "requestId": "94c4f2f1-9218-43ce-afd3-eb0d853c5174",
  "handle": [
    {
      "payload": [
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MTEyMyIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDExMjMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381123",
            "etag": "1"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b01123",
            "etag": "3"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a22954123",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-text",
              "etag": "2",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a22954123",
                "format": "text/text",
                "language": [
                  "en"
                ],
                "content": "20% Off on shipping",
                "characteristics": {
                  "foo2": "bar2"
                }
              }
            }
          ]
        },
        {
          "id": "a2804dfb-a0ec-4df9-8311-59d3ecdeb642",
          "scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==",
          "activity": {
            "id": "xcore:offer-activity:11cfb1fa93381aca",
            "etag": "2"
          },
          "placement": {
            "id": "xcore:offer-placement:1175009612b0100c",
            "etag": "1"
          },
          "items": [
            {
              "id": "xcore:personalized-offer:11e36d4a2295415d",
              "schema": "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
              "etag": "1",
              "data": {
                "id": "xcore:personalized-offer:11e36d4a2295415d",
                "format": "image/png",
                "language": [
                  "en"
                ],
                "deliveryURL": "https://image.jpeg",
                "characteristics": {
                  "foo": "bar",
                  "foo1": "bar1"
                }
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

| Propiedad | Descripción | Ejemplo |
|---|---|---|
| `scope` | El ámbito de decisión que dio lugar a las ofertas propuestas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID exclusivo de la actividad de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | ID exclusivo de la ubicación de la oferta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Esquema del contenido asociado con la oferta propuesta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | El formato del contenido asociado con la oferta propuesta. | `"format": "text/text"` |
| `language` | Matriz de idiomas asociados al contenido de la oferta propuesta. | `"language": [ "en-US" ]` |
| `content` | Contenido asociado con la oferta propuesta en formato de cadena. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenido de imagen asociado con la oferta propuesta en formato de URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características asociadas con la oferta propuesta en el formato de un objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
