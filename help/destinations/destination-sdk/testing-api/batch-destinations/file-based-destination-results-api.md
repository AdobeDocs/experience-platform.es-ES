---
description: Esta página explica cómo utilizar el extremo de la API /testing/destinationInstance para ver los detalles completos de los resultados de las pruebas. Este extremo de API devuelve el mismo resultado que obtendría al utilizar la API de Flow Service para monitorizar flujos de datos.
title: Ver resultados detallados de la activación
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 2%

---

# Ver resultados detallados de la activación {#view-test-results}

## Información general {#overview}

Esta página explica cómo usar el extremo de API `/testing/destinationInstance` para ver los detalles completos de los resultados de las pruebas de destino basadas en archivos.

Si ya ha [probado su destino](file-based-destination-testing-api.md) y ha recibido una respuesta de API válida, su destino funciona correctamente.

Si desea ver información más detallada sobre el flujo de activación, puede utilizar la propiedad `results` de la respuesta de extremo [prueba de destino](file-based-destination-testing-api.md), tal como se describe más adelante.

>[!NOTE]
>
>Este extremo de API devuelve el mismo resultado que obtendría al usar la [API de servicio de flujo](../../../api/update-destination-dataflows.md) para supervisar flujos de datos.

## Introducción {#getting-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Requisitos previos {#prerequisites}

Antes de usar el extremo `/testing/destinationInstance`, asegúrese de cumplir las siguientes condiciones:

* Ya tiene un destino basado en archivos creado mediante Destination SDK y puede verlo en su [catálogo de destinos](../../../ui/destinations-workspace.md).
* Ha creado al menos un flujo de activación para su destino en la interfaz de usuario de Experience Platform.
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debe utilizar en la llamada de API desde la dirección URL cuando busque una conexión con su destino en la interfaz de usuario de Experience Platform.

  ![Imagen de interfaz de usuario que muestra cómo obtener el identificador de instancia de destino de la dirección URL.](../../assets/testing-api/get-destination-instance-id.png)
* Anteriormente [probó la configuración de destino](file-based-destination-testing-api.md) y recibió una respuesta de API válida, que incluye una propiedad de `results`. Utilizará este valor `results` para probar aún más su destino.

## Ver resultados detallados de las pruebas de destino {#test-activation-results}

Una vez que haya [validado su configuración de destino](file-based-destination-testing-api.md), puede ver los resultados detallados de la activación realizando una petición GET al extremo `authoring/testing/destinationInstance/` y proporcionando el ID de la instancia de destino del destino que está probando, así como los ID de ejecución de flujo de las audiencias activadas.

Puede encontrar la dirección URL de API completa que necesita usar en la propiedad `results` devuelta en la [respuesta de la llamada de prueba de destino](file-based-destination-testing-api.md).

**Formato de API**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Parámetros de ruta | Descripción |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | El ID de la instancia de destino para la que está generando perfiles de muestra. Consulte la sección [requisitos previos](#prerequisites) para obtener más información sobre cómo obtener este ID. |

| Parámetros de cadena de consulta | Descripción |
| -------- | ----------- |
| `flowRunIds` | Los ID de ejecución de flujo correspondientes a las audiencias activadas. Puede encontrar los ID de ejecución de flujo en la propiedad `results` devuelta en la [respuesta de la llamada de prueba de destino](file-based-destination-testing-api.md). |

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

La respuesta contiene los detalles completos del flujo de activación. Puede obtener la misma respuesta llamando a la [API de Flow Service](../../../api/update-destination-dataflows.md) para supervisar los flujos de datos.

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

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo probar la configuración de destino basada en archivos y ver los detalles completos de los resultados de activación.

Si estás creando un destino público, ahora puedes [enviar tu configuración de destino](../../guides/submit-destination.md) a Adobe para que la revisen.
