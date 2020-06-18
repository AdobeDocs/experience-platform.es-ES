---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de Almacenamiento de archivos de Azure mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: c843ebb72ee3f1e8d2233dd2be4021403417813b
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---


# Creación de un conector de Almacenamiento de archivos de Azure mediante la API de servicio de flujo

>[!NOTE]
>El conector del Almacenamiento de archivos de Azure está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar el Almacenamiento de archivos de Azure con el Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente al Almacenamiento de archivos de Azure mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con el Almacenamiento de archivos de Azure, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Extremo de la instancia de Almacenamiento de archivos de Azure a la que está accediendo. |
| `userId` | El usuario con acceso suficiente al extremo del Almacenamiento de archivos de Azure. |
| `password` | La contraseña de la instancia de Almacenamiento de archivos de Azure |
| ID de especificación de conexión | Identificador único necesario para crear una conexión. El ID de especificación de conexión para el Almacenamiento de archivos de Azure es: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

Para obtener más información sobre cómo empezar, consulte [este documento](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)de Almacenamiento de archivos de Azure.

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de Almacenamiento de archivos de Azure, ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una nueva conexión de Almacenamiento de archivos de Azure, configurada por las propiedades proporcionadas en la carga útil:


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
| `auth.params.host` | Extremo de la instancia de Almacenamiento de archivos de Azure a la que está accediendo. |
| `auth.params.userId` | El usuario con acceso suficiente al extremo del Almacenamiento de archivos de Azure. |
| `auth.params.password` | Clave de acceso del Almacenamiento de archivos de Azure. |
| `connectionSpec.id` | ID de especificación de conexión de Almacenamiento de archivos de Azure: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de Almacenamiento de archivos de Azure mediante la API de servicio de flujo y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar un almacenamiento de nube de terceros mediante la API](../../explore/cloud-storage.md)de servicio de flujo.
