---
title: Extremo de la búsqueda
description: Aprenda a realizar llamadas al extremo de la búsqueda en la API de Reactor.
exl-id: 14eb8d8a-3b42-42f3-be87-f39e16d616f4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 97%

---

# Extremo de la búsqueda

El extremo `/search` de la API de Reactor proporciona una forma de encontrar recursos que coincidan con los criterios deseados, expresados como una consulta.

Se pueden buscar los siguientes tipos de recursos de API, utilizando la misma estructura de datos que los documentos basados en recursos devueltos a través de la API:

* `audit_events`
* `builds`
* `callbacks`
* `data_elements`
* `environments`
* `extension_packages`
* `extensions`
* `hosts`
* `libraries`
* `properties`
* `rule_components`
* `rules`

Todas las consultas tienen ámbitos de la empresa actual y propiedades accesibles.

>[!IMPORTANT]
>
>La funcionalidad de búsqueda tiene las siguientes advertencias y excepciones:
>* meta no se puede buscar y no se devuelve en los resultados de búsqueda.
>* Campos de esquema para delegados de paquetes de extensiones (acciones, condiciones, etc.) se pueden buscar como texto, no como una estructura de datos anidada.
>* Actualmente, las consultas de rango solo admiten números enteros.


Para obtener información detallada sobre cómo utilizar esta funcionalidad, consulte la [guía de búsqueda](../guides/search.md).

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Realizar una búsqueda {#perform}

Puede realizar una búsqueda realizando una solicitud de POST.

**Formato de API**

```http
POST /search
```

**Solicitud**

```shell
curl -X POST \
  https://reactor.adobe.io/search \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "from": 0,
          "size": 25,
          "query": {
            "attributes.name": {
              "value": "Performance"
            },
            "attributes.revision_number": {
              "range": {
                "lte": "2",
                "gt": "0"
              }
            }
          },
          "sort": [
            {
              "attributes.revision_number": "desc"
            }
          ],
          "resource_types": [
            "data_elements",
            "rule_components"
          ]
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `from` | El número de resultados por el que se desplaza la respuesta. |
| `size` | Cantidad máxima de resultados que se van a devolver. Los resultados no pueden superar los 100 elementos. |
| `query` | Un objeto que representa la consulta de búsqueda. Para cada propiedad de este objeto, la clave debe representar una ruta de campo para la consulta y el valor debe ser un objeto cuyas subpropiedades determinen qué consultar.<br><br>Para cada ruta de campo, se pueden utilizar las siguientes subpropiedades:<ul><li>`exists`: Devuelve true si el campo existe en el recurso.</li><li>`value`: Devuelve true si el valor del campo coincide con el valor de esta propiedad.</li><li>`value_operator`: La lógica booleana utilizada para determinar cómo se debe gestionar una consulta `value`. Los valores permitidos son `AND` y `OR`. Cuando se excluye, se asume la lógica `AND`. Consulte la sección sobre la [lógica del operador de valores](#value-operator) para obtener más información.</li><li>`range` Devuelve true si el valor del campo se encuentra dentro de un intervalo numérico específico. El propio intervalo está determinado por las siguientes subpropiedades:<ul><li>`gt`: Mayor que el valor proporcionado, no inclusivo.</li><li>`gte`: Mayor o igual al valor proporcionado.</li><li>`lt`: Menor que el valor proporcionado, no incluido.</li><li>`lte`: Menor o igual que el valor proporcionado.</li></ul></li></ul> |
| `sort` | Matriz de objetos que indica el orden en que se ordenarán los resultados. Cada objeto debe contener una sola propiedad: la clave representa la ruta del campo por la que ordenar y el valor representa el criterio de ordenación (`asc` para ascendente, `desc` para descendente). |
| `resource_types` | Matriz de cadenas que indica los tipos de recurso específicos que se van a buscar. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve una lista de recursos coincidentes para la consulta. Para obtener más información sobre cómo determina la API las coincidencias para valores específicos, consulte la sección del apéndice sobre [convenciones coincidentes](#conventions).

```json
{
  "data": [
    {
      "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
      "type": "data_elements",
      "attributes": {
        "created_at": "2020-12-14T17:36:09.045Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Performance Indicator",
        "published": false,
        "published_at": null,
        "revision_number": 1,
        "updated_at": "2020-12-14T17:36:09.045Z",
        "clean_text": false,
        "default_value": null,
        "delegate_descriptor_id": "kessel-test::dataElements::dom-attribute",
        "force_lower_case": false,
        "review_status": "unsubmitted",
        "storage_duration": null,
        "settings": "{\"elementProperty\":\"html\",\"elementSelector\":\".target-element\"}"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/property"
          },
          "data": {
            "id": "PR97d92a379a5f48758947cdf44f607a0d",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/origin"
          },
          "data": {
            "id": "DE5d11b3ed301d4ce99b530a5121e392b2",
            "type": "data_elements"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/extension"
          },
          "data": {
            "id": "EX0348d463358c4c89afe726245576f112",
            "type": "extensions"
          }
        },
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2/updated_with_extension"
          },
          "data": {
            "id": "EX1cc78b39339242da82a0e0752fa53375",
            "type": "extensions"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR97d92a379a5f48758947cdf44f607a0d",
        "origin": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "self": "https://reactor.adobe.io/data_elements/DE5d11b3ed301d4ce99b530a5121e392b2",
        "extension": "https://reactor.adobe.io/extensions/EX0348d463358c4c89afe726245576f112"
      },
      "meta": {
        "latest_revision_number": 1
      }
    }
  ],
  "meta": {
    "total_hits": 1
  }
}
```

## Apéndice

La siguiente sección contiene información adicional sobre el uso del extremo `/search`.

### Lógica del operador de valor {#value-operator}

Los valores de consulta de búsqueda se dividen en términos que coinciden con los documentos indexados. Entre cada término, se asume una relación `AND`.

Cuando se utiliza `AND` como `value_operator`, un valor de consulta de `My Rule Holiday Sale` se interpreta como documentos con un campo que contiene `My AND Rule AND Holiday AND Sale`.

Cuando se utiliza `OR` como `value_operator`, un valor de consulta de `My Rule Holiday Sale` se interpreta como documentos con un campo que contiene `My OR Rule OR Holiday OR Sale`. Cuantos más términos coincidan, más alto será el `match_score`. Debido a la naturaleza de la coincidencia de términos parciales, cuando nada coincide con el valor deseado, puede obtener un conjunto de resultados en el que el valor solo coincida en un nivel muy básico, como algunos caracteres de texto.

### Convenciones de coincidencia {#conventions}

La búsqueda consiste en responder a la relevancia de un documento para una consulta suministrada. La forma en que se analizan y se indexan los datos del documento afecta directamente a esto.

La siguiente tabla desglosa las convenciones de coincidencia para los tipos de campo comunes:

| Tipo de campo | Convenciones de coincidencia |
| --- | --- |
| Cadenas | Texto con análisis de términos parciales, sin distinción entre mayúsculas y minúsculas |
| Valores de enumeración | Coincidencia exacta, con distinción entre mayúsculas y minúsculas |
| Enteros | Coincidencia exacta |
| Float | Coincidencia exacta |
| Marcas de hora | Coincidencia exacta (formato DateTime) |
| Mostrar nombres | Texto con análisis de términos parciales, sin distinción entre mayúsculas y minúsculas |

Existen convenciones adicionales para campos específicos que aparecen en la API:

| Campo | Convenciones de coincidencia |
| --- | --- |
| `id` | Coincidencia exacta, con distinción entre mayúsculas y minúsculas |
| `delegate_descriptor_id` | Coincidencia exacta, con distinción entre mayúsculas y minúsculas, con términos divididos en `::` |
| `name` | Coincidencia exacta, con distinción entre mayúsculas y minúsculas |
| `settings` | Texto con análisis de términos parciales, sin distinción entre mayúsculas y minúsculas |
| `type` | Coincidencia exacta, con distinción entre mayúsculas y minúsculas |
