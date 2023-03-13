---
title: Interactuar con Adobe Analytics
description: Aprenda a utilizar la API del servidor de red perimetral para interactuar con Adobe Analytics.
exl-id: b5e7a4d0-9aea-4e70-a7d6-b9aad09aaddf
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# Interactuar con Adobe Analytics

## Información general {#overview}

La recopilación de datos de Adobe Analytics funciona traduciendo datos XDM a un formato que Adobe Analytics puede comprender. Varios campos XDM son [asignado automáticamente](../edge/data-collection/adobe-analytics/automatically-mapped-vars.md) a variables de Analytics.

También puede [asignar valores XDM manualmente](../edge/data-collection/adobe-analytics/manually-mapping-variables.md) a variables de Analytics heredadas.

Para permitir que Adobe Analytics reciba datos de la API del servidor, debe [configuración de la secuencia de datos](../edge/datastreams/overview.md#adobe-analytics-settings) para reenviar eventos a Adobe Analytics, introduzca el ID del grupo de informes en la página de configuración del conjunto de datos.

![Configuración de flujo de datos Adobe Analytics](assets/analytics-datastream.png)

## Interactuar con Adobe Analytics {#interacting-analytics}

### Formato de API {#format}

```http
POST /ee/v2/interact?dataStreamId={DATASTREAM_ID}
```

### Solicitud {#request}

El ejemplo siguiente incluye varios valores asignados automáticamente del `_experience.analytics` grupo de campos. También incluye capas de datos basadas en JSON. Aunque estas capas de datos no se pueden asignar automáticamente, es posible utilizar [Preparación de datos para la recopilación de datos](../edge/datastreams/data-prep.md) para asignar estos valores a un esquema que contenga los grupos de campos a los que se hace referencia anteriormente.

Todos los valores que los usuarios asignen a esos campos se asignarán automáticamente a los valores de Analytics adecuados, como si se incluyeran en la solicitud de API.

```shell
curl -X POST "https://server.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" \
-H "Authorization: Bearer {TOKEN}" 
-H "x-gw-ims-org-id: {ORG_ID}" 
-H "x-api-key: {API_KEY}" 
-H "Content-Type: application/json" \
-d '{
   "event": {
      "xdm": {
         "eventType": "web.webpagedetails.pageViews",
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev",
               "name": "Home Page"
            },
            "webReferrer": {
               "URL": ""
            }
         },
         "device": {
            "screenHeight": 1440,
            "screenWidth": 3440,
            "screenOrientation": "landscape"
         },
         "environment": {
            "type": "browser",
            "browserDetails": {
               "viewportWidth": 3440,
               "viewportHeight": 1440
            }
         },
         "placeContext": {
            "localTime": "2022-03-22T22:45:21.193-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-23T04:45:21.193Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "2.8.0+2.9.0",
            "environment": "browser"
         },
         "_experience": {
            "analytics": {
               "customDimensions": {
                  "eVars": {
                     "eVar14": "eVar14"
                  }
               },
               "event1to100": {
                  "event13": {
                     "value": 1
                  },
                  "event14": {
                     "value": 2
                  }
               }
            }
         }
      }
   },
   "data": {
      "page": {
         "pageInfo": {
            "pageName": "Promotions",
            "siteSection": "Home"
         },
         "promos": {
            "heroPromos": "purse,shoes,sunglasses"
         },
         "customVariables": {
            "testGroup": "orange/black theme"
         },
         "events": {
            "homePage": true
         },
         "products": [
            {
               "productSKU": "abc123",
               "productName": "shirt"
            }
         ]
      }
   }
}'
```

### Respuesta {#response}

```json
{
   "requestId": "d2ad6364-5675-4a86-ba41-50e7a4c4a299",
   "handle": []
}
```
