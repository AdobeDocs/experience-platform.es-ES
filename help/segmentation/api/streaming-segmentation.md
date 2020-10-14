---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;streaming segmentation;Streaming segmentation;Continuous evaluation;
solution: Experience Platform
title: Segmentación por flujo continuo
topic: developer guide
description: Este documento contiene ejemplos de cómo utilizar la segmentación de flujo con la API de segmentación de flujo.
translation-type: tm+mt
source-git-commit: 578579438ca1d6a7a8c0a023efe2abd616a6dff2
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 1%

---


# Evaluar eventos en tiempo casi real con segmentación de flujo continuo

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo mediante la API. Para obtener información sobre el uso de la segmentación de flujo mediante la interfaz de usuario, consulte la guía de la interfaz de usuario de segmentación de [flujo continuo](../ui/streaming-segmentation.md).

La segmentación por flujo continuo [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real mientras se concentran en la riqueza de los datos. Con la segmentación de flujo continuo, la cualificación de segmentos ahora se produce cuando los datos de flujo llegan a [!DNL Platform]su destino, lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que se pasan los datos [!DNL Platform], lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentación por flujo continuo solo se puede utilizar para evaluar los datos que se transmiten a la plataforma. En otras palabras, los datos ingeridos mediante la ingestión por lotes no se evaluarán mediante la segmentación de flujo continuo y se evaluarán junto con el trabajo segmentado programado por la noche.

## Primeros pasos

Esta guía para desarrolladores requiere un conocimiento práctico de los distintos [!DNL Adobe Experience Platform] servicios relacionados con la segmentación por flujo continuo. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md):: Proporciona la capacidad de crear segmentos y audiencias a partir de sus [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas a [!DNL Platform] las API de forma satisfactoria.

### Leer llamadas de API de muestra

Esta guía para desarrolladores proporciona llamadas de API de ejemplo para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados de [!DNL Platform], consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

Es posible que se requieran encabezados adicionales para completar solicitudes específicas. Los encabezados correctos se muestran en cada uno de los ejemplos de este documento. Preste especial atención a las solicitudes de muestra para asegurarse de que se incluyen todos los encabezados necesarios.

### Tipos de consulta habilitados para la segmentación por flujo {#streaming-segmentation-query-types}

>[!NOTE]
>
>Deberá habilitar la segmentación programada para la organización para que funcione la segmentación de flujo continuo. Encontrará información sobre cómo habilitar la segmentación programada en la sección [Activar segmentación programada](#enable-scheduled-segmentation)

Para que un segmento se evalúe mediante la segmentación de flujo continuo, la consulta debe cumplir las siguientes directrices.

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. |
| Visita entrante dentro de un período de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. |
| Visita entrante que hace referencia a un perfil dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o varios atributos de perfil. |
| Varios eventos que hacen referencia a un perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o varios atributos de perfil. |

La siguiente sección lista ejemplos de definición de segmentos que **no se habilitarán** para la segmentación de flujo continuo.

| Tipo de consulta | Detalles |
| ---------- | ------- | 
| Visita entrante que hace referencia a un perfil dentro de una ventana relativa | Definición de segmento que incluye segmentos o características de Adobe Audience Manager (AAM). |
| Varios eventos que hacen referencia a un perfil | Definición de segmento que incluye segmentos o características de Adobe Audience Manager (AAM). |
| Consultas de varias entidades | Las consultas de varias entidades **no son** compatibles con la segmentación por flujo. |

Además, se aplican algunas directrices al realizar la segmentación de flujo:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites para la ventana retroactiva. |
| Consulta con historial de eventos | <ul><li>La ventana retroactiva está limitada a **un día**.</li><li>Entre los eventos **debe** existir una condición estricta de ordenación de tiempo.</li><li>Solo se permiten pedidos de tiempo simples (antes y después) entre los eventos.</li><li>Los eventos individuales **no se pueden** negar. Sin embargo, toda la consulta **puede** ser anulada.</li></ul> |

## Recuperar todos los segmentos activados para la segmentación de flujo continuo

Puede recuperar una lista de todos los segmentos que están habilitados para la segmentación de flujo continuo dentro de la organización de IMS realizando una solicitud de GET al `/segment/definitions` extremo.

**Formato API**

Para recuperar segmentos con transmisión habilitada, debe incluir el parámetro de consulta `evaluationInfo.continuous.enabled=true` en la ruta de la solicitud.

```http
GET /segment/definitions?evaluationInfo.continuous.enabled=true
```

**Solicitud**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.continuous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve una matriz de segmentos en la organización de IMS que están habilitados para la segmentación por flujo continuo.

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": true
                },
                "continuous": {
                    "enabled": true
                },
                "synchronous": {
                    "enabled": false
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

## Creación de un segmento con transmisión habilitada

Un segmento se habilitará automáticamente para la transmisión si coincide con uno de los tipos de segmentación de [flujo enumerados arriba](#streaming-segmentation-query-types).

**Formato API**

```http
POST /segment/definitions
```

**Solicitud**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    }
}'
```

>[!NOTE]
>
>Se trata de una solicitud estándar para &quot;crear un segmento&quot;. Para obtener más información sobre la creación de una definición de segmento, lea el tutorial sobre la [creación de un segmento](../tutorials/create-a-segment.md).

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición de segmento habilitado para flujo recién creada.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true,
                   },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1572021085000,
    "updateEpoch": 1572021086000,
    "updateTime": 1572021086000
}
```

## Habilitar evaluación programada {#enable-scheduled-segmentation}

Una vez habilitada la evaluación de flujo continuo, se debe crear una línea de base (después de la cual el segmento siempre estará actualizado). La evaluación programada (también conocida como segmentación programada) debe habilitarse en primer lugar para que el sistema realice automáticamente la asignación de la base. Con la segmentación programada, su organización de IMS puede adherirse a una programación recurrente para ejecutar automáticamente trabajos de exportación para evaluar segmentos.

>[!NOTE]
>
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] dentro de un solo entorno de simulación de pruebas, no podrá usar la evaluación programada.

### Crear una programación

Al realizar una solicitud de POST al extremo, puede crear una programación e incluir la hora específica en la que se debe activar la programación. `/config/schedules`

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
| `properties.segments` | **(Necesario cuando `type` es igual a `batch_segmentation`)** El uso `["*"]` garantiza que se incluyan todos los segmentos. |
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

De forma predeterminada, una programación se desactiva cuando se crea, a menos que la `state` propiedad se establezca `active` en el cuerpo de solicitud create (POST). Puede habilitar una programación (establecer la `state` en `active``/config/schedules` ) realizando una solicitud de PATCH al extremo e incluyendo el ID de la programación en la ruta de acceso.

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

## Pasos siguientes

Ahora que ha habilitado segmentos nuevos y existentes para la segmentación de flujo continuo y ha habilitado la segmentación programada para desarrollar una línea de base y realizar evaluaciones recurrentes, puede empezar a crear segmentos para su organización.

Para obtener información sobre cómo realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la guía del usuario [del Generador de segmentos](../ui/segment-builder.md).