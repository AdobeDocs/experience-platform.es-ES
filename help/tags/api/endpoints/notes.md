---
title: Punto final de las notas
description: Aprenda a realizar llamadas al extremo /notes en la API de Reactor.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 7%

---

# Punto final de las notas

En la API de Reactor, las notas son anotaciones que se pueden agregar a determinados recursos. Las notas son esencialmente comentarios sobre sus respectivos recursos. El contenido de las notas no afecta al comportamiento de los recursos y se puede utilizar en varios casos de uso, entre los que se incluyen los siguientes:

* Proporcionar información básica
* Funcionamiento como listas de tareas pendientes
* Pasar consejos sobre el uso de los recursos
* Dar instrucciones a otros integrantes del equipo
* Registro del contexto histórico

El extremo `/notes` de la API de Reactor le permite administrar estas notas de forma programada.

Las notas se pueden aplicar en los siguientes recursos:

* [Elementos de datos](./data-elements.md)
* [Extensiones](./extensions.md)
* [Bibliotecas](./libraries.md)
* [Propiedades](./properties.md)
* [Regla componentes](./rule-components.md)
* [Reglas](./rules.md)

Estos seis tipos se conocen colectivamente como recursos &quot;notables&quot;. Cuando se elimina un recurso notable, también se eliminan sus notas asociadas.

>[!NOTE]
>
>Para los recursos que pueden tener varias revisiones, cualquier nota debe crearse en la revisión actual (head). No podrán adjuntarse a otras revisiones.
>
>Sin embargo, las notas pueden seguir siendo leídas de las revisiones. En estos casos, la API devuelve solo las notas que existían antes de la creación de la revisión. Proporcionan una instantánea de las anotaciones tal y como estaban cuando se cortó la revisión. Por el contrario, leer las notas de la revisión actual (head) devuelve todas sus notas.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [API del reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperar una lista de notas {#list}

Puede recuperar una lista de notas para un recurso anexando `/notes` a la ruta de una solicitud de GET para el recurso en cuestión.

**Formato de API**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parámetro | Descripción |
| --- | --- |
| `RESOURCE_TYPE` | Tipo de recurso para el que está recuperando notas. Debe tener uno de los siguientes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | El `id` del recurso específico cuyas notas desea enumerar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud enumera las notas adjuntas a una biblioteca.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de notas adjuntas al recurso especificado.

```json
{
  "data": [
    {
      "id": "NTa40de8d76bfd4e40835830900ce83b7b",
      "type": "notes",
      "attributes": {
        "author_display_name": "John Smith",
        "author_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:51:00.411Z",
        "text": "this is a note on a library"
      },
      "relationships": {
        "resource": {
          "links": {
            "related": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d"
          },
          "data": {
            "id": "LBcffea1a38c52408cae2398868625a12d",
            "type": "libraries"
          }
        }
      },
      "links": {
        "resource": "https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d",
        "self": "https://reactor.adobe.io/notes/NTa40de8d76bfd4e40835830900ce83b7b"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Buscar una nota {#lookup}

Puede buscar una nota proporcionando su ID en la ruta de una solicitud de GET.

**Formato de API**

```http
GET /notes/{NOTE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `NOTE_ID` | El `id` de la nota que desea buscar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la nota.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "this is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```

## Crear una nota {#create}

>[!WARNING]
>
>Antes de crear una nota nueva, tenga en cuenta que las notas no se pueden editar y la única forma de eliminarlas es eliminar el recurso correspondiente.

Puede crear una nota nueva anexando `/notes` a la ruta de una solicitud de POST para el recurso en cuestión.

**Formato de API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parámetro | Descripción |
| --- | --- |
| `RESOURCE_TYPE` | Tipo de recurso para el que está creando una nota. Debe tener uno de los siguientes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | El `id` del recurso específico para el que desea crear una nota. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud crea una nota nueva para una propiedad.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "type": "notes",
          "attributes": {
            "text": "this is a note on a property"
          }
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `type` | **(Obligatorio)** El tipo de recurso que se está actualizando. Para este extremo, el valor debe ser `notes`. |
| `attributes.text` | **(Obligatorio)** El texto que contiene la nota. Cada nota está limitada a 512 caracteres Unicode. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devolverá los detalles de la nota recién creada.

```json
{
  "data": {
    "id": "NT550b7a17ab304d49ba289a2978d673e5",
    "type": "notes",
    "attributes": {
      "author_display_name": "John Smith",
      "author_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:51:10.316Z",
      "text": "This is a note on a property"
    },
    "relationships": {
      "resource": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8"
        },
        "data": {
          "id": "PR4537ac6f1f204ffd864ec47c4b27c2e8",
          "type": "properties"
        }
      }
    },
    "links": {
      "resource": "https://reactor.adobe.io/properties/PR4537ac6f1f204ffd864ec47c4b27c2e8",
      "self": "https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5"
    }
  }
}
```
