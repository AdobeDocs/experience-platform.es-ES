---
title: Identificación de visitantes mediante FPID
description: Aprenda a identificar de forma consistente a los visitantes a través de la API del servidor, utilizando FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: red perimetral;puerta de enlace;api;visitante;identificación;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Identificación de visitantes mediante FPID

[!DNL First-party IDs] (`FPIDs`) son ID de dispositivo generados, administrados y almacenados por los clientes. Esto proporciona a los clientes control sobre la identificación de dispositivos de usuario. Enviando `FPIDs`, la red perimetral no genera una red completamente nueva `ECID` para una solicitud que no contenga una.

La variable `FPID` se puede incluir en el cuerpo de la solicitud de API como parte del `identityMap` o se puede enviar como una cookie.

Un `FPID` se puede traducir determinísticamente en un `ECID` por la red perimetral, así que `FPID` las identidades son totalmente compatibles con las soluciones de Experience Cloud. Obtención de un `ECID` de un `FPID` siempre arroja el mismo resultado, por lo que los usuarios tendrán una experiencia coherente.

La variable `ECID` obtenido de esta forma se puede recuperar mediante un `identity.fetch` consulta:

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

Para solicitudes que contienen un `FPID` y `ECID`, el `ECID` ya presente en la solicitud tendrá prioridad sobre el que se podría generar a partir de la variable `FPID`. En otras palabras, la red perimetral utiliza la variable `ECID` ya se han proporcionado y `FPID` se ignora. Un nuevo `ECID` solo se genera cuando `FPID` se proporciona por su cuenta.

En términos de ID de dispositivo, la variable `server` los conjuntos de datos deben utilizar `FPID` como ID de dispositivo. Otras identidades (p. ej. `EMAIL`) también se puede proporcionar dentro del cuerpo de la solicitud, pero la red perimetral requiere que se proporcione explícitamente una identidad principal. La identidad principal es la identidad base en la que se almacenan los datos de perfil.

>[!NOTE]
>
>Las solicitudes que no tengan identidad, respectivamente, ni identidad principal establecida explícitamente dentro del cuerpo de la solicitud, fallarán.

Lo siguiente `identityMap` el grupo de campos está formado correctamente para un `server` solicitud de flujo de datos:

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

Lo siguiente `identityMap` grupo de campos dará como resultado una respuesta de error cuando se establezca en un `server` solicitud de flujo de datos:

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

La respuesta de error devuelta por la red perimetral en este caso es similar a la siguiente:

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

Para identificar a los usuarios mediante `FPID`, asegúrese de que `FPID` se ha enviado antes de realizar cualquier solicitud a la red perimetral. La variable `FPID` se puede pasar en una cookie o como parte del `identityMap` en el cuerpo de la solicitud.

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

## Solicitar con `FPID` pasó como `identityMap` field

El ejemplo siguiente pasa el [!DNL FPID] como `identityMap` parámetro.

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
