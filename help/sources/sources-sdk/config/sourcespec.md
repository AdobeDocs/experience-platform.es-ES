---
keywords: Experience Platform;inicio;temas populares;fuentes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Configuración de las especificaciones de origen para orígenes de autoservicio (SDK por lotes)
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: 1fdce7c798d8aff49ab4953298ad7aa8dddb16bd
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Configuración de la especificación de origen para orígenes de autoservicio (SDK por lotes)

Las especificaciones de la fuente contienen información específica de una fuente, incluidos los atributos pertenecientes a la categoría de una fuente, el estado beta y el icono de catálogo. También contienen información útil, como parámetros de URL, contenido, encabezado y programación. Las especificaciones de origen también describen el esquema de los parámetros necesarios para crear una conexión de origen a partir de una conexión base. El esquema es necesario para crear una conexión de origen.

Consulte la [apéndice](#source-spec) para ver un ejemplo de una especificación de origen completamente rellenada.


```json
"sourceSpec": {
  "attributes": {
    "uiAttributes": {
      "isSource": true,
      "isPreview": true,
      "isBeta": true,
      "category": {
        "key": "protocols"
      },
      "icon": {
        "key": "genericRestIcon"
      },
      "description": {
        "key": "genericRestDescription"
      },
      "label": {
        "key": "genericRestLabel"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Defines static and user input parameters to fetch resource values.",
      "properties": {
        "urlParams": {
          "type": "object",
          "properties": {
            "host": {
              "type": "string",
              "description": "Enter resource url host path.",
              "example": "https://{domain}.api.mailchimp.com"
            },
            "path": {
              "type": "string",
              "description": "Enter resource path",
              "example": "/3.0/reports/campaignId/email-activity"
            },
            "method": {
              "type": "string",
              "description": "HTTP method type.",
              "enum": [
                "GET",
                "POST"
              ]
            },
            "queryParams": {
              "type": "object",
              "description": "The query parameters in json format",
            }
          },
          "required": [
            "host",
            "path",
            "method"
          ]
        },
        "headerParams": {
          "type": "object",
          "description": "The header parameters in json format",
        },
        "contentPath": {
          "type": "object",
          "description": "The parameters required for main collection content.",
          "properties": {
            "path": {
              "description": "The path to the main content.",
              "type": "string",
              "example": "$.emails"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the root content path node.",
              "example": "email"
            }
          },
          "required": [
            "path"
          ]
        },
        "explodeEntityPath": {
          "type": "object",
          "description": "The parameters required for the sub-array content.",
          "properties": {
            "path": {
              "description": "The path to the sub-array content.",
              "type": "string",
              "example": "$.email.activity"
            },
            "skipAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be skipped while fattening sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "keepAttributes": {
              "type": "array",
              "description": "The list of attributes that needs to be kept while fattening the sub-array.",
              "example": "[total_items]",
              "items": {
                "type": "string"
              }
            },
            "overrideWrapperAttribute": {
              "type": "string",
              "description": "The new name to be used for the  root content path node.",
              "example": "activity"
            }
          },
          "required": [
            "path"
          ]
        },
        "paginationParams": {
          "type": "object",
          "description": "The parameters required to fetch data using pagination.",
          "properties": {
            "type": {
              "description": "The pagination fetch type.",
              "type": "string",
              "enum": [
                "OFFSET",
                "POINTER"
              ]
            },
            "limitName": {
              "type": "string",
              "description": "The limit property name",
              "example": "limit or count"
            },
            "limitValue": {
              "type": "integer",
              "description": "The number of records to fetch per page.",
              "example": "limit=10 or count=10"
            },
            "offsetName": {
              "type": "string",
              "description": "The offset property name",
              "example": "offset"
            },
            "pointerPath": {
              "type": "string",
              "description": "The path to pointer property",
              "example": "$.paging.next"
            }
          },
          "required": [
            "type",
            "limitName",
            "limitValue"
          ]
        },
        "scheduleParams": {
          "type": "object",
          "description": "The parameters required to fetch data for batch schedule.",
          "properties": {
            "scheduleStartParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleEndParamName": {
              "type": "string",
              "description": "The order property name to get the order by date."
            },
            "scheduleStartParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            },
            "scheduleEndParamFormat": {
              "type": "string",
              "description": "The order property name to get the order by date.",
              "example": "yyyy-MM-ddTHH:mm:ssZ"
            }
          },
          "required": [
            "scheduleStartParamName",
            "scheduleEndParamName"
          ]
        }
      },
      "required": [
        "urlParams",
        "contentPath",
        "paginationParams",
        "scheduleParams"
      ]
    }
  },
}
```

| Propiedad | Descripción | Ejemplo |
| --- | --- | --- |
| `sourceSpec.attributes` | Contiene información sobre el origen específico de la interfaz de usuario o la API de. |
| `sourceSpec.attributes.uiAttributes` | Muestra información sobre el origen específico de la interfaz de usuario. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Un atributo booleano que indica si el origen requiere más comentarios de los clientes para agregar a su funcionalidad. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Define la categoría del origen. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Define el icono utilizado para la renderización del origen en la interfaz de usuario de Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Muestra una breve descripción del origen. |
| `sourceSpec.attributes.uiAttributes.label` | Muestra la etiqueta que se utilizará para la renderización del origen en la interfaz de usuario de Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contiene información sobre la ruta de acceso del recurso de URL, el método y los parámetros de consulta admitidos. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Define la ruta del recurso desde la que se recuperan los datos. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Define el método HTTP que se utilizará para realizar la solicitud al recurso para recuperar los datos. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Define los parámetros de consulta admitidos que se pueden utilizar para anexar la dirección URL de origen al realizar una solicitud de obtención de datos. **Nota**: cualquier valor de parámetro proporcionado por el usuario debe tener el formato de marcador de posición. Por ejemplo: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` se adjuntará a la dirección URL de origen como: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Define los encabezados que deben proporcionarse en la solicitud HTTP a la URL de origen al recuperar los datos. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Este atributo se puede configurar para enviar el cuerpo HTTP a través de una solicitud del POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Define el nodo que contiene la lista de elementos que se deben introducir en Platform. Este atributo debe seguir una sintaxis de ruta JSON válida y señalar a una matriz en particular. | Ver el [sección de recursos adicionales](#content-path) para ver un ejemplo del recurso contenido en una ruta de contenido. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | La ruta que señala a los registros de colección que se van a ingerir en Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Esta propiedad le permite identificar elementos específicos del recurso identificado en la ruta de contenido que se excluirán de la ingesta. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Esta propiedad permite especificar explícitamente los atributos individuales que desea conservar. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Esta propiedad permite anular el valor del nombre de atributo especificado en `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Esta propiedad permite acoplar dos matrices y transformar los datos de recursos en un recurso de plataforma. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Ruta de acceso que señala a los registros de colección que desea acoplar. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Esta propiedad permite identificar elementos específicos del recurso identificado en la ruta de entidad que se excluirán de la ingesta. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Esta propiedad permite especificar explícitamente los atributos individuales que desea conservar. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Esta propiedad permite anular el valor del nombre de atributo especificado en `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Define los parámetros o campos que se deben proporcionar para obtener un vínculo a la página siguiente desde la respuesta de página actual del usuario o durante la creación de una dirección URL de página siguiente. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Muestra el tipo de paginación compatible con el origen. | <ul><li>`OFFSET`: este tipo de paginación le permite analizar los resultados especificando un índice desde el que iniciar la matriz resultante y un límite en la cantidad de resultados devueltos.</li><li>`POINTER`: este tipo de paginación le permite utilizar un `pointer` para que apunte a un elemento concreto que debe enviarse con una solicitud. La paginación de tipo de puntero requiere una ruta en la carga útil que dirija a la página siguiente.</li><li>`CONTINUATION_TOKEN`: este tipo de paginación le permite anexar los parámetros de consulta o encabezado con un token de continuación para recuperar los datos de retorno restantes de su origen, que no se devolvieron inicialmente debido a un máximo predeterminado.</li><li>`PAGE`: este tipo de paginación le permite anexar el parámetro de consulta con un parámetro de paginación para recorrer los datos devueltos por páginas, empezando por la página cero.</li><li>`NONE`: este tipo de paginación se puede utilizar para orígenes que no admiten ninguno de los tipos de paginación disponibles. Tipo de paginación `NONE` devuelve todos los datos de respuesta después de una solicitud.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nombre del límite a través del cual la API puede especificar el número de registros que se recuperarán en una página. | `limit` o `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | El número de registros que se recuperarán en una página. | `limit=10` o `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | Nombre del atributo de desplazamiento. Esto es necesario si el tipo de paginación está establecido en `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | Nombre del atributo de puntero. Esto requiere una ruta json al atributo que señalará a la página siguiente. Esto es necesario si el tipo de paginación está establecido en `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contiene parámetros que definen los formatos de programación admitidos para el origen. Los parámetros de programación incluyen `startTime` y `endTime`, ambos le permiten establecer intervalos de tiempo específicos para ejecuciones por lotes, lo que garantiza que los registros recuperados en una ejecución por lotes anterior no se recuperen. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Define el nombre del parámetro de hora de inicio | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Define el nombre del parámetro de hora de finalización | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Define el formato admitido para `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Define el formato admitido para `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Define los parámetros proporcionados por el usuario para recuperar los valores de los recursos. | Consulte la [recursos adicionales](#user-input) por ejemplo, parámetros introducidos por el usuario para `spec.properties`. |

{style="table-layout:auto"}

## Recursos adicionales {#appendix}

En las siguientes secciones se proporciona información sobre las configuraciones adicionales que puede realizar para `sourceSpec`, incluidos la programación avanzada y los esquemas personalizados.

### Ejemplo de ruta de contenido {#content-path}

A continuación se muestra un ejemplo del contenido de `contentPath` propiedad en un [!DNL MailChimp Members] especificación de conexión.

```json
"contentPath": {
  "path": "$.members",
  "skipAttributes": [
    "_links",
    "total_items",
    "list_id"
  ],
  "overrideWrapperAttribute": "member"
}
```

### `spec.properties` ejemplo de entrada de usuario {#user-input}

El siguiente es un ejemplo de un archivo proporcionado por el usuario `spec.properties` uso de un [!DNL MailChimp Members] especificación de conexión.

En este ejemplo, `listId` se proporciona como parte de `urlParams.path`. Si necesita recuperar `listId` de un cliente, también debe definirlo como parte de `spec.properties`.


```json
"urlParams": {
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      }
"spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
```

### Ejemplo de especificación de fuente {#source-spec}

A continuación se muestra una especificación de origen completada utilizando [!DNL MailChimp Members]:

```json
  "sourceSpec": {
    "attributes": {
      "uiAttributes": {
        "isSource": true,
        "isPreview": true,
        "isBeta": true,
        "category": {
          "key": "marketingAutomation"
        },
        "icon": {
          "key": "mailchimpMembersIcon"
        },
        "description": {
          "key": "mailchimpMembersDescription"
        },
        "label": {
          "key": "mailchimpMembersLabel"
        }
      },
      "urlParams": {
        "host": "https://{domain}.api.mailchimp.com",
        "path": "/3.0/lists/${listId}/members",
        "method": "GET"
      },
      "contentPath": {
        "path": "$.members",
        "skipAttributes": [
          "_links",
          "total_items",
          "list_id"
        ],
        "overrideWrapperAttribute": "member"
      },
      "paginationParams": {
        "type": "OFFSET",
        "limitName": "count",
        "limitValue": "100",
        "offSetName": "offset"
      },
      "scheduleParams": {
        "scheduleStartParamName": "since_last_changed",
        "scheduleEndParamName": "before_last_changed",
        "scheduleStartParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK",
        "scheduleEndParamFormat": "yyyy-MM-ddTHH:mm:ss:fffffffK"
      }
    },
    "spec": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "description": "Define user input parameters to fetch resource values.",
      "properties": {
        "listId": {
          "type": "string",
          "description": "listId for which members need to fetch."
        }
      }
    }
  }
```

### Configurar diferentes tipos de paginación para el origen {#pagination}

A continuación se muestran ejemplos de otros tipos de paginación admitidos por las fuentes de autoservicio (SDK por lotes):

>[!BEGINTABS]

>[!TAB Desplazamiento]

Este tipo de paginación le permite analizar los resultados especificando un índice desde el que iniciar la matriz resultante y un límite en la cantidad de resultados devueltos. Por ejemplo:

```json
"paginationParams": {
        "type": "OFFSET",
        "limitName": "limit",
        "limitValue": "4",
        "offSetName": "offset",
        "endConditionName": "$.hasMore",
        "endConditionValue": "Const:false"
}
```

| Propiedad | Descripción |
| --- | --- |
| `type` | El tipo de paginación utilizado para devolver datos. |
| `limitName` | Nombre del límite a través del cual la API puede especificar el número de registros que se recuperarán en una página. |
| `limitValue` | El número de registros que se recuperarán en una página. |
| `offSetName` | Nombre del atributo de desplazamiento. Esto es necesario si el tipo de paginación está establecido en `offset`. |
| `endConditionName` | Un valor definido por el usuario que indica la condición que pondrá fin al bucle de paginación en la siguiente solicitud HTTP. Debe proporcionar el nombre del atributo en el que desea colocar la condición final. |
| `endConditionValue` | El valor del atributo en el que desea colocar la condición final. |

>[!TAB Puntero]

Este tipo de paginación le permite utilizar un `pointer` para que apunte a un elemento concreto que debe enviarse con una solicitud. La paginación de tipo de puntero requiere una ruta en la carga útil que dirija a la página siguiente. Por ejemplo:

```json
{
 "type": "POINTER",
 "limitName": "limit",
 "limitValue": 1,
 "pointerPath": "paging.next"
}
```

| Propiedad | Descripción |
| --- | --- |
| `type` | El tipo de paginación utilizado para devolver datos. |
| `limitName` | Nombre del límite a través del cual la API puede especificar el número de registros que se recuperarán en una página. |
| `limitValue` | El número de registros que se recuperarán en una página. |
| `pointerPath` | Nombre del atributo de puntero. Esto requiere una ruta json al atributo que señalará a la página siguiente. |

>[!TAB Token de continuación]

Un tipo de token de continuación de paginación devuelve un token de cadena que indica la existencia de más elementos que no se pudieron devolver, debido a un número máximo predeterminado de elementos que se pueden devolver en una sola respuesta.

Un origen que admite el tipo de token de continuación de paginación puede tener un parámetro de paginación similar al siguiente:

```json
"paginationParams": {
  "type": "CONTINUATION_TOKEN",
  "continuationTokenPath": "$.meta.after_cursor",
  "parameterType": "QUERYPARAM",
  "parameterName": "page[after]",
  "delayRequestMillis": "850"
}
```

| Propiedad | Descripción |
| --- | --- |
| `type` | El tipo de paginación utilizado para devolver datos. |
| `continuationTokenPath` | El valor que debe añadirse a los parámetros de consulta para pasar a la siguiente página de los resultados devueltos. |
| `parameterType` | El `parameterType` define dónde se encuentra la propiedad `parameterName` debe añadirse. El `QUERYPARAM` type le permite anexar la consulta con el `parameterName`. El `HEADERPARAM` le permite añadir su `parameterName` a su solicitud de encabezado. |
| `parameterName` | Nombre del parámetro utilizado para incorporar el token de continuación. El formato es el siguiente: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | El `delayRequestMillis` La propiedad en la paginación permite controlar la velocidad de las solicitudes realizadas al origen. Algunas fuentes pueden tener un límite en la cantidad de solicitudes que se pueden realizar por minuto. Por ejemplo, [!DNL Zendesk] tiene un límite de 100 solicitudes por minuto y define  `delayRequestMillis` hasta `850` permite configurar el origen para realizar llamadas a solo alrededor de 80 solicitudes por minuto, muy por debajo del umbral de 100 solicitudes por minuto. |

El siguiente es un ejemplo de una respuesta devuelta mediante el tipo de token de continuación de paginación:

```json
{
  "results": [
    {
      "id": 5624716025745,
      "url": "https://dev.zendesk.com/api/v2/users/5624716025745.json",
      "name": "newinctest@zenaep.com",
      "email": "newinctest@zenaep.com",
      "created_at": "2022-04-22T10:27:30Z",
      
    }
  ],
  "facets": null,
  "meta": {
    "has_more": false,
    "after_cursor": "eyJmaWVsZCI6ImNyZWF0ZWRfYXQiLCJk",
    "before_cursor": null
  },
  "links": {
    "prev": null,
    "next": "https://dev.zendesk.com/api/v2/search/export.json?filter%5Btype%5D=user&page%5Bafter%5D=eyJmaWVsZCI6"
  }
}
```

>[!TAB Activity Map]

El `PAGE` El tipo de paginación le permite recorrer los datos devueltos en función del número de páginas a partir de cero. Al utilizar `PAGE` Para la paginación de tipo, debe proporcionar el número de registros dados en una sola página.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "pageSize",
  "limitValue": 100,
  "initialPageIndex": 1,
  "endPageIndex": "headers.x-pagecount",
  "pageParamName": "pageNumber",
  "maximumRequest": 10000
}
```

| Propiedad | Descripción |
| --- | --- |
| `type` | El tipo de paginación utilizado para devolver datos. |
| `limitName` | Nombre del límite a través del cual la API puede especificar el número de registros que se recuperarán en una página. |
| `limitValue` | El número de registros que se recuperarán en una página. |
| `initialPageIndex` | (Opcional) El índice de página inicial define el número de página desde el que se iniciará la paginación. Este campo se puede utilizar para orígenes en los que la paginación no comienza desde 0. Si no se proporciona, el índice de página inicial se establecerá de forma predeterminada en 0. Este campo espera un entero. |
| `endPageIndex` | (Opcional) El índice de página final permite establecer una condición final y detener la paginación. Este campo se puede utilizar cuando las condiciones de finalización predeterminadas para detener la paginación no están disponibles. Este campo también se puede utilizar si el número de páginas que se van a introducir o el último número de página se proporcionan a través del encabezado de respuesta, que es común al utilizar `PAGE` escriba paginación. El valor del índice de página final puede ser el último número de página o un valor de expresión de tipo cadena del encabezado de respuesta. Por ejemplo, puede utilizar `headers.x-pagecount` para asignar un índice de página final a `x-pagecount` valor de los encabezados de respuesta. **Nota**: `x-pagecount` es un encabezado de respuesta obligatorio para algunas fuentes y contiene el valor número de páginas que se van a introducir. |
| `pageParamName` | Nombre del parámetro que debe anexar a los parámetros de consulta para recorrer diferentes páginas de los datos devueltos. Por ejemplo, `https://abc.com?pageIndex=1` devolvería la segunda página de la carga útil devuelta de una API. |
| `maximumRequest` | Número máximo de solicitudes que un origen puede realizar para una ejecución incremental determinada. El límite predeterminado actual es 10000. |

{style="table-layout:auto"}


>[!TAB Ninguna]

El `NONE` el tipo de paginación se puede utilizar para orígenes que no admiten ninguno de los tipos de paginación disponibles. Orígenes que utilizan el tipo de paginación de `NONE` simplemente devuelva todos los registros recuperables cuando se realice una solicitud de GET.

```json
"paginationParams": {
  "type": "NONE"
}
```

>[!ENDTABS]

### Programación avanzada de orígenes de autoservicio (SDK por lotes)

Configure la programación incremental y de relleno del origen mediante la programación avanzada. El `incremental` permite configurar una programación en la que el origen solo ingestará registros nuevos o modificados, mientras que la propiedad `backfill` La propiedad permite crear una programación para introducir datos históricos.

Con la programación avanzada, puede utilizar expresiones y funciones específicas del origen para configurar programaciones incrementales y de relleno. En el ejemplo siguiente, la variable [!DNL Zendesk] El origen requiere que la programación incremental tenga el formato `type:user updated > {START_TIME} updated < {END_TIME}` y relleno como `type:user updated < {END_TIME}`.

```json
"scheduleParams": {
        "type": "ADVANCE",
        "paramFormat": "yyyy-MM-ddTHH:mm:ssK",
        "incremental": "type:user updated > {START_TIME} updated < {END_TIME}",
        "backfill": "type:user updated < {END_TIME}"
      }
```

| Propiedad | Descripción |
| --- | --- |
| `scheduleParams.type` | El tipo de programación que utilizará el origen. Establezca este valor en `ADVANCE` para utilizar el tipo de programación avanzada. |
| `scheduleParams.paramFormat` | El formato definido del parámetro de programación. Este valor puede ser el mismo que el de la fuente `scheduleStartParamFormat` y `scheduleEndParamFormat` valores. |
| `scheduleParams.incremental` | La consulta incremental del origen. Incremental hace referencia a un método de ingesta en el que solo se incorporan datos nuevos o modificados. |
| `scheduleParams.backfill` | La consulta de relleno del origen. El relleno se refiere a un método de ingesta en el que se ingieren datos históricos. |

Una vez configurada la programación avanzada, debe consultar la `scheduleParams` en la sección URL, body o header params, según lo que admita la fuente concreta. En el ejemplo siguiente, `{SCHEDULE_QUERY}` es un marcador de posición que se utiliza para especificar dónde se utilizarán las expresiones de programación incremental y de relleno. En el caso de un [!DNL Zendesk] origen, `query` se utiliza en la `queryParams` para especificar la programación avanzada.

```json
"urlParams": {
        "path": "/api/v2/search/export@{if(empty(coalesce(pipeline()?.parameters?.ingestionStart,'')),'?query=type:user&filter[type]=user&','')}",
        "method": "GET",
        "queryParams": {
          "query": "{SCHEDULE_QUERY}",
          "filter[type]": "user"
        }
      }
```

### Añada un esquema personalizado para definir los atributos dinámicos del origen

Puede incluir un esquema personalizado en su `sourceSpec` para definir todos los atributos necesarios para el origen, incluidos los atributos dinámicos que pueda necesitar. Puede actualizar la especificación de conexión correspondiente del origen realizando una solicitud del PUT al `/connectionSpecs` punto final del [!DNL Flow Service] API, mientras proporciona su esquema personalizado en la `sourceSpec` de la especificación de conexión.

A continuación se muestra un ejemplo de esquema personalizado que puede agregar a la especificación de conexión del origen:

```json
      "schema": {
        "type": "object",
        "properties": {
          "results": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "organization_id": {
                  "type": "integer",
                  "minimum": -9007199254740992,
                  "maximum": 9007199254740991
                }
                "active": {
                  "type": "boolean"
                },
                "created_at": {
                  "type": "string"
                },
                "email": {
                  "type": "string"
                },
                "iana_time_zone": {
                  "type": "string"
                },
                "id": {
                  "type": "integer"
                },
                "locale": {
                  "type": "string"
                },
                "locale_id": {
                  "type": "integer"
                },
                "moderator": {
                  "type": "boolean"
                },
                "name": {
                  "type": "string"
                },
                "only_private_comments": {
                  "type": "boolean"
                },
                "report_csv": {
                  "type": "boolean"
                },
                "restricted_agent": {
                  "type": "boolean"
                },
                "result_type": {
                  "type": "string"
                },
                "role": {
                  "type": "integer"
                },
                "shared": {
                  "type": "boolean"
                },
                "shared_agent": {
                  "type": "boolean"
                },
                "suspended": {
                  "type": "boolean"
                },
                "ticket_restriction": {
                  "type": "string"
                },
                "time_zone": {
                  "type": "string"
                },
                "two_factor_auth_enabled": {
                  "type": "boolean"
                },
                "updated_at": {
                  "type": "string"
                },
                "url": {
                  "type": "string"
                },
                "verified": {
                  "type": "boolean"
                },
                "tags": {
                  "type": "array",
                  "items": {
                    "type": "string"
                  }
                }
              }
            }
          }
        }
      }
```


## Pasos siguientes

Una vez rellenadas las especificaciones de origen, puede continuar con la configuración de las especificaciones de exploración del origen que desea integrar en Platform. Consulte el documento sobre [configuración de especificaciones de exploración](./explorespec.md) para obtener más información.
