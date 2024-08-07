---
title: Secretos en la API de Reactor
description: Conozca los aspectos básicos de cómo configurar secretos en la API de Reactor para utilizarlos en el reenvío de eventos.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Secretos en la API de Reactor

En la API de Reactor, un secreto es un recurso que representa una credencial de autenticación. Los secretos se utilizan en el reenvío de eventos para autenticarse en otro sistema y asegurar el intercambio de datos. Por lo tanto, los secretos solo se pueden crear en propiedades de reenvío de eventos (propiedades cuyo atributo `platform` está establecido en `edge`).

Actualmente hay tres tipos de secretos admitidos indicados en el atributo `type_of`:

| Tipo de secreto | Descripción |
| --- | --- |
| `token` | Una única cadena de caracteres que representa un valor de token de autenticación conocido y entendido por ambos sistemas. |
| `simple-http` | Contiene dos atributos de cadena para un nombre de usuario y una contraseña, respectivamente. |
| `oauth2-client_credentials` | Contiene varios atributos para admitir la especificación de autenticación [OAuth](https://datatracker.ietf.org/doc/html/rfc6749). El reenvío de eventos le solicita la información necesaria y, a continuación, se encarga de la renovación de estos tokens en un intervalo especificado. |

{style="table-layout:auto"}

Esta guía proporciona información general de alto nivel sobre cómo configurar secretos para usarlos en el reenvío de eventos. Para obtener instrucciones detalladas sobre cómo administrar secretos en la API de Reactor, incluido el ejemplo JSON de la estructura de un secreto, consulte la [guía de extremo de secretos](../endpoints/secrets.md).

## Credenciales

Cada secreto contiene un atributo `credentials` que contiene sus valores de credenciales respectivos. Al [crear un secreto en la API](../endpoints/secrets.md#create), cada tipo de secreto tiene diferentes atributos requeridos, como se muestra en las secciones siguientes:

* [`token`](#token)
* [`simple-http`](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

Los secretos con un valor `type_of` de `token` solo requieren un único atributo en `credentials`:

| Atributo de credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `token` | Cadena | Un token secreto que comprende el sistema de destino. |

{style="table-layout:auto"}

El token se almacena como un valor estático y, por lo tanto, las propiedades `expires_at` y `refresh_at` del secreto se establecen en `null` cuando se crea el secreto.

### `simple-http` {#simple-http}

Los secretos con un valor `type_of` de `simple-http` requieren los siguientes atributos en `credentials`:

| Atributo de credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `username` | Cadena | Un nombre de usuario. |
| `password` | Cadena | Una contraseña. Este valor no se incluye en la respuesta de la API. |

{style="table-layout:auto"}

Cuando se crea el secreto, los dos atributos se intercambian con una codificación BASE64 de `username:password`. Después del intercambio, las propiedades `expires_at` y `refresh_at` del secreto se establecen en `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Los secretos con un valor `type_of` de `oauth2-client_credentials` requieren los siguientes atributos en `credentials`:

| Atributo de credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `client_id` | Cadena | El ID de cliente para la integración de OAuth. |
| `client_secret` | Cadena | Secreto de cliente para la integración de OAuth. Este valor no se incluye en la respuesta de la API. |
| `token_url` | Cadena | URL de autorización para la integración de OAuth. |
| `refresh_offset` | Entero | *(Opcional)* El valor, en segundos, para compensar la operación de actualización. Si se omite este atributo al crear el secreto, el valor se establece en `14400` (cuatro horas) de forma predeterminada. |
| `options` | Objeto | *(Opcional)* Especifica opciones adicionales para la integración de OAuth:<ul><li>`scope`: cadena que representa el [ámbito de OAuth 2.0](https://oauth.net/2/scope/) para las credenciales.</li><li>`audience`: cadena que representa un [token de acceso Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Cuando se crea o actualiza un secreto `oauth2-client_credentials`, `client_id` y `client_secret` (y posiblemente `options`) se intercambian en una solicitud de POST a `token_url`, según el flujo de credenciales de cliente del protocolo de OAuth.

>[!NOTE]
>
>Se espera que el cuerpo de respuesta del servicio de autorización sea compatible con el protocolo OAuth.

Si el servicio de autorización responde con `200 OK` y un cuerpo de respuesta JSON, se analiza el cuerpo y se inserta `access_token` en el entorno de Edge y se utiliza `expires_in` para calcular los atributos `expires_at` y `refresh_at` del secreto. Si no hay ninguna asociación de entorno en el secreto, `access_token` se descarta.

Un intercambio de credenciales se considera exitoso bajo las siguientes condiciones:

* `expires_in` es mayor que `28800` (ocho horas).
* `refresh_offset` es menor que el valor de `expires_in` menos `14400` (cuatro horas). Por ejemplo, si `expires_in` es `36000` (diez horas) y `refresh_offset` es `28800` (ocho horas), el intercambio se considera erróneo porque `28800` es mayor que `36000` - `14400` (`21600`).

Si el intercambio se realiza correctamente, el atributo de estado del secreto se establece en `succeeded` y los valores de `expires_at` y `refresh_at` se establecen:

* `expires_at` es la hora UTC actual más el valor de `expires_in`.
* `refresh_at` es la hora UTC actual más el valor de `expires_in`, menos el valor de `refresh_offset`. Por ejemplo, si `expires_in` es `43200` (doce horas) y `refresh_offset` es `14400` (cuatro horas), la propiedad `refresh_at` se establecería en `28800` (ocho horas) después de la hora UTC actual.

Si el intercambio falla por algún motivo, el atributo `status_details` del objeto `meta` se actualiza con información relevante.

#### Actualizando un secreto `oauth2-client_credentials`

Si se ha asignado un secreto `oauth2-client_credentials` a un entorno y su estado es `succeeded` (las credenciales se intercambiaron correctamente), se realiza un nuevo intercambio automáticamente en `refresh_at`.

Si el intercambio se realiza correctamente, el atributo `refresh_status` del objeto `meta` se establece en `succeeded`, mientras que `expires_at`, `refresh_at` y `activated_at` se actualizan en consecuencia.

Si el intercambio falla, la operación se intenta tres veces más, con el último intento no más de dos horas antes de que caduque el token de acceso. Si todos los intentos fallan, el atributo `refresh_status_details` del objeto `meta` se actualiza con los detalles relevantes.

### `oauth2-google` {#oauth2-google}

Los secretos con un valor `type_of` de `oauth2-google` requieren el siguiente atributo en `credentials`:

| Atributo de credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `scopes` | Matriz | Enumera los ámbitos del producto de Google para la autenticación. Se admiten los siguientes ámbitos:<ul><li>[Anuncios de Google](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Pub Google/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Después de crear el secreto `oauth2-google`, la respuesta incluye una propiedad `meta.authorization_url`. Debe copiar y pegar esta dirección URL en un explorador para completar el flujo de autenticación de Google.

#### Volver a autorizar un secreto `oauth2-google`

La dirección URL de autorización para un secreto `oauth2-google` caduca una hora después de crearse el secreto (tal como indica `meta.authorization_url_expires_at`). Después de este tiempo, el secreto debe volver a autorizarse para renovar el proceso de autenticación.

Consulte la [guía de extremo de secretos](../endpoints/secrets.md#reauthorize) para obtener detalles sobre cómo volver a autorizar un secreto `oauth2-google` realizando una solicitud del PATCH a la API de Reactor.

## Relación del entorno

Cuando cree un secreto, debe especificar el [entorno](../endpoints/environments.md) en el que existirá. Los secretos se implementan inmediatamente en el entorno en el que se crean.

Un secreto solo se puede asociar a un entorno. Una vez establecida la relación entre un secreto y un entorno, el secreto no se puede borrar del entorno y no se puede asociar con un entorno diferente.

>[!NOTE]
>
>La única excepción a esta regla es que se elimine el entorno en cuestión. En este caso, la relación se borra y el secreto se puede asignar a un entorno diferente.

Después de intercambiar correctamente las credenciales de un secreto, para que un secreto se asocie a un entorno, el artefacto de intercambio (la cadena de token para `token`, la cadena codificada en Base64 para `simple-http` o el token de acceso para `oauth2-client_credentials`) se guarda de forma segura en el entorno.

Una vez guardado correctamente el artefacto de intercambio en el entorno, el atributo `activated_at` del secreto se establece en la hora UTC actual y ahora se puede hacer referencia a él mediante un elemento de datos. Consulte la [sección siguiente](#referencing-secrets) para obtener más información sobre cómo hacer referencia a secretos.

## Secretos de referencia {#referencing-secrets}

Para hacer referencia a un secreto, debe crear un elemento de datos de tipo &quot;[!UICONTROL Secreto]&quot; (proporcionado por la extensión [[!UICONTROL Core]](../../extensions/client/core/overview.md)) en una propiedad de reenvío de eventos. Al configurar este elemento de datos, se le pedirá que indique qué secreto utilizar para cada entorno. A continuación, puede crear reglas que hagan referencia a un elemento de datos secreto, como dentro del encabezado de una llamada HTTP.

![Elemento de datos secreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Para agregar un elemento de datos secreto a una biblioteca, debe tener al menos un secreto `succeeded` asociado al entorno en el que se está creando la biblioteca. Por ejemplo, si una biblioteca tiene un elemento de datos secreto que no tiene un secreto `succeeded` configurado para la sección [!UICONTROL Secreto de ensayo], al intentar crear esa biblioteca en el entorno de ensayo se producirá un error.

Durante el tiempo de ejecución, el elemento de datos secreto se reemplaza por el artefacto de intercambio secreto correspondiente guardado en el entorno.

## Pasos siguientes

Esta guía abarcaba los aspectos básicos del trabajo con secretos en la API de Reactor. Para obtener más información sobre cómo administrar secretos mediante llamadas API, consulte la [guía de extremo de secretos](../endpoints/secrets.md).
