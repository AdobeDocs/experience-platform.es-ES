---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;segmentación por secuencias;Segmentación por secuencias;Evaluación continua;
solution: Experience Platform
title: Evaluar eventos en tiempo casi real con segmentación por transmisión
topic-legacy: developer guide
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación de flujo continuo con la API del servicio de segmentación de Adobe Experience Platform.
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: 5a4a8a8b77d06890f212a457e599b66aa46d8b7e
workflow-type: tm+mt
source-wordcount: '1915'
ht-degree: 1%

---

# Evaluar eventos en tiempo casi real con segmentación de flujo continuo

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la API de . Para obtener información sobre el uso de la segmentación de flujo continuo mediante la interfaz de usuario, lea la [guía de la interfaz de usuario de segmentación por secuencias](../ui/streaming-segmentation.md).

Segmentación por transmisión en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real, mientras se centran en la riqueza de los datos. Con la segmentación de flujo continuo, la calificación de segmentos ahora se produce cuando los datos de flujo continuo llegan a [!DNL Platform], aliviando la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que se pasan los datos a [!DNL Platform], lo que significa que la pertenencia a un segmento se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentación por transmisión funciona en todos los datos que se introdujeron mediante una fuente de flujo continuo. Los segmentos introducidos mediante un origen basado en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación de flujo continuo.
>
>Además, los segmentos evaluados con la segmentación de flujo continuo pueden variar entre la pertenencia ideal y real si el segmento se basa en otro segmento que se evalúa mediante la segmentación por lotes. Por ejemplo, si el segmento A se basa en el segmento B y el segmento B se evalúa mediante la segmentación por lotes, ya que el segmento B solo se actualiza cada 24 horas, el segmento A se alejará más de los datos reales hasta que se vuelva a sincronizar con la actualización del segmento B.

## Primeros pasos

Esta guía para desarrolladores requiere una comprensión práctica de las distintas [!DNL Adobe Experience Platform] servicios relacionados con la segmentación de flujo continuo. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md): Proporciona la capacidad de crear segmentos y audiencias a partir de [!DNL Real-time Customer Profile] datos.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que debe conocer para realizar llamadas a [!DNL Platform] API.

### Leer llamadas de API de ejemplo

Esta guía para desarrolladores proporciona llamadas de API de ejemplo para demostrar cómo dar formato a sus solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en el [!DNL Experience Platform] guía de solución de problemas.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todos los [!DNL Experience Platform] Llamadas de API, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] Las API requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en [!DNL Platform], consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

Es posible que se requieran encabezados adicionales para completar solicitudes específicas. Los encabezados correctos se muestran en cada uno de los ejemplos de este documento. Preste especial atención a las solicitudes de muestra para asegurarse de que se incluyen todos los encabezados necesarios.

### Tipos de consultas habilitadas para la segmentación por transmisión {#query-types}

>[!NOTE]
>
>Deberá habilitar la segmentación programada para la organización para que funcione la segmentación de flujo continuo. La información sobre cómo habilitar la segmentación programada se encuentra en la [habilitar la sección de segmentación programada](#enable-scheduled-segmentation)

Para que un segmento se evalúe utilizando la segmentación de flujo continuo, la consulta debe cumplir las siguientes directrices.

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Un solo evento | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. |
| Un solo evento dentro de un periodo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante. |
| Un solo evento con una ventana de tiempo | Cualquier definición de segmento que haga referencia a un solo evento entrante con un intervalo de tiempo. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Un solo evento con un atributo de perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. **Nota:** La consulta se evalúa inmediatamente cuando se produce el evento. Sin embargo, en el caso de un evento de perfil, debe esperar 24 horas para incorporarse. |
| Un solo evento con un atributo de perfil dentro de un periodo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o más atributos de perfil. |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se utiliza un segmento de segmentos, se producirá la descalificación del perfil **cada 24 horas**. |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o más atributos de perfil. |

Una definición de segmento **not** esté habilitado para la segmentación de flujo continuo en los siguientes casos:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager (AAM).
- La definición del segmento incluye varias entidades (consultas de varias entidades).

Tenga en cuenta las siguientes directrices cuando realice la segmentación de flujo continuo:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva se limita a **un día**.</li><li>Condición estricta de orden de tiempo **must** existen entre los eventos.</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **cannot** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición del segmento pasará automáticamente de &quot;Transmisión&quot; a &quot;Lote&quot;.

Además, la descalificación de segmentos, similar a la calificación de segmentos, se produce en tiempo real. Como resultado, si una audiencia ya no cumple los requisitos para un segmento, quedará inmediatamente sin clasificar. Por ejemplo, si la definición del segmento requiere &quot;Todos los usuarios que compraron zapatos rojos en las últimas tres horas&quot;, después de tres horas, todos los perfiles que inicialmente calificaron para la definición del segmento no se calificarán.

## Recuperar todos los segmentos habilitados para la segmentación de flujo continuo

Puede recuperar una lista de todos los segmentos que están habilitados para la segmentación de flujo continuo dentro de su organización IMS realizando una solicitud de GET al `/segment/definitions` punto final.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Se habilitará automáticamente la transmisión de un segmento si coincide con uno de los [tipos de segmentación de flujo continuo enumerados arriba](#query-types).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
>Se trata de una solicitud estándar &quot;crear un segmento&quot;. Para obtener más información sobre la creación de una definición de segmento, lea el tutorial sobre [creación de segmentos](../tutorials/create-a-segment.md).

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición de segmento de flujo continuo recién creada.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{ORG_ID}",
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
>La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] en un entorno limitado, no se puede utilizar la evaluación programada.

### Crear una programación

Haciendo una solicitud de POST al `/config/schedules` , puede crear una programación e incluir la hora específica en la que se debe activar la programación.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `name` | **(Obligatorio)** Nombre de la programación. Debe ser una cadena. |
| `type` | **(Obligatorio)** El tipo de trabajo en formato de cadena. Los tipos compatibles son `batch_segmentation` y `export`. |
| `properties` | **(Obligatorio)** Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **(obligatorio cuando `type` es igual que `batch_segmentation`)** Uso `["*"]` garantiza que se incluyan todos los segmentos. |
| `schedule` | **(Obligatorio)** Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para ejecutarse una vez al día, lo que significa que no se puede programar la ejecución de un trabajo más de una vez durante un período de 24 horas. El ejemplo mostrado (`0 0 1 * * ?`) significa que el trabajo se activa todos los días a las 1.:00:00 UTC. Para obtener más información, consulte el apéndice de la [formato de expresión cron](./schedules.md#appendix) en la documentación sobre programaciones dentro de la segmentación. |
| `state` | *(Opcional)* Cadena que contiene el estado de programación. Valores disponibles: `active` y `inactive`. El valor predeterminado es `inactive`. Una organización de IMS solo puede crear una programación. Los pasos para actualizar la programación están disponibles más adelante en este tutorial. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la programación recién creada.

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{ORG_ID}",
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

De forma predeterminada, una programación está inactiva cuando se crea a menos que el `state` la propiedad se establece en `active` en el cuerpo de la solicitud create (POST). Puede activar una programación (establezca la variable `state` a `active`) realizando una solicitud de PATCH al `/config/schedules` y incluyendo el ID de la programación en la ruta.

**Formato de API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitud**

La siguiente solicitud utiliza [Formato de parche JSON](https://datatracker.ietf.org/doc/html/rfc6902) para actualizar el `state` de la programación a `active`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Para aprender a realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [Guía del usuario del Generador de segmentos](../ui/segment-builder.md).

## Apéndice

La siguiente sección enumera las preguntas más frecuentes sobre la segmentación de flujo continuo:

### ¿La &quot;incalificación&quot; de la segmentación por transmisión también se produce en tiempo real?

En la mayoría de los casos, la descalificación de la segmentación de flujo continuo se produce en tiempo real. Sin embargo, los segmentos de flujo continuo que utilizan segmentos de segmentos sí **not** no cumple los requisitos en tiempo real, en lugar de no cumplir los requisitos después de 24 horas.

### ¿En qué datos funciona la segmentación por secuencias?

La segmentación por transmisión funciona en todos los datos que se introdujeron mediante una fuente de flujo continuo. Los segmentos introducidos mediante un origen basado en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación de flujo continuo. Los eventos transmitidos al sistema con una marca de tiempo de más de 24 horas se procesarán en el siguiente trabajo por lotes.

### ¿Cómo se definen los segmentos como segmentación por lotes o de flujo continuo?

Un segmento se define como segmentación por lotes o de flujo continuo basada en una combinación de tipo de consulta y duración del historial de eventos. Puede encontrar una lista de los segmentos que se evaluarán como un segmento de flujo continuo en la [sección tipos de consulta de segmentación de flujo continuo](#query-types).

Tenga en cuenta que si un segmento contiene **both** an `inSegment` y una cadena directa de un solo evento, no se pueden calificar para la segmentación de flujo continuo. Si desea que este segmento cumpla los requisitos para la segmentación de flujo continuo, debe hacer que la cadena directa de un solo evento sea su propio segmento.

### ¿Por qué el número de segmentos &quot;cualificados totales&quot; sigue aumentando mientras que el número de &quot;Últimos X días&quot; permanece en cero en la sección de detalles del segmento?

El número total de segmentos cualificados se obtiene del trabajo diario de segmentación, que incluye audiencias que cumplen los requisitos para segmentos de flujo y por lotes. Este valor se muestra tanto para los segmentos de lote como de flujo continuo.

El número de &quot;Últimos X días&quot; **only** incluye audiencias cualificadas en segmentación de flujo continuo y **only** aumenta si ha transmitido datos al sistema y cuenta para esa definición de flujo continuo. Este valor es **only** para segmentos de flujo continuo. Como resultado, este valor **may** se muestra como 0 para los segmentos por lotes.

Como resultado, si ve que el número en &quot;Últimos X días&quot; es cero y el gráfico de líneas también está reportando cero, tiene **not** transmite todos los perfiles al sistema que cumplen los requisitos para ese segmento.