---
description: Aprenda a utilizar la API de prueba de destino para probar la configuración de destino de flujo continuo antes de publicarla.
title: Resumen de API de prueba de destino de streaming
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Resumen de API de prueba de destino de streaming

Como parte de Destination SDK, Adobe proporciona herramientas para desarrolladores que le ayudarán a configurar y probar su destino. Esta página describe cómo probar la configuración de destino. Para obtener información sobre cómo crear una plantilla de transformación de mensajes, lea [Crear y probar una plantilla de transformación de mensajes](../../testing-api/streaming-destinations/create-template.md).

Para **comprobar si el destino está configurado correctamente y comprobar la integridad de los flujos de datos al destino configurado**, use la *herramienta de prueba de destino*. Con esta herramienta, puede probar la configuración de destino enviando mensajes al punto final de la API de REST.

A continuación se ilustra cómo encaja probar el destino en el [flujo de trabajo de configuración de destino](../../guides/configure-destination-instructions.md) en Destination SDK:

![Gráfico de dónde encaja el paso de prueba de destino en el flujo de trabajo de configuración de destino](../../assets/testing-api/test-destination-step.png)

## Herramienta de prueba de destino: propósito y requisitos previos {#destination-testing-tool}

Utilice la herramienta de prueba de destino para probar la configuración de destino enviando mensajes al extremo del socio que ha proporcionado en la [configuración del servidor](../../authoring-api/destination-server/create-destination-server.md).

Antes de usar la herramienta, asegúrese de lo siguiente:

* Configure su destino siguiendo los pasos descritos en [flujo de trabajo de configuración de destino](../../authoring-api/destination-configuration/create-destination-configuration.md) y
* Establezca una conexión con su destino, tal como se detalla en [Cómo obtener el identificador de instancia de destino](../../testing-api/streaming-destinations/destination-testing-api.md#get-destination-instance-id).

Con esta herramienta, después de haber configurado el destino, puede:

* Comprobar si el destino está configurado correctamente;
* Compruebe la integridad de los flujos de datos al destino configurado.

### Cómo usar {#how-to-use}

>[!NOTE]
>
>Para obtener la documentación de referencia completa de la API, lea [Operaciones de API de prueba de destino](../../testing-api/streaming-destinations/destination-testing-api.md).

Puede realizar llamadas al extremo de la API de prueba de destino con o sin agregar perfiles en la solicitud.

Si no agrega ningún perfil a la solicitud, Adobe los generará internamente para usted y los agregará a la solicitud. Si desea generar perfiles para usarlos en esta solicitud, consulte la [Referencia de API de generación de perfiles de muestra](../../testing-api/streaming-destinations/sample-profile-generation-api.md). Debe generar perfiles basados en el esquema XDM de origen, como se muestra en la [referencia de API](../../testing-api/streaming-destinations/sample-profile-generation-api.md#generate-sample-profiles-source-schema). Tenga en cuenta que el esquema de origen es el [esquema de unión](../../../../profile/ui/union-schema.md) de la zona protegida que está utilizando.

La respuesta contiene el resultado del procesamiento de la solicitud de destino. La solicitud incluye tres secciones principales:

* La solicitud generada por Adobe para el destino.
* La respuesta recibida desde su destino.
* La lista de perfiles enviados en la solicitud, ya sean [agregados por usted en la solicitud](../../testing-api/streaming-destinations/destination-testing-api.md#test-with-added-profiles) o generados por Adobe si [el cuerpo de la solicitud de prueba de destino estaba vacío](../../testing-api/streaming-destinations/destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe puede generar varios pares de solicitud y respuesta. Por ejemplo, si envía 10 perfiles a un destino que tiene un valor `maxUsersPerRequest` de 7, habrá una solicitud con 7 perfiles y otra solicitud con 3 perfiles.

**Solicitud de muestra con parámetro de perfiles en el cuerpo**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw '{
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "374a9a6c-c719-4cdb-a660-155a2838e6d6":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248585Z",
                  "status":"realized"
               },
               "896f8776-9498-47b4-b994-51cb3f61c2c5":{
                  "lastQualificationTime":"2021-05-13T12:16:27.248605Z",
                  "status":"realized"
               }
            }
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "attributes":{
            "key":{
               "value":"string"
            }
         }
      }
   ]
}'
```

**Solicitud de muestra sin parámetro de perfiles en el cuerpo**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Respuesta de muestra**

Tenga en cuenta que el contenido del parámetro `results.httpCalls` es específico de la API de REST.

```json
{
   "results":[
      {
         "aggregationKey":{
            "destinationInstanceId":"string",
            "segmentId":"string",
            "segmentStatus":"realized",
            "identityNamespaces":[
               [
                  "email",
                  "phone"
               ]
            ]
         },
         "httpCalls":[
            {
               "traceId":"a06fec2d-a886-4219-8975-4e4b7ed26539",
               "request":{
                  "body":"{ \"attributes\": [  { \"external_id\": \"external_id-h29Fq\"  , \"AdobeExperiencePlatformSegments\": { \"add\": [  \"Nirvana fans\" ,  \"RHCP fans\"   ], \"remove\": [  ] }  ,  \"key\":  \"string\"    }  ] }",
                  "headers":[
                     {
                        "Content-Type":"application/json"
                     }
                  ],
                  "method":"POST",
                  "uri":"https://api.moviestar.com/users/track"
               },
               "response":{
                  "body":"{\"status\": \"success\"}",
                  "code":"200",
                  "headers":[
                     {
                        "Connection":"keep-alive"
                     },
                     {
                        "Content-Type":"application/json"
                     },
                     {
                        "Server":"nginx"
                     },
                     {
                        "Vary":"Origin,Accept-Encoding"
                     },
                     {
                        "transfer-encoding":"chunked"
                     }
                  ]
               }
            }
         ]
      }
   ],
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "03fb9938-8537-4b4c-87f9-9c4d413a0ee5":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872039Z",
                  "status":"realized"
               },
               "27e05542-d6a3-46c7-9c8e-d59d50229530":{
                  "lastQualificationTime":"2021-06-17T12:25:12.872042Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "Email":[
               {
                  "id":"Email-iIyJc"
               }
            ],
            "IDFA":[
               {
                  "id":"IDFA-viPAW"
               }
            ],
            "GAID":[
               {
                  "id":"GAID-Bc6LE"
               }
            ],
            "Email_LC_SHA256":[
               {
                  "id":"Email_LC_SHA256-gEOdj"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string"
            }
         }
      }
   ]
}
```

Para obtener descripciones de los parámetros de solicitud y respuesta, consulte [Operaciones de API de prueba de destino](../../testing-api/streaming-destinations/destination-testing-api.md).

## Próximos pasos

Después de probar el destino y confirmar que está configurado correctamente, use la [API de publicación de destino](../../publishing-api/create-publishing-request.md) para enviar la configuración a Adobe para que la revise.
