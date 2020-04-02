---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Crear un segmento
topic: tutorial
translation-type: tm+mt
source-git-commit: a6a1ecd9ce49c0a55e14b0d5479ca7315e332904

---


# Crear un segmento

Este documento proporciona un tutorial para desarrollar, probar, previsualizar y guardar una definición de segmento mediante la API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)de segmentación.

Para obtener información sobre cómo generar segmentos mediante la interfaz de usuario, consulte la guía [Generador de segmentos](../ui/overview.md).

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los distintos servicios de Adobe Experience Platform que intervienen en la creación de segmentos de audiencia. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [Perfil](../../profile/home.md)del cliente en tiempo real: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Servicio](../home.md)de segmentación de la plataforma Adobe Experience: Le permite generar segmentos de audiencia a partir de datos de Perfil del cliente en tiempo real.
- [Modelo de datos de experiencia (XDM)](../../xdm/home.md): El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

Las siguientes secciones proporcionan información adicional que deberá conocer para realizar llamadas exitosas a las API de plataforma.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

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

## Desarrollar una definición de segmento

El primer paso en la segmentación es definir un segmento, representado en una construcción denominada definición **de** segmento. Una definición de segmento es un objeto que encapsula una consulta escrita en lenguaje de Consulta de Perfil (PQL). Este objeto también se denomina predicado **PQL**. Los predicados PQL definen las reglas para el segmento en función de las condiciones relacionadas con cualquier registro o serie temporal que proporcione al Perfil del cliente en tiempo real. Consulte la guía [](../pql/overview.md) PQL para obtener más información sobre cómo escribir consultas PQL.

Puede crear una nueva definición de segmento realizando una solicitud POST al extremo en la API de Perfil del cliente en tiempo real `/segment/definitions` . El siguiente ejemplo describe cómo dar formato a una solicitud de definición, incluida la información necesaria para que un segmento se defina correctamente.

Las definiciones de segmentos se pueden evaluar de dos maneras: segmentación por lotes y segmentación de flujo. La segmentación por lotes evalúa los segmentos en función de una programación preestablecida o cuando la evaluación se activa manualmente, mientras que la segmentación por flujo continuo evalúa los segmentos tan pronto como los datos se ingieren en la plataforma. Este tutorial utilizará la segmentación por **lotes**. Para obtener más información sobre la segmentación de flujo continuo, lea la [información general sobre la segmentación](../api/streaming-segmentation.md)de flujo continuo.

**Formato API**

```http
POST /segment/definitions
```

**Solicitud**

La siguiente solicitud crea una nueva definición de segmento para un esquema llamado &quot;MiPerfil&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "My Sample Cart Abandons Segment Definition",
        "schema": {
            "name": "MyProfile",
        },
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "xEvent.metrics.commerce.abandons.value > 0",
        },
        "mergePolicyId": "mpid1",
        "description": "This Segment represents those users who have abandoned a cart"
    }'
```

| Propiedad | Descripción |
| --------- | ------------ | 
| `name` | **Requerido.** Un nombre único por el cual hacer referencia al segmento. |
| `schema` | **Requerido.** El esquema asociado a las entidades del segmento. Consiste en un `id` campo o `name` . |
| `expression` | **Requerido.** Entidad que contiene información de campos sobre la definición del segmento. |
| `expression.type` | Especifica el tipo de expresión. Actualmente, solo se admite &quot;PQL&quot;. |
| `expression.format` | Indica la estructura de la expresión en valor. Actualmente, se admite el siguiente formato: <ul><li>`pql/text`:: Representación textual de una definición de segmento, según la gramática PQL publicada.  Por ejemplo, `workAddress.stateProvince = homeAddress.stateProvince`.</li></ul> |
| `expression.value` | Una expresión que se ajusta al tipo indicado en `expression.format`. |
| `mergePolicyId` | Identificador de la directiva de combinación que se va a utilizar para los datos exportados. Para obtener más información, lea el documento [de configuración de directivas de](../../profile/api/merge-policies.md)combinación. |
| `description` | Una descripción legible de la definición. |

**Respuesta**

Una respuesta correcta devuelve los detalles de la definición de segmento recién creada, incluyendo su definición de solo lectura generada por el sistema `id` que se utilizará más adelante en este tutorial.

```json
{
    "id": "1234",
    "name": "My Sample Cart Abandons Segment Definition",
    "description": "This Segment represents those users who have abandoned a cart",
    "type": "PQL",
    "format": "pql/text",
    "expression": "xEvent.metrics.commerce.abandons.value > 0",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/core/ups/segment/definitions/1234"
        }
    }
}
```

## Calcular y previsualización de una audiencia

A medida que desarrolla la definición del segmento, puede utilizar las herramientas de estimación y previsualización dentro del Perfil del cliente en tiempo real para obtener información de nivel de resumen de vista que le ayudará a aislar la audiencia esperada. Las estimaciones proporcionan información estadística sobre una definición de segmento, como el tamaño de audiencia proyectado y el intervalo de confianza. Las Previsualizaciones proporcionan listas paginadas de perfiles de cualificación para una definición de segmento, lo que le permite comparar los resultados con lo que espera.

Al estimar y previsualizar su audiencia, puede probar y optimizar sus predicados PQL hasta que produzcan un resultado deseado, donde se pueden utilizar en una definición de segmento actualizada.

Existen dos pasos necesarios para realizar una previsualización o una estimación del segmento:

1. [Crear un trabajo de previsualización](#create-a-preview-job)
2. [previsualización](#view-an-estimate-or-preview) o estimación de Vista con el ID del trabajo de previsualización

### Cómo se generan las estimaciones

Las muestras de datos se utilizan para evaluar segmentos y estimar el número de perfiles aptos. Los nuevos datos se cargan en la memoria cada mañana (entre las 12:00 y las 2:00 PT, que es entre las 7:00 y las 9:00 UTC), y todas las consultas de segmentación se calculan utilizando los datos de muestra de ese día. En consecuencia, cualquier campo nuevo agregado o datos adicionales recopilados se reflejarán en las estimaciones al día siguiente.

El tamaño de la muestra depende del número total de entidades del almacén de perfiles. Estos tamaños de muestra se representan en la siguiente tabla:

| Entidades de la tienda de perfiles | Tamaño de la muestra |
| ------------------------- | ----------- |
| Menos de 1 millón | Conjunto de datos completo |
| 1 a 20 millones | 1 millón |
| Más de 20 millones | 5 % del total |

Las estimaciones suelen durar entre 10 y 15 segundos, comenzando con una estimación aproximada y refinándose a medida que se leen más registros.

### Crear un trabajo de previsualización

Puede crear un nuevo trabajo de previsualización realizando una solicitud POST al `/preview` extremo.

**Formato API**

```http
POST /preview
```

**Solicitud**

La siguiente solicitud crea un nuevo trabajo de previsualización. El cuerpo de la solicitud contiene la información de consulta relacionada con el segmento.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/preview \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -d '{
        "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
        "predicateType": "pql/text",
        "predicateModel": "_xdm.context.profile",
        "graphType": "simple",
        "mergeStrategy": "simple"
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `predicateExpression` | expresión de PQL para la consulta de los datos. |
| `predicateModel` | Nombre del esquema XDM en el que se basan los datos de Perfil. |

**Respuesta**

Una respuesta correcta devuelve los detalles del trabajo de previsualización recién creado, incluidos su ID y el estado de procesamiento actual.

```json
{
   "state": "RUNNING",
   "previewQueryId": "4a45e853-ac91-4bb7-a426-150937b6af5c",
   "previewQueryStatus": "RUNNING",
   "previewId": "MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg",
   "previewExecutionId": 42
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `state` | Estado actual del trabajo de previsualización. Estará en el estado &quot;EN EJECUCIÓN&quot; hasta que se complete el procesamiento, momento en el que se convierte en &quot;RESULT_READY&quot; o &quot;FALLADO&quot;. |
| `previewId` | ID del trabajo de previsualización, que se utilizará con fines de búsqueda al ver una estimación o previsualización, como se describe en la siguiente sección. |

### Vista de una estimación o previsualización

Los procesos de estimación y previsualización se ejecutan de forma asíncrona, ya que diferentes consultas pueden tardar varios períodos en completarse. Una vez iniciada la consulta, puede utilizar las llamadas de API para recuperar (GET) el estado actual de la estimación o previsualización a medida que avanza.

Mediante la API de Perfil de cliente en tiempo real, puede buscar el estado actual de un trabajo de previsualización por su ID. Si el estado es &quot;RESULT_READY&quot;, puede realizar la vista de los resultados. Dependiendo de si desea realizar una vista de una estimación o una previsualización, cada uno tiene su propio punto final en la API. A continuación se proporcionan ejemplos para ambos.

### Vista de una estimación

**Formato API**

```http
GET /estimate/{PREVIEW_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID del trabajo de previsualización que desea vista. |

**Solicitud**

La siguiente solicitud recupera una estimación, utilizando el `previewId` creado en el paso anterior.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/estimate/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la estimación.

```json
{
    "estimatedSize": 45,
    "state": "RESULT_READY",
    "profilesReadSoFar": 83834,
    "standardError": 0,
    "error": {
        "description": "",
        "traceback": ""
    },
    "profilesMatchedSoFar": 46,
    "totalRows": 82473,
    "confidenceInterval": "95%",
    "_links": {
        "preview": "https://platform.adobe.io/data/core/ups/preview?previewQueryId=f88bc056-ee48-40d5-9ddb-8865d7d6a0e0"
    }
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `state` | Estado actual del trabajo de previsualización. Se &quot;EJECUTARÁ&quot; hasta que se complete el procesamiento, momento en el que se convierte en &quot;RESULT_READY&quot; o &quot;FALLADO&quot;. |
| `_links.preview` | Cuando el estado actual del trabajo de previsualización es &quot;RESULT_READY&quot;, este atributo proporciona una URL para la vista de la estimación. |

### Vista de una previsualización

**Formato API**

```http
GET /preview/{PREVIEW_ID}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `{PREVIEW_ID}` | ID del trabajo de previsualización que desea vista. |

**Solicitud**

La siguiente solicitud recupera una previsualización, utilizando el `previewId` elemento creado en el paso anterior.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/preview/MDoyOjRhNDVlODUzLWFjOTEtNGJiNy1hNDI2LTE1MDkzN2I2YWY1Yzo0Mg \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve detalles de la previsualización.

```json
{
   "results": [{
         "XID_ADOBE-MARKETING-CLOUD-ID-1": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1",
            "endCustomerIds": {
               "XID_COOKIE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_1"
               },
               "XID_PROFILE_ID_1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_1"
               }
            }
         }
      },
      {
         "XID_COOKIE-ID-2": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE-ID-2",
            "endCustomerIds": {
               "XID_COOKIE_ID_2-1": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_COOKIE_ID_2-1"

               },
               "XID_PROFILE_ID_2": {
                  "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_PROFILE_ID_2"
               }
            }
         },
         "XID_ADOBE-MARKETING-CLOUD-ID-3": {
            "_href": "https://platform.adobe.io/data/core/ups/models/profile/XID_ADOBE-MARKETING-CLOUD-ID-1000"
         },
         "state": "RESULT_READY",
         "links": {
            "_self": "https://platform.adobe.io/data/core/ups/preview?expression=<expr-1>&limit=1000",
            "next": "",
            "prev": ""
         }
      }
   ],
   "page": {
      "offset": 0,
      "size": 3
   }
}
```

## Pasos siguientes

Una vez desarrollada, probada y guardada la definición del segmento, puede crear un trabajo de segmento para crear una audiencia mediante la API de Perfil del cliente en tiempo real. Consulte el tutorial sobre la [evaluación y el acceso a los resultados](./evaluate-a-segment.md) de los segmentos para ver los pasos detallados sobre cómo hacerlo.