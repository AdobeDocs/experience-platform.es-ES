---
title: Punto de conexión de llamadas
description: Aprenda a realizar llamadas al extremo /callbacks en la API de Reactor.
exl-id: dd980f91-89e3-4ba0-a6fc-64d66b288a22
source-git-commit: 7f3b9ef9270b7748bc3366c8c39f503e1aee2100
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 96%

---

# Punto de conexión de llamadas

Una llamada de retorno es un mensaje que la API de Reactor envía a una URL específica (normalmente una que aloja su organización).

Las llamadas de retorno están pensadas para utilizarse junto con [eventos de auditoría](./audit-events.md) para rastrear actividades en la API de Reactor. Cada vez que se genera un evento de auditoría de un tipo determinado, una llamada de retorno puede enviar un mensaje correspondiente a la dirección URL especificada.

El servicio detrás de la URL especificada en la llamada de retorno debe responder con el código de estado HTTP 200 (OK) o 201 (Created). Si el servicio no responde con ninguno de estos códigos de estado, se vuelve a intentar enviar el mensaje en los siguientes intervalos:

* 1 minuto
* 5 minutos
* 30 minutos
* 1 hora
* 12 horas
* 1 día
* 3 días

>[!NOTE]
>
>Los intervalos de reintento son relativos al intervalo anterior. Por ejemplo, si el reintento a un minuto falla, el siguiente intento se programa durante cinco minutos después del error del intento de un minuto (seis minutos después de que se generara el mensaje).

Si todos los intentos de envío no se han realizado correctamente, el mensaje se descarta.

Una llamada de retorno pertenece exactamente a una [propiedad](./properties.md). Una propiedad puede tener muchas llamadas de retorno.

## Primeros pasos

El extremo utilizado en esta guía forma parte de la [API de Reactor](https://www.adobe.io/experience-platform-apis/references/reactor/). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Listado de llamadas de retorno {#list}

Puede enumerar todas las llamadas de retorno en una propiedad realizando una petición GET.

**Formato de API**

```http
GET  /properties/{PROPERTY_ID}/callbacks
```

| Parámetro | Descripción |
| --- | --- |
| `{PROPERTY_ID}` | El `id` de la propiedad cuyas llamadas de retorno desea enumerar. |

{style="table-layout:auto"}

>[!NOTE]
>
>Mediante parámetros de consulta, las llamadas de retorno enumeradas se pueden filtrar según los atributos siguientes:<ul><li>`created_at`</li><li>`updated_at`</li></ul>Consulte la guía de [filtrado de respuestas](../guides/filtering.md) para obtener más información.

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de llamadas de retorno para la propiedad especificada.

```json
{
  "data": [
    {
      "id": "CB26edef8d709243579589107bcda034da",
      "type": "callbacks",
      "attributes": {
        "created_at": "2020-12-14T17:34:47.082Z",
        "subscriptions": [
          "rule.created"
        ],
        "updated_at": "2020-12-14T17:34:47.082Z",
        "url": "https://www.example.com"
      },
      "relationships": {
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da/property"
          },
          "data": {
            "id": "PR66a3356c73fc4aabb67ee22caae53d70",
            "type": "properties"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR66a3356c73fc4aabb67ee22caae53d70",
        "self": "https://reactor.adobe.io/callbacks/CB26edef8d709243579589107bcda034da"
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

## Búsqueda de una llamada de retorno {#lookup}

Puede buscar una llamada de retorno proporcionando su ID en la ruta de una petición GET.

**Formato de API**

```http
GET /callbacks/{CALLBACK_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `CALLBACK_ID` | El `id` de la llamada de retorno que desea buscar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la llamada de retorno.

```json
{
  "data": {
    "id": "CBeef389cee8d84e69acef8665e4dcbef6",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:36.872Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:36.872Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6/property"
        },
        "data": {
          "id": "PRb513bbab52114573ac87f9848eea6ead",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRb513bbab52114573ac87f9848eea6ead",
      "self": "https://reactor.adobe.io/callbacks/CBeef389cee8d84e69acef8665e4dcbef6"
    }
  }
}
```

## Creación de una llamada de retorno {#create}

Puede crear una nueva llamada de retorno realizando una petición POST.

**Formato de API**

```http
POST /properties/{PROPERTY_ID}/callbacks
```

| Parámetro | Descripción |
| --- | --- |
| `PROPERTY_ID` | El `id` de la [propiedad](./properties.md) en la que está definiendo la llamada de retorno. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d/callbacks \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.com",
            "subscriptions": [
              "rule.created"
            ]
          }
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `url` | El destino URL del mensaje de llamada de retorno. La URL debe utilizar la extensión de protocolo HTTPS. |
| `subscriptions` | Matriz de cadenas que indica los tipos de eventos de auditoría que desencadenarán la llamada de retorno. Consulte la [guía de extremos de eventos de auditoría](./audit-events.md) para obtener una lista de posibles tipos de eventos. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devolverá los detalles de la llamada de retorno recién creada.

```json
{
  "data": {
    "id": "CB32d8f23d5ee548278d32076af4c442a0",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:27.059Z",
      "subscriptions": [
        "rule.created"
      ],
      "updated_at": "2020-12-14T17:34:27.059Z",
      "url": "https://www.example.com"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0/property"
        },
        "data": {
          "id": "PR5e22de986a7c4070965e7546b2bb108d",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR5e22de986a7c4070965e7546b2bb108d",
      "self": "https://reactor.adobe.io/callbacks/CB32d8f23d5ee548278d32076af4c442a0"
    }
  }
}
```

## Actualización de una llamada de retorno

Puede actualizar una llamada de retorno incluyendo su ID en la ruta de una petición del PATCH.

**Formato de API**

```http
PATCH /callbacks/{CALLBACK_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `CALLBACK_ID` | El `id` de la llamada de retorno que desea actualizar. |

{style="table-layout:auto"}

**Solicitud**

La siguiente solicitud actualiza la matriz `subscriptions` para una llamada de retorno existente.

```shell
curl -X PATCH \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "url": "https://www.example.net",
            "subscriptions": [
              "rule.created",
              "build.created"
            ]
          },
          "type": "callbacks",
          "id": "CB4310904d415549888cc9e31ebe1e1e45"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `attributes` | Un objeto cuyas propiedades representan los atributos que se van a actualizar para la llamada de retorno. Cada clave representa el atributo de llamada de retorno particular que se va a actualizar, junto con el valor correspondiente al que se debe actualizar.<br><br>Se pueden actualizar los atributos siguientes para las llamadas de retorno:<ul><li>`subscriptions`</li><li>`url`</li></ul> |
| `id` | El `id` de la llamada de retorno que desea actualizar. Debe coincidir con el valor `{CALLBACK_ID}` proporcionado en la ruta de solicitud. |
| `type` | Tipo de recurso que se actualiza. Para este extremo, el valor debe ser `callbacks`. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve los detalles de la llamada de retorno actualizada.

```json
{
  "data": {
    "id": "CB4310904d415549888cc9e31ebe1e1e45",
    "type": "callbacks",
    "attributes": {
      "created_at": "2020-12-14T17:34:56.884Z",
      "subscriptions": [
        "rule.created",
        "build.created"
      ],
      "updated_at": "2020-12-14T17:34:57.614Z",
      "url": "https://www.example.net"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45/property"
        },
        "data": {
          "id": "PR0a8ef3ca31dc456a8566e9288960bd79",
          "type": "properties"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PR0a8ef3ca31dc456a8566e9288960bd79",
      "self": "https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45"
    }
  }
}
```

## Eliminación de una llamada de retorno

Puede eliminar una llamada de retorno incluyendo su ID en la ruta de una petición DELETE.

**Formato de API**

```http
DELETE /callbacks/{CALLBACK_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `CALLBACK_ID` | El `id` de la llamada de retorno que desea eliminar. |

{style="table-layout:auto"}

**Solicitud**

```shell
curl -X DELETE \
  https://reactor.adobe.io/callbacks/CB4310904d415549888cc9e31ebe1e1e45 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) sin cuerpo de respuesta, lo que indica que se ha eliminado la llamada de retorno.
