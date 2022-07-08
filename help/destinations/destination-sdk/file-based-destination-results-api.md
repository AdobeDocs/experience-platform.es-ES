---
description: En esta página se explica cómo utilizar el extremo de la API /testing/destinationInstance para ver los detalles completos de los resultados de las pruebas. Este extremo de API devuelve el mismo resultado que obtendría al utilizar la API de servicio de flujo para monitorizar los flujos de datos.
title: Ver resultados de activación detallados
source-git-commit: 5b62203113dd55dad8adeb96cbcc2d46b3420c3a
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# Ver resultados de activación detallados {#view-test-results}

## Información general {#overview}

Esta página explica cómo usar la variable `/testing/destinationInstance` Punto final de API para ver los detalles completos de los resultados de las pruebas de destino basadas en archivos.

Si ya ha [probó su destino](file-based-destination-testing-api.md) y ha recibido una respuesta de API válida, su destino funciona correctamente.

Si desea ver información más detallada sobre el flujo de activación, puede usar la variable `results` de la variable [prueba de destino](file-based-destination-testing-api.md) como se describe más abajo.

>[!NOTE]
>
>Este extremo de API devuelve el mismo resultado que obtendría al usar la variable [API del servicio de flujo](../api/update-destination-dataflows.md) para controlar los flujos de datos.

## Primeros pasos {#getting-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Requisitos previos {#prerequisites}

Antes de usar la variable `/testing/destinationInstance` , asegúrese de cumplir las siguientes condiciones:

* Tiene un destino basado en archivos creado mediante el Destination SDK y puede verlo en su [catálogo de destinos](../ui/destinations-workspace.md).
* Ha creado al menos un flujo de activación para el destino en la interfaz de usuario del Experience Platform.
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debería usar en la llamada de API, desde la dirección URL, al examinar una conexión con su destino en la interfaz de usuario de Platform.

   ![Imagen de la interfaz de usuario que muestra cómo obtener el ID de instancia de destino desde la dirección URL.](assets/get-destination-instance-id.png)
* Anteriormente [probó la configuración de destino](file-based-destination-testing-api.md)y ha recibido una respuesta de API válida, que incluye un `results` propiedad. Utilizará esta `results` para probar más el destino.

## Ver los resultados detallados de las pruebas de destino {#test-activation-results}

Una vez que haya [validó la configuración de destino](file-based-destination-testing-api.md), puede ver los resultados de activación detallados realizando una solicitud de GET al `authoring/testing/destinationInstance/` y proporcionando el ID de instancia de destino del destino que está probando y los ID de ejecución de flujo de los segmentos activados.

Puede encontrar la URL completa de la API que necesita usar en la `results` propiedad devuelta en la variable [respuesta de la llamada de prueba de destino](file-based-destination-testing-api.md).

**Formato de API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Parámetros de ruta | Descripción |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | El ID de la instancia de destino para la que está generando perfiles de muestra. Consulte la [requisitos previos](#prerequisites) para obtener más información sobre cómo obtener este ID. |

| Parámetros de cadena de consulta | Descripción |
| -------- | ----------- |
| `flowRunIds` | ID de ejecución de flujo correspondientes a los segmentos activados. Puede encontrar los ID de ejecución de flujo en la `results` propiedad devuelta en la variable [respuesta de la llamada de prueba de destino](file-based-destination-testing-api.md). |

**Solicitud**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta contiene los detalles completos del flujo de activación. Para obtener la misma respuesta, llame a la función [API del servicio de flujo](../api/update-destination-dataflows.md) para controlar los flujos de datos.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## Gestión de errores de API {#api-error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo probar la configuración de destino basada en archivos y ver todos los detalles de los resultados de activación.

Si está creando un destino público, ahora puede [enviar la configuración de destino](../destination-sdk/submit-destination.md) a Adobe para su revisión.
