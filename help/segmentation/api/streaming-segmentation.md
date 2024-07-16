---
solution: Experience Platform
title: Evaluar eventos en tiempo casi real con segmentación de streaming
description: Este documento contiene ejemplos sobre cómo utilizar la segmentación de flujo continuo con la API del servicio de segmentación de Adobe Experience Platform.
role: Developer
exl-id: 119508bd-5b2e-44ce-8ebf-7aef196abd7a
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 4%

---

# Evaluar eventos en tiempo casi real con segmentación de streaming

>[!NOTE]
>
>El siguiente documento indica cómo utilizar la segmentación de flujo continuo mediante la API. Para obtener información sobre el uso de la segmentación de transmisión por secuencias con la interfaz de usuario, lea la [guía de la interfaz de usuario de segmentación por transmisión](../ui/streaming-segmentation.md).

La segmentación de streaming en [!DNL Adobe Experience Platform] permite a los clientes realizar la segmentación en tiempo casi real al tiempo que se centran en la riqueza de datos. Con la segmentación por streaming, la calificación de segmentos ahora se produce cuando los datos de streaming llegan a [!DNL Platform], lo que alivia la necesidad de programar y ejecutar trabajos de segmentación. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a [!DNL Platform], lo que significa que el abono a segmentos se mantendrá actualizado sin ejecutar trabajos de segmentación programados.

![](../images/api/streaming-segment-evaluation.png)

>[!NOTE]
>
>La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los segmentos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión.
>
>Además, las definiciones de segmentos evaluadas con la segmentación de flujo continuo pueden variar entre la pertenencia ideal y real si la definición del segmento se basa en otra definición de segmento que se evalúa mediante la segmentación por lotes. Por ejemplo, si el segmento A se basa en el segmento B y el segmento B se evalúa mediante la segmentación por lotes, ya que el segmento B solo se actualiza cada 24 horas, el segmento A se alejará más de los datos reales hasta que se vuelva a sincronizar con la actualización del segmento B.

## Introducción

Esta guía para desarrolladores requiere una comprensión práctica de los distintos servicios de [!DNL Adobe Experience Platform] relacionados con la segmentación de flujo continuo. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona un perfil de consumidor unificado en tiempo real, basado en los datos agregados de varias fuentes.
- [[!DNL Segmentation]](../home.md): proporciona la capacidad de crear audiencias utilizando definiciones de segmento y otros orígenes externos a partir de los datos de [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente.

Las secciones siguientes proporcionan información adicional que necesitará saber para poder realizar llamadas exitosas a [!DNL Platform] API.

### Lectura de llamadas de API de muestra

Esta guía para desarrolladores proporciona ejemplos de llamadas a la API para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas de [!DNL Experience Platform].

### Recopilación de valores para los encabezados obligatorios

Para poder realizar llamadas a las API de [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados obligatorios en todas las llamadas de API de [!DNL Experience Platform], como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos los recursos de [!DNL Experience Platform] están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de [!DNL Platform] requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en [!DNL Platform], consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

Es posible que se requieran encabezados adicionales para completar solicitudes específicas. Los encabezados correctos se muestran en cada uno de los ejemplos de este documento. Preste especial atención a las solicitudes de ejemplo para asegurarse de que se incluyen todos los encabezados obligatorios.

### Tipos de consulta habilitados para segmentación de streaming {#query-types}

>[!NOTE]
>
>Deberá habilitar la segmentación programada para la organización a fin de que la segmentación de streaming funcione. Encontrará información sobre cómo habilitar la segmentación programada en la sección [habilitar segmentación programada](#enable-scheduled-segmentation)

Para que una definición de segmento se evalúe mediante la segmentación de flujo continuo, la consulta debe cumplir las siguientes directrices.

| Tipo de consulta | Detalles |
| ---------- | ------- |
| Evento único | Cualquier definición de segmento que haga referencia a un único evento entrante sin restricción horaria. |
| Evento único dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un único evento entrante. |
| Evento único con una ventana de tiempo | Cualquier definición de segmento que haga referencia a un único evento entrante con un intervalo de tiempo. |
| Solo perfil | Cualquier definición de segmento que haga referencia únicamente a un atributo de perfil. |
| Evento único con un atributo de perfil en un intervalo de tiempo relativo inferior a 24 horas | Cualquier definición de segmento que haga referencia a un único evento entrante, con uno o más atributos de perfil, y que se produzca en un intervalo de tiempo relativo inferior a 24 horas. |
| Segmento de segmentos | Cualquier definición de segmento que contenga uno o más segmentos de flujo continuo o por lotes. **Nota:** Si se usa un segmento de segmentos, la descalificación del perfil se producirá **cada 24 horas**. |
| Varios eventos con un atributo de perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tenga uno o más atributos de perfil. |

Una definición de segmento **no** se habilitará para la segmentación de flujo continuo en los siguientes casos:

- La definición del segmento incluye segmentos o rasgos de Adobe Audience Manager AAM ().
- La definición del segmento incluye varias entidades (consultas de varias entidades).
- La definición del segmento incluye una combinación de un solo evento y un evento `inSegment`.
   - Sin embargo, si el segmento contenido en el evento `inSegment` es solo de perfil, la definición del segmento **se habilitará** para la segmentación de flujo continuo.
- La definición del segmento utiliza &quot;Ignorar año&quot; como parte de sus restricciones de tiempo.

Tenga en cuenta las siguientes directrices a la hora de realizar la segmentación por streaming:

| Tipo de consulta | Pauta |
| ---------- | -------- |
| Consulta de evento único | No hay límites en la ventana retrospectiva. |
| Consulta con historial de eventos | <ul><li>La ventana retrospectiva está limitada a **un día**.</li><li>Debe **existir una condición de orden de tiempo estricta entre los eventos.**</li><li>Se admiten consultas con al menos un evento denegado. Sin embargo, todo el evento **no puede** ser una negación.</li></ul> |

Si se modifica una definición de segmento para que ya no cumpla los criterios de segmentación de flujo continuo, la definición de segmento cambiará automáticamente de &quot;Flujo&quot; a &quot;Lote&quot;.

Además, la descalificación de segmentos, de manera similar a la calificación de segmentos, se produce en tiempo real. Como resultado, si un perfil ya no cumple los requisitos para una definición de segmento, se descalifica inmediatamente. Por ejemplo, si la definición del segmento solicita &quot;Todos los usuarios que compraron zapatos rojos en las últimas tres horas&quot;, después de tres horas, todos los perfiles que inicialmente se calificaron para la definición del segmento serán no calificados.

## Recupere todas las definiciones de segmentos habilitadas para la segmentación de streaming

Puede recuperar una lista de todas las definiciones de segmentos que están habilitadas para la segmentación de flujo continuo dentro de su organización realizando una solicitud de GET al extremo `/segment/definitions`.

**Formato de API**

Para recuperar las definiciones de segmento habilitadas para flujo continuo, debe incluir el parámetro de consulta `evaluationInfo.continuous.enabled=true` en la ruta de solicitud.

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

Una respuesta correcta devuelve una matriz de definiciones de segmentos en su organización que están habilitadas para la segmentación de flujo continuo.

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

## Creación de una definición de segmento habilitada para streaming

Una definición de segmento se habilitará automáticamente si coincide con uno de los [tipos de segmentación de transmisión enumerados arriba](#query-types).

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
    }
}'
```

>[!NOTE]
>
>Esta es una solicitud estándar de &quot;creación de definición de segmento&quot;. Para obtener más información acerca de cómo crear una definición de segmento, lea el tutorial sobre [creación de una definición de segmento](../tutorials/create-a-segment.md).

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición del segmento habilitado para flujo continuo recién creada.

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

Una vez habilitada la evaluación de la transmisión, se debe crear una línea de base (después de la cual la definición del segmento siempre estará actualizada). La evaluación programada (también conocida como segmentación programada) debe habilitarse primero para que el sistema realice la línea de base automáticamente. Con la segmentación programada, su organización puede adherirse a una programación recurrente para ejecutar automáticamente los trabajos de exportación y evaluar las definiciones de segmentos.

>[!NOTE]
>
>La evaluación programada se puede habilitar para las zonas protegidas con un máximo de cinco (5) políticas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco políticas de combinación para [!DNL XDM Individual Profile] en un solo entorno de zona protegida, no podrá utilizar la evaluación programada.

### Creación de una programación

Al realizar una solicitud de POST al extremo `/config/schedules`, puede crear una programación e incluir la hora específica en que se debe activar la programación.

**Formato de API**

```http
POST /config/schedules
```

**Solicitud**

La siguiente solicitud crea un nuevo programa basado en las especificaciones proporcionadas en la carga útil.

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
| `name` | **(Obligatorio)** El nombre de la programación. Debe ser una cadena. |
| `type` | **(Obligatorio)** El tipo de trabajo en formato de cadena. Los tipos compatibles son `batch_segmentation` y `export`. |
| `properties` | **(Obligatorio)** Un objeto que contiene propiedades adicionales relacionadas con la programación. |
| `properties.segments` | **(Necesario cuando `type` es igual a `batch_segmentation`)** Si se usa `["*"]`, se garantiza que se incluyan todas las definiciones de segmentos. |
| `schedule` | **(Obligatorio)** Una cadena que contiene la programación del trabajo. Los trabajos solo se pueden programar para que se ejecuten una vez al día, lo que significa que no puede programar un trabajo para que se ejecute más de una vez durante un período de 24 horas. El ejemplo mostrado (`0 0 1 * * ?`) significa que el trabajo se activa todos los días a las 1:00:00 UTC. Para obtener más información, consulte el apéndice sobre el [formato de expresión cron](./schedules.md#appendix) en la documentación sobre programaciones dentro de la segmentación. |
| `state` | *(Opcional)* Cadena que contiene el estado de programación. Valores disponibles: `active` y `inactive`. El valor predeterminado es `inactive`. Una organización solo puede crear una programación. Los pasos para actualizar la programación están disponibles más adelante en este tutorial. |

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

### Habilitar una programación

De manera predeterminada, una programación está inactiva cuando se crea a menos que la propiedad `state` se establezca en `active` en el cuerpo de la solicitud de creación (POST). Puede habilitar una programación (establecer `state` en `active`) realizando una solicitud de PATCH al extremo `/config/schedules` e incluyendo el ID de la programación en la ruta de acceso.

**Formato de API**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**Solicitud**

La siguiente solicitud usa el formato de [parche JSON](https://datatracker.ietf.org/doc/html/rfc6902) para actualizar `state` de la programación a `active`.

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

Una actualización correcta devuelve un cuerpo de respuesta vacío y un estado HTTP 204 (sin contenido).

Se puede utilizar la misma operación para desactivar una programación sustituyendo el &quot;valor&quot; de la solicitud anterior por &quot;inactivo&quot;.

## Pasos siguientes

Ahora que ha habilitado definiciones de segmentos nuevas y existentes para la segmentación de flujo continuo, y ha habilitado la segmentación programada para desarrollar una línea de base y realizar evaluaciones recurrentes, puede empezar a crear definiciones de segmentos habilitadas para flujo continuo para su organización.

Para aprender a realizar acciones similares y trabajar con definiciones de segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la [guía del usuario del Generador de segmentos](../ui/segment-builder.md).

## Apéndice

En la siguiente sección se enumeran las preguntas más frecuentes sobre la segmentación de streaming:

### ¿La &quot;descalificación&quot; de la segmentación de streaming también se produce en tiempo real?

En la mayoría de los casos, la descalificación de la segmentación de streaming se produce en tiempo real. Sin embargo, las definiciones de segmentos de streaming que usan segmentos de segmentos **no** descalifican en tiempo real, en lugar de descalificar después de 24 horas.

### ¿En qué datos funciona la segmentación por streaming?

La segmentación por flujo funciona en todos los datos que se ingirieron con una fuente de flujo continuo. Los segmentos ingeridos mediante una fuente basada en lotes se evaluarán todas las noches, incluso si cumplen los requisitos para la segmentación por transmisión. Los eventos transmitidos al sistema con una marca de tiempo de más de 24 horas se procesarán en el trabajo por lotes siguiente.

### ¿Cómo se definen las definiciones de segmentos como segmentación por lotes o de flujo continuo?

Una definición de segmento se define como segmentación por lotes o de flujo continuo basada en una combinación de tipo de consulta y duración del historial de eventos. Se puede encontrar una lista de las definiciones de segmentos que se evaluarán como segmento de flujo continuo en la [sección de tipos de consulta de segmentación de flujo continuo](#query-types).

Tenga en cuenta que si un segmento contiene **tanto** como una expresión `inSegment` y una cadena de evento único directa, no puede calificar para la segmentación de flujo continuo. Si desea que esta definición de segmento cumpla los requisitos de la segmentación de flujo continuo, debe hacer de la cadena de evento único directo su propia definición de segmento.

### ¿Por qué sigue aumentando el número de definiciones de segmento &quot;cualificadas totales&quot; mientras que el número de &quot;últimos X días&quot; permanece en cero dentro de la sección de detalles de la definición del segmento?

El número total de definiciones de segmentos cualificados se obtiene del trabajo de segmentación diario, que incluye audiencias que cumplen los requisitos para las definiciones de segmentos por lotes y de flujo continuo. Este valor se muestra para las definiciones de segmentos por lotes y de flujo continuo.

El número bajo los &quot;últimos X días&quot; **solo** incluye audiencias que se califican en la segmentación por transmisión y **solo** aumenta si ha transmitido datos al sistema y cuenta para esa definición de transmisión. Este valor se muestra **solamente** para las definiciones de segmentos de streaming. Como resultado, este valor **may** se muestra como 0 para las definiciones de segmentos por lotes.

Como resultado, si ve que el número bajo &quot;Últimos X días&quot; es cero y el gráfico de líneas también informa cero, tiene **no** transmitido ningún perfil al sistema que cumpla con esa definición de segmento.

### ¿Cuánto tiempo tarda una definición de segmento en estar disponible?

Una definición de segmento tarda hasta una hora en estar disponible.

### ¿Existen limitaciones a los datos que se transmiten en?

Para que los datos transmitidos se usen en la segmentación de flujo continuo, **debe** haber un espacio entre los eventos transmitidos. Si se transmiten demasiados eventos en el mismo segundo, Platform los tratará como datos generados por bots y se descartarán. Como práctica recomendada, debe tener **al menos** cinco segundos entre los datos de evento para asegurarse de que los datos se utilizan correctamente.
