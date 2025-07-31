---
title: Personalización híbrida mediante Web SDK y API de Edge Network
description: Este artículo muestra cómo se puede utilizar Web SDK junto con la API de Edge Network para implementar la personalización híbrida en las propiedades web.
keywords: personalización; híbrido; api de servidor; lado del servidor; implementación híbrida;
exl-id: 506991e8-701c-49b8-9d9d-265415779876
source-git-commit: 35429ec2dffacb9c0f2c60b608561988ea487606
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 2%

---

# Personalización híbrida mediante Web SDK y API de Edge Network

## Información general {#overview}

La personalización híbrida describe el proceso de recuperar contenido de personalización del lado del servidor, utilizando la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/) y procesándolo del lado del cliente, utilizando [Web SDK](../home.md).

Puede utilizar la personalización híbrida con soluciones de personalización como Adobe Target, Adobe Journey Optimizer o Offer Decisioning, la diferencia es el contenido de la carga útil [!UICONTROL Edge Network API].

## Requisitos previos {#prerequisites}

Antes de implementar la personalización híbrida en las propiedades web, asegúrese de cumplir las siguientes condiciones:

* Ha decidido qué solución de personalización desea utilizar. Esto afectará el contenido de la carga útil [!UICONTROL Edge Network API].
* Tiene acceso a un servidor de aplicaciones que puede usar para hacer las llamadas a la [!UICONTROL API de Edge Network].
* Tiene acceso a la [API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/).
* Ha [configurado](/help/web-sdk/commands/configure/overview.md) correctamente e implementado Web SDK en las páginas que desea personalizar.

## Diagrama de flujo {#flow-diagram}

El diagrama de flujo siguiente describe el orden de los pasos realizados para ofrecer una personalización híbrida.

![Diagrama de flujo visual que muestra el orden de los pasos tomados para ofrecer la personalización híbrida.](assets/hybrid-personalization-diagram.png)

1. Cualquier cookie existente previamente almacenada por el explorador, con el prefijo `kndctr_`, se incluye en la solicitud del explorador.
1. El explorador web cliente solicita la página web desde el servidor de aplicaciones.
1. Cuando el servidor de aplicaciones recibe la solicitud de página, realiza una solicitud `POST` al [extremo interactivo de recopilación de datos de la API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) para recuperar el contenido de personalización. La solicitud `POST` contiene `event` y `query`. Las cookies del paso anterior, si están disponibles, se incluyen en la matriz `meta>state>entries`.
1. La API de Edge Network devuelve el contenido de personalización a su servidor de aplicaciones.
1. El servidor de aplicaciones devuelve una respuesta de HTML al explorador del cliente, que contiene las [cookies de identidad y de clúster](#cookies).
1. En la página del cliente, se llama al comando [!DNL Web SDK] `applyResponse`, pasando los encabezados y el cuerpo de la respuesta de la [!UICONTROL API de Edge Network] del paso anterior.
1. [!DNL Web SDK] procesa automáticamente las ofertas de Target [[!DNL Visual Experience Composer (VEC)]](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=es) y los elementos del canal web de Journey Optimizer porque el indicador `renderDecisions` está establecido en `true`.
1. Las ofertas [!DNL HTML]/[!DNL JSON] basadas en formularios de Target y las experiencias basadas en código de Journey Optimizer se aplican manualmente mediante el método `applyProposition` para actualizar [!DNL DOM] según el contenido de personalización de la propuesta.
1. Para las ofertas [!DNL HTML]/[!DNL JSON] basadas en formularios de Target y las experiencias basadas en código de Journey Optimizer, los eventos de visualización deben enviarse manualmente para indicar cuándo se ha mostrado el contenido devuelto. Esto se realiza mediante el comando `sendEvent`.

## Cookies {#cookies}

Las cookies se utilizan para mantener la identidad del usuario y la información de clúster.  Al utilizar una implementación híbrida, el servidor de aplicaciones web gestiona el almacenamiento y el envío de estas cookies durante el ciclo vital de la solicitud.

| Cookie | Objetivo | Almacenado por | Enviado por |
|---|---|---|---|
| `kndctr_AdobeOrg_identity` | Contiene detalles de identidad del usuario. | Servidor de aplicaciones | Servidor de aplicaciones |
| `kndctr_AdobeOrg_cluster` | Indica qué clúster de Edge Network se debe usar para cumplir las solicitudes. | Servidor de aplicaciones | Servidor de aplicaciones |

## Solicitar ubicación {#request-placement}

Las solicitudes de API de Edge Network son necesarias para obtener propuestas y enviar una notificación de visualización. Al utilizar una implementación híbrida, el servidor de aplicaciones realiza estas solicitudes a la API de Edge Network.

| Solicitud | Realizado por |
|---|---|
| Solicitud de interacción para recuperar propuestas | Servidor de aplicaciones |
| Solicitud de interacción para enviar notificaciones de visualización | Servidor de aplicaciones |


## Establecimiento del host regional de Edge Network {#regional-host}

Para establecer el host regional de Edge Network, lea primero la sugerencia de ubicación de la cookie `kndctr_<orgId>_AdobeOrg_cluster`, que puede tener los siguientes valores:

* `va6`
* `or2`
* `irl1`
* `ind1`
* `sgp3`
* `jpn3`
* `aus3`

Ejemplo: `kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster: va6`

El host regional de Edge Network utiliza el siguiente formato: `<location_hint>.server.adobedc.net` y puede tener los siguientes valores:

* `va6.server.adobedc.net`
* `or2.server.adobedc.net`
* `irl1.server.adobedc.net`
* `ind1.server.adobedc.net`
* `sgp3.server.adobedc.net`
* `jpn3.server.adobedc.net`
* `aus3.server.adobedc.net`

Al utilizar estos hosts específicos, las solicitudes se dirigen a la misma ubicación de Edge Network que el usuario visitó anteriormente y el sistema puede ofrecer la mejor experiencia, ya que los datos de usuario están presentes en la ubicación.

Si no hay ninguna sugerencia de ubicación (es decir, ninguna cookie), use el host predeterminado: `server.adobedc.net`.

>[!TIP]
>
>Se recomienda utilizar una lista de ubicaciones permitidas. Esto evita que la sugerencia de ubicación se manipule, ya que se proporciona mediante cookies del lado del cliente.

## Implicaciones de Analytics {#analytics}

Al implementar la personalización híbrida, debe prestar especial atención para que las visitas a la página no se cuenten varias veces en Analytics.

Al [configurar una secuencia de datos](../../datastreams/overview.md) para Analytics, los eventos se reenvían automáticamente para que se capturen las visitas a la página.

El ejemplo de esta implementación utiliza dos flujos de datos diferentes:

* Un conjunto de datos configurado para Analytics. Este conjunto de datos se utiliza para interacciones de Web SDK.
* Un segundo flujo de datos sin una configuración de Analytics. Este conjunto de datos se utiliza para solicitudes de API de Edge Network. Debe configurar este conjunto de datos con la misma configuración de destino que el conjunto de datos configurado para Analytics.

De este modo, la solicitud del lado del servidor no registra ningún evento de Analytics, pero las solicitudes del lado del cliente sí. Esto hace que las solicitudes de Analytics se cuenten con precisión.

## Generar la solicitud del lado del servidor {#server-side-request}

La solicitud de ejemplo siguiente ilustra una solicitud de API de Edge Network que el servidor de aplicaciones podría utilizar para recuperar el contenido de personalización.

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
         "entries": [{
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_identity",
           "value":"CiY0NzE0NzkwMTUyMzYzMzI4NDAxMjc3NDcwNzA2NTcxMjI3OTI1NVIRCJ_S-uCRMRABGAEqBElSTDHwAZ_S-uCRMQ=="
         }, {
           "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_consent",
           "value": "general=in"
         }, {
            "key": "kndctr_53A16ACB5CC1D3760A495C99_AdobeOrg_cluster",
            "value": "va6"
         }]
      }
   }
}'
```

| Parámetro | Tipo | Requerido | Descripción |
| --- | --- | --- | --- |
| `dataStreamId` | `String` | Sí. | El ID de la secuencia de datos que utiliza para pasar las interacciones a Edge Network. Consulte la [descripción general de flujos de datos](../../datastreams/overview.md) para obtener información sobre cómo configurar un flujo de datos. |
| `requestId` | `String` | No | ID aleatorio para correlacionar solicitudes internas del servidor. Si no se proporciona ninguno, Edge Network generará uno y lo devolverá en la respuesta. |

### Encabezados de proxy {#proxy-headers}

Se requieren los siguientes encabezados para procesar correctamente la solicitud.

* `Referer`
* `X-Forwarded-For`
* `X-Forwarded-Proto`
* `X-Forwarded-Host`

Asegúrese de configurarlas correctamente para que indiquen la información real del cliente. Por ejemplo, el encabezado `X-Forwarded-For` debe contener la dirección IP del cliente para que se realice la geolocalización adecuada.

### Encabezados de agente de usuario {#user-agent-headers}

Utilice los siguientes encabezados de usuario-agente para procesar correctamente la solicitud.

**Predeterminado**

* `User-Agent`

**Baja entropía (obligatoria):**

* `Sec-CH-UA`
* `Sec-CH-UA-Mobile`
* `Sec-CH-UA-Platform`

**Alta entropía (opcional):**

* `Sec-CH-UA-Platform-Version`
* `Sec-CH-UA-Arch`
* `Sec-CH-UA-Model`
* `Sec-CH-UA-Bitness`
* `Sec-CH-UA-WoW64`

La solicitud debe enviarse tal como se muestra en la [especificación de API de Edge Network](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/). Consulte la [documentación de personalización](https://developer.adobe.com/data-collection-apis/docs/getting-started/personalization/) si su caso de uso lo requiere.

### Respuesta del lado del servidor {#server-response}

La respuesta de Edge Network contendrá `state:store` instrucciones, que deben transformarse en `Set-Cookie` encabezados. Se guardan en el explorador y la implementación de Web SDK puede utilizarlos.

Las cookies deben configurarse en el dominio de nivel superior para que se envíen junto con solicitudes a la implementación del servidor y a la del cliente. (O al menos un subdominio común utilizado por ambas implementaciones)

Por ejemplo:

* Las llamadas del lado del servidor utilizan `api.example.com`
* Las llamadas del lado del cliente utilizan `adobe.example.com`

Las cookies deben establecerse en `.example.com` para que se compartan en ambos casos.

La respuesta del lado del servidor está organizada en fragmentos llamados `Handles`, que se generan según la configuración de la secuencia de datos. Por ejemplo, los motores de personalización en tiempo real devuelven identificadores de `personalization:decisions`, mientras que el motor de activación en tiempo real produce identificadores de `activation:pull`.

La respuesta de ejemplo siguiente muestra cómo podría ser la respuesta de la API de Edge Network.

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
