---
keywords: Experience Platform;inicio;temas populares;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Creación de una conexión de origen de almacenamiento de archivos de Azure mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar el almacenamiento de archivos de Azure a Adobe Experience Platform mediante la API de servicio de flujo.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 2%

---

# Crear una conexión de origen [!DNL Azure File Storage] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL Azure File Storage] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Azure File Storage] con [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Azure File Storage] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Azure File Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El extremo de la instancia [!DNL Azure File Storag]e a la que está accediendo. |
| `userId` | El usuario con acceso suficiente al extremo [!DNL Azure File Storage]. |
| `password` | La contraseña de la instancia [!DNL Azure File Storage] |
| ID de especificación de conexión | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Azure File Storage] es: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Para obtener más información sobre cómo empezar, consulte [este documento de almacenamiento de archivos de Azure](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cada cuenta [!DNL Azure File Storage], ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Azure File Storage], su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Azure File Storage] es `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`.

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
| `auth.params.host` | El punto final de la instancia [!DNL Azure File Storage] a la que está accediendo. |
| `auth.params.userId` | El usuario con acceso suficiente al extremo [!DNL Azure File Storage]. |
| `auth.params.password` | La clave de acceso [!DNL Azure File Storage]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Azure File Storage]: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Azure File Storage] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial, mientras aprende a explorar [un almacenamiento en la nube de terceros mediante la API de servicio de flujo](../../explore/cloud-storage.md).
