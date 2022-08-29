---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Configuración de especificaciones de origen para fuentes de autoservicio (SDK por lotes)
topic-legacy: overview
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar fuentes de autoservicio (SDK por lotes).
exl-id: f814c883-b529-4ecc-bedd-f638bf0014b5
source-git-commit: adaa0e1a63536bc1fdf751eec477e5cda9fd20ae
workflow-type: tm+mt
source-wordcount: '1690'
ht-degree: 1%

---

# Configuración de la especificación de origen para orígenes de autoservicio (SDK por lotes)

Las especificaciones de origen contienen información específica de una fuente, incluidos los atributos que pertenecen a la categoría de la fuente, el estado beta y el icono de catálogo. También contienen información útil, como parámetros de URL, contenido, encabezado y programación. Las especificaciones de origen también describen el esquema de los parámetros necesarios para crear una conexión de origen a partir de una conexión base. El esquema es necesario para crear una conexión de origen.

Consulte la [apéndice](#source-spec) para ver un ejemplo de una especificación de origen totalmente rellenada.


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
| `sourceSpec.attributes` | Contiene información sobre la fuente específica de la interfaz de usuario o la API. |
| `sourceSpec.attributes.uiAttributes` | Muestra información sobre la fuente específica de la interfaz de usuario. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Un atributo booleano que indica si la fuente requiere más comentarios de los clientes para agregar a su funcionalidad. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Define la categoría del origen. | <ul><li>`advertising`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Define el icono utilizado para procesar el origen en la interfaz de usuario de Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Muestra una breve descripción de la fuente. |
| `sourceSpec.attributes.uiAttributes.label` | Muestra la etiqueta que se utilizará para procesar el origen en la interfaz de usuario de Platform. |
| `sourceSpec.attributes.spec.properties.urlParams` | Contiene información sobre la ruta de acceso del recurso de URL, el método y los parámetros de consulta admitidos. |
| `sourceSpec.attributes.spec.properties.urlParams.properties.path` | Define la ruta del recurso desde donde recuperar los datos. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.method` | Define el método HTTP que se utilizará para realizar la solicitud al recurso para recuperar datos. | `GET`, `POST` |
| `sourceSpec.attributes.spec.properties.urlParams.properties.queryParams` | Define los parámetros de consulta admitidos que se pueden usar para anexar la dirección URL de origen al realizar una solicitud para recuperar datos. **Nota**: Cualquier valor de parámetro proporcionado por el usuario debe tener el formato de marcador de posición. Por ejemplo: `${USER_PARAMETER}`. | `"queryParams" : {"key" : "value", "key1" : "value1"}` se adjuntará a la URL de origen como: `/?key=value&key1=value1` |
| `sourceSpec.attributes.spec.properties.spec.properties.headerParams` | Define los encabezados que se deben proporcionar en la solicitud HTTP para crear la URL al recuperar datos. | `"headerParams" : {"Content-Type" : "application/json", "x-api-key" : "key"}` |
| `sourceSpec.attributes.spec.properties.bodyParams` | Este atributo se puede configurar para enviar cuerpo HTTP a través de una solicitud de POST. |
| `sourceSpec.attributes.spec.properties.contentPath` | Define el nodo que contiene la lista de elementos necesarios para su ingesta en Platform. Este atributo debe seguir una sintaxis de ruta JSON válida y debe señalar a una matriz concreta. | Consulte la [sección de recursos adicionales](#content-path) para ver un ejemplo del recurso contenido en una ruta de contenido. |
| `sourceSpec.attributes.spec.properties.contentPath.path` | La ruta que señala a los registros de recopilación que se van a introducir en Platform. | `$.emails` |
| `sourceSpec.attributes.spec.properties.contentPath.skipAttributes` | Esta propiedad le permite identificar elementos específicos del recurso identificado en la ruta de contenido que se van a excluir de la ingesta. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.keepAttributes` | Esta propiedad le permite especificar explícitamente los atributos individuales que desea conservar. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.contentPath.overrideWrapperAttribute` | Esta propiedad permite anular el valor del nombre de atributo especificado en `contentPath`. | `email` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath` | Esta propiedad le permite acoplar dos matrices y transformar los datos de recursos en recursos de Platform. |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.path` | Ruta que señala a los registros de recopilación que desea acoplar. | `$.email.activity` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.skipAttributes` | Esta propiedad permite identificar elementos específicos del recurso identificado en la ruta de entidad que se van a excluir de la ingesta. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.keepAttributes` | Esta propiedad le permite especificar explícitamente los atributos individuales que desea conservar. | `[total_items]` |
| `sourceSpec.attributes.spec.properties.explodeEntityPath.overrideWrapperAttribute` | Esta propiedad permite anular el valor del nombre de atributo especificado en `explodeEntityPath`. | `activity` |
| `sourceSpec.attributes.spec.properties.paginationParams` | Define los parámetros o campos que deben suministrarse para obtener un vínculo a la página siguiente desde la respuesta de página actual del usuario, o al crear una URL de página siguiente. |
| `sourceSpec.attributes.spec.properties.paginationParams.type` | Muestra el tipo de paginación compatible con el origen. | <ul><li>`OFFSET`: Este tipo de paginación le permite analizar los resultados especificando un índice desde donde iniciar la matriz resultante y un límite en cuanto a cuántos resultados se devuelven.</li><li>`POINTER`: Este tipo de paginación le permite utilizar un `pointer` para que apunten a un elemento en particular que debe enviarse con una solicitud. La paginación del tipo de puntero requiere una ruta en la carga útil que señala a la página siguiente.</li><li>`CONTINUATION_TOKEN`: Este tipo de paginación le permite anexar los parámetros de consulta o encabezado con un token de continuación para recuperar los datos devueltos restantes de su origen, que inicialmente no se devolvieron debido a un máximo predeterminado.</li><li>`PAGE`: Este tipo de paginación le permite anexar su parámetro de consulta con un parámetro de paginación para recorrer los datos devueltos por páginas, empezando desde la página cero.</li><li>`NONE`: Este tipo de paginación se puede utilizar para orígenes que no admiten ninguno de los tipos de paginación disponibles. Tipo de paginación `NONE` devuelve todos los datos de respuesta después de una solicitud.</li></ul> |
| `sourceSpec.attributes.spec.properties.paginationParams.limitName` | Nombre del límite mediante el cual la API puede especificar el número de registros que se recuperarán en una página. | `limit` o `count` |
| `sourceSpec.attributes.spec.properties.paginationParams.limitValue` | Número de registros que se van a recuperar en una página. | `limit=10` o `count=10` |
| `sourceSpec.attributes.spec.properties.paginationParams.offSetName` | El nombre del atributo de desplazamiento. Esto es necesario si el tipo de paginación está establecido en `offset`. | `offset` |
| `sourceSpec.attributes.spec.properties.paginationParams.pointerPath` | El nombre del atributo del puntero. Esto requiere una ruta json al atributo que apuntará a la página siguiente. Esto es necesario si el tipo de paginación está establecido en `pointer`. | `pointer` |
| `sourceSpec.attributes.spec.properties.scheduleParams` | Contiene parámetros que definen formatos de programación admitidos para el origen. Los parámetros de programación incluyen `startTime` y `endTime`, ambos permiten establecer intervalos de tiempo específicos para ejecuciones por lotes, lo que garantiza que los registros recuperados en una ejecución por lotes anterior no se recuperen de nuevo. |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamName` | Define el nombre del parámetro de hora de inicio | `since_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamName` | Define el nombre del parámetro de hora de finalización | `before_last_changed` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleStartParamFormat` | Define el formato admitido para la variable `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.spec.properties.scheduleParams.scheduleEndParamFormat` | Define el formato admitido para la variable `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Define los parámetros proporcionados por el usuario para recuperar valores de recursos. | Consulte la [recursos adicionales](#user-input) para ver un ejemplo de parámetros introducidos por el usuario para `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Recursos adicionales {#appendix}

Las secciones siguientes proporcionan información sobre las configuraciones adicionales que puede realizar en su `sourceSpec`, incluidos esquemas personalizados y de programación avanzados.

### Ejemplo de ruta de contenido {#content-path}

El siguiente es un ejemplo del contenido de la variable `contentPath` propiedad en un [!DNL MailChimp Members] especificación de conexión.

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

A continuación se muestra un ejemplo de `spec.properties` usando un [!DNL MailChimp Members] especificación de conexión.

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

### Ejemplo de especificación de origen {#source-spec}

A continuación se muestra una especificación de origen completada que utiliza [!DNL MailChimp Members]:

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

A continuación se muestran algunos ejemplos de otros tipos de paginación compatibles con las fuentes de autoservicio (SDK por lotes):

#### `CONTINUATION_TOKEN`

Un tipo de token de continuación de paginación devuelve un token de cadena que significa la existencia de más elementos que no se pudieron devolver, debido a un número máximo predeterminado de elementos que se pueden devolver en una única respuesta.

Una fuente que admita el tipo de token de continuación pagination puede tener un parámetro de paginación similar a:

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
| `type` | Tipo de paginación que se utiliza para devolver datos. |
| `continuationTokenPath` | El valor que debe añadirse a los parámetros de consulta para pasar a la siguiente página de los resultados devueltos. |
| `parameterType` | La variable `parameterType` define dónde `parameterName` debe añadirse. La variable `QUERYPARAM` permite adjuntar la consulta con el `parameterName`. La variable `HEADERPARAM` le permite agregar su `parameterName` a su solicitud de encabezado. |
| `parameterName` | Nombre del parámetro utilizado para incorporar el token de continuación. El formato es el siguiente: `{PARAMETER_NAME}={CONTINUATION_TOKEN}`. |
| `delayRequestMillis` | La variable `delayRequestMillis` en paginación permite controlar la velocidad de las solicitudes realizadas al origen. Algunas fuentes pueden tener un límite en el número de solicitudes que se pueden realizar por minuto. Por ejemplo, [!DNL Zendesk] tiene un límite de 100 solicitudes por minuto y define  `delayRequestMillis` a `850` le permite configurar el origen para que realice llamadas a unas 80 solicitudes por minuto, muy por debajo del umbral de 100 solicitudes por minuto. |

A continuación se muestra un ejemplo de una respuesta devuelta utilizando el tipo de token de continuación pagination:

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

#### `PAGE`

La variable `PAGE` tipo de paginación le permite recorrer los datos devueltos por número de páginas que comienzan desde cero. Al usar `PAGE` paginación, debe proporcionar el número de registros dados en una sola página.

```json
"paginationParams": {
  "type": "PAGE",
  "limitName": "records",
  "limitValue": "100",
  "pageParamName": "pageIndex",
  "maximumRequest": 10000
}
```

| Propiedad | Descripción |
| --- | --- |
| `type` | Tipo de paginación que se utiliza para devolver datos. |
| `limitName` | Nombre del límite mediante el cual la API puede especificar el número de registros que se recuperarán en una página. |
| `limitValue` | Número de registros que se van a recuperar en una página. |
| `pageParamName` | Nombre del parámetro que debe anexar a los parámetros de consulta para recorrer diferentes páginas de los datos devueltos. Por ejemplo, `https://abc.com?pageIndex=1` devolverá la segunda página de la carga útil de retorno de una API. |
| `maximumRequest` | Número máximo de solicitudes que un origen puede realizar para una ejecución incremental determinada. El límite predeterminado actual es 10 000. |

#### `NONE`

La variable `NONE` el tipo de paginación se puede usar para orígenes que no admiten ninguno de los tipos de paginación disponibles. Fuentes que utilizan el tipo de paginación de `NONE` simplemente devuelven todos los registros recuperables cuando se realiza una solicitud de GET.

```json
"paginationParams": {
  "type": "NONE"
}
```

### Programación avanzada para orígenes de autoservicio (SDK por lotes)

Configure la programación incremental y de relleno de la fuente mediante programación avanzada. La variable `incremental` permite configurar una programación en la que el origen solo ingerirá registros nuevos o modificados, mientras que la variable `backfill` permite crear una programación para introducir datos históricos.

Con la programación avanzada, puede utilizar expresiones y funciones específicas del origen para configurar programaciones de relleno y aumento. En el ejemplo siguiente, la variable [!DNL Zendesk] origen requiere que la programación incremental tenga el formato `type:user updated > {START_TIME} updated < {END_TIME}` y rellenar como `type:user updated < {END_TIME}`.

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
| `scheduleParams.type` | El tipo de programación que utilizará el origen. Establezca este valor como `ADVANCE` para utilizar el tipo de programación avanzado. |
| `scheduleParams.paramFormat` | El formato definido del parámetro de programación. Este valor puede ser el mismo que el de la fuente `scheduleStartParamFormat` y `scheduleEndParamFormat` valores. |
| `scheduleParams.incremental` | La consulta incremental del origen. Incremental se refiere a un método de ingesta en el que solo se introducen datos nuevos o modificados. |
| `scheduleParams.backfill` | La consulta de relleno del origen. El relleno se refiere a un método de ingesta en el que se introducen datos históricos. |

Una vez configurada la programación avanzada, debe consultar la `scheduleParams` en la sección URL, body o header params , según lo que admita su origen en particular. En el ejemplo siguiente, `{SCHEDULE_QUERY}` es un marcador de posición que se utiliza para especificar dónde se utilizarán las expresiones de programación incremental y de relleno. En el caso de una [!DNL Zendesk] origen, `query` se usa en la variable `queryParams` para especificar la programación avanzada.

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

### Añada un esquema personalizado para definir los atributos dinámicos de la fuente

Puede incluir un esquema personalizado en el `sourceSpec` para definir todos los atributos necesarios para la fuente, incluidos los atributos dinámicos que pueda necesitar. Puede actualizar la especificación de conexión correspondiente de su origen realizando una solicitud de PUT al `/connectionSpecs` punto final del [!DNL Flow Service] API, mientras proporciona su esquema personalizado en la variable `sourceSpec` de la especificación de conexión.

A continuación se muestra un ejemplo de esquema personalizado que puede añadir a la especificación de conexión de la fuente:

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

Con las especificaciones de origen rellenadas, puede continuar configurando las especificaciones de exploración para el origen que desea integrar en Platform. Consulte el documento en [configuración de especificaciones de exploración](./explorespec.md) para obtener más información.
