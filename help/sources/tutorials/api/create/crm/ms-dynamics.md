---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;dinámica;Dynamics
solution: Experience Platform
title: Crear una conexión de Microsoft Dynamics Source mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Platform a una cuenta de Microsoft Dynamics mediante la API de servicio de flujo.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Microsoft Dynamics] mediante la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar Platform a una cuenta [!DNL Microsoft Dynamics] (en adelante denominada &quot;Dynamics&quot;) mediante la API de servicio de flujo.

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectar correctamente Platform a una cuenta de Dynamics mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL Dynamics], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La URL de servicio de su instancia [!DNL Dynamics]. |
| `username` | El nombre de usuario de su cuenta de usuario [!DNL Dynamics]. |
| `password` | La contraseña de su cuenta [!DNL Dynamics]. |
| `servicePrincipalId` | El ID de cliente de su cuenta [!DNL Dynamics]. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `servicePrincipalKey` | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |

Para obtener más información sobre cómo empezar, visite [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos del Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cada cuenta [!DNL Dynamics], ya que se puede utilizar para crear varios flujos de datos para introducir datos diferentes.

### Crear una conexión [!DNL Dynamics] utilizando la autenticación básica

Para crear una conexión [!DNL Dynamics] utilizando la autenticación básica, realice una solicitud de POST a la API [!DNL Flow Service] y proporcione los valores `serviceUri`, `username` y `password` de la conexión.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Dynamics], su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Dynamics] es `38ad80fe-8b06-4938-94f4-d4ee80266b07`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUri` | El URI de servicio asociado a su instancia [!DNL Dynamics]. |
| `auth.params.username` | El nombre de usuario asociado a su cuenta [!DNL Dynamics]. |
| `auth.params.password` | La contraseña asociada a su cuenta [!DNL Dynamics]. |
| `connectionSpec.id` | La especificación de conexión `id` de su cuenta [!DNL Dynamics] recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Creación de una conexión [!DNL Dynamics] mediante autenticación de claves principales de servicio

Para crear una conexión [!DNL Dynamics] utilizando la autenticación basada en claves principales del servicio, realice una solicitud de POST a la API [!DNL Flow Service] mientras proporciona valores para las `serviceUri`, `servicePrincipalId` y `servicePrincipalKey` de la conexión.

**Formato de API**

```http
POST /connections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUri` | El URI de servicio asociado a su instancia [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | El ID de cliente de su cuenta [!DNL Dynamics]. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `auth.params.servicePrincipalKey` | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Dynamics] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial, mientras aprende a [explorar los sistemas CRM mediante la API de servicio de flujo](../../explore/crm.md).
