---
title: Identificación de visitante mediante FPID
description: Aprenda a identificar visitantes de forma consistente a través de la API de Edge Network mediante el FPID
seo-description: Learn how to consistently identify visitors via the Edge Network API, by using the FPID
keywords: red perimetral;puerta de enlace;api;visitante;identificación;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Identificación de visitante mediante FPID

[!DNL First-party IDs] (`FPIDs`) son identificadores de dispositivo generados, administrados y almacenados por clientes. Esto proporciona a los clientes control sobre la identificación de dispositivos de usuario. Al enviar `FPIDs`, Edge Network no genera un `ECID` completamente nuevo para una solicitud que no contiene ninguno.

`FPID` se puede incluir en el cuerpo de solicitud de API como parte de `identityMap` o se puede enviar como una cookie.

Edge Network puede traducir de forma determinista un(a) `FPID` a un(a) `ECID`, por lo que las identidades de `FPID` son totalmente compatibles con las soluciones de Experience Cloud. La obtención de un(a) `ECID` de un(a) `FPID` específico(a) siempre genera el mismo resultado, por lo que los usuarios tendrán una experiencia coherente.

Los `ECID` obtenidos de esta manera se pueden recuperar mediante una consulta `identity.fetch`:

```json
{
   "query":{
      "identity":{
         "fetch":[
            "ECID"
         ]
      }
   }
}
```

Para las solicitudes que contienen tanto un `FPID` como un `ECID`, el `ECID` ya presente en la solicitud tendrá prioridad sobre el que se podría generar a partir del `FPID`. En otras palabras, Edge Network usa el `ECID` ya proporcionado y se omite el `FPID`. Un nuevo(a) `ECID` solo se genera cuando se proporciona un(a) `FPID` por sí solo.

En cuanto a los ID de dispositivo, los flujos de datos de `server` deben usar `FPID` como ID de dispositivo. También se pueden proporcionar otras identidades (es decir, `EMAIL`) dentro del cuerpo de la solicitud, pero Edge Network requiere que se proporcione explícitamente una identidad principal. La identidad principal es la identidad base en la que se almacenan los datos de perfil.

>[!NOTE]
>
>Las solicitudes que no tengan identidad, ni identidad principal establecida explícitamente en el cuerpo de la solicitud, fallarán.

El siguiente grupo de campos `identityMap` está correctamente formado para una solicitud de secuencia de datos `server`:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous",
            "primary":true
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

El siguiente grupo de campos `identityMap` generará una respuesta de error cuando se establezca en una solicitud de secuencia de datos `server`:

```json
{
   "identityMap":{
      "FPID":[
         {
            "id":"123e4567-e89b-12d3-a456-426614174000",
            "authenticatedState":"ambiguous"
         }
      ],
      "EMAIL":[
         {
            "id":"email@mail.com",
            "authenticatedState":"authenticated"
         }
      ]
   }
}
```

La respuesta de error devuelta por Edge Network en este caso es similar a la siguiente:

```json
{
   "type":"https://ns.adobe.com/aep/errors/EXEG-0306-400",
   "status":400,
   "title":"No primary identity set in request (event)",
   "detail":"No primary identity found in the input event. Update the request accordingly to your schema and try again.",
   "report":{
      "requestId":"{REQUEST_ID}",
      "configId":"{CONFIG_ID}",
      "orgId":"{ORG_ID}"
   }
}
```

## Identificación de visitante con `FPID`

Para identificar a los usuarios a través de `FPID`, asegúrese de que la cookie `FPID` se haya enviado antes de realizar cualquier solicitud a Edge Network. `FPID` se puede pasar en una cookie o como parte de `identityMap` en el cuerpo de la solicitud.

<!--

## Request with `FPID` passed as cookie header

```shell
curl -X POST 'https://edge.adobedc.net/v2/interact?dataStreamId={Data Stream ID}' \
-H 'cookie: FPID=e98f38e6-6183-442d-8cd2-0e384f4c8aa8' \
-H 'Content-Type: application/json' \
-d '{
    "event": 
        {
            "xdm": {
                "web": {
                    "webPageDetails": {
                        "URL": "https://alloystore.dev"
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
                        "viewportWidth": 1907,
                        "viewportHeight": 545
                    }
                },
                "placeContext": {
                    "localTime": "2022-03-21T21:32:59.991-06:00",
                    "localTimezoneOffset": 360
                },
                "timestamp": "2022-03-22T03:32:59.992Z",
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "1.0",
                    "environment": "serverapi"
                }
            }
        },
    "query": {
        "identity": {
            "fetch": [
                "ECID"
            ]
        }
    },
    "meta":
        {
            "state":
            {
                "domain": "alloystore.dev",
                "cookiesEnabled": true
            }
        }
}'
```
-->

## La solicitud con `FPID` se pasó como campo `identityMap`

El ejemplo siguiente pasa [!DNL FPID] como un parámetro `identityMap`.

```shell
curl -X POST "https://server.adobedc.net/v2/interact?dataStreamId={DATASTREAM_ID}"
-H "Authorization: Bearer {TOKEN}"
-H "x-gw-ims-org-id: {ORG_ID}"
-H "x-api-key: {API_KEY}"
-H "Content-Type: application/json"
-d '{
   "event": {
      "xdm": {
         "identityMap": {
            "FPID": [
               {
                  "id": "e98f38e6-6183-442d-8cd2-0e384f4c8aa8",
                  "authenticatedState": "ambiguous",
                  "primary": true
               }
            ]
         },
         "web": {
            "webPageDetails": {
               "URL": "https://alloystore.dev"
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
               "viewportWidth": 1907,
               "viewportHeight": 545
            }
         },
         "placeContext": {
            "localTime": "2022-03-21T21:32:59.991-06:00",
            "localTimezoneOffset": 360
         },
         "timestamp": "2022-03-22T03:32:59.992Z",
         "implementationDetails": {
            "name": "https://ns.adobe.com/experience/alloy/reactor",
            "version": "1.0",
            "environment": "serverapi"
         }
      }
   },
   "query": {
      "identity": {
         "fetch": [
            "ECID"
         ]
      }
   }
}'
```
