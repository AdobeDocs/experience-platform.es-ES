---
keywords: Experience Platform;home;popular topics; notifications
description: Con los Eventos de Adobe I/O, puede suscribirse a los eventos y utilizar los enlaces web para recibir notificaciones sobre el estado de las ejecuciones de flujo. Estas notificaciones contienen información sobre el éxito de la ejecución del flujo o los errores que contribuyeron al error de una ejecución.
solution: Experience Platform
title: Notificaciones de ejecución de flujo
topic: overview
translation-type: tm+mt
source-git-commit: c5455dc0812b251483170ac19506d7c60ad4ecaa
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---


# Notificaciones de ejecución de flujo

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras.

[[!DNL Adobe Experience Platform Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de [!DNL Platform]. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Con los Eventos de Adobe I/O, puede suscribirse a eventos y utilizar enlaces web para recibir notificaciones sobre el estado de las ejecuciones de flujo. Estas notificaciones contienen información sobre el éxito de la ejecución del flujo o los errores que contribuyeron al error de una ejecución.

Este documento proporciona pasos para suscribirse a eventos, registrar enlaces web y recibir notificaciones que contengan información sobre el estado de las ejecuciones de flujo.

## Primeros pasos

En este tutorial se asume que ya ha creado al menos una conexión de origen cuyas ejecuciones de flujo desea supervisar. Si todavía no ha configurado una conexión de origen, consulte la información general [de](./home.md) fuentes para configurar el origen de su elección antes de volver a esta guía.

Este documento también requiere una comprensión práctica de los enlaces web y de cómo conectar un enlace web de una aplicación a otra. Consulte la [[!DNL I/O Events] documentación](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para obtener una introducción a los enlaces web.

## Registro de un enlace web para notificaciones de ejecución de flujo

Para recibir notificaciones de ejecución de flujo, debe utilizar la consola de desarrollador de Adobe para registrar un enlace web en la [!DNL Experience Platform] integración.

Siga el tutorial sobre la [suscripción de [!DNL I/O Event] notificaciones](../observability/notifications/subscribe.md) para ver los pasos detallados sobre cómo hacerlo.

>[!IMPORTANT]
>
>Durante el proceso de suscripción, asegúrese de seleccionar las notificaciones **[!UICONTROL de]** plataforma como proveedor de evento y seleccionar las siguientes suscripciones de evento:
>
>* **[!UICONTROL Ejecución de flujo de origen de Experience Platform correcta]**
>* **[!UICONTROL Error en la ejecución del flujo de la fuente de Experience Platform]**


## Recibir notificaciones de ejecución de flujo

Con su webgancho conectado y la suscripción de evento completa, puede inicio recibir notificaciones de flujo a través del panel de weblink.

Una notificación devuelve información como el número de trabajos de inserción ejecutados, el tamaño del archivo y los errores. Una notificación también devuelve una carga útil asociada con la ejecución de flujo en formato JSON. La carga útil de respuesta puede clasificarse como `sources_flow_run_success` o `sources_flow_run_failure`.

>[!IMPORTANT]
>
>Si la ingestión parcial está habilitada durante el proceso de creación de flujo, un flujo que contenga tanto las ingestaciones correctas como las fallidas se marcará como `sources_flow_run_success` solo si el número de errores está por debajo del porcentaje de umbral de error establecido durante el proceso de creación de flujo. Si una ejecución de flujo correcta contiene errores, estos se incluirán como parte de la carga útil de retorno.

### Correcto

Una respuesta correcta devuelve un conjunto de `metrics` que definen las características de una ejecución de flujo específica y `activities` que describen cómo se transforman los datos.

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
    "imsOrgId": "{IMS_ORG}",
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
              "fileInfo": "https://platform-int.adobe.io/data/foundation/export/batches/01E4TSJNM2H5M74J0XB8MFWDHK/meta?path=input_files"
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
        "imsOrgId": "{IMS_ORG}",
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
| `durationSummary` | Define el inicio y la hora de finalización de la ejecución del flujo. |
| `sizeSummary` | Define el volumen de los datos en bytes. |
| `recordSummary` | Define el recuento de registros de los datos. |
| `fileSummary` | Define el recuento de archivos de los datos. |
| `fileInfo` | Dirección URL que permite obtener información general sobre los archivos ingestados correctamente. |
| `statusSummary` | Define si la ejecución del flujo es un éxito o un error. |

### Fallo

La siguiente respuesta es un ejemplo de una ejecución de flujo fallida, con un error al procesar los datos copiados. También pueden producirse errores mientras se copian datos del origen. Una ejecución de flujo fallida incluye información sobre los errores que contribuyeron al error de la ejecución, incluyendo su error y descripción.

```json
[
  {
    "messages": [
      {
        "msgType": "eventNotification",
        "version": "1.0",
        "timestamp": 1597434157622,
        "imsOrgId": "{IMS_ORG}",
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
          "imsOrgId": "{IMS_ORG}",
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
| `fileInfo` | Dirección URL que proporciona información general sobre los archivos que se ingirieron de forma satisfactoria o no. |

>[!NOTE]
>
>Consulte el [apéndice](#errors) para obtener más información sobre los mensajes de error.

## Pasos siguientes

Ahora puede suscribirse a eventos que le permiten recibir notificaciones en tiempo real sobre los estados de ejecución de flujo. Para obtener más información sobre las ejecuciones y fuentes de flujo, consulte la información general [sobre](./home.md)las fuentes.

## Apéndice

Las secciones siguientes proporcionan información adicional para trabajar con notificaciones de ejecución de flujo.

### Explicación de los mensajes de error {#errors}

Los errores de inserción pueden producirse cuando se copian datos del origen o cuando se procesan los datos copiados en [!DNL Platform]. Consulte la tabla siguiente para obtener más información sobre errores específicos.

| Error | Descripción |
| ---------- | ----------- |
| `CONNECTOR-1001-500` | Error al copiar datos de un origen. |
| `CONNECTOR-2001-500` | Error al procesar los datos copiados en [!DNL Platform]. Este error puede deberse a analizar, validar o transformar. |