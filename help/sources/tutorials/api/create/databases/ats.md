---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creación de un conector de Almacenamiento de tabla de Azure mediante la API de servicio de flujo
topic: overview
translation-type: tm+mt
source-git-commit: e4ed6ae3ee668cd0db741bd07d2fb7be593db4c9
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 2%

---


# Creación de un conector de Almacenamiento de tabla de Azure mediante la API de servicio de flujo

>[!NOTE]
>El conector de Almacenamiento de tabla de Azure está en versión beta. Consulte la descripción general [de](../../../../home.md#terms-and-conditions) Fuentes para obtener más información sobre el uso de conectores con etiquetas beta.

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de distintas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos necesarios para conectar el Almacenamiento de tablas de Azure (en adelante denominado &quot;ATS&quot;) al Experience Platform.

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes del Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a ATS mediante la API de servicio de flujo.

### Recopilar las credenciales necesarias

Para que el servicio de flujo se conecte con ATS, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a una instancia de ATS. El patrón de cadena de conexión para ATS es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | ID utilizado para generar una conexión. El ID de especificación de conexión fija para ATS es `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

Para obtener más información sobre la obtención de una cadena de conexión, consulte [este documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)ATS.

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Sólo se requiere un conector por cuenta ATS, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión ATS, su ID de especificación de conexión única debe proporcionarse como parte de la solicitud POST. El ID de especificación de conexión para ATS es `ecde33f2-c56f-46cc-bdea-ad151c16cd69`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión utilizada para conectarse a una instancia de ATS. El patrón de cadena de conexión para ATS es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | El ID de especificación de conexión ATS es: `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión ATS mediante la API de servicio de flujo y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar bases de datos mediante la API](../../explore/database-nosql.md)de servicio de flujo.
