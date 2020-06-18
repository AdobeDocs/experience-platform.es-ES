---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector Phoenix mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 1%

---


# Creación de un conector Phoenix mediante la API de servicio de flujo

>[!NOTE]
>El conector Phoenix está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar una base de datos Phoenix al Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a Phoenix mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con Phoenix, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | La dirección IP o el nombre de host del servidor Phoenix. |
| `username` | El nombre de usuario que utiliza para acceder a Phoenix Server. |
| `password` | La contraseña correspondiente al usuario. |
| `port` | El puerto TCP que utiliza el servidor Phoenix para escuchar las conexiones de cliente. Si se conecta a Azure HDInsights, especifique el puerto como 443. |
| `httpPath` | La URL parcial correspondiente al servidor Phoenix. Especifique /hbasephoenix0 si utiliza el clúster de Azure HDInsights. |
| `enableSsl` | Un valor booleano. Especifica si las conexiones al servidor se cifran mediante SSL. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para Phoenix es: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Para obtener más información sobre cómo empezar, consulte [este documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html)de Phoenix.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de Platform, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de Experience Platform, incluidos los que pertenecen al servicio de flujo, están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de Phoenix, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión Phoenix, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud POST. El ID de especificación de conexión para Phoenix es `102706fb-a5cd-42ee-afe0-bc42f017ff43`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Phoenix test connection",
        "description": "Phoenix test connection",
        "auth": {
            "specName": "Basic Authentication",
        "params": {
            "host" :  "{HOST}",
            "username" : "{USERNAME}",
            "password" :"{PASSWORD}",
            "port" : {PORT},
            "httpPath" : "{PATH}",
            "enableSsl" : {SSL}
            }
        },
        "connectionSpec": {
            "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | El host del servidor Phoenix. |
| `auth.params.username` | El nombre de usuario asociado a su conexión Phoenix. |
| `auth.params.password` | La contraseña asociada a su conexión Phoenix. |
| `auth.params.port` | El puerto TCP para la conexión Phoenix. |
| `auth.params.httpPath` | Ruta http parcial para la conexión Phoenix. |
| `auth.params.enableSsl` | El valor booleano que especifica si las conexiones al servidor se cifran mediante SSL. |
| `connectionSpec.id` | ID de especificación de conexión Phoenix: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión Phoenix con la API de servicio de flujo y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar bases de datos mediante la API](../../explore/database-nosql.md)de servicio de flujo.