---
description: Como parte del SDK de destino, Adobe proporciona herramientas para desarrolladores que le ayudan a configurar y probar el destino. Esta página describe cómo probar la configuración de destino.
title: Probar la configuración de destino
exl-id: 21e4d647-1168-4cb4-a2f8-22d201e39bba
source-git-commit: 3d7151645bc90a2dcbd6b31251ed459029ab77c9
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# Probar la configuración de destino {#developer-tools}

## Información general {#overview}

Como parte del SDK de destino, Adobe proporciona herramientas para desarrolladores que le ayudan a configurar y probar el destino. Esta página describe cómo probar la configuración de destino. Para obtener información sobre cómo crear una plantilla de transformación de mensaje, lea [Crear y probar una plantilla de transformación de mensaje](./create-template.md).

Para **probar si el destino está configurado correctamente y para verificar la integridad de los flujos de datos en su destino configurado**, utilice la *Herramienta de prueba de destino*. Con esta herramienta, puede probar la configuración de destino enviando mensajes al extremo de la API de REST.

A continuación se ilustra cómo la prueba de destino encaja en el [flujo de trabajo de configuración de destino](./configure-destination-instructions.md) en el SDK de destino:

![Gráfico de dónde encaja el paso de prueba de destino en el flujo de trabajo de configuración de destino](./assets/test-destination-step.png)

## Herramienta de prueba de destino {#destination-testing-tool}

Utilice esta herramienta para probar la configuración de destino enviando mensajes al extremo del socio que proporcionó en la [configuración del servidor](./server-and-template-configuration.md).

Con esta herramienta, después de haber configurado el destino, puede:
* Pruebe si el destino está configurado correctamente;
* Compruebe la integridad de los flujos de datos al destino configurado.

### Utilización {#how-to-use}

>[!NOTE]
>
>Para obtener toda la documentación de referencia de la API, lea [Destination testing API operations](./destination-testing-api.md).

Puede realizar llamadas al extremo de la API de prueba de destino con o sin añadir perfiles en la solicitud.

Si no agrega ningún perfil en la solicitud, Adobe los generará internamente y los agregará a la solicitud. Si desea generar perfiles para utilizarlos en esta solicitud, consulte la [Referencia de la API de generación de perfiles de muestra](./sample-profile-generation-api.md). Debe generar perfiles en función del esquema XDM de origen, como se muestra en la [referencia de API](./sample-profile-generation-api.md#generate-sample-profiles-source-schema). Tenga en cuenta que el esquema de origen es el [esquema de unión](https://experienceleague.adobe.com/docs/experience-platform/profile/union-schemas/union-schema.html?lang=en) del entorno limitado que está utilizando.

La respuesta contiene el resultado del procesamiento de la solicitud de destino. La solicitud incluye tres secciones principales:
* La solicitud generada por el Adobe para el destino.
* La respuesta recibida de su destino.
* La lista de perfiles enviados en la solicitud, independientemente de si los perfiles fueron [agregados por usted en la solicitud](./destination-testing-api.md/#test-with-added-profiles) o generados por el Adobe si [el cuerpo de la solicitud de prueba de destino estaba vacío](./destination-testing-api.md#test-without-adding-profiles).

>[!NOTE]
>
>Adobe puede generar varios pares de solicitud y respuesta. Por ejemplo, si envía 10 perfiles a un destino que tiene un valor `maxUsersPerRequest` de 7, habrá una solicitud con 7 perfiles y otra solicitud con 3 perfiles.

**Solicitud de ejemplo con parámetro de perfiles en el cuerpo**

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
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

**Solicitud de ejemplo sin parámetro de perfiles en el cuerpo**


```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/3e0ac39c-ef14-4101-9fd9-cf0909814510' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--data-raw ''
```

**Respuesta de ejemplo**

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

Para obtener descripciones de los parámetros de solicitud y respuesta, consulte [Destination testing API operations](./destination-testing-api.md).

## Pasos siguientes

Después de probar el destino y confirmar que está configurado correctamente, utilice la [API de publicación de destino](./destination-publish-api.md) para enviar la configuración a Adobe para su revisión.
