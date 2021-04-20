---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;segmentación por secuencias;Segmentación por secuencias;Evaluación continua;
solution: Experience Platform
title: 'Evaluar eventos en tiempo casi real con segmentación por transmisión '
topic: developer guide
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación de flujo continuo con la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
translation-type: tm+mt
source-git-commit: e1ae20412f449c991f53fdd0f095d0c3a6de262c
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 1%

---

# Evaluar eventos en tiempo casi real con segmentación de flujo continuo

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la API de . Para obtener información sobre el uso de la segmentación de flujo continuo mediante la interfaz de usuario, lea la [guía de la interfaz de segmentación de flujo](../ui/streaming-segmentation.md).

La segmentación por transmisión en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real, mientras se concentra en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos de flujo continuo llegan a [!DNL Platform], lo que reduce la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar ya que los datos se pasan a [!DNL Platform], lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentación por transmisión solo se puede utilizar para evaluar los datos que se transmiten a Platform. En otras palabras, los datos ingestados mediante la ingesta por lotes no se evaluarán mediante la segmentación de flujo continuo y se evaluarán junto con el trabajo segmentado programado por la noche.

## Primeros pasos

Esta guía para desarrolladores requiere una comprensión práctica de los diversos servicios [!DNL Adobe Experience Platform] que intervienen en la segmentación de flujo continuo. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md): Proporciona la capacidad de crear segmentos y audiencias a partir de los  [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que deberá conocer para realizar llamadas a las API [!DNL Platform] correctamente.

### Leer llamadas de API de ejemplo

Esta guía para desarrolladores proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform] están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general del entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

Es posible que se requieran encabezados adicionales para completar solicitudes específicas. Los encabezados correctos se muestran en cada uno de los ejemplos de este documento. Preste especial atención a las solicitudes de muestra para asegurarse de que se incluyen todos los encabezados necesarios.

### Tipos de consulta habilitados para la segmentación por transmisión {#streaming-segmentation-query-types}

>[!NOTE]
>
>Deberá habilitar la segmentación programada para la organización para que funcione la segmentación de flujo continuo. Puede encontrar información sobre cómo habilitar la segmentación programada en la sección [habilitar la segmentación programada](#enable-scheduled-segmentation)

Para que un segmento se evalúe utilizando la segmentación de flujo continuo, la consulta debe cumplir las siguientes directrices.

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. |
| Visita entrante dentro de un periodo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante. |
| Visita entrante con una ventana de tiempo | Cualquier definición de segmento que haga referencia a un solo evento entrante con un intervalo de tiempo. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. |
| Visita entrante que hace referencia a un perfil dentro de un periodo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o más atributos de perfil. |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. |
| Varios eventos que hacen referencia a un perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o más atributos de perfil. |

Una definición de segmento **no** se habilitará para la segmentación de flujo continuo en los siguientes escenarios:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager (AAM).
- La definición del segmento incluye varias entidades (consultas de varias entidades).

Además, se aplican algunas directrices al realizar segmentación de flujo continuo:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva está limitada a **un día**.</li><li>Existe una condición estricta de ordenación de tiempo **debe** entre los eventos.</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

## Recuperar todos los segmentos habilitados para la segmentación de flujo continuo

Puede recuperar una lista de todos los segmentos que están habilitados para la segmentación de flujo continuo dentro de su organización IMS realizando una solicitud de GET al extremo `/segment/definitions` .

**Formato de API**

Para recuperar segmentos habilitados para flujo continuo, debe incluir el parámetro de consulta `evaluationInfo.continuous.enabled=true` en la ruta de solicitud.

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

Una respuesta correcta devuelve una matriz de segmentos en su organización de IMS que están habilitados para la segmentación de flujo continuo.

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

## Creación de segmentos con flujo continuo activado

Un segmento se habilitará automáticamente para la transmisión si coincide con uno de los [tipos de segmentación de flujo continuo enumerados arriba](#streaming-segmentation-query-types).

**Formato de API**

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
>Se trata de una solicitud estándar &quot;crear un segmento&quot;. Para obtener más información sobre la creación de una definición de segmento, lea el tutorial sobre la [creación de un segmento](../tutorials/create-a-segment.md).

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición de segmento de flujo continuo recién creada.

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

Una vez habilitada la evaluación de flujo continuo, se debe crear una línea de base (después de lo cual el segmento siempre estará actualizado). La evaluación programada (también conocida como segmentación programada) debe habilitarse primero para que el sistema realice automáticamente la asignación de basl. Con la segmentación programada, su organización de IMS puede adherirse a una programación recurrente para ejecutar automáticamente trabajos de exportación para evaluar segmentos.

>[!NOTE]
>
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] dentro de un entorno limitado único, no podrá utilizar la evaluación programada.

### Crear una programación

Al realizar una solicitud de POST al extremo `/config/schedules` , puede crear una programación e incluir la hora específica en la que se debe activar la programación.

**Formato de API**

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
| `name` | **(Obligatorio)** El nombre de la programación. Debe ser una cadena. |
| `type` | **(Obligatorio)** El tipo de trabajo en formato de cadena. Los tipos admitidos son `batch_segmentation` y `export`. |
| `properties` | **(Obligatorio)** Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **(Necesario cuando es  `type` igual a  `batch_segmentation`)**  El uso de  `["*"]` garantiza que se incluyen todos los segmentos. |
| `schedule` | **(Obligatorio)** Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. El ejemplo mostrado (`0 0 1 * * ?`) significa que el trabajo se activa todos los días a la 1:00:00 UTC. Para obtener más información, consulte la documentación de [cron expression format](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html). |
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

### Activación de una programación

De forma predeterminada, una programación está inactiva cuando se crea a menos que la propiedad `state` esté establecida en `active` en el cuerpo de la solicitud de creación (POST). Puede habilitar una programación (establezca `state` en `active`) realizando una solicitud de PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta.

**Formato de API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitud**

La siguiente solicitud utiliza [JSON Patch formatting](http://jsonpatch.com/) para actualizar el `state` de la programación a `active`.

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

Una actualización correcta devuelve un cuerpo de respuesta vacío y el estado HTTP 204 (sin contenido).

Se puede utilizar la misma operación para deshabilitar una programación reemplazando el &quot;valor&quot; de la solicitud anterior por &quot;inactivo&quot;.

## Pasos siguientes

Ahora que ha habilitado los segmentos nuevos y existentes para la segmentación de flujo continuo y la segmentación programada para desarrollar una línea de base y realizar evaluaciones recurrentes, puede empezar a crear segmentos con transmisión habilitada para su organización.

Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [guía del usuario del Generador de segmentos](../ui/segment-builder.md).
