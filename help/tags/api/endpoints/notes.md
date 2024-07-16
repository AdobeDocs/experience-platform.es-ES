---
title: Extremo de las notas
description: Aprenda a realizar llamadas al extremo /notes en la API de Reactor.
exl-id: fa3bebc0-215e-4515-87b9-d195c9ab76c1
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 99%

---

# Extremo de las notas

En la API de Reactor, las notas son anotaciones que se pueden añadir a determinados recursos. Las notas son esencialmente comentarios sobre sus respectivos recursos. El contenido de las notas no afecta al comportamiento de los recursos y se puede utilizar en varios casos de uso, entre los que se incluyen los siguientes:

* Proporcionar información básica
* Usarlas como listas de tareas pendientes
* Pasar consejos sobre el uso de los recursos
* Dar instrucciones a otros integrantes del equipo
* Registrar el contexto histórico

El extremo `/notes` de la API de Reactor le permite administrar estas notas de forma programada.

Las notas se pueden aplicar a los siguientes recursos:

* [Elementos de datos](./data-elements.md)
* [Extensiones](./extensions.md)
* [Bibliotecas](./libraries.md)
* [Propiedades](./properties.md)
* [Componentes de regla](./rule-components.md)
* [Reglas](./rules.md)
* [Secretos](./secrets.md)

Estos seis tipos se conocen colectivamente como recursos “anotables”. Cuando se elimina un recurso anotable, también se eliminan sus notas asociadas.

>[!NOTE]
>
>Para los recursos que pueden tener varias revisiones, cualquier nota debe crearse en la revisión actual (principal). No podrán adjuntarse a otras revisiones.
>
>Sin embargo, las notas pueden seguirse leyendo desde las revisiones. En estos casos, la API devuelve solo las notas que existían antes de la creación de la revisión. Proporcionan una instantánea de las anotaciones tal y como estaban cuando se cortó la revisión. Por el contrario, leer las notas de la revisión actual (principal) devuelve todas sus notas.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperación de una lista de notas {#list}

Puede recuperar una lista de notas para un recurso añadiendo `/notes` a la ruta de una petición GET para el recurso en cuestión.

**Formato de API**

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parámetro | Descripción |
| --- | --- |
| `RESOURCE_TYPE` | El tipo de recurso para el que recupera notas. Debe tener uno de los siguientes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | El `id` del recurso específico cuyas notas desea enumerar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud enumera las notas adjuntas a una biblioteca.

```shell
curl -X GET \
  https://reactor.adobe.io/libraries/LBcffea1a38c52408cae2398868625a12d/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

## Búsqueda de una nota {#lookup}

Puede buscar una nota proporcionando su ID en la ruta de una petición GET.

**Formato de API**

```http
GET /notes/{NOTE_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `NOTE_ID` | El `id` de la nota que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/notes/NT550b7a17ab304d49ba289a2978d673e5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Puede crear una nota nueva añadiendo `/notes` a la ruta de una petición POST para el recurso en cuestión.

**Formato de API**

```http
POST /{RESOURCE_TYPE}/{RESOURCE_ID}/notes
```

| Parámetro | Descripción |
| --- | --- |
| `RESOURCE_TYPE` | El tipo de recurso para el que crea una nota. Debe tener uno de los siguientes valores: <ul><li>`data_elements`</li><li>`extensions`</li><li>`libraries`</li><li>`properties`</li><li>`rule_components`</li><li>`rules`</li></ul> |
| `RESOURCE_ID` | El `id` del recurso específico para el que desea crear una nota. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud crea una nota nueva para una propiedad.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/notes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `type` | **(Obligatorio)** El tipo de recurso que se actualiza. Para este extremo, el valor debe ser `notes`. |
| `attributes.text` | **(Obligatorio)** El texto que contiene la nota. Cada nota está limitada a 512 caracteres Unicode. |

{style="table-layout:auto"}

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
