---
title: Personalización híbrida mediante SDK web y API de servidor de Edge Network
description: Este artículo muestra cómo se puede utilizar el SDK web junto con la API de servidor para implementar la personalización híbrida en las propiedades web.
keywords: personalización; híbrido; api de servidor; lado del servidor; implementación híbrida;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 9489b5345c2b13b9d05b26d646aa7f1576840fb8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 3%

---

# Personalización híbrida mediante SDK web y API de servidor de Edge Network

## Información general {#overview}

La personalización híbrida describe el proceso de recuperar contenido personalizado del lado del servidor, mediante la [API de Edge Network Server](../../server-api/overview.md) y procesarlo del lado del cliente, mediante [SDK web](../home.md).

Puede utilizar la personalización híbrida con soluciones de personalización como Adobe Target, Adobe Journey Optimizer o Offer Decisioning, la diferencia es el contenido de la carga útil de [!UICONTROL Server API].

## Requisitos previos {#prerequisites}

Antes de implementar la personalización híbrida en las propiedades web, asegúrese de cumplir las siguientes condiciones:

* Ha decidido qué solución de personalización desea utilizar. Esto afectará el contenido de la carga útil [!UICONTROL API de servidor].
* Tiene acceso a un servidor de aplicaciones que puede usar para realizar las llamadas a la API de [!UICONTROL servidor].
* Tiene acceso a la [API de Edge Network Server](../../server-api/authentication.md).
* Ha [configurado](/help/web-sdk/commands/configure/overview.md) correctamente e implementado el SDK web en las páginas que desea personalizar.

## Diagrama de flujo {#flow-diagram}

El diagrama de flujo siguiente describe el orden de los pasos realizados para ofrecer una personalización híbrida.

![Diagrama de flujo visual que muestra el orden de los pasos tomados para ofrecer la personalización híbrida.](assets/hybrid-personalization-diagram.png)

1. Cualquier cookie existente previamente almacenada por el explorador, con el prefijo `kndctr_`, se incluye en la solicitud del explorador.
1. El explorador web cliente solicita la página web desde el servidor de aplicaciones.
1. Cuando el servidor de aplicaciones recibe la solicitud de página, realiza una solicitud `POST` al extremo [de recopilación de datos interactivos de la API del servidor](../../server-api/interactive-data-collection.md) para recuperar el contenido de personalización. La solicitud `POST` contiene `event` y `query`. Las cookies del paso anterior, si están disponibles, se incluyen en la matriz `meta>state>entries`.
1. La API del servidor devuelve el contenido de personalización al servidor de aplicaciones.
1. El servidor de aplicaciones devuelve una respuesta del HTML al explorador del cliente, que contiene [cookies de identidad y de clúster](#cookies).
1. En la página cliente, se llama al comando [!DNL Web SDK] `applyResponse`, pasando los encabezados y el cuerpo de la respuesta de la [!UICONTROL API de servidor] del paso anterior.
1. [!DNL Web SDK] procesa automáticamente las ofertas de Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) y los elementos del canal web de Journey Optimizer porque el indicador `renderDecisions` está establecido en `true`.
1. Las ofertas [!DNL HTML]/[!DNL JSON] basadas en formularios de Target y las experiencias basadas en código de Journey Optimizer se aplican manualmente mediante el método `applyProposition` para actualizar [!DNL DOM] según el contenido de personalización de la propuesta.
1. Para las ofertas [!DNL HTML]/[!DNL JSON] basadas en formularios de Target y las experiencias basadas en código de Journey Optimizer, los eventos de visualización deben enviarse manualmente para indicar cuándo se ha mostrado el contenido devuelto. Esto se realiza mediante el comando `sendEvent`.

## Cookies {#cookies}

Las cookies se utilizan para mantener la identidad del usuario y la información de clúster.  Al utilizar una implementación híbrida, el servidor de aplicaciones web gestiona el almacenamiento y el envío de estas cookies durante el ciclo vital de la solicitud.

| Cookie | Objetivo | Almacenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contiene detalles de identidad del usuario. | Servidor de aplicaciones | Servidor de aplicaciones |
| `kndctr_AdobeOrg_cluster` | Indica qué clúster de Edge Network se debe usar para cumplir las solicitudes. | Servidor de aplicaciones | Servidor de aplicaciones |

## Solicitar ubicación {#request-placement}

Las solicitudes de API del servidor son necesarias para obtener propuestas y enviar una notificación de visualización. Al utilizar una implementación híbrida, el servidor de aplicaciones realiza estas solicitudes a la API del servidor.

| Solicitud | Realizado por |
|---|---|
| Solicitud de interacción para recuperar propuestas | Servidor de aplicaciones |
| Solicitud de interacción para enviar notificaciones de visualización | Servidor de aplicaciones |

## Implicaciones de Analytics {#analytics}

Al implementar la personalización híbrida, debe prestar especial atención para que las visitas a la página no se cuenten varias veces en Analytics.

Al [configurar una secuencia de datos](../../datastreams/overview.md) para Analytics, los eventos se reenvían automáticamente para que se capturen las visitas a la página.

El ejemplo de esta implementación utiliza dos flujos de datos diferentes:

* Un conjunto de datos configurado para Analytics. Este conjunto de datos se utiliza para interacciones del SDK web.
* Un segundo flujo de datos sin una configuración de Analytics. Este conjunto de datos se utiliza para solicitudes de API de servidor. Debe configurar este conjunto de datos con la misma configuración de destino que el conjunto de datos configurado para Analytics.

De este modo, la solicitud del lado del servidor no registra ningún evento de Analytics, pero las solicitudes del lado del cliente sí. Esto hace que las solicitudes de Analytics se cuenten con precisión.


## Solicitud del lado del servidor {#server-side-request}

La solicitud de ejemplo siguiente ilustra una solicitud de API de servidor que el servidor de aplicaciones podría utilizar para recuperar el contenido de personalización.

>[!IMPORTANT]
>
>Esta solicitud de ejemplo utiliza Adobe Target como solución de personalización. La solicitud puede variar según la solución de personalización que haya elegido.


**Formato de API**

```http
POST /ee/v2/interact
```

### Solicitud {#request}

```shell
curl -X POST "https://edge.adobedc.net/ee/v2/interact?dataStreamId={DATASTREAM_ID}" 
-H "Content-Type: text/plain" 
-d '{
   "event":{
      "xdm":{
         "web":{
            "webPageDetails":{
               "URL":"http://localhost/"
            },
            "webReferrer":{
               "URL":""
            }
         },
         "identityMap":{
            "FPID":[
               {
                  "id":"xyz",
                  "authenticatedState":"ambiguous",
                  "primary":true
               }
            ]
         },
         "timestamp":"2022-06-23T22:21:00.878Z"
      },
      "data":{
         
      }
   },
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      },
      "personalization":{
         "schemas":[
            "https://ns.adobe.com/personalization/default-content-item",
            "https://ns.adobe.com/personalization/html-content-item",
            "https://ns.adobe.com/personalization/json-content-item",
            "https://ns.adobe.com/personalization/redirect-item",
            "https://ns.adobe.com/personalization/dom-action"
         ],
         "decisionScopes":[
            "__view__",
            "sample-json-offer"
         ]
      }
   },
   "meta":{
      "state":{
         "domain":"localhost",
         "cookiesEnabled":true,
         "entries":[
            {
               "key":"kndctr_XXX_AdobeOrg_identity",
               "value":"abc123"
            },
            {
               "key":"kndctr_XXX_AdobeOrg_cluster",
               "value":"or2"
            }
         ]
      }
   }
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sí. | El ID de la secuencia de datos que utiliza para pasar las interacciones al Edge Network. Consulte la [descripción general de flujos de datos](../../datastreams/overview.md) para obtener información sobre cómo configurar un flujo de datos. |
| `requestId` | `String` | No | ID aleatorio para correlacionar solicitudes internas del servidor. Si no se proporciona ninguno, el Edge Network genera uno y lo devuelve en la respuesta. |

### Respuesta del lado del servidor {#server-response}

La respuesta de ejemplo siguiente muestra el aspecto que podría tener la respuesta de la API del servidor.


```json
{
   "requestId":"5c539bd0-33bf-43b6-a054-2924ac58038b",
   "handle":[
      {
         "payload":[
            {
               "id":"XXX",
               "namespace":{
                  "code":"ECID"
               }
            }
         ],
         "type":"identity:result"
      },
      {
         "payload":[
            {
               "..."
            },
            {
               "..."
            }
         ],
         "type":"personalization:decisions",
         "eventIndex":0
      }
   ]
}
```

## Solicitud del lado del cliente {#client-request}

En la página del cliente, se llama al comando [!DNL Web SDK] `applyResponse`, pasando los encabezados y el cuerpo de la respuesta del lado del servidor.

```js
   alloy("applyResponse", {
      "renderDecisions": true,
      "responseHeaders": {
         "cache-control": "no-cache, no-store, max-age=0, no-transform, private",
         "connection": "close",
         "content-encoding": "deflate",
         "content-type": "application/json;charset=utf-8",
         "date": "Mon, 11 Jul 2022 19:42:01 GMT",
         "server": "jag",
         "strict-transport-security": "max-age=31536000; includeSubDomains",
         "transfer-encoding": "chunked",
         "vary": "Origin",
         "x-adobe-edge": "OR2;9",
         "x-content-type-options": "nosniff",
         "x-konductor": "22.6.78-BLACKOUTSERVERDOMAINS:7fa23f82",
         "x-rate-limit-remaining": "599",
         "x-request-id": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "x-xss-protection": "1; mode=block"
      },
      "responseBody": {
         "requestId": "5c539bd0-33bf-43b6-a054-2924ac58038b",
         "handle": [
         {
            "payload": [
               {
               "id": "XXX",
               "namespace": {
                  "code": "ECID"
               }
               }
            ],
            "type": "identity:result"
         },
         {
            "payload": [
               {...}, 
               {...}
            ],
            "type": "personalization:decisions",
            "eventIndex": 0
         }
         ]
      }
   }
   ).then(applyPersonalization("sample-json-offer"));
```

Las ofertas [!DNL JSON] basadas en formularios se aplican manualmente mediante el método `applyPersonalization` para actualizar [!DNL DOM] según la oferta de personalización. Para las actividades basadas en formularios, los eventos de visualización deben enviarse manualmente para indicar cuándo se ha mostrado la oferta. Esto se realiza mediante el comando `sendEvent`.

```js
function sendDisplayEvent(decision) {
    const { id, scope, scopeDetails = {} } = decision;

    alloy("sendEvent", {
        "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
                "decisioning": {
                    "propositions": [{
                        "id": id,
                        "scope": scope,
                        "scopeDetails": scopeDetails
                    }],
                    "propositionEventType": {
                        "display": 1
                    }
                }
            }
        }
    });
}
```

## Aplicación de ejemplo {#sample-app}

Para ayudarle a experimentar y obtener más información sobre este tipo de personalización, le proporcionamos una aplicación de muestra que puede descargar y utilizar para realizar pruebas. Puede descargar la aplicación, junto con instrucciones detalladas sobre cómo utilizarla, desde este [repositorio de GitHub](https://github.com/adobe/alloy-samples).
