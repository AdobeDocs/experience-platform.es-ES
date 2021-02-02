---
keywords: Experience Platform;inicio;temas populares;controlar flujos de datos;API de servicio de flujo;Servicio de flujo
solution: Experience Platform
title: Monitorear flujos y ejecuciones
topic: overview
type: Tutorial
description: En este tutorial se explican los pasos para supervisar los datos de ejecución del flujo para comprobar si están completos, los errores y las métricas que utilizan la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 1%

---


# Monitorear flujos de datos mediante la API de servicio de flujo

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante servicios [!DNL Platform]. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamientos basados en la nube, bases de datos y muchas otras. Además, el Experience Platform permite activar datos en socios externos.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todos los orígenes y destinos admitidos.

En este tutorial se explican los pasos para monitorear los datos de ejecución del flujo para conocer la integridad, los errores y las métricas que utilizan la [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Este tutorial requiere que tenga el valor de ID de un flujo de datos válido. Si no tiene un ID de flujo de datos válido, seleccione el conector que desee en la [información general de orígenes](../../sources/home.md) o [información general de destinos](../../destinations/catalog/overview.md) y siga los pasos descritos antes de intentar este tutorial.

Este tutorial también requiere que tenga conocimientos prácticos sobre los siguientes componentes de Adobe Experience Platform:

- [Destinos](../../destinations/home.md): Los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación sin fisuras de datos de la Plataforma para campañas de marketing en canal cruzado, campañas por correo electrónico, publicidad de destino y muchos otros casos de uso.
- [Fuentes](../../sources/home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
- [Simuladores](../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para poder monitorear correctamente las ejecuciones de flujo mediante la API [!DNL Flow Service].

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

- `Content-Type: application/json`

## Monitoreo de las ejecuciones de flujo

Una vez que haya realizado un flujo de datos, realice una solicitud de GET a la API [!DNL Flow Service].

**Formato API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El valor único `id` del flujo de datos que desea monitorear. |

**Solicitud**

La siguiente solicitud recupera las especificaciones de un flujo de datos existente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve detalles sobre la ejecución del flujo, incluida información sobre la fecha de creación, las conexiones de origen y destinatario, así como el identificador único de la ejecución del flujo (`id`).

```json
{
    "items": [
        {
            "id": "65b7cfcc-6b2e-47c8-8194-13005b792752",
            "createdAt": 1607520228894,
            "updatedAt": 1607520276948,
            "createdBy": "{CREATED_BY}",
            "updatedBy": "{UPDATED_BY}",
            "createdClient": "{CREATED_CLIENT}",
            "updatedClient": "{UPDATED_CLIENT}",
            "sandboxId": "{SANDBOX_ID}",
            "sandboxName": "prod",
            "imsOrgId": "{IMS_ORG_ID}",
            "flowId": "f00c8762-df2f-432b-a7d7-38999fef5e8e",
            "etag": "\"560266dc-0000-0200-0000-5fd0d0140000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1607520205922,
                    "completedAtUTC": 1607520262413
                },
                "sizeSummary": {
                    "inputBytes": 87885,
                    "outputBytes": 56730
                },
                "recordSummary": {
                    "inputRecordCount": 26758,
                    "outputRecordCount": 26758,
                    "failedRecordCount": 0
                },
                "fileSummary": {
                    "inputFileCount": 11,
                    "outputFileCount": 11,
                    "activityRefs": [
                        "37b34f84-1ada-11eb-adc1-0242ac120002"
                    ]
                },
                "statusSummary": {
                    "status": "success"
                }
            },
            "activities": [
                {
                    "id": "4f008a00-3a04-11eb-adc1-0242ac120002",
                    "name": "Copy Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520205922,
                        "completedAtUTC": 1607520236968
                    },
                    "sizeSummary": {
                        "inputBytes": 87885,
                        "outputBytes": 87885
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 11
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                },
                {
                    "id": "37b34f84-1ada-11eb-adc1-0242ac120002",
                    "name": "Promotion Activity",
                    "updatedAtUTC": 0,
                    "durationSummary": {
                        "startedAtUTC": 1607520244985,
                        "completedAtUTC": 1607520262413
                    },
                    "sizeSummary": {
                        "inputBytes": 26758,
                        "outputBytes": 56730
                    },
                    "recordSummary": {
                        "inputRecordCount": 26758,
                        "outputRecordCount": 26758,
                        "failedRecordCount": 0
                    },
                    "fileSummary": {
                        "inputFileCount": 11,
                        "outputFileCount": 2,
                        "extensions": {
                            "manifest": {
                                "fileInfo": "https://platform.adobe.io/data/foundation/export/batches/01ES3TRN69E9W2DZ770XCGYAH1/meta?path=input_files",
                                "pathPrefix": "bucket1/csv_test/"
                            }
                        }
                    },
                    "statusSummary": {
                        "status": "success"
                    }
                }
            ]
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `items` | Contiene una única carga útil de metadatos asociada con la ejecución de flujo específica. |
| `metrics` | Características de los datos en la ejecución de flujo. |
| `activities` | Muestra cómo se transforman los datos. |
| `durationSummary` | El inicio y la hora de finalización de la ejecución del flujo. |
| `sizeSummary` | Volumen de los datos en bytes. |
| `recordSummary` | El recuento de registros de los datos. |
| `fileSummary` | El archivo cuenta los datos. |
| `fileSummary.extensions` | Contiene información específica de la actividad. Por ejemplo, `manifest` es sólo parte de la &quot;Actividad de promoción&quot; y, por lo tanto, se incluye con el objeto `extensions`. |
| `statusSummary` | Muestra si la ejecución del flujo es un éxito o un error. |

## Pasos siguientes

Siguiendo este tutorial, ha recuperado métricas e información de error en el flujo de datos mediante la API [!DNL Flow Service]. Ahora puede seguir monitoreando el flujo de datos, según el programa de ingestión, para rastrear su estado y las tasas de ingestión. Para obtener información sobre cómo monitorear flujos de datos para fuentes, lea el tutorial [monitorear flujos de datos para fuentes que utilizan el tutorial de interfaz de usuario](../ui/monitor-sources.md). Para obtener más información sobre cómo supervisar flujos de datos para destinos, lea el tutorial [monitorear flujos de datos para destinos mediante el tutorial de interfaz de usuario](../ui/monitor-destinations.md).