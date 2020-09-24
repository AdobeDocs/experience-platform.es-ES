---
keywords: Experience Platform;home;popular topics;Azure Data Explorer;data explorer;Data Explorer
solution: Experience Platform
title: Creación de un conector de Data Explorer de Azure mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar la Data Explorer de Azure (en adelante denominada "Data Explorer") a Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 1%

---


# Creación de un [!DNL Azure Data Explorer] conector mediante la [!DNL Flow Service] API

>[!NOTE]
>
>El [!DNL Azure Data Explorer] conector está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la [!DNL Flow Service] API para guiarle por los pasos a los que conectarse [!DNL Azure Data Explorer] (en adelante, &quot;Data Explorer&quot;) a [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Data Explorer] través de la [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] conectarse con [!DNL Data Explorer], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL Data Explorer] server. |
| `database` | Nombre de la [!DNL Data Explorer] base de datos. |
| `tenant` | ID de inquilino único que se utiliza para conectarse a la [!DNL Data Explorer] base de datos. |
| `servicePrincipalId` | ID de principal de servicio único que se utiliza para conectarse a la [!DNL Data Explorer] base de datos. |
| `servicePrincipalKey` | Clave principal de servicio única utilizada para conectarse a la [!DNL Data Explorer] base de datos. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Data Explorer] es `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obtener más información sobre cómo empezar, consulte [este documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)de Data Explorer.

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de ejemplo en la guía de solución de problemas [!DNL Experience Platform] .

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el tutorial [de](../../../../../tutorials/authentication.md)autenticación. La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de la API de E[!DNL xperience Platform] , como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen al [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a [!DNL Platform] las API requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere un conector por [!DNL Data Explorer] cuenta, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una [!DNL Data Explorer] conexión, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Data Explorer] es `0479cc14-7651-4354-b233-7480606c2ac3`.

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
| `auth.params.endpoint` | The endpoint of the [!DNL Data Explorer] server. |
| `auth.params.database` | Nombre de la [!DNL Data Explorer] base de datos. |
| `auth.params.tenant` | ID de inquilino único que se utiliza para conectarse a la [!DNL Data Explorer] base de datos. |
| `auth.params.servicePrincipalId` | ID de principal de servicio único que se utiliza para conectarse a la [!DNL Data Explorer] base de datos. |
| `auth.params.servicePrincipalKey` | Clave principal de servicio única utilizada para conectarse a la [!DNL Data Explorer] base de datos. |
| `connectionSpec.id` | ID de especificación de [!DNL Data Explorer] conexión: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una [!DNL Data Explorer] conexión mediante la [!DNL Flow Service] API y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar bases de datos mediante la API](../../explore/database-nosql.md)de servicio de flujo.
