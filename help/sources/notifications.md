---
keywords: Experience Platform;inicio;temas populares; notificaciones
description: Al suscribirse a Adobe I/O Events, puede utilizar los webhooks para recibir notificaciones sobre los estados de ejecución de flujo de sus conexiones de origen. Estas notificaciones contienen información sobre el éxito de la ejecución de flujo o los errores que contribuyeron al error de una ejecución.
solution: Experience Platform
title: Notificaciones de ejecución de flujo
exl-id: 0f1cde97-3030-4b8e-be08-21f64e78b794
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---

# Notificaciones de ejecución de flujo

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

La [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/) se usa para recopilar y centralizar datos de clientes de distintos orígenes en [!DNL Experience Platform]. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes de datos admitidas.

Con Adobe I/O Events, puede suscribirse a eventos y utilizar webhooks para recibir notificaciones sobre el estado de las ejecuciones del flujo. Estas notificaciones contienen información sobre el éxito de la ejecución de flujo o los errores que contribuyeron al error de una ejecución.

Este documento proporciona pasos sobre cómo suscribirse a eventos, registrar webhooks y recibir notificaciones que contengan información sobre el estado de las ejecuciones del flujo.

## Introducción

En este tutorial se da por hecho que ya ha creado al menos una conexión de origen cuyo flujo de trabajo se ejecuta y que desea supervisar. Si aún no ha configurado una conexión de origen, comience por visitar la [descripción general de orígenes](./home.md) para configurar el origen que elija antes de volver a esta guía.

Este documento también requiere una comprensión práctica de los webhooks y cómo conectar un webhook de una aplicación a otra. Consulte la [[!DNL I/O Events] documentación](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para ver una introducción a los webhooks.

## Registrar un webhook para notificaciones de ejecución de flujo

Para recibir notificaciones de ejecución de flujo, debe usar Adobe Developer Console para registrar un webhook en su integración con [!DNL Experience Platform].

Siga el tutorial de [suscripción a las notificaciones de [!DNL I/O Event]](../observability/alerts/subscribe.md) para ver los pasos detallados sobre cómo hacerlo.

>[!IMPORTANT]
>
>Durante el proceso de suscripción, asegúrate de seleccionar **[!UICONTROL Notificaciones de plataforma]** como proveedor de eventos y selecciona las siguientes suscripciones a eventos:
>
>* **[!UICONTROL Ejecución correcta del flujo de Experience Platform Source]**
>* **[!UICONTROL Error al ejecutar flujo en Experience Platform Source]**

## Recibir notificaciones de ejecución de flujo

Con el webhook conectado y la suscripción al evento completada, puede empezar a recibir notificaciones de ejecución de flujo a través del panel del webhook.

Una notificación devuelve información como el número de trabajos de ingesta ejecutados, el tamaño del archivo y los errores. Una notificación también devuelve una carga útil asociada con la ejecución del flujo en formato JSON. La carga de respuesta puede clasificarse como `sources_flow_run_success` o `sources_flow_run_failure`.

>[!IMPORTANT]
>
>Si la ingesta parcial está habilitada durante el proceso de creación de flujo, un flujo que contenga ingestas correctas y fallidas se marcará como `sources_flow_run_success` solo si el número de errores está por debajo del porcentaje de umbral de error establecido durante el proceso de creación de flujo. Si una ejecución de flujo correcta contiene errores, estos se incluirán como parte de la carga útil de retorno.

### Correcto

Una respuesta correcta devuelve un conjunto de `metrics` que define las características de una ejecución de flujo específica y `activities` que describe cómo se transforman los datos.

```json
{
  "event_id": "aec55616-1715-487f-8044-ba648cc8ffee",
  "event": {
    "createdAt": 1597213529158,
    "updatedAt": 1597213530760,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "7127a4f0-def8-11e9-83ce-e79494b1c2a5",
    "sandboxName": "prod",
    "imsOrgId": "{ORG_ID}",
    "id": "933cf9f4-cf01-4d75-bcf9-f4cf010d750a",
    "flowId": "1c6f1047-dcaf-48fe-af10-47dcaf08feaf",
    "providerRefId": "test1234",
    "etag": "\"5100ec97-0000-0200-0000-5f338b5b0000\"",
    "metrics": {
      "durationSummary": {
        "startedAtUTC": 1590512053,
        "completedAtUTC": 1590512053
      },
      "sizeSummary": {
        "inputBytes": 2048,
        "outputBytes": 1024
      },
      "recordSummary": {
        "inputRecordCount": 100,
        "outputRecordCount": 70
      },
      "fileSummary": {
        "inputFileCount": 10,
        "outputFileCount": 10
      },
      "statusSummary": {
        "status": "success"
      }
    },
    "activities": [
      {
        "id": "copyActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "startedAtUTC": 1590512053,
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 2048,
          "outputBytes": 1098
        },
        "recordSummary": {
          "inputRecordCount": 100,
          "outputRecordCount": 100
        },
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "adf/pipeline/id": "abcd",
            "adf/run/id": "1234"
          }
        },
        "sourceInfo": [
          {
            "id": "sourceConnectionId1",
            "type": "SourceConnection",
            "reference": {
              "type": "AdfRunId"
            }
          }
        ]
      },
      {
        "id": "promotionActivity",
        "updatedAtUTC": 87473822,
        "durationSummary": {
          "completedAtUTC": 1590512053
        },
        "sizeSummary": {
          "inputBytes": 1098,
          "outputBytes": 1024
        },
        "recordSummary": {},
        "fileSummary": {
          "inputFileCount": 10,
          "outputFileCount": 10,
          "extensions": {
            "manifest": {
              "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
            }
          }
        },
        "statusSummary": {
          "status": "success",
          "extensions": {
            "batchId": "b1",
            "acp_request_id": "1234"
          }
        },
        "targetInfo": [
          {
            "id": "targetConnectionId1",
            "type": "TargetConnection",
            "reference": {
              "type": "batch"
            }
          }
        ]
      }
    ],
    "slaCreatedAt": 1597213531124,
    "processStartTime": 1597213531213,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "platform_notifications",
        "eventCode": "sources_flow_run_success"
      }
    },
    "transformedTime": 1597213531214
  }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `metrics` | Define las características de los datos en la ejecución de flujo. |
| `activities` | Define los diferentes pasos y actividades que se realizan para transformar los datos. |
| `durationSummary` | Define la hora de inicio y finalización de la ejecución del flujo. |
| `sizeSummary` | Define el volumen de los datos en bytes. |
| `recordSummary` | Define el recuento de registros de los datos. |
| `fileSummary` | Define el recuento de archivos de los datos. |
| `fileInfo` | Una URL que lleva a una descripción general de los archivos ingeridos correctamente. |
| `statusSummary` | Define si la ejecución del flujo es un éxito o un error. |

### Error

La siguiente respuesta es un ejemplo de una ejecución de flujo fallida, con un error que se produce cuando se procesan los datos copiados. También pueden producirse errores mientras se copian los datos desde el origen. Una ejecución de flujo fallida incluye información sobre los errores que contribuyeron al fallo de la ejecución, incluido su error y descripción.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{ORG_ID}",
        "schema": {
          "name": "run-notification",
          "version": "1.0"
        },
        "provider": "FlowService",
        "_eventNotificationMeta": {
          "category": "Platform Notifications",
          "type": "sources_flow_run_failed"
        },
        "value": {
          "createdAt": 1597434147259,
          "updatedAt": 1597434157567,
          "createdBy": "{CREATED_BY}",
          "updatedBy": "{UPDATED_BY}",
          "createdClient": "{CREATED_CLIENT}",
          "updatedClient": "{UPDATED_CLIENT}",
          "sandboxId": "e49ebb00-d0fa-11e9-b164-ed6a398c8b35",
          "sandboxName": "prod",
          "imsOrgId": "{ORG_ID}",
          "id": "d9024c32-2174-4271-824c-322174627101",
          "flowId": "cf4fce79-8822-456d-8fce-798822556dc6",
          "etag": "\"0c003dbf-0000-0200-0000-5f36e92d0000\"",
          "metrics": {
            "durationSummary": {
              "startedAtUTC": 1597434147190
            },
            "sizeSummary": {
              "inputBytes": -1
            },
            "fileSummary": {
              "inputFileCount": -1
            },
            "statusSummary": {
              "status": "failed",
              "errors": [
                {
                  "code": "CONNECTOR-2001-500",
                  "message": "Error in processing (parsing, validation or transformation) the copied data."
                }
              ]
            }
          },
          "activities": [
            {
              "id": "promotionActivity",
              "updatedAtUTC": 1597434157529,
              "durationSummary": {
                "startedAtUTC": 1597434147190,
                "completedAtUTC": 1597434157212
              },
              "sizeSummary": {
                "inputBytes": -1
              },
              "recordSummary": {},
              "fileSummary": {
                "inputFileCount": -1,
                "extensions": {
                  "manifest": {
                    "fileInfo": "https://platform-stage.adobe.io/data/foundation/export/batches/6f6a900f-e40d-4f0e-9bb9-b614436c3465/meta?path=input_files"
                  }
                }
              },
              "statusSummary": {
                "status": "failed",
                "errors": [
                  {
                    "code": "CONNECTOR-2001-500",
                    "message": "Error in processing (parsing, validation or transformation) the copied data."
                  }
                ],
                "extensions": {
                  "errors": [
                    {
                      "code": "133",
                      "message": "We are unable to locate any files uploaded for this batch. Please upload files to ingest."
                    }
                  ]
                }
              },
              "targetInfo": [
                {
                  "id": "e88737aa-27b8-4795-8737-aa27b8f7959e",
                  "type": "TargetConnection",
                  "reference": {
                    "type": "Batch",
                    "ids": [
                      "6f6a900f-e40d-4f0e-9bb9-b614436c3465"
                    ]
                  }
                }
              ]
            }
          ]
        }
      }
    ]
  }
]
```

| Propiedad | Descripción |
| ---------- | ----------- |
| `fileInfo` | Una dirección URL que proporciona una descripción general de los archivos que se han ingerido correctamente y no correctamente. |

>[!NOTE]
>
>Consulte el [apéndice](#errors) para obtener más información sobre los mensajes de error.

## Pasos siguientes

Ahora puede suscribirse a eventos que le permiten recibir notificaciones en tiempo real sobre los estados de ejecución de flujo. Para obtener más información sobre las ejecuciones de flujo y los orígenes, vea la [descripción general de orígenes](./home.md).

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con notificaciones de ejecución de flujo.

### Explicación de los mensajes de error {#errors}

Pueden producirse errores de ingesta cuando los datos se copian del origen o cuando los datos copiados se procesan en [!DNL Experience Platform]. Consulte la tabla siguiente para obtener más información sobre errores específicos.

| Error | Descripción |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Error al copiar los datos desde un origen. |
| `CONNECTOR-2001-500` | Error al procesar los datos copiados en [!DNL Experience Platform]. Este error puede estar relacionado con el análisis, la validación o la transformación. |
