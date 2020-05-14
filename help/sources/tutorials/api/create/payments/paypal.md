---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de PayPal mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: 37a5f035023cee1fc2408846fb37d64b9a3fc4b6
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 1%

---


# Creación de un conector de PayPal mediante la API de servicio de flujo

>[!NOTE]
>El conector PayPal está en fase beta. Las funciones y la documentación están sujetas a cambios.

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes en Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar PayPal con la plataforma de experiencia.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): La plataforma de experiencia permite la ingesta de datos de diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): La plataforma de experiencia proporciona entornos limitados virtuales que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a PayPal mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con PayPal, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| Host | Dirección URL de la instancia de PayPal. (predeterminado: api.sandbox.paypal.com). |
| ID de cliente | ID de cliente asociado a la aplicación PayPal. |
| Secreto del cliente | El secreto de cliente asociado a la aplicación PayPal. |
| ID de especificación de conexión | Identificador único necesario para crear una conexión. El ID de especificación de conexión para PayPal es: `221c7626-58f6-4eec-8ee2-042b0226f03b` |

Para obtener más información sobre cómo empezar, consulte [este documento](https://developer.paypal.com/docs/api/overview/#get-credentials)de PayPal.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas de la plataforma de experiencia.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas de API de la plataforma de experiencia, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de la plataforma de experiencia, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de plataforma requieren un encabezado que especifique el nombre del simulador para pruebas en el que tendrá lugar la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de PayPal, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión PayPal, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud POST. El ID de especificación de conexión para PayPal es `221c7626-58f6-4eec-8ee2-042b0226f03b`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | Dirección URL de la instancia de PayPal. |
| `auth.params.clientId` | ID de cliente asociado a su instancia de PayPal. |
| `auth.params.clientSecret` | El secreto de cliente asociado a la instancia de PayPal. |
| `connectionSpec.id` | ID de especificación de conexión de PayPal: `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión PayPal con la API de servicio de flujo y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar la aplicación de pagos mediante la API](../../explore/payments.md)de servicio de flujo.
