---
description: Esta página proporciona toda la información necesaria para enviar a revisión un destino de productos creado con Destination SDK.
title: Enviar para revisión un destino de productos creado en Destination SDK
exl-id: eef0d858-ebd9-426e-91a1-5c93903b0eb5
source-git-commit: 2c778f98815af87453e84f24ba8bf077774349a1
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 0%

---

# Enviar para revisión un destino de productos creado en Destination SDK

## Información general {#overview}

>[!IMPORTANT]
>
>* El proceso documentado aquí solo es necesario para los socios que envían destinos productizados (públicos). Si está creando un destino privado para su propio uso, no necesita producir y compartir estos materiales con el Adobe.
>
>* El tiempo de respuesta estándar de los Adobes para revisar las solicitudes de publicación de destino es de cinco días hábiles.
>
>* Si el equipo de Adobe le pide que realice actualizaciones en las configuraciones después del envío inicial, debe enviar otra solicitud de publicación de destino después de realizar las actualizaciones.
>
>* Incluso después de que el destino esté activo en el catálogo del Experience Platform, si necesita realizar alguna actualización en las configuraciones, debe enviar una nueva solicitud de publicación de destino para que las actualizaciones se reflejen en las configuraciones.
>
>* El cronograma de revisión y los artefactos requeridos son los mismos para los destinos nuevos y los destinos existentes que está actualizando.

Antes de publicar el destino en [catálogo de destinos de Experience Platform](/help/destinations/catalog/overview.md), debe proporcionar al Adobe determinada información sobre el destino y las pruebas que ha realizado para garantizar que los usuarios disfruten de la mejor experiencia posible al activar datos en su plataforma.

En esta página se muestra toda la información que debe proporcionar al enviar o actualizar un destino creado con Adobe Experience Platform Destination SDK. Para enviar correctamente un destino en Adobe Experience Platform, envíe un correo electrónico a <aepdestsdk@adobe.com> que incluye:

* Una descripción de los casos de uso que resuelve su destino. Esto solo es necesario si envía una nueva configuración de destino.
* Una descripción del motivo del envío de destino. Esto solo es necesario si está actualizando una configuración de destino existente.
* Resultados de la prueba después de usar el punto final de la API de destino de prueba para realizar una llamada HTTP a su destino. Comparta con el Adobe una llamada de API realizada al extremo de destino y la respuesta de API recibida desde el extremo de destino.
* Requisitos adicionales para destinos basados en archivos:
   * Comparta una solicitud y un ejemplo de respuesta después de usar la API de prueba para lo siguiente [prueba del destino basado en archivos con perfiles de muestra](../testing-api/batch-destinations/file-based-destination-testing-api.md).
   * Adjunte un archivo de muestra generado por el destino y exportado a la ubicación de almacenamiento.
   * Envíe algún tipo de prueba de que ha ingerido correctamente el archivo exportado desde la ubicación de almacenamiento en el sistema.
* Prueba de que ha enviado una solicitud de publicación de destino para su destino utilizando [API de publicación de destino](../publishing-api/create-publishing-request.md).
* Una PR de documentación (solicitud de extracción), siguiendo las instrucciones descritas en la [proceso de documentación de autoservicio](../docs-framework/documentation-instructions.md).
* Un archivo de imagen que se mostrará como un logotipo para la tarjeta de destino en el catálogo de destinos de Experience Platform.

Puede encontrar información detallada sobre cada elemento en las secciones siguientes:

## Descripción del caso de uso {#use-case-description}

Proporcione una descripción de los casos de uso que el destino resuelve para los clientes de Experience Platform. Las descripciones pueden ser similares a los casos de uso de los socios existentes:

* [Pinterest](/help/destinations/catalog/advertising/pinterest.md): cree audiencias a partir de las listas de clientes, personas que hayan visitado el sitio o personas que ya hayan interactuado con el contenido en Pinterest.
* [Yahoo Data X](/help/destinations/catalog/advertising/datax.md#use-cases): Las API de DataX están disponibles para anunciantes que desean dirigirse a un grupo de audiencia específico que no tiene clave de dirección de correo electrónico en Verizon Media (VMG) y pueden crear rápidamente una nueva audiencia y enviar el grupo de audiencia deseado mediante la API de VMG en tiempo casi real.

## Motivo de la actualización {#reason-for-update}

>[!NOTE]
>
>Esta sección solo es necesaria cuando actualiza una configuración existente.

Proporcione una breve descripción del problema que su envío resuelve para el destino existente. Por ejemplo, el envío puede actualizar el nombre, la descripción y el logotipo del destino a medida que pasa de la versión beta a la disponibilidad general. O bien, el envío podría corregir un error descubierto en la configuración de destino.

## Resultados de la prueba después de usar la API de destino de prueba {#testing-api-response}

Proporcione los resultados de la prueba después de usar el [probar API de destino](../testing-api/streaming-destinations/streaming-destination-testing-overview.md) extremo para realizar una llamada HTTP a su destino. Esto incluye lo siguiente:

* La solicitud de API completa (encabezados y cuerpo) realizada al extremo de destino mediante la API de prueba.
* La respuesta de API recibida desde su extremo de destino.

Por ejemplo, su solicitud y respuesta pueden ser similares a los ejemplos siguientes:

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

## Requisitos adicionales para destinos basados en archivos {#additional-file-based-destination-requirements}

Para los destinos basados en archivos, debe proporcionar una prueba adicional de que ha configurado correctamente el destino. Asegúrese de incluir los siguientes elementos:

### Prueba de respuesta de API {#testing-api-response-file-based}

Incluya una solicitud y un ejemplo de respuesta después de usar la API de prueba para [prueba del destino basado en archivos con perfiles de muestra](../testing-api/batch-destinations/file-based-destination-testing-api.md).

### Adjuntar archivo exportado {#attach-exported-file}

En su [correo electrónico de envío](#download-sample-email), adjunte un archivo CSV que el destino configurado haya exportado a su ubicación de almacenamiento.

### Prueba de ingesta correcta {#proof-of-successful-ingestion}

Por último, debe proporcionar algún tipo de prueba de que los datos se han introducido correctamente en el sistema después de exportarlos a la ubicación de almacenamiento proporcionada. Proporcione cualquiera de los siguientes elementos:

* Capturas de pantalla o un breve vídeo de captura de pantalla en el que toma el archivo manualmente desde la ubicación de almacenamiento e lo introduce en el sistema.
* Capturas de pantalla o un breve vídeo de captura de pantalla en el que la interfaz de usuario del sistema confirma que el nombre de archivo generado por el Experience Platform se ha introducido correctamente en el sistema.
* Las líneas de registro del sistema que contienen Adobes pueden correlacionarse con el nombre del archivo o con los datos generados a partir del Experience Platform.

## Prueba de que ha enviado una solicitud de publicación de destino {#destination-publishing-request-proof}

Después de probar correctamente el destino, debe usar el complemento [API de publicación de destino](../publishing-api/create-publishing-request.md) para enviar el destino al Adobe para su revisión y publicación.

Proporcione el ID de la solicitud de publicación de su destino. Para obtener información sobre cómo recuperar el ID de solicitud de publicación, lea cómo [recuperar solicitudes de publicación de destino](../publishing-api/retrieve-publishing-request.md).

## Documentación de destino PR (solicitud de extracción) para integraciones producidas {#documentation-pr}

Si es un proveedor de software independiente (ISV) o integrador de sistemas (SI) que crea un [integración de productos](../overview.md#productized-custom-integrations), debe utilizar el [proceso de documentación de autoservicio](../docs-framework/documentation-instructions.md) para crear una página de documentación del producto para el destino. Como parte del proceso de envío, proporcione la solicitud de extracción (PR) para la documentación de destino.

## Logotipo para su destino {#logo}

El catálogo de destinos incluye un logotipo para cada tarjeta de destino. En el correo electrónico de envío, incluya una imagen con el logotipo de su destino.

Los requisitos de imagen son:
* **Formato**: `SVG`
* **Tamaño**: menos de 2 MB

## Descargar correo electrónico de muestra {#download-sample-email}

[Descargar](../assets/guides/sample-email-submit-destination.rtf) un correo electrónico de ejemplo con toda la información que necesita proporcionar al Adobe.
