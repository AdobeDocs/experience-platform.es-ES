---
description: Esta página proporciona toda la información que debe enviar para su revisión a un destino de producto creado mediante Destination SDK.
title: Enviar para revisión un destino productivo creado en Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 50f205a5ddd9ec264d7390911fef45dc595ca6a1
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# Enviar para revisión un destino productivo creado en Destination SDK

## Información general {#overview}

>[!IMPORTANT]
>
>* El proceso documentado aquí solo es necesario para socios que envían destinos productizados (públicos). Si está creando un destino privado para su propio uso, no necesita producir y compartir estos materiales con Adobe.
>
>* El tiempo de respuesta estándar del Adobe para revisar las solicitudes de publicación de destino es de cinco días laborables.
>
>* Si el equipo de Adobe le pide que actualice las configuraciones después del envío inicial, debe enviar otra solicitud de publicación de destino después de realizar las actualizaciones.
>
>* Incluso después de que el destino esté activo en el catálogo de Experience Platform, si necesita realizar actualizaciones en las configuraciones, debe enviar una nueva solicitud de publicación de destino para que las actualizaciones se reflejen en las configuraciones.


Antes de que el destino se pueda publicar en la variable [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md), debe proporcionar al Adobe cierta información sobre el destino y las pruebas que ha realizado para garantizar que los usuarios disfruten de la mejor experiencia posible al activar datos en su plataforma.

Esta página enumera toda la información que debe proporcionar al enviar o actualizar un destino que creó con Adobe Experience Platform Destination SDK. Para enviar correctamente un destino en Adobe Experience Platform, envíe un correo electrónico a <aepdestsdk@adobe.com> que incluye:

* Descripción de los casos de uso que resuelve su destino. Esto no es necesario si está actualizando una configuración de destino existente.
* Pruebe los resultados después de usar el extremo de la API de destino de prueba para realizar una llamada HTTP al destino. Comparta con el Adobe:
   * Se ha realizado una llamada API al extremo de destino.
   * La respuesta de API recibida del extremo de destino.
* Prueba de que ha enviado una solicitud de publicación de destino para su destino utilizando la variable [API de publicación de destino](./destination-publish-api.md).
* Una PR de documentación (solicitud de extracción), siguiendo las instrucciones descritas en la variable [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md).
* Archivo de imagen que se mostrará como logotipo para la tarjeta de destino en el catálogo de destinos del Experience Platform.

Puede encontrar información detallada sobre cada elemento en las secciones siguientes:

## Descripción del caso de uso

Proporcione una descripción de los casos de uso que resuelva su destino para los clientes Experience Platform. Las descripciones pueden ser similares a los casos de uso de socios existentes:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): Cree audiencias a partir de las listas de clientes, las personas que hayan visitado el sitio o las personas que ya hayan interactuado con el contenido en Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): Las API de DataX están disponibles para los anunciantes que deseen dirigirse a un grupo de audiencia específico con claves de direcciones de correo electrónico en Verizon Media (VMG) pueden crear rápidamente un nuevo segmento e insertar el grupo de audiencia deseado con la API casi en tiempo real de VMG.

## Resultados de la prueba después de usar la API de destino de la prueba

Proporcione los resultados de la prueba después de usar la variable [API de destino de prueba](./test-destination.md) para realizar una llamada HTTP a su destino. Esto incluye:

* La solicitud de API completa (encabezados y cuerpo) realizada al extremo de destino mediante la API de prueba.
* La respuesta de API recibida del extremo de destino.

Por ejemplo, su solicitud y respuesta pueden tener un aspecto similar al de los ejemplos siguientes:

**Solicitud**

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

**Respuesta**

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

## Prueba de que ha enviado una solicitud de publicación de destino

Después de probar correctamente el destino, debe usar la variable [API de publicación de destino](./destination-publish-api.md) para enviar el destino al Adobe para su revisión y publicación.

Proporcione el ID de la solicitud de publicación para su destino. Para obtener información sobre cómo recuperar el ID de solicitud de publicación, lea [Enumerar solicitudes de publicación de destino](./destination-publish-api.md#retrieve-list).

## Documentación de destino PR (solicitud de extracción) para integraciones producidas

Si es un proveedor de software independiente (ISV) o un integrador de sistemas (SI) que crea un [integración de productos](./overview.md#productized-custom-integrations), use el [proceso de documentación de autoservicio](./docs-framework/documentation-instructions.md) para crear una página de documentación del producto para el destino. Como parte del proceso de envío, proporcione la solicitud de extracción (PR) para la documentación de destino.

## Logotipo de destino

El catálogo de destinos incluye un logotipo para cada tarjeta de destino. En el correo electrónico de envío, incluya una imagen con el logotipo de para el destino.

Los requisitos de imagen son:
* **Formato**: `SVG`
* **Tamaño**: menos de 2 MB

## Descargar correo electrónico de ejemplo

[Descargar](./assets/sample-email-submit-destination.rtf) un correo electrónico de muestra con toda la información que debe proporcionar al Adobe.
