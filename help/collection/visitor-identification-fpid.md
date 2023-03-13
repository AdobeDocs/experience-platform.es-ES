---
title: Identificación de visitante mediante FPID
description: Aprenda a identificar visitantes de forma coherente mediante la API de servidor mediante el FPID
seo-description: Learn how to consistently identify visitors via the Server API, by using the FPID
keywords: red perimetral;puerta de enlace;api;visitante;identificación;fpid
exl-id: c61d2e7c-7b5e-4b14-bd52-13dde34e32e3
source-git-commit: 1ab1c269fd43368e059a76f96b3eb3ac4e7b8388
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Identificación de visitante mediante FPID

[!DNL First-party IDs] (`FPIDs`) son ID de dispositivo generados, administrados y almacenados por los clientes. Esto proporciona a los clientes control sobre la identificación de dispositivos de usuario. Mediante envío `FPIDs`, la red perimetral no genera una nueva `ECID` para una solicitud que no contiene uno.

El `FPID` se puede incluir en el cuerpo de la solicitud de API como parte de `identityMap` o se puede enviar como una cookie.

Un `FPID` puede traducirse de forma determinista en un `ECID` por Edge Network, por lo que `FPID` Las identidades son totalmente compatibles con las soluciones de Experience Cloud. Obtención de un `ECID` de un específico `FPID` siempre produce el mismo resultado, por lo que los usuarios tendrán una experiencia coherente.

El `ECID` obtenido de esta forma se puede recuperar mediante una `identity.fetch` consulta:

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

Para solicitudes que contienen un `FPID` y un `ECID`, el `ECID` ya presente en la solicitud tendrá prioridad sobre la que se podría generar a partir de `FPID`. En otras palabras, la red perimetral utiliza el `ECID` ya se ha proporcionado y el `FPID` se ignora. Un nuevo `ECID` solo se genera cuando un `FPID` se proporciona por sí solo.

En términos de ID de dispositivo, la variable `server` las secuencias de datos deben utilizar `FPID` como ID de dispositivo. Otras identidades (por ejemplo, `EMAIL`) también se puede proporcionar dentro del cuerpo de la solicitud, pero la red perimetral requiere que se proporcione explícitamente una identidad principal. La identidad principal es la identidad base en la que se almacenan los datos de perfil.

>[!NOTE]
>
>Las solicitudes que no tengan identidad, ni identidad principal establecida explícitamente en el cuerpo de la solicitud, fallarán.

Lo siguiente `identityMap` el grupo de campos está correctamente formado para una `server` solicitud de secuencia de datos:

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

Lo siguiente `identityMap` grupo de campos generará una respuesta de error cuando se configure en una `server` solicitud de secuencia de datos:

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

## Identificación del visitante con `FPID`

Para identificar a los usuarios mediante `FPID`, asegúrese de que las variables `FPID` se ha enviado antes de realizar cualquier solicitud a la red perimetral. El `FPID` se puede pasar en una cookie o como parte de `identityMap` en el cuerpo de la solicitud.

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

## Solicitud con `FPID` pasado como `identityMap` campo

El ejemplo siguiente pasa el [!DNL FPID] como un `identityMap` parámetro.

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
