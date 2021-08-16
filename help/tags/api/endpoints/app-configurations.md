---
title: Punto final de las configuraciones de aplicación
description: Aprenda a realizar llamadas al extremo /app_configuration en la API de Reactor.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 7%

---

# Punto final de las configuraciones de aplicación

>[!WARNING]
>
>La implementación del punto final `/app_configurations` está en proceso de cambio a medida que se agregan, eliminan y vuelven a trabajar las funciones.

Las configuraciones de aplicación permiten almacenar y recuperar las credenciales para usarlas más adelante. El extremo `/app_configurations` de la API de Reactor le permite administrar mediante programación las configuraciones de aplicación dentro de la aplicación de experiencia.

## Primeros pasos

El punto final utilizado en esta guía forma parte de la [API del reactor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante sobre cómo autenticarse en la API.

## Recuperar una lista de configuraciones de aplicación {#list}

**Formato de API**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| Parámetro | Descripción |
| --- | --- |
| `COMPANY_ID` | El `id` de la [empresa](./companies.md) que posee las configuraciones de la aplicación. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Mediante parámetros de consulta, las configuraciones de aplicación enumeradas se pueden filtrar según los atributos siguientes:<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>Consulte la guía sobre [filtrado de respuestas](../guides/filtering.md) para obtener más información.

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve una lista de configuraciones de aplicación.

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
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

## Buscar una configuración de aplicación {#lookup}

Puede buscar una configuración de aplicación proporcionando su ID en la ruta de una solicitud de GET.

**Formato de API**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `APP_CONFIGURATION_ID` | El `id` de la configuración de la aplicación que desea buscar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Respuesta**

Una respuesta correcta devuelve los detalles de la configuración de la aplicación.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Crear una configuración de aplicación {#create}

Puede crear una nueva configuración de aplicación realizando una solicitud de POST.

**Formato de API**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| Parámetro | Descripción |
| --- | --- |
| `COMPANY_ID` | El `id` de la [empresa](./companies.md) en la que define la configuración de la aplicación. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `platform` | La plataforma en la que se ejecuta la aplicación (web o móvil). Esto determina qué servicios de mensajería están disponibles. |
| `messaging_service` | El servicio de mensajería asociado a la aplicación, como [Apple Push Notification service (APNS)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) y [Firebase Cloud Messaging (FCM)](https://firebase.google.com/docs/cloud-messaging). Esto determina qué tipos de claves se pueden utilizar. |
| `key_type` | Representa el protocolo que admite un proveedor de servicios push y determina el formato del objeto `push_credential`. A medida que evolucionan los protocolos para los servicios de mensajería, se crean nuevos valores `key_type` para admitir los protocolos actualizados. |
| `push_credential` | El valor de credencial real, que se cifra en reposo. Normalmente, este campo no se descifra ni se incluye en las respuestas de API. Solo ciertos servicios de Adobe pueden obtener una respuesta que contenga una credencial push descifrada. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la configuración de la aplicación recién creada.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Actualizar la configuración de una aplicación

Puede actualizar una configuración de aplicación incluyendo su ID en la ruta de una solicitud del PUT.

**Formato de API**

```http
PUT /app_configurations/{APP_CONFIGURATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `APP_CONFIGURATION_ID` | El `id` de la configuración de la aplicación que desea actualizar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

La siguiente solicitud actualiza el `app_id` para una configuración de aplicación existente.

```shell
curl -X PUT \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `attributes` | Un objeto cuyas propiedades representan los atributos que se van a actualizar para la configuración de la aplicación. Cada clave representa el atributo de configuración de la aplicación que se va a actualizar, junto con el valor correspondiente al que se debe actualizar.<br><br>Se pueden actualizar los siguientes atributos para las configuraciones de la aplicación:<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | El `id` de la configuración de la aplicación que desea actualizar. Debe coincidir con el valor `{APP_CONFIGURATION_ID}` proporcionado en la ruta de solicitud. |
| `type` | Tipo de recurso que se actualiza. Para este extremo, el valor debe ser `app_configurations`. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve los detalles de la configuración actualizada de la aplicación.

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## Eliminar una configuración de aplicación

Puede eliminar una configuración de aplicación incluyendo su ID en la ruta de una solicitud del DELETE.

**Formato de API**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| Parámetro | Descripción |
| --- | --- |
| `APP_CONFIGURATION_ID` | El `id` de la configuración de la aplicación que desea eliminar. |

{style=&quot;table-layout:auto&quot;}

**Solicitud**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 204 (sin contenido) sin cuerpo de respuesta, lo que indica que se ha eliminado la configuración de la aplicación.
