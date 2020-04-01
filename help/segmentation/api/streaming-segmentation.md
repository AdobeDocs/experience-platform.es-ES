---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Segmentación por flujo continuo
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Evaluar eventos en tiempo real con segmentación de flujo continuo (Beta)

>[!NOTE] La segmentación por flujo continuo es una función beta y estará disponible bajo petición.

La segmentación por flujo continuo (también conocida como evaluación continua de consultas) es la capacidad de evaluar instantáneamente a un cliente en cuanto un evento entra en un grupo de segmentos en particular. Con esta capacidad, la mayoría de las reglas de segmentos ahora se pueden evaluar a medida que los datos se pasan a Adobe Experience Platform, lo que significa que la pertenencia a segmentos se mantendrá actualizada sin ejecutar trabajos de segmentación programados.

![](../images/api/streaming-segment-evaluation.png)

## Primeros pasos

Esta guía para desarrolladores requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform relacionados con la segmentación por flujo continuo. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de cliente unificado en tiempo real, basado en datos agregados de varias fuentes.
- [Segmentación](../home.md): Proporciona la capacidad de crear segmentos y audiencias a partir de los datos de Perfil del cliente en tiempo real.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API de plataforma.

### Leer llamadas de API de muestra

Esta guía para desarrolladores proporciona llamadas de API de ejemplo para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

- Autorización: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Para obtener más información sobre los entornos limitados en la plataforma, consulte la documentación [general del](../../sandboxes/home.md)entorno limitado.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado adicional:

- Content-Type: application/json

Es posible que se requieran encabezados adicionales para completar solicitudes específicas. Los encabezados correctos se muestran en cada uno de los ejemplos de este documento. Preste especial atención a las solicitudes de muestra para asegurarse de que se incluyen todos los encabezados necesarios.

### Tipos de consulta habilitados para la segmentación por flujo

La siguiente tabla lista los diferentes tipos de consultas de segmentación y si admiten o no la segmentación de flujo.

| Tipo de Consulta | consulta de muestra | Segmentación por flujo continuo admitida |
| ---------- | ------------ | --------------------------------- |
| Demografía simple | &quot;Dame a todas las personas cuya dirección está en Canadá&quot;. | Compatible |
| eventos de series temporales | &quot;Dame a todas las personas que descargaron Lightroom&quot;. | Compatible |
| Demografía y series cronológicas | &quot;Denme a todas las personas que viven en Canadá y han hecho un pedido en los últimos 30 días&quot;. | Compatible |
| Ausencia de eventos | &quot;Dadme a todas las personas que han abandonado dos carros separados dentro de dos días entre sí&quot;. | Compatible |
| Varias entidades | &quot;Dame a todas las personas cuyo tipo de asignación de derechos sea &#39;Experienciado&#39;&quot;. | No admitido |
| Funciones avanzadas de PQL | &quot;Dame todos los perfiles que hicieron un pedido la semana pasada, e incluye el SKU y el nombre de todos los productos comprados&quot;. | No admitido |

## Recuperar todos los segmentos habilitados para la segmentación de flujo continuo

Antes de crear un nuevo segmento habilitado para flujo continuo o actualizar un segmento existente para que se pueda transmitir por flujo continuo, debe asegurarse de que no está duplicando información recuperando una lista de todos los segmentos habilitados para flujo continuo.

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
  -H 'x-sandbox-name: {SANDBOX_NAME'
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

Después de confirmar que el segmento que desea crear no existe aún, puede crear un nuevo segmento que esté habilitado para la segmentación de flujo continuo.

**Formato API**

```http
POST /segment/definitions
```

**Solicitud**

La siguiente solicitud crea un nuevo segmento que está habilitado para la segmentación de flujo. Note that the `continuous` section is set to `enabled: true`.

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

>[!NOTE] Se trata de una solicitud estándar de &quot;crear un segmento&quot;, con el parámetro agregado de la `continuous` sección definido como `enabled: true`. Para obtener más información sobre la creación de una definición de segmento, lea la documentación sobre la creación [de](../tutorials/create-a-segment.md)segmentos.

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

## Habilitar un segmento existente para la segmentación de flujo continuo

Puede habilitar un segmento existente para la segmentación de flujo continuo suministrando el ID de la definición del segmento en la ruta de una solicitud PATCH. Además, la carga útil de esta solicitud PATCH debe incluir todos los detalles de la definición de segmento existente, a la que se puede acceder mediante una solicitud GET a la definición de segmento en cuestión.

### Buscar una definición de segmento existente

Para buscar una definición de segmento existente, debe proporcionar su ID en la ruta de una solicitud GET.

**Formato API**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | ID de la definición de segmento que desea buscar. |

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004\
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devolverá detalles de la definición del segmento solicitada.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "sandbox": {
        "sandboxId": "",
        "sandboxName": "",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    }
}
```

>[!NOTE] Para la siguiente solicitud, necesitará los detalles completos de la definición del segmento que se devolvieron en esta respuesta. Por favor, copie los detalles de esta respuesta para utilizarla en el cuerpo de la siguiente solicitud.

### Habilitar el segmento existente para la segmentación de flujo continuo

Ahora que conoce los detalles del segmento que desea actualizar, puede realizar una solicitud PATCH para actualizar el segmento a fin de habilitar la segmentación de flujo.

**Formato API**

```http
PATCH /segment/definitions/{SEGMENT_DEFINITION_ID}
```

**Solicitud**

La carga útil de la siguiente solicitud proporciona los detalles de la definición del segmento (obtenida en el paso [](#look-up-an-existing-segment-definition)anterior) y la actualiza cambiando su `continuous.enabled` propiedad a `true`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/segment/definitions/15063cb-2da8-4851-a2e2-bf59ddd2f004 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -d '{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "mergePolicyId": "50de2f9c-990c-4b96-945f-9570337ffe6d",
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

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición del segmento recién actualizada.

```json
{
    "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "4A21D36B544916100A4C98A7@AdobeOrg",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "TestStreaming1",
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
    },
    "creationTime": 1572029711000,
    "updateEpoch": 1572029712000,
    "updateTime": 1572029712000
}
```

## Habilitar evaluación programada

Una vez habilitada la evaluación de flujo continuo, se debe crear una línea de base (después de la cual el segmento siempre estará actualizado). Esto lo hace automáticamente el sistema, sin embargo, la evaluación programada (también conocida como segmentación programada) debe habilitarse primero para que se produzca la conexión de base.

Con la segmentación programada, su organización de IMS puede crear una programación recurrente para ejecutar automáticamente trabajos de exportación para evaluar segmentos.

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

## Pasos siguientes

Ahora que ha habilitado segmentos nuevos y existentes para la segmentación de flujo continuo y ha habilitado la segmentación programada para desarrollar una línea de base y realizar evaluaciones recurrentes, puede empezar a crear segmentos para su organización.

Para obtener información sobre cómo realizar acciones similares y trabajar con segmentos mediante la interfaz de usuario de Adobe Experience Platform, visite la guía [de usuario del Generador de](../ui/overview.md)segmentos.