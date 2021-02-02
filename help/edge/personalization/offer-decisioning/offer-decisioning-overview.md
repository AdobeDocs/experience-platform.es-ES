---
title: Información general de Offer Decisioning
seo-title: Offer Decisioning y Adobe Experience Platform Web SDK
description: El SDK web de Adobe Experience Platform puede entregar y procesar ofertas personalizadas administradas en Offer Decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario o la API de Offer Decisioning.
seo-description: El SDK web de Adobe Experience Platform puede entregar y procesar ofertas personalizadas administradas en Offer Decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario o la API de Offer Decisioning.
keywords: decisiones de oferta;decisiones;SDK web;SDK web de plataforma;ofertas personalizadas;enviar ofertas;envío de oferta;personalización de oferta;
translation-type: tm+mt
source-git-commit: 05049025bdfc67af4d811e90218bf6e2613fab51
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 9%

---


# [!DNL Offer Decisioning] Información general

>[!NOTE]
>
>El uso de Offer Decisioning en Adobe Experience Platform Web SDK está actualmente disponible en el acceso anticipado a determinados usuarios. Esta funcionalidad no está disponible para todas las organizaciones de IMS.

Adobe Experience Platform [!DNL Web SDK] puede entregar y procesar ofertas personalizadas que se administran en Offer Decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario (IU) o las API de Offer Decisioning.

## Requisitos previos

* La organización de IMS está habilitada para la toma de decisiones de Edge
* Ofertas, Actividades creadas
* La configuración de Edge está publicada

## Terminología

Es importante comprender la siguiente terminología al trabajar con Offer Decisioning. Para obtener más información y vista de términos adicionales, visite el [glosario de Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contenedor:** Un contenedor es un mecanismo de aislamiento para mantener diferentes preocupaciones. El ID de contenedor es el primer elemento de ruta para todas las API de repositorio. Todos los objetos de decisión residen en un contenedor.

* **Ámbitos de decisión:** para Offer Decisioning, estas son las cadenas codificadas Base64 de JSON que contienen los ID de actividad y colocación que desea que utilice el servicio de decisiones de oferta para proponer ofertas.

   *Ámbito de decisión JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Cadena con codificación Base64 del ámbito de decisión:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Puede copiar el valor del ámbito de decisión de la página **Información general de Actividad** en la interfaz de usuario.

   ![](assets/decision-scope-copy.png)

* **Configuración de Edge:** para obtener más información, lea la documentación de  [Edge ](../../fundamentals/edge-configuration.md) Configuration.

* **Identidad**: Para obtener más información, lea esta documentación en la que se describe cómo  [Platform Web SDK aprovecha Identity Service](../../identity/overview.md).

## Activación de Offer Decisioning

Para habilitar Offer Decisioning, debe realizar los siguientes pasos:

1. Se habilitó Adobe Experience Platform en la [configuración de Edge](../../fundamentals/edge-configuration.md) y se marcó la casilla &quot;Offer Decisioning&quot;
   ![oferta-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)
2. Siga las instrucciones para [instalar el SDK](../../fundamentals/installing-the-sdk.md) (el SDK se puede instalar de forma independiente o a través de [Adobe Experience Platform Launch](http://launch.adobe.com/es). Esta es una [guía rápida de inicio al lanzamiento de plataforma](https://docs.adobe.com/content/help/es-ES/launch/using/intro/get-started/quick-start.html)).
3. [Configure el ](../../fundamentals/configuring-the-sdk.md) SDK para Offer Decisioning. A continuación se proporcionan pasos adicionales específicos de Offer Decisioning.
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
   * SDK instalado de inicio de plataforma
      1. [Crear una propiedad de inicio de plataforma](https://docs.adobe.com/content/help/es-ES/launch/using/reference/admin/companies-and-properties.html)
      2. [Añadir el código incrustado de inicio de plataforma](https://docs.adobe.com/content/help/en/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      3. Instale y configure la extensión AEP Web SDK con la configuración de Edge que acaba de crear seleccionando la configuración en la lista desplegable &quot;Configuración de Edge&quot;. Documentación útil sobre [extensiones](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html).
         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)
      4. Cree los [elementos de datos](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/data-elements.html) necesarios. Como mínimo, deberá crear un mapa de identidad del SDK web de plataforma y un elemento de datos de objeto XDM del SDK web de plataforma.
         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)
      5. Cree sus [reglas](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html).
         * Añadir una acción de Evento de envío de SDK web de plataforma y agregar el `decisionScopes` relevante a la configuración de esa acción
            ![send-evento-action-decisionsScopes](./assets/send-event-action-decisionScopes.png)
      6. [Cree y publique una ](https://docs.adobe.com/content/help/es-ES/launch/using/reference/publish/libraries.html) biblioteca que contenga todas las reglas, elementos de datos y extensiones relevantes que haya configurado


## Solicitudes y respuestas de muestra

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
| `decisionScopes` | Sí | Matriz de cadenas codificadas Base64 de JSON que contiene los ID de actividad y colocación. | Máximo 30 `decisionScopes` por solicitud. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | El alcance de la decisión que dio lugar a las ofertas propuestas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID exclusivo de la actividad de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID única de la ubicación de la oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | ID de la oferta propuesta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | Esquema del contenido asociado a la oferta propuesta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | ID de la oferta propuesta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | Formato del contenido asociado con la oferta propuesta. | `"format": "text/html"` |
| `language` | Una matriz de idiomas asociados con el contenido de la oferta propuesta. | `"language": [ "en-US" ]` |
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
| `decisionScopes` | Sí | Matriz de cadenas codificadas Base64 de JSON que contiene los ID de actividad y colocación. | Máximo 30 `decisionScopes` por solicitud. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | El alcance de la decisión que dio lugar a las ofertas propuestas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID exclusivo de la actividad de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | ID única de la ubicación de la oferta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | ID de la oferta propuesta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | Esquema del contenido asociado a la oferta propuesta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | ID de la oferta propuesta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | Formato del contenido asociado con la oferta propuesta. | `"format": "text/text"` |
| `language` | Una matriz de idiomas asociados con el contenido de la oferta propuesta. | `"language": [ "en-US" ]` |
| `content` | Contenido asociado con la oferta propuesta en formato de cadena. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenido de imagen asociado con la oferta propuesta en formato de URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características asociadas con la oferta propuesta en el formato de un objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |
