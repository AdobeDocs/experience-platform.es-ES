---
keywords: Experience Platform;inicio;temas populares;monitorizar flujos de datos;api de servicio de flujo;Flow Service
solution: Experience Platform
title: Monitorización de flujos de datos mediante la API de Flow Service
type: Tutorial
description: Este tutorial cubre los pasos para monitorizar los datos de ejecución de flujo en busca de integridad, errores y métricas mediante la API de Flow Service.
exl-id: c4b2db97-eba4-460d-8c00-c76c666ed70e
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 1%

---

# Monitorización de flujos de datos mediante la API de Flow Service

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras. Además, Experience Platform permite activar datos en socios externos.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de varias fuentes diferentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todos los orígenes y destinos admitidos.

Este tutorial cubre los pasos para monitorizar los datos de ejecución de flujo en busca de integridad, errores y métricas mediante [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Este tutorial requiere que tenga el valor ID de un flujo de datos válido. Si no tiene un ID de flujo de datos válido, seleccione el conector que desee en el [información general de orígenes](../../sources/home.md) o [información general sobre destinos](../../destinations/catalog/overview.md) y siga los pasos descritos antes de intentar realizar este tutorial.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Destinos](../../destinations/home.md): los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
- [Fuentes](../../sources/home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [Zonas protegidas](../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para monitorizar correctamente las ejecuciones de flujo mediante [!DNL Flow Service] API.

### Leer llamadas de API de muestra

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para los encabezados obligatorios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos de [!DNL Experience Platform], incluidos los pertenecientes a [!DNL Flow Service], están aisladas para zonas protegidas virtuales específicas. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

- `Content-Type: application/json`

## Monitorización de ejecuciones de flujo

Una vez que haya realizado un flujo de datos, realice una solicitud de GET a [!DNL Flow Service] API.

**Formato de API**

```http
GET /runs?property=flowId=={FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | La exclusiva `id` valor del flujo de datos que desea monitorizar. |

**Solicitud**

La siguiente solicitud recupera las especificaciones de un flujo de datos existente.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==c9cef9cb-c934-4467-8ef9-cbc934546741' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve detalles sobre la ejecución de flujo, incluida información sobre su fecha de creación, las conexiones de origen y destino, así como el identificador único de la ejecución de flujo (`id`).

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
            "imsOrgId": "{ORG_ID}",
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
| `items` | Contiene una única carga útil de metadatos asociados a la ejecución de flujo específica. |
| `metrics` | Las características de los datos en la ejecución de flujo. |
| `activities` | Muestra cómo se transforman los datos. |
| `durationSummary` | Hora de inicio y finalización de la ejecución del flujo. |
| `sizeSummary` | Volumen de los datos en bytes. |
| `recordSummary` | El recuento de registros de los datos. |
| `fileSummary` | El recuento de archivos de los datos. |
| `fileSummary.extensions` | Contiene información específica de la actividad. Por ejemplo, `manifest` es solo parte de la &quot;Actividad de promoción&quot; y, por lo tanto, se incluye con la `extensions` objeto. |
| `statusSummary` | Muestra si la ejecución del flujo es un éxito o un error. |

## Pasos siguientes

Con este tutorial, ha recuperado las métricas y la información de error del flujo de datos con la variable [!DNL Flow Service] API. Ahora puede seguir monitorizando el flujo de datos, según la programación de ingesta, para rastrear su estado y las tasas de ingesta. Para obtener información sobre cómo monitorizar los flujos de datos de las fuentes, lea la [monitorización de flujos de datos para fuentes mediante la interfaz de usuario](../ui/monitor-sources.md) tutorial. Para obtener más información sobre cómo monitorizar los flujos de datos de los destinos, lea la [monitorización de flujos de datos para destinos mediante la interfaz de usuario](../ui/monitor-destinations.md) tutorial.
