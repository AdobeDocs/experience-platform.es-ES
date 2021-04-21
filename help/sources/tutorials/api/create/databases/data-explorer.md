---
keywords: Experience Platform;inicio;temas populares;Data Explorer de Azure;explorador de datos;Data Explorer
solution: Experience Platform
title: Creación de una conexión de origen de Data Explorer de Azure mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar la Data Explorer de Azure a Adobe Experience Platform mediante la API de servicio de flujo.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL Azure Data Explorer] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL Azure Data Explorer] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Azure Data Explorer] (en adelante denominada &quot;Data Explorer&quot;) con [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Data Explorer] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Data Explorer], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | El extremo del servidor [!DNL Data Explorer]. |
| `database` | Nombre de la base de datos [!DNL Data Explorer]. |
| `tenant` | ID de inquilino único que se utiliza para conectarse a la base de datos [!DNL Data Explorer]. |
| `servicePrincipalId` | ID de entidad de seguridad de servicio único utilizado para conectarse a la base de datos [!DNL Data Explorer]. |
| `servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse a la base de datos [!DNL Data Explorer]. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Data Explorer] es `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Data Explorer](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere un conector por cada cuenta [!DNL Data Explorer], ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Data Explorer], su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Data Explorer] es `0479cc14-7651-4354-b233-7480606c2ac3`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Data Explorer connection",
        "description": "A connection for Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.endpoint` | El extremo del servidor [!DNL Data Explorer]. |
| `auth.params.database` | Nombre de la base de datos [!DNL Data Explorer]. |
| `auth.params.tenant` | ID de inquilino único que se utiliza para conectarse a la base de datos [!DNL Data Explorer]. |
| `auth.params.servicePrincipalId` | ID de entidad de seguridad de servicio único utilizado para conectarse a la base de datos [!DNL Data Explorer]. |
| `auth.params.servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse a la base de datos [!DNL Data Explorer]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Data Explorer]: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Data Explorer] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial, mientras aprende a explorar las [bases de datos mediante la API de servicio de flujo](../../explore/database-nosql.md).
