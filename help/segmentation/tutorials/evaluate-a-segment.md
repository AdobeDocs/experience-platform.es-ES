---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Evaluar un segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 2%

---


# Evaluar y acceder a los resultados de los segmentos

Este documento proporciona un tutorial para evaluar segmentos y acceder a los resultados de los mismos mediante la API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)de segmentación.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que intervienen en la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real basado en datos agregados de varias fuentes.
- [Servicio](../home.md)de segmentación de Adobes Experience Platform: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.
- [Simuladores](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Encabezados requeridos

Este tutorial también requiere que haya completado el tutorial [de](../../tutorials/authentication.md) autenticación para poder realizar correctamente llamadas a las API de Platform. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos del Experience Platform están aislados en entornos limitados virtuales específicos. Las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados de Platform, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes POST, PUT y PATCH requieren un encabezado adicional:

- Content-Type: application/json

## Evaluar un segmento

Una vez desarrollada, probada y guardada la definición del segmento, puede evaluar el segmento mediante una evaluación programada o una evaluación a petición.

[La evaluación](#scheduled-evaluation) programada (también conocida como &#39;segmentación programada&#39;) le permite crear una programación recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que la evaluación [](#on-demand-evaluation) a petición implica crear un trabajo de segmento para generar la audiencia inmediatamente. A continuación se describen los pasos para cada uno de ellos.

Si todavía no ha completado el tutorial [Crear un segmento con la API](./create-a-segment.md) de Perfil del cliente en tiempo real o ha creado una definición de segmento con el Generador [de segmentos](../ui/overview.md), hágalo antes de continuar con este tutorial.

## Evaluación programada {#scheduled-evaulation}

Mediante una evaluación programada, su organización de IMS puede crear una programación recurrente para ejecutar automáticamente los trabajos de exportación.

>[!NOTE] La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para Perfiles individuales XDM. Si su organización cuenta con más de cinco directivas de combinación para Perfiles individuales XDM dentro de un solo entorno de simulador de pruebas, no podrá usar la evaluación programada.

### Crear una programación

Al realizar una solicitud POST al extremo, puede crear una programación e incluir la hora específica en la que se debe activar la programación. `/config/schedules`

**Formato API**

```http
POST /config/schedules
```

**Solicitud**

La siguiente solicitud crea una nueva programación basada en las especificaciones proporcionadas en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | **(Requerido)** El nombre de la programación. Debe ser una cadena. |
| `type` | **(Requerido)** El tipo de trabajo en formato de cadena. Los tipos admitidos son `batch_segmentation` y `export`. |
| `properties` | **(Requerido)** Objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **(Necesario cuando`type`es igual a`batch_segmentation`)** El uso `["*"]` garantiza que se incluyan todos los segmentos. |
| `schedule` | **(Requerido)** Una cadena que contiene la programación de trabajos. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar que se ejecute más de una vez durante un período de 24 horas. El ejemplo mostrado (`0 0 1 * * ?`) significa que el trabajo se activa todos los días a la 1:00:00 UTC. Para obtener más información, consulte la documentación sobre el formato [de expresión](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron. |
| `state` | *(Opcional)* Cadena que contiene el estado de programación. Valores disponibles: `active` y `inactive`. El valor predeterminado es `inactive`. Una organización de IMS solo puede crear una programación. Los pasos para actualizar la programación están disponibles más adelante en este tutorial. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la programación recién creada.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### Habilitar una programación

De forma predeterminada, una programación se desactiva cuando se crea, a menos que la `state` propiedad se establezca `active` en el cuerpo de la solicitud create (POST). Puede habilitar una programación (establecer la `state` en `active``/config/schedules` ) realizando una solicitud PATCH en el extremo e incluyendo el ID de la programación en la ruta de acceso.

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitud**

La siguiente solicitud utiliza el formato [de parche](http://jsonpatch.com/) JSON para actualizar el formato `state` de la programación a `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**Respuesta**

Una actualización correcta devuelve un cuerpo de respuesta vacío y Estado HTTP 204 (sin contenido).

La misma operación puede utilizarse para deshabilitar una programación reemplazando el &quot;valor&quot; en la solicitud anterior por &quot;inactivo&quot;.

### Actualizar la hora de programación

La temporización de programación se puede actualizar realizando una solicitud PATCH al extremo e incluyendo el ID de la programación en la ruta de acceso. `/config/schedules`

**Formato API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitud**

La siguiente solicitud utiliza el formato [](http://jsonpatch.com/) JSON Patch para actualizar la expresión [](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) cron de la programación. En este ejemplo, la programación ahora se activaría a las 10:15:00 UTC.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**Respuesta**

Una actualización correcta devuelve un cuerpo de respuesta vacío y Estado HTTP 204 (sin contenido).

## Evaluación a petición

La evaluación a petición le permite crear un trabajo de segmento para generar un segmento de audiencia cuando lo necesite. A diferencia de la evaluación programada, esto solo sucederá cuando se solicite y no se repita.

### Crear un trabajo de segmento

Un trabajo de segmento es un proceso asincrónico que crea un nuevo segmento de audiencia. Hace referencia a una definición de segmento, así como a cualquier política de combinación que controle la forma en que el Perfil del cliente en tiempo real combina atributos superpuestos en los fragmentos de perfil. Cuando un trabajo de segmento se completa correctamente, puede recopilar información diversa sobre el segmento, como los errores que se hayan producido durante el procesamiento y el tamaño final de la audiencia.

Puede crear un nuevo trabajo de segmento realizando una solicitud POST al extremo en la API de Perfil del cliente en tiempo real `/segment/jobs` .

**Formato API**

```http
POST /segment/jobs
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de segmento basado en las dos definiciones de segmento proporcionadas en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentId` | El identificador de una definición de segmento desde la cual generar la audiencia. Se debe proporcionar al menos un ID de segmento en la matriz de carga útil. |

**Respuesta**

Una respuesta correcta devuelve los detalles del trabajo de segmento recién creado, incluido su `id`valor de sólo lectura generado por el sistema que es único para este trabajo de segmento.

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador del nuevo trabajo de segmento, que se utiliza con fines de búsqueda. |
| `status` | Estado actual del trabajo del segmento. Será &quot;PROCESAMIENTO&quot; hasta que se complete el procesamiento, momento en el cual se convierte en &quot;CORRECTO&quot; o &quot;FALLIDO&quot;. |

### Buscar estado del trabajo del segmento

Puede usar el `id` para un trabajo de segmento específico para realizar una solicitud de búsqueda (GET) con el fin de vista del estado actual del trabajo.

**Formato API**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | El `id` del trabajo del segmento al que desea acceder. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve los detalles del trabajo de segmentación y proporciona información diferente según el estado actual del trabajo. Puede repetir la solicitud de búsqueda hasta que `status` alcance &quot;SUCCEEDED&quot;, momento en el que puede exportar el segmento a un conjunto de datos.


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentedProfileCounter` | El número total de perfiles combinados que cumplen los requisitos para el segmento. |
| `segmentedProfileByNamespaceCounter` | Un desglose de los perfiles que cumplen los requisitos para el segmento por código de Área de nombres de identidad. Puede encontrar una lista de los códigos de Área de nombres de identidad en la descripción general [de la Área de nombres de](../../identity-service/namespaces.md)identidad. |

## Interpretar resultados de segmentos

Cuando los trabajos de segmentos se ejecutan correctamente, el `segmentMembership` mapa se actualiza para cada perfil incluido en el segmento. `segmentMembership` también almacena todos los segmentos de audiencia preevaluados que se ingieren en Platform, lo que permite la integración con otras soluciones como Adobe Audience Manager.

El siguiente ejemplo muestra el aspecto del `segmentMembership` atributo para cada registro de perfil individual:

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `lastQualificationTime` | Marca de hora cuando se hizo la afirmación de pertenencia a segmentos y el perfil entró o salió del segmento. |
| `status` | El estado de la participación de segmentos como parte de la solicitud actual. Debe ser igual a uno de los siguientes valores conocidos: <ul><li>`existing`:: La entidad sigue estando en el segmento.</li><li>`realized`:: La entidad está ingresando al segmento.</li><li>`exited`:: La entidad está saliendo del segmento.</li></ul> |

## Acceso a los resultados de los segmentos

Se puede acceder a los resultados de un trabajo de segmento de una de las dos maneras siguientes: puede acceder a perfiles individuales o exportar una audiencia completa a un conjunto de datos.

Las siguientes secciones describen estas opciones con más detalle.

## Buscar un perfil

Si conoce el perfil específico al que desea acceder, puede hacerlo mediante la API de Perfil del cliente en tiempo real. Los pasos completos para acceder a perfiles individuales están disponibles en [Access Real-time Customer Perfil data mediante el tutorial de la API](../../profile/api/entities.md) de Perfil.

## Exportación de un segmento {#export}

Una vez completado correctamente un trabajo de segmentación (el valor del `status` atributo es &quot;SUCCEEDED&quot;), puede exportar la audiencia a un conjunto de datos en el que se pueda acceder a él y tomar medidas al respecto.

Se requieren los siguientes pasos para exportar la audiencia:

- [Crear un conjunto de datos](#create-a-target-dataset) de destinatario: cree el conjunto de datos para albergar miembros de audiencia.
- [Generar perfiles de audiencia en el conjunto de datos](#generate-profiles-for-audience-members) : Rellene el conjunto de datos con Perfiles individuales XDM basados en los resultados de un trabajo de segmento.
- [Monitorear el progreso](#monitor-export-progress) de exportación: compruebe el progreso actual del proceso de exportación.
- [Leer datos](#next-steps) de audiencia: recupere los Perfiles individuales XDM resultantes que representan a los miembros de la audiencia.

### Creación de un conjunto de datos de destinatario

Al exportar una audiencia, primero se debe crear un conjunto de datos de destinatario. Es importante que el conjunto de datos se configure correctamente para garantizar que la exportación se realiza correctamente.

Una de las consideraciones clave es el esquema en el que se basa el conjunto de datos (`schemaRef.id` en la solicitud de muestra de API que se muestra a continuación). Para exportar un segmento, el conjunto de datos debe basarse en el Esquema de Unión de Perfil individual XDM (`https://ns.adobe.com/xdm/context/profile__union`). Un esquema de unión es un esquema de sólo lectura generado por el sistema que agrega los campos de esquemas que comparten la misma clase, en este caso la clase de Perfil individual XDM. Para obtener más información sobre los esquemas de vista de uniones, consulte la sección Perfil de clientes en tiempo [real de la guía](../../xdm/api/getting-started.md)para desarrolladores de Esquema Registry.

Existen dos maneras de crear el conjunto de datos necesario:

- **Uso de API:** Los pasos siguientes en este tutorial describen cómo crear un conjunto de datos que haga referencia al Esquema de Unión de Perfil individual XDM mediante la API de catálogo.
- **Uso de la interfaz de usuario:** Para utilizar la interfaz de usuario de Adobe Experience Platform para crear un conjunto de datos que haga referencia al esquema de unión, siga los pasos del tutorial [de](../ui/overview.md) IU y vuelva a este tutorial para continuar con los pasos para [generar perfiles](#generate-xdm-profiles-for-audience-members)de audiencia.

Si ya tiene un conjunto de datos compatible y conoce su ID, puede continuar directamente con el paso para [generar perfiles](#generate-xdm-profiles-for-audience-members)de audiencia.

**Formato API**

```http
POST /dataSets
```

**Solicitud**

La siguiente solicitud crea un nuevo conjunto de datos, que proporciona parámetros de configuración en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `name` | Un nombre descriptivo para el conjunto de datos. |
| `schemaRef.id` | ID de la vista de unión (esquema) con la que se asociará el conjunto de datos. |
| `fileDescription.persisted` | Un valor booleano que cuando se establece en `true`, permite que el conjunto de datos persista en la vista de unión. |

**Respuesta**

Una respuesta correcta devuelve una matriz que contiene la ID única de sólo lectura generada por el sistema del conjunto de datos recién creado. Se requiere un ID de conjunto de datos configurado correctamente para exportar correctamente los miembros de la audiencia.

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### Generar perfiles para miembros de audiencia

Una vez que tenga un conjunto de datos que mantenga la unión, puede crear un trabajo de exportación para que los miembros de la audiencia permanezcan en el conjunto de datos realizando una solicitud POST al extremo en la API de Perfil del cliente en tiempo real y proporcionando la ID del conjunto de datos y la información del segmento para los segmentos que desea exportar. `/export/jobs`

**Formato API**

```http
POST /export/jobs
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de exportación, proporcionando parámetros de configuración en la carga útil.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `fields` | *(Opcional)* Limita los campos de datos que se van a incluir en la exportación solo a los proporcionados en este parámetro. El mismo parámetro también está disponible al crear un segmento, por lo que es posible que los campos del segmento ya se hayan filtrado. Si se omite este valor, todos los campos se incluirán en los datos exportados |
| `mergePolicy` | *(Opcional)* Especifica la directiva de combinación que regirá los datos exportados. Incluya este parámetro cuando se exporten varios segmentos. Si se omite este valor, el servicio de exportación usará la directiva de combinación proporcionada por el segmento. |
| `mergePolicy.id` | ID de la directiva de combinación |
| `mergePolicy.version` | Versión específica de la directiva de combinación que se va a utilizar. Si se omite este valor, se pasará de forma predeterminada a la versión más reciente. |
| `filter` | *(Opcional)* Especifica uno o varios de los siguientes filtros que se aplicarán al segmento antes de la exportación: |
| `filter.segments` | *(Opcional)* Especifica los segmentos que se van a exportar. Si se omite este valor, se exportarán todos los datos de todos los perfiles. Acepta una matriz de objetos de segmento, cada uno de los cuales contiene los campos siguientes: |
| `filter.segments.segmentId` | **(Necesario si se utiliza`segments`)** ID de segmento para la exportación de perfiles. |
| `filter.segments.segmentNs` | *(Opcional)* Área de nombres de segmentos para el `segmentID`. |
| `filter.segments.status` | *(Opcional)* Matriz de cadenas que proporciona un filtro de estado para el `segmentID`. De forma predeterminada, `status` tendrá el valor `["realized", "existing"]` que representa todos los perfiles que entran en el segmento en el momento actual. Los valores posibles incluyen: `"realized"`, `"existing"`, y `"exited"`. |
| `filter.segmentQualificationTime` | *(Opcional)* Filtre según el tiempo de calificación del segmento. Se puede proporcionar la hora de inicio y/o la hora de finalización. |
| `filter.segmentQualificationTime.startTime` | *(Opcional)* Tiempo de inicio de cualificación del segmento para un ID de segmento para un estado determinado. No se proporciona, no habrá ningún filtro en el tiempo de inicio para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.segmentQualificationTime.endTime` | *(Opcional)* Hora de finalización de la calificación del segmento para un ID de segmento para un estado determinado. No se proporciona, no habrá ningún filtro en la hora de finalización para una calificación de ID de segmento. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` | *(Opcional)* Limita los perfiles exportados para incluir solo aquellos que se hayan actualizado después de esta marca de tiempo. La marca de tiempo debe proporcionarse en formato [RFC 3339](https://tools.ietf.org/html/rfc3339) . |
| `filter.fromIngestTimestamp` para **perfiles**, si se proporcionan | Incluye todos los perfiles combinados en los que la marca de tiempo actualizada combinada es buena que la marca de tiempo dada. Admite `greater_than` operando. |
| `filter.fromTimestamp` para eventos | Todos los eventos ingeridos después de esta marca de tiempo se exportarán según el resultado de perfil resultante. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos. |
| `filter.emptyProfiles` | *(Opcional)* Booleano. Los Perfiles pueden contener registros de Perfiles, registros de ExperienceEvent o ambos. Los Perfiles sin registros de Perfil y solo los registros de ExperienceEvent se denominan &quot;emptyProfiles&quot;. Para exportar todos los perfiles del almacén de Perfiles, incluido &quot;emptyProfiles&quot;, establezca el valor de `emptyProfiles` en `true`. Si `emptyProfiles` se establece en `false`, solo se exportan los perfiles con registros de Perfil en el almacén. De forma predeterminada, si no se incluye `emptyProfiles` el atributo, solo se exportan los perfiles que contienen registros de Perfil. |
| `additionalFields.eventList` | *(Opcional)* Controla los campos de evento de la serie temporal exportados para objetos secundarios o asociados proporcionando una o varias de las siguientes opciones de configuración: |
| `additionalFields.eventList.fields` | Controle los campos que desea exportar. |
| `additionalFields.eventList.filter` | Especifica criterios que limitan los resultados incluidos de los objetos asociados. Espera un valor mínimo necesario para la exportación, normalmente una fecha. |
| `additionalFields.eventList.filter.fromIngestTimestamp` | Filtros eventos de series temporales a los que se han ingerido después de la marca de tiempo proporcionada. Este no es el tiempo de evento en sí mismo sino el tiempo de ingestión de los eventos. |
| `destination` | **(Requerido)** Información de destino de los datos exportados |
| `destination.datasetId` | **(Requerido)** El ID del conjunto de datos en el que se exportan los datos. |
| `destination.segmentPerBatch` | *(Opcional)* Un valor booleano que, si no se proporciona, toma como valor predeterminado `false`. Un valor de `false` exporta todos los ID de segmento en un único ID de lote. Un valor de `true` exporta un ID de segmento en un ID de lote. Tenga en cuenta que la configuración del valor que se va a definir `true` puede afectar al rendimiento de exportación de lotes. |
| `schema.name` | **(Requerido)** El nombre del esquema asociado con el conjunto de datos donde se exportan los datos. |

**Respuesta**

Una respuesta correcta devuelve un conjunto de datos rellenado con perfiles que se calificaron para la última ejecución completada del trabajo del segmento. Se han eliminado todos los perfiles que anteriormente existían en el conjunto de datos pero que no cumplían los requisitos para el segmento durante la última ejecución completa del trabajo del segmento.

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

Si no `destination.segmentPerBatch` se hubiera incluido en la solicitud (si no está presente, se establece de forma predeterminada en `false`) o el valor se hubiera establecido en `false`, el `destination` objeto de la respuesta anterior no tendría una `batches` matriz y, en su lugar, incluiría sólo una `batchId`, como se muestra a continuación. Ese único lote incluiría todos los ID de segmento, mientras que la respuesta anterior muestra un único ID de segmento por ID de lote.

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### Lista de todos los trabajos de exportación

Puede devolver una lista de todos los trabajos de exportación para una organización IMS concreta realizando una solicitud GET al `export/jobs` extremo. La solicitud también admite los parámetros de consulta `limit` y `offset`, como se muestra a continuación.

**Formato API**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| Propiedad | Descripción |
| -------- | ----------- |
| `limit` | Especifique el número de registros que se van a devolver. |
| `offset` | Desplaza la página de resultados que devuelve el número proporcionado. |


**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

La respuesta incluye un `records` objeto que contiene los trabajos de exportación creados por la organización de IMS.

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### Monitorear el progreso de exportación

Como proceso de trabajo de exportación, puede supervisar su estado realizando una solicitud GET al extremo e incluyendo el `/export/jobs` `id` del trabajo de exportación en la ruta de acceso. El trabajo de exportación se completa una vez que el `status` campo devuelve el valor &quot;SUCCEEDED&quot;.

**Formato API**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | El `id` del trabajo de exportación al que desea acceder. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `batchId` | El identificador de los lotes creados a partir de una exportación correcta, que se utilizará con fines de búsqueda al leer datos de audiencia. |

## Pasos siguientes

Una vez que la exportación se haya completado correctamente, los datos estarán disponibles en el Experience Platform Data Lake. A continuación, puede utilizar la API [de acceso a](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) datos para acceder a los datos mediante el `batchId` vínculo asociado a la exportación. Según el tamaño del segmento, los datos pueden estar en fragmentos y el lote puede constar de varios archivos.

Para obtener instrucciones paso a paso sobre cómo utilizar la API de acceso a datos para acceder y descargar archivos por lotes, siga el tutorial [de acceso a](../../data-access/tutorials/dataset-data.md)datos.

También puede acceder a los datos de segmentos exportados correctamente mediante el servicio de Consulta de Adobe Experience Platform. El servicio de Consulta, que utiliza la interfaz de usuario o la API RESTful, le permite escribir, validar y ejecutar consultas en los datos dentro de Data Lake.

Para obtener más información sobre cómo consulta de datos de audiencia, consulte la documentación [del servicio de](../../query-service/home.md)Consulta.
