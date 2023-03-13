---
title: Uso del Offer decisioning con el SDK web de Platform
description: El SDK web de Adobe Experience Platform puede entregar y procesar ofertas personalizadas administradas en Offer Decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario o la API de Offer decisioning.
keywords: offer decisioning;toma de decisiones;SDK web;SDK web de Platform;ofertas personalizadas;entregar ofertas;entrega de ofertas;personalización de ofertas;
exl-id: 4ab51f9d-3c44-4855-b900-aa2cde673a9a
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 5%

---

# Uso del Offer decisioning con el SDK web de Platform

>[!NOTE]
>
>El uso del Offer decisioning en el SDK web de Adobe Experience Platform está disponible en el acceso anticipado para usuarios seleccionados. Esta funcionalidad no está disponible para todas las organizaciones IMS.

Adobe Experience Platform [!DNL Web SDK] puede entregar y procesar ofertas personalizadas que se administran en Offer decisioning. Puede crear sus ofertas y otros objetos relacionados mediante la interfaz de usuario (IU) o las API de Offer decisioning.

## Requisitos previos

* La organización IMS está habilitada para la toma de decisiones perimetrales
* Ofertas, Actividades creadas
* Flujo de datos publicado

## Terminología

Es importante comprender la siguiente terminología al trabajar con Offer decisioning. Para obtener más información y ver términos adicionales, visite la [glosario de offer decisioning](https://experienceleague.adobe.com/docs/offer-decisioning/using/get-started/glossary.html).

* **Contenedor:** Un contenedor es un mecanismo de aislamiento para mantener separadas las diferentes preocupaciones. El ID de contenedor es el primer elemento de ruta para todas las API del repositorio. Todos los objetos de toma de decisiones residen en un contenedor.

* **Ámbitos de decisión:** Para el Offer decisioning, los ámbitos de decisión son las cadenas codificadas en Base64 de JSON que contienen los ID de actividad y ubicación que desea que el servicio de offer decisioning utilice para proponer ofertas.

   *Ámbito de decisión JSON:*

   ```json
   {
     "activityId":"xcore:offer-activity:11cfb1fa93381aca",
     "placementId":"xcore:offer-placement:1175009612b0100c"
   }
   ```

   *Cadena codificada en Base64 del ámbito de decisión:*

   ```json
   "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="
   ```

   >[!TIP]
   >
   >Puede copiar el valor del ámbito de decisión desde el **Resumen de actividad** en la interfaz de usuario.

   ![](assets/decision-scope-copy.png)

* **Flujos de datos:** Para obtener más información, lea la [flujos de datos](../../datastreams/overview.md) documentación.

* **Identidad**: Para obtener más información, lea esta documentación que describe cómo [El SDK web de Platform utiliza el servicio de identidad](../../identity/overview.md).

## Habilitando Offer decisioning

Para habilitar el Offer decisioning, realice los siguientes pasos:

1. Se ha habilitado Adobe Experience Platform en su [secuencia de datos](../../datastreams/overview.md) y marque la casilla &quot;Offer decisioning&quot;

   ![offer-decisioning-edge-config](./assets/offer-decisioning-edge-config.png)

1. Siga las instrucciones de [instalar el SDK](../../fundamentals/installing-the-sdk.md) (El SDK se puede instalar de forma independiente o mediante la interfaz de usuario de. Consulte la [guía de inicio rápido de etiquetas](../../../tags/quick-start/quick-start.md)) para obtener más información.
1. [Configuración del SDK](../../fundamentals/configuring-the-sdk.md) para el Offer decisioning. A continuación se proporcionan pasos adicionales específicos del Offer decisioning.

   * Instalación del SDK independiente

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
   * Instalación del SDK mediante etiquetas

      1. [Creación de una propiedad de etiqueta](../../../tags/ui/administration/companies-and-properties.md)
      1. [Añadir el código de incrustación de ](https://experienceleague.adobe.com/docs/core-services-learn/implementing-in-websites-with-launch/configure-launch/launch-add-embed.html)
      1. Instale y configure la extensión del SDK web de Platform con la secuencia de datos que ha creado seleccionando la configuración en la lista desplegable &quot;Secuencia de datos&quot;. Consulte la documentación sobre [extensiones](../../../tags/ui/managing-resources/extensions/overview.md).

         ![install-aep-web-sdk-extension](./assets/install-aep-web-sdk-extension.png)

         ![configure-aep-web-sdk-extension](./assets/configure-aep-web-sdk-extension.png)

      1. Cree los necesarios [Elementos de datos](../../../tags/ui/managing-resources/data-elements.md). Como mínimo, debe crear un mapa de identidad del SDK web de Platform y un elemento de datos del objeto XDM de SDK web de Platform.

         ![identity-map-data-element](./assets/identity-map-data-element.png)

         ![xdm-object-data-element](./assets/xdm-object-data-element.png)

      1. Cree su [Reglas](../../../tags/ui/managing-resources/rules.md).

         * Añada una acción Enviar evento del SDK web de Platform y agregue la acción correspondiente `decisionScopes` a la configuración de esa acción

            ![send-event-action-decisionScopes](./assets/send-event-action-decisionScopes.png)
      1. [Crear y publicar una biblioteca](../../../tags/ui/publishing/libraries.md) que contenga todas las reglas, elementos de datos y extensiones relevantes que haya configurado



## Solicitudes y respuestas de ejemplo

### Uno `decisionScopes` valor

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
| `identityMap` | Sí | Consulte esta sección [Documentación del servicio de identidad](../../identity/overview.md). | Una identidad por solicitud. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Nota: Los usuarios no necesitan incluir la variable `ECID` en la llamada de API. Este parámetro se agrega automáticamente a la llamada de si es necesario. |
| `decisionScopes` | Sí | Matriz de cadenas JSON codificadas en Base64 que contiene los ID de actividad y ubicación. | Máximo 30 `decisionScopes` por solicitud. | `"decisionScopes": ["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="]` |

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
| `scope` | Ámbito de decisión que dio lugar a las ofertas propuestas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID único de la actividad de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381aca"` |
| `placement.id` | ID único de la ubicación de la oferta. | `"id": "xcore:offer-placement:1175009612b0100c"` |
| `items.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `schema` | El esquema del contenido asociado con la oferta propuesta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-html"` |
| `data.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:124cc332095cfa74"` |
| `format` | El formato del contenido asociado con la oferta propuesta. | `"format": "text/html"` |
| `language` | Una matriz de idiomas asociados con el contenido de la oferta propuesta. | `"language": [ "en-US" ]` |
| `content` | Contenido asociado con la oferta propuesta en formato de cadena. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenido de imagen asociado con la oferta propuesta en formato de dirección URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características asociadas con la oferta propuesta en formato de objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

### Múltiple `decisionScopes` values

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
| `identityMap` | Sí | Consulte esta sección [Documentación del servicio de identidad](../../identity/overview.md). | Una identidad por solicitud. | `{ "identityMap": { "ECID": [ { "id": "91133425615229052182584359620783097099" } ] } }`. <br><br> Nota: Los usuarios no necesitan incluir la variable `ECID` en la llamada de API. Este parámetro se agrega automáticamente a la llamada de si es necesario. |
| `decisionScopes` | Sí | Matriz de cadenas JSON codificadas en Base64 que contiene los ID de actividad y ubicación. | Máximo 30 `decisionScopes` por solicitud. | `"decisionScopes":["eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ==", "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTIyMjA4YjNhODc0MDU1OCIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjEyMjIwNDUyOTUxNGEyYzAifQ=="` |

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
| `scope` | Ámbito de decisión que dio lugar a las ofertas propuestas. | `"scope": "eyJhY3Rpdml0eUlkIjoieGNvcmU6b2ZmZXItYWN0aXZpdHk6MTFjZmIxZmE5MzM4MWFjYSIsInBsYWNlbWVudElkIjoieGNvcmU6b2ZmZXItcGxhY2VtZW50OjExNzUwMDk2MTJiMDEwMGMifQ=="` |
| `activity.id` | ID único de la actividad de oferta. | `"id": "xcore:offer-activity:11cfb1fa93381123"` |
| `placement.id` | ID único de la ubicación de la oferta. | `"xcore:offer-placement:1175009612b01123"` |
| `items.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `schema` | El esquema del contenido asociado con la oferta propuesta. | `"schema": "https://ns.adobe.com/experience/offer-management/content-component-text"` |
| `data.id` | El ID de la oferta propuesta. | `"id": "xcore:personalized-offer:11e36d4a22954123"` |
| `format` | El formato del contenido asociado con la oferta propuesta. | `"format": "text/text"` |
| `language` | Una matriz de idiomas asociados con el contenido de la oferta propuesta. | `"language": [ "en-US" ]` |
| `content` | Contenido asociado con la oferta propuesta en formato de cadena. | `"content": "<p style="color:red;">20% Off on shipping</p>"` |
| `deliveryUrl` | Contenido de imagen asociado con la oferta propuesta en formato de dirección URL. | `"deliveryURL": "https://image.jpeg"` |
| `characteristics` | Características asociadas con la oferta propuesta en formato de objeto JSON. | `"characteristics": { "foo": "bar", "foo1": "bar1" }` |

## Limitaciones

Actualmente, algunas restricciones de oferta no son compatibles con los flujos de trabajo de Experience Edge móviles, por ejemplo, Límite. El valor del campo Límite especifica el número de veces que se puede presentar una oferta entre todos los usuarios. Para obtener más información, consulte [Documentación de restricciones y reglas de idoneidad de ofertas](https://experienceleague.adobe.com/docs/offer-decisioning/using/managing-offers-in-the-offer-library/creating-personalized-offers.html#eligibility).
