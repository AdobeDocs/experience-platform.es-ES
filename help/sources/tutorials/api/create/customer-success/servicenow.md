---
keywords: Experience Platform;inicio;temas populares;servicio ahora;ServicioAhora
solution: Experience Platform
title: Crear una conexión de origen de ServiceNow mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor de ServiceNow mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL ServiceNow] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL ServiceNow] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a un servidor [!DNL ServiceNow].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a un servidor [!DNL ServiceNow] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL ServiceNow], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | Extremo del servidor [!DNL ServiceNow]. |
| `username` | El nombre de usuario utilizado para conectarse al servidor [!DNL ServiceNow] para la autenticación. |
| `password` | La contraseña para conectarse al servidor [!DNL ServiceNow] para la autenticación. |

Para obtener más información sobre cómo empezar, consulte [este documento de ServiceNow](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL ServiceNow], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL ServiceNow], se debe proporcionar su ID de especificación de conexión única como parte de la solicitud del POST. El identificador de especificación de conexión para [!DNL ServiceNow] es `eb13cb25-47ab-407f-ba89-c0125281c563`.

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| ------------- | --------------- |
| `auth.params.server` | Extremo del servidor [!DNL ServiceNow]. |
| `auth.params.username` | El nombre de usuario utilizado para conectarse al servidor [!DNL ServiceNow] para la autenticación. |
| `auth.params.password` | La contraseña para conectarse al servidor [!DNL ServiceNow] para la autenticación. |
| `connectionSpec.id` | El ID de especificación de conexión asociado a [!DNL ServiceNow]. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el próximo paso.

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL ServiceNow] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este identificador de conexión en el siguiente tutorial cuando aprenda a [explorar los sistemas de éxito de los clientes mediante la API de servicio de flujo](../../explore/customer-success.md).