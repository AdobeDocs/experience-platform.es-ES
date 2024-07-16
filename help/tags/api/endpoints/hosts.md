---
title: Extremo de hosts
description: Aprenda a realizar llamadas al extremo /hosts en la API de Reactor.
exl-id: 9d0d2a65-49e9-429c-a665-754b59a11cf1
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 91%

---

# Extremo de hosts

>[!NOTE]
>
>Este documento explica cómo administrar hosts en la API de Reactor. Para obtener información más general sobre los hosts para etiquetas, consulte la guía de [información general sobre hosts](../../ui/publishing/hosts/hosts-overview.md) en la documentación de publicación.

En la API de Reactor, un host define un destino en el que se puede entregar una [compilación](./builds.md).

Cuando un usuario de etiquetas solicita una compilación en Adobe Experience Platform, el sistema comprueba la biblioteca para determinar a qué [entorno](./environments.md) se debe crear la biblioteca. Cada entorno tiene una relación con un host, que indica dónde enviar la compilación.

Un host pertenece exactamente a una [propiedad](./properties.md), mientras que una propiedad puede tener muchos hosts. Una propiedad debe tener al menos un host para poder publicar.

Más de un entorno dentro de una propiedad puede utilizar un host. Es común tener un solo host en una propiedad y hacer que todos los entornos de esa propiedad utilicen el mismo host.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperación de una lista de hosts {#list}

Puede recuperar una lista de hosts de una propiedad, incluyendo el ID de la propiedad en la ruta de una petición GET.

**Formato de API**

```http
GET /properties/{PROPERTY_ID}/hosts
```

| Parámetro | Descripción |
| --- | --- |
| `PROPERTY_ID` | El `id` de la propiedad que posee los hosts. |

{style="table-layout:auto"}

>[!NOTE]
>
>Mediante parámetros de consulta, los hosts enumerados se pueden filtrar según los atributos siguientes:<ul><li>`created_at`</li><li>`name`</li><li>`type_of`</li><li>`updated_at`</li></ul>Consulte la guía de [filtrado respuestas](../guides/filtering.md) para obtener más información.

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de hosts de la propiedad especificada.

```json
{
  "data": [
    {
      "id": "HT405b8d9306004eb38106e66c8a4afc09",
      "type": "hosts",
      "attributes": {
        "created_at": "2020-12-14T17:42:35.239Z",
        "server": null,
        "name": "Example Akamai Host",
        "path": null,
        "port": null,
        "status": "succeeded",
        "type_of": "akamai",
        "updated_at": "2020-12-14T17:42:35.239Z",
        "username": null
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09/property"
          },
          "data": {
            "id": "PRd428c2a25caa4b32af61495f5809b737",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PRd428c2a25caa4b32af61495f5809b737",
        "self": "https://reactor.adobe.io/hosts/HT405b8d9306004eb38106e66c8a4afc09"
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

## Búsqueda de un host {#lookup}

Puede buscar un host proporcionando su ID en la ruta de una petición GET.

**Formato de API**

```http
GET /hosts/{HOST_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `HOST_ID` | El `id` del host que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del host.

```json
{
  "data": {
    "id": "HT5d90148e72224224aac9bc0b01498b84",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:25.353Z",
      "server": "https://server.example.com",
      "name": "Example Akamai Host",
      "path": "/akamai",
      "port": 8000,
      "status": "succeeded",
      "type_of": "akamai",
      "updated_at": "2020-12-14T17:42:25.353Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property"
        },
        "data": {
          "id": "PRd7cf174259f34057b5c435ef873a79bf",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRd7cf174259f34057b5c435ef873a79bf",
      "self": "https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84"
    }
  }
}
```

## Creación de un host {#create}

Puede crear un nuevo host realizando una petición POST.

**Formato de API**

```http
POST /properties/{PROPERTY_ID}/hosts
```

| Parámetro | Descripción |
| --- | --- |
| `PROPERTY_ID` | El `id` de la [propiedad](./properties.md) en la que está definiendo el host. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud crea un nuevo host para la propiedad especificada. La llamada también asocia el host con una extensión existente a través de la propiedad `relationships`. Consulte la guía de [relaciones](../guides/relationships.md) para obtener más información.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31/hosts \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Example SFTP Host",
            "type_of": "sftp",
            "username": "John Doe",
            "encrypted_private_key": "{PRIVATE_KEY}",
            "server": "https://example.com",
            "skip_symlinks": true,
            "path": "assets",
            "port": 22
          },
          "type": "hosts"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `attributes.name` | **(Obligatorio)** Un nombre legible en lenguaje natural para el host. |
| `attributes.type_of` | **(Obligatorio)** El tipo de host. Puede ser una de las dos opciones: <ul><li>`akamai` para [hosts administrados por Adobe](../../ui/publishing/hosts/managed-by-adobe-host.md)</li><li>`sftp` para [hosts SFTP](../../ui/publishing/hosts/sftp-host.md)</li></ul> |
| `attributes.encrypted_private_key` | Una clave privada opcional que se utilizará para la autenticación de host. |
| `attributes.path` | Ruta de acceso que se anexará a la dirección URL `server`. |
| `attributes.port` | Un entero que indica el puerto de servidor específico que se va a utilizar. |
| `attributes.server` | La URL de host del servidor. |
| `attributes.skip_symlinks`<br><br>(solo para hosts SFTP) | De forma predeterminada, todos los hosts SFTP utilizan vínculos simbólicos (enlaces simbólicos) para hacer referencia a las compilaciones de biblioteca guardadas en el servidor. Sin embargo, no todos los servidores admiten el uso de enlaces simbólicos. Cuando este atributo se incluye y se establece en `true`, el host utiliza una operación de copia para actualizar los recursos de compilación directamente en lugar de utilizar enlaces simbólicos. |
| `attributes.username` | Un nombre de usuario opcional para la autenticación. |
| `type` | Tipo de recurso que se actualiza. Para este extremo, el valor debe ser `hosts`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles del host recién creado.

```json
{
  "data": {
    "id": "HT69bfe634dead4a9a8c659f5d4d94cecd",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:07.033Z",
      "server": "//example.com",
      "name": "Example SFTP Host",
      "path": "assets",
      "port": 22,
      "status": "pending",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:07.033Z",
      "username": "John Doe"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd/property"
        },
        "data": {
          "id": "PRb25a704c0b7c4562835ccdf96d3afd31",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb25a704c0b7c4562835ccdf96d3afd31",
      "self": "https://reactor.adobe.io/hosts/HT69bfe634dead4a9a8c659f5d4d94cecd"
    }
  }
}
```

## Actualización de un host {#update}

>[!NOTE]
>
>Solo se pueden actualizar los hosts SFTP.

Puede actualizar un host incluyendo su ID en la ruta de una petición PATCH.

**Formato de API**

```http
PATCH /hosts/{HOST_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `HOST_ID` | El `id` del host que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud actualiza el `name` de un host existente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "New host Name"
          },
          "id": "HT5d90148e72224224aac9bc0b01498b84",
          "type": "hosts"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `attributes` | Un objeto cuyas propiedades representan los atributos que se van a actualizar para el host. Los siguientes atributos se pueden actualizar para un host: <ul><li>`encrypted_private_key`</li><li>`name`</li><li>`path`</li><li>`port`</li><li>`server`</li><li>`type_of`</li><li>`username`</li></ul> |
| `id` | El `id` del host que desea actualizar. Debe coincidir con el valor `{HOST_ID}` proporcionado en la ruta de solicitud. |
| `type` | Tipo de recurso que se actualiza. Para este extremo, el valor debe ser `hosts`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles del host actualizado.

```json
{
  "data": {
    "id": "HTb14e136a6fe147459b298a4645d2a6f5",
    "type": "hosts",
    "attributes": {
      "created_at": "2020-12-14T17:42:45.087Z",
      "server": null,
      "name": "My SFTP host",
      "path": null,
      "port": null,
      "status": "succeeded",
      "skip_symlinks": true,
      "type_of": "sftp",
      "updated_at": "2020-12-14T17:42:45.696Z",
      "username": null
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5/property"
        },
        "data": {
          "id": "PR8f240526f7b54a4dbd46965e79519fde",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR8f240526f7b54a4dbd46965e79519fde",
      "self": "https://reactor.adobe.io/hosts/HTb14e136a6fe147459b298a4645d2a6f5"
    }
  }
}
```

## Eliminación de un host

Puede eliminar un host incluyendo su ID en la ruta de una petición DELETE.

**Formato de API**

```http
DELETE /hosts/{HOST_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `HOST_ID` | El `id` del host que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) sin cuerpo de respuesta, lo que indica que el host se ha eliminado.

## Recuperación de recursos relacionados para un host {#related}

Las siguientes llamadas muestran cómo recuperar los recursos relacionados para un host. Cuando [busca un host](#lookup), estas relaciones se enumeran en la propiedad `relationships`.

Consulte la [guía de relaciones](../guides/relationships.md) para obtener más información sobre las relaciones en la API de Reactor.

### Búsqueda de la propiedad relacionada para un host {#property}

Puede buscar la propiedad que posee un host anexando `/property` a la ruta de una solicitud de consulta.

**Formato de API**

```http
GET /hosts/{HOST_ID}/property
```

| Parámetro | Descripción |
| --- | --- |
| `{HOST_ID}` | El `id` del host cuya propiedad desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/hosts/HT5d90148e72224224aac9bc0b01498b84/property \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la propiedad del host especificado.

```json
{
  "data": {
    "id": "PRbdfaffb7bf374b87be50e672f0cf9309",
    "type": "properties",
    "attributes": {
      "created_at": "2020-12-14T17:52:05.900Z",
      "enabled": true,
      "name": "Kessel Example Property",
      "updated_at": "2020-12-14T17:52:05.900Z",
      "platform": "web",
      "development": false,
      "token": "47d65c7c98db",
      "domains": [
        "example.com"
      ],
      "undefined_vars_return_empty": false,
      "rule_component_sequencing_enabled": false
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      },
      "callbacks": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/callbacks"
        }
      },
      "hosts": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/hosts"
        }
      },
      "environments": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments"
        }
      },
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/libraries"
        }
      },
      "data_elements": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements"
        }
      },
      "extensions": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/notes"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "data_elements": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/data_elements",
      "environments": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/environments",
      "extensions": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/extensions",
      "rules": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309/rules",
      "self": "https://reactor.adobe.io/properties/PRbdfaffb7bf374b87be50e672f0cf9309"
    },
    "meta": {
      "rights": [
        "approve",
        "develop",
        "manage_environments",
        "manage_extensions",
        "publish"
      ]
    }
  }
}
```
