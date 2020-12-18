---
keywords: Experience Platform;home;popular topics;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Creación de un conector de Almacenamiento de archivos de Azure mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar el Almacenamiento de archivos de Azure con el Experience Platform.
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 2%

---


# Cree un conector [!DNL Azure File Storage] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL Azure File Storage] está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Azure File Storage] a [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse con éxito a [!DNL Azure File Storage] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Azure File Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Extremo de la instancia [!DNL Azure File Storag]e a la que está accediendo. |
| `userId` | El usuario con acceso suficiente al extremo [!DNL Azure File Storage]. |
| `password` | La contraseña de la instancia [!DNL Azure File Storage] |
| ID de especificación de conexión | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Azure File Storage] es: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Para obtener más información sobre cómo empezar, consulte [este documento de Almacenamiento de archivos de Azure](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](../../../../../tutorials/authentication.md). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL Azure File Storage], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Azure File Storage], se debe proporcionar su ID de especificación de conexión única como parte de la solicitud del POST. El identificador de especificación de conexión para [!DNL Azure File Storage] es `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | Extremo de la instancia [!DNL Azure File Storage] a la que está accediendo. |
| `auth.params.userId` | El usuario con acceso suficiente al extremo [!DNL Azure File Storage]. |
| `auth.params.password` | La clave de acceso [!DNL Azure File Storage]. |
| `connectionSpec.id` | El identificador de especificación de conexión [!DNL Azure File Storage]: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Azure File Storage] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar un almacenamiento de nube de terceros mediante la API de servicio de flujo](../../explore/cloud-storage.md).
