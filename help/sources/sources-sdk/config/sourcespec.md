---
keywords: Experience Platform;inicio;temas populares;orígenes;conectores;conectores de origen;sdk de fuentes;sdk;SDK
title: Configuración de especificaciones de autenticación para el SDK de fuentes
topic-legacy: overview
description: Este documento proporciona información general sobre las configuraciones que debe preparar para utilizar el SDK de fuentes.
hide: true
hidefromtoc: true
source-git-commit: d4b5b54be9fa2b430a3b45eded94a523b6bd4ef8
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 1%

---


# Configuración de la especificación de origen para el SDK de fuentes

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
        "key": "{CATEGORY}"
      },
      "icon": {
        "key": "{ICON}"
      },
      "description": {
        "key": "{DESCRIPTION}"
      },
      "label": {
        "key": "{LABEL}"
      }
    },
    "urlParams": {
      "path": "{RESOURCE_PATH}",
      "method": "{GET_or_POST}",
      "queryParams": "{QUERY_PARAMS}"
    },
    "headerParams": "{HEADER_VALUES}",
    "bodyParams": "{BODY_PARAMS_USED_IF_METHOD_IS_POST}",
    "contentPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "explodeEntityPath": {
      "path": "{PATH_SHOULD_POINT_TO_COLLECTION_OF_RECORDS}",
      "skipAttributes": [],
      "overrideWrapperAttribute": "{OVERRIDE_ATTRIBUTES}",
      "keepAttributes": ["action", "type", "timestamp"]
    },
    "paginationParams": {
      "type": "{OFFSET_OR_POINTER}",
      "limitName": "{NUMBER_OF_RECORDS_ATTRIBUTE_NAME}",
      "limitValue": "{NUMBER_OF_RECORDS_PER_PAGE}",
      "offSetName": "{OFFSET_ATTRIBUTE_NAME_REQUIRED_IN_CASE_OF_OFFSET BASED_PAGINATION}",
      "pointerName": "{POINTER_PATH_REQUIRED_IN__CASE_OF_POINTER BASED_PAGINATION}"
    },
    "scheduleParams": {
      "scheduleStartParamName": "{START_TIME_PARAMETER_NAME}",
      "scheduleEndParamName": "{END_TIME_PARAMETER_NAME}",
      "scheduleStartParamFormat": "{DATE_TIME_FORMAT_FOR_START_TIME}",
      "scheduleEndParamFormat": "{END_TIME_FORMAT_FOR_START_TIME}"
    }
  },
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define user input parameters to fetch resource values.",
    "properties": "{USER_INPUT}"
  }
}
```

| Propiedad | Descripción | Ejemplo |
| --- | --- | --- |
| `sourceSpec.attributes` | Contiene información sobre la fuente específica de la interfaz de usuario o la API. |
| `sourceSpec.attributes.uiAttributes` | Muestra información sobre la fuente específica de la interfaz de usuario. |
| `sourceSpec.attributes.uiAttributes.isBeta` | Un atributo booleano que indica si la fuente requiere más comentarios de los clientes para agregar a su funcionalidad. | <ul><li>`true`</li><li>`false`</li></ul> |
| `sourceSpec.attributes.uiAttributes.category` | Define la categoría del origen. | <ul><li>`advertising`</li><li>`cloud storage`</li><li>`crm`</li><li>`customer success`</li><li>`database`</li><li>`ecommerce`</li><li>`marketing automation`</li><li>`payments`</li><li>`protocols`</li><li>`streaming`</li></ul> |
| `sourceSpec.attributes.uiAttributes.icon` | Define el icono utilizado para procesar el origen en la interfaz de usuario de Platform. | `mailchimp-icon.svg` |
| `sourceSpec.attributes.uiAttributes.description` | Muestra una breve descripción de la fuente. |
| `sourceSpec.attributes.uiAttributes.label` | Muestra la etiqueta que se utilizará para procesar el origen en la interfaz de usuario de Platform. |
| `sourceSpec.attributes.urlParams` | Contiene información sobre la ruta de acceso del recurso de URL, el método y los parámetros de consulta admitidos. |
| `sourceSpec.attributes.urlParams.path` | Define la ruta del recurso desde donde recuperar los datos. | `/3.0/reports/${campaignId}/email-activity` |
| `sourceSpec.attributes.urlParams.method` | Define el método HTTP que se utilizará para realizar la solicitud al recurso para recuperar datos. | `GET`, `POST` |
| `sourceSpec.attributes.urlParams.queryParams` | Define los parámetros de consulta admitidos que se pueden usar para anexar la dirección URL de origen al realizar una solicitud para recuperar datos. Los parámetros de consulta deben ser una coma (`,`) pares de clave-valor separados. **Nota**: Cualquier valor de parámetro proporcionado por el usuario debe tener el formato de marcador de posición. Por ejemplo: `${USER_PARAMETER}`. | `exclude_fields=emails._links,id=${id}` |
| `sourceSpec.attributes.headerParams` | Define la coma (`,`) encabezados separados que deben proporcionarse en la solicitud HTTP para crear la URL al recuperar datos. | `Content-Type=application/json,foo=bar&userHeader={{USER_HEADER_VALUE}}` |
| `sourceSpec.attributes.bodyParams` | Define los parámetros de cuerpo necesarios. Esta propiedad solo se utiliza si `urlParams.method` está configurado como `POST`. |
| `sourceSpec.attributes.contentPath` | Define el nodo que contiene la lista de elementos necesarios para su ingesta en Platform. Este atributo debe seguir una sintaxis de ruta JSON válida y debe señalar a una matriz concreta. | Consulte la [apéndice](#content-path) para ver un ejemplo del recurso contenido en una ruta de contenido. |
| `sourceSpec.attributes.contentPath.path` | La ruta que señala a los registros de recopilación que se van a introducir en Platform. | `$.emails` |
| `sourceSpec.attributes.contentPath.skipAttributes` | Esta propiedad le permite identificar elementos específicos del recurso identificado en la ruta de contenido que se van a excluir de la ingesta. |
| `sourceSpec.attributes.contentPath.overrideWrapperAttribute` | Esta propiedad permite anular el valor del nombre de atributo especificado en `contentPath`. |
| `sourceSpec.attributes.contentPath.keepAttributes` | Esta propiedad le permite especificar explícitamente los atributos individuales que desea asignar. |
| `sourceSpec.attributes.explodeEntityPath` | Esta propiedad le permite acoplar dos matrices y transformar los datos de recursos en recursos de Platform. |
| `sourceSpec.attributes.explodeEntityPath.path` | Ruta que señala a los registros de recopilación que desea acoplar. | `$.email.activity` |
| `sourceSpec.attributes.explodeEntityPath.skipAttributes` | Esta propiedad permite identificar elementos específicos del recurso identificado en la ruta de entidad que se van a excluir de la ingesta. |
| `sourceSpec.attributes.explodeEntityPath.overrideWrapperAttribute` | Esta propiedad permite anular el valor del nombre de atributo especificado en `explodeEntityPath`. |
| `sourceSpec.attributes.explodeEntityPath.keepAttributes` | Esta propiedad le permite especificar explícitamente los atributos individuales que desea asignar. |
| `sourceSpec.attributes.paginationParams` | Define los parámetros o campos que deben suministrarse para obtener un vínculo a la página siguiente desde la respuesta de página actual del usuario, o al crear una URL de página siguiente. |
| `sourceSpec.attributes.paginationParams.type` | Muestra el tipo de paginación compatible con el origen. | <ul><li>`offset`: Este tipo de paginación le permite analizar los resultados especificando un índice desde donde iniciar la matriz resultante y un límite en cuanto a cuántos resultados se devuelven.</li><li>`pointer`: Este tipo de paginación le permite utilizar un `pointer` para que apunten a un elemento en particular que debe enviarse con una solicitud. La paginación del tipo de puntero requiere una ruta en la carga útil que señala a la página siguiente</li></ul> |
| `sourceSpec.attributes.paginationParams.limitName` | Nombre del límite mediante el cual la API puede especificar el número de registros que se recuperarán en una página. | `count` |
| `sourceSpec.attributes.paginationParams.limitValue` | Número de registros que se van a recuperar en una página. | `100` |
| `sourceSpec.attributes.paginationParams.offSetName` | El nombre del atributo de desplazamiento. Esto es necesario si el tipo de paginación está establecido en `offset`. | `offset` |
| `sourceSpec.attributes.paginationParams.pointerName` | El nombre del atributo del puntero. Esto requiere una ruta json al atributo que apuntará a la página siguiente. Esto es necesario si el tipo de paginación está establecido en `pointer`. | `pointer` |
| `sourceSpec.attributes.scheduleParams` | Contiene parámetros que definen formatos de programación admitidos para el origen. Los parámetros de programación incluyen `startTime` y `endTime`, ambos permiten establecer intervalos de tiempo específicos para ejecuciones por lotes, lo que garantiza que los registros recuperados en una ejecución por lotes anterior no se recuperen de nuevo. |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamName` | Define el nombre del parámetro de hora de inicio | `since_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamName` | Define el nombre del parámetro de hora de finalización | `before_last_changed` |
| `sourceSpec.attributes.scheduleParams.scheduleStartParamFormat` | Define el formato admitido para la variable `scheduleStartParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.attributes.scheduleParams.scheduleEndParamFormat` | Define el formato admitido para la variable `scheduleEndParamName`. | `yyyy-MM-ddTHH:mm:ssZ` |
| `sourceSpec.spec.properties` | Define los parámetros proporcionados por el usuario para recuperar valores de recursos. | Consulte la [apéndice](#user-input) para ver un ejemplo de parámetros introducidos por el usuario para `spec.properties`. |

{style=&quot;table-layout:auto&quot;}

## Apéndice {#appendix}

### Ejemplo de ruta de contenido {#content-path}

El siguiente es un ejemplo del contenido de la variable `contentPath` propiedad en un [!DNL MailChimp Campaigns] especificación de conexión.

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

## Pasos siguientes

Con las especificaciones de origen rellenadas, puede continuar configurando las especificaciones de exploración para el origen que desea integrar en Platform. Consulte el documento en [configuración de especificaciones de exploración](./explorespec.md) para obtener más información.