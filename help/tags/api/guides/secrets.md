---
title: Secretos en la API de Reactor
description: Conozca los aspectos básicos de cómo configurar los secretos en la API de Reactor para usarlos en el reenvío de eventos.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 4f3c97e2cad6160481adb8b3dab3d0c8b23717cc
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 2%

---

# Secretos en la API de Reactor

En la API de Reactor, un secreto es un recurso que representa una credencial de autenticación. Los secretos se utilizan en el reenvío de eventos para autenticarse en otro sistema para el intercambio seguro de datos. Por lo tanto, los secretos solo se pueden crear dentro de las propiedades de reenvío de eventos (propiedades cuyas `platform` se configura como `edge`).

Actualmente existen tres tipos de secreto compatibles que se identifican en la variable `type_of` atributo:

| Tipo secreto | Descripción |
| --- | --- |
| `token` | Una cadena única de caracteres que representa un valor de token de autenticación conocido y entendido por ambos sistemas. |
| `simple-http` | Contiene dos atributos de cadena para un nombre de usuario y una contraseña, respectivamente. |
| `oauth2-client_credentials` | Contiene varios atributos para admitir la variable [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) especificación de autenticación. El reenvío de eventos le solicita la información necesaria y, a continuación, se encarga de la renovación de estos tokens en un intervalo especificado. |

{style=&quot;table-layout:auto&quot;}

Esta guía proporciona información general de alto nivel sobre cómo configurar los secretos para utilizarlos en el reenvío de eventos. Para obtener instrucciones detalladas sobre cómo administrar los secretos en la API de Reactor, incluido el JSON de la estructura de un secreto, consulte [guía de extremo secret](../endpoints/secrets.md).

## Credenciales

Cada secreto contiene un `credentials` que contiene sus respectivos valores de credencial. When [creación de un secreto en la API](../endpoints/secrets.md#create), cada tipo de secreto tiene diferentes atributos requeridos, como se muestra en las secciones siguientes:

* [`token`](#token)
* [`simple-http`](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [`oauth2-google`](#oauth2-google)

### `token` {#token}

Secretos con un `type_of` valor de `token` solo se necesita un atributo único en `credentials`:

| Atributo de Credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `token` | Cadena | Token secreto que comprende el sistema de destino. |

{style=&quot;table-layout:auto&quot;}

El token se almacena como un valor estático y, por lo tanto, el valor de `expires_at` y `refresh_at` las propiedades se establecen en `null` cuando se crea el secreto.

### `simple-http` {#simple-http}

Secretos con un `type_of` valor de `simple-http` requieren los siguientes atributos en `credentials`:

| Atributo de Credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `username` | Cadena | Un nombre de usuario. |
| `password` | Cadena | Una contraseña. Este valor no se incluye en la respuesta de API. |

{style=&quot;table-layout:auto&quot;}

Cuando se crea el secreto, los dos atributos se intercambian con una codificación BASE64 de `username:password`. Después del intercambio, el secreto `expires_at` y `refresh_at` las propiedades se establecen en `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Secretos con un `type_of` valor de `oauth2-client_credentials` requieren los siguientes atributos en `credentials`:

| Atributo de Credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `client_id` | Cadena | El ID de cliente para la integración de OAuth. |
| `client_secret` | Cadena | El secreto del cliente para la integración de OAuth. Este valor no se incluye en la respuesta de API. |
| `token_url` | Cadena | La URL de autorización para la integración de OAuth. |
| `refresh_offset` | Número entero | *(Opcional)* El valor, en segundos, para compensar la operación de actualización por. Si se omite este atributo al crear el secreto, el valor se establece en `14400` (cuatro horas) de forma predeterminada. |
| `options` | Objeto | *(Opcional)* Especifica opciones adicionales para la integración de OAuth:<ul><li>`scope`: Una cadena que representa la variable [Ámbito de OAuth 2.0](https://oauth.net/2/scope/) para las credenciales.</li><li>`audience`: Una cadena que representa una [Token de acceso Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Cuando una `oauth2-client_credentials` se crea o actualiza el secreto, la variable `client_id` y `client_secret` (y `options`) se intercambian en una solicitud de POST con el `token_url`, según el flujo de credenciales del cliente del protocolo OAuth.

>[!NOTE]
>
>Se espera que el cuerpo de respuesta del servicio de autorización sea compatible con el protocolo OAuth.

Si el servicio de autorización responde con `200 OK` y un cuerpo de respuesta JSON, el cuerpo se analiza y la variable `access_token` se inserta en el entorno de Edge y `expires_in` se utiliza para calcular la variable `expires_at` y `refresh_at` para el secreto. Si no hay ninguna asociación de entorno en el secreto, `access_token` se descarta.

Un intercambio de credenciales se considera exitoso bajo las siguientes condiciones:

* `expires_in` es bueno que `28800` (ocho horas).
* `refresh_offset` es menor que el valor de `expires_in` menos `14400` (cuatro horas). Por ejemplo, si `expires_in` es `36000` (diez horas) y `refresh_offset` es `28800` (ocho horas), el intercambio se considera fallido porque `28800` es bueno que `36000` - `14400` (`21600`).

Si el intercambio se realiza correctamente, el atributo de estado del secreto se establece en `succeeded` y valores para `expires_at` y `refresh_at` están configuradas:

* `expires_at` es la hora UTC actual más el valor de `expires_in`.
* `refresh_at` es la hora UTC actual más el valor de `expires_in`, menos el valor de `refresh_offset`. Por ejemplo, si `expires_in` es `43200` (doce horas) y `refresh_offset` es `14400` (cuatro horas), `refresh_at` se establecería en `28800` (ocho horas) después de la hora UTC actual.

Si el intercambio falla por cualquier razón, la variable `status_details` en la variable `meta` actualizaciones de objeto con información relevante.

#### Actualización de un `oauth2-client_credentials` secreto

Si una `oauth2-client_credentials` se ha asignado el secreto a un entorno y su estado es `succeeded` (las credenciales se intercambiaron correctamente), se realiza un nuevo intercambio automáticamente en `refresh_at`.

Si el intercambio es exitoso, la variable `refresh_status` en la variable `meta` el objeto está definido como `succeeded` while `expires_at`, `refresh_at`y `activated_at` se actualizan en consecuencia.

Si el intercambio falla, la operación se intenta tres veces más con el último intento no más de dos horas antes de que caduque el token de acceso. Si todos los intentos fallan, la variable `refresh_status_details` del `meta` actualizaciones de objeto con detalles relevantes.

### `oauth2-google` {#oauth2-google}

Secretos con un `type_of` valor de `oauth2-google` requiere el siguiente atributo en `credentials`:

| Atributo de Credencial | Tipo de datos | Descripción |
| --- | --- | --- |
| `scopes` | Matriz | Enumera los ámbitos de producto de Google para la autenticación. Se admiten los siguientes ámbitos:<ul><li>[Publicidades de Google](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Después de crear la variable `oauth2-google` secreto, la respuesta incluye un `meta.token_url` propiedad. Debe copiar y pegar esta dirección URL en un navegador para completar el flujo de autenticación de Google.

#### Volver a autorizar una `oauth2-google` secreto

La dirección URL de autorización de un `oauth2-google` el secreto caduca una hora después de crearse (como indica `meta.token_url_expires_at`). Después de este tiempo, el secreto debe volver a autorizarse para renovar el proceso de autenticación.

Consulte la [guía de extremo secret](../endpoints/secrets.md#reauthorize) para obtener detalles sobre cómo volver a autorizar una `oauth2-google` secreto realizando una solicitud de PATCH a la API de Reactor.

## Relación de entorno

Al crear un secreto, debe especificar la variable [entorno](../endpoints/environments.md) en el que existirá. Los secretos se implementan inmediatamente en el entorno en el que se crean.

Un secreto solo puede asociarse con un entorno. Una vez establecida la relación entre un secreto y un entorno, el secreto no se puede borrar del entorno y no se puede asociar con otro.

>[!NOTE]
>
>La única excepción a esta regla es si se elimina el entorno en cuestión. En este caso, la relación se borra y el secreto se puede asignar a un entorno diferente.

Una vez intercambiadas correctamente las credenciales de un secreto, para que un secreto se asocie a un entorno, el artefacto de intercambio (la cadena de token de `token`, la cadena codificada Base64 para `simple-http`o el token de acceso para `oauth2-client_credentials`) se guarda de forma segura en el entorno.

Una vez guardado correctamente el artefacto de intercambio en el entorno, el secreto `activated_at` se establece en la hora UTC actual y ahora se puede hacer referencia a él mediante un elemento de datos. Consulte la [sección siguiente](#referencing-secrets) para obtener más información sobre la referencia a secretos.

## Referencia a secretos {#referencing-secrets}

Para hacer referencia a un secreto, debe crear un elemento de datos de tipo &quot;[!UICONTROL Secreto]&quot; (proporcionado por el [[!UICONTROL Principal] Extensión](../../extensions/web/core/overview.md)) en una propiedad de reenvío de eventos. Al configurar este elemento de datos, se le pedirá que indique qué secreto utilizar para cada entorno. A continuación, puede crear reglas que hagan referencia a un elemento de datos secreto, como en el encabezado de una llamada HTTP.

![Elemento de datos secreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Para agregar un elemento de datos secreto a una biblioteca, debe tener al menos una `succeeded` secreto asociado al entorno en el que se está creando la biblioteca. Por ejemplo, si una biblioteca tiene un elemento de datos secreto que no tiene `succeeded` secreto configurado para el [!UICONTROL Secreto de ensayo] , al intentar crear esa biblioteca en el entorno de ensayo, se producirá un error.

Durante el tiempo de ejecución, el elemento de datos secreto se sustituye por el artefacto de intercambio secreto correspondiente guardado en el entorno.

## Pasos siguientes

Esta guía abarcaba los aspectos básicos del trabajo con secretos en la API de Reactor. Para obtener más información sobre cómo administrar secretos mediante llamadas a API, consulte la [guía de extremo secret](../endpoints/secrets.md).
