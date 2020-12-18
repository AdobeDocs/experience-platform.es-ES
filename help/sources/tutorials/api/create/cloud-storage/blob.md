---
keywords: Experience Platform;home;popular topics;Azure;azure blob;blob;Blob
solution: Experience Platform
title: Creación de un conector Blob de Azure mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Este tutorial utiliza la API de servicio de flujo para guiarle por los pasos para conectar a un Experience Platform a un almacenamiento de blob de Azure (en lo sucesivo denominado "Blob").
translation-type: tm+mt
source-git-commit: fc6449d260ea7b96956689ce6c95c5e8b9002d89
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 1%

---


# Cree un conector [!DNL Azure Blob] mediante la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] a un almacenamiento [!DNL Azure Blob] (en adelante, &quot;Blob&quot;).

Si prefiere utilizar la interfaz de usuario en [!DNL Experience Platform], el [tutorial de interfaz de usuario del conector de origen de blob de Azure](../../../ui/create/cloud-storage/blob.md) proporciona instrucciones paso a paso para realizar acciones similares.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse correctamente a un almacenamiento Blob mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con el almacenamiento Blob, debe proporcionar valores para la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión necesaria para acceder a los datos del almacenamiento Blob. El patrón de la cadena de conexión Blob es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para Blob es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

Para obtener más información sobre cómo obtener una cadena de conexión, consulte [este documento de blob de Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string).

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

* `Content-Type: application/json&quot;

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta de Blob, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión Blob, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud del POST. El ID de especificación de conexión para Blob es `4c10e202-c428-4796-9208-5f1f5732b1cf`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Blob Connection",
        "description": "Cnnection for an Azure Blob account",
        "auth": {
            "specName": "ConnectionString",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión necesaria para acceder a los datos del almacenamiento Blob. El patrón de la cadena de conexión Blob es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | El ID de la especificación de conexión del almacenamiento Blob es: `4c10e202-c428-4796-9208-5f1f5732b1cf` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar su almacenamiento en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700c57b-0000-0200-0000-5e3b3f440000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de Blob mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md) o [ingesta de datos de parqué mediante la API de servicio de flujo](../../cloud-storage-parquet.md).