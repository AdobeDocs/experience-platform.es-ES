---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos Oracle;almacenamiento de objetos oracle
solution: Experience Platform
title: Creación de una conexión de origen de Almacenamiento de objetos Oracle mediante la API de servicio de flujo
topic: sobre validación
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform al Almacenamiento de objetos Oracle mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL Oracle Object Storage] mediante la API [!DNL Flow Service]

Este tutorial utiliza la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para guiarle por los pasos para conectar Adobe Experience Platform a [!DNL Oracle Object Storage].

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectarse con éxito a [!DNL Oracle Object Storage] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | El extremo [!DNL Oracle Object Storage] requerido para la autenticación. El formato del extremo es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | Se requiere el ID de la clave de acceso [!DNL Oracle Object Storage] para la autenticación. |
| `secretKey` | La contraseña [!DNL Oracle Object Storage] requerida para la autenticación. |
| `bucketName` | Se requiere el nombre del bloque permitido si el usuario tiene acceso restringido. El nombre del bloque debe tener entre tres y 63 caracteres, debe comenzar y finalizar con una letra o un número y sólo puede contener letras minúsculas, números o guiones (`-`). No se puede dar formato al nombre del bloque como una dirección IP. |
| `folderPath` | La ruta de la carpeta permitida que se requiere si el usuario tiene acceso restringido. |

Para obtener más información sobre cómo obtener estos valores, consulte la [guía de autenticación del Almacenamiento de objetos Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API de plataforma, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). La finalización del tutorial de autenticación proporciona los valores para cada uno de los encabezados necesarios en todas las llamadas de API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL Oracle Object Storage], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Oracle Object Storage], se debe proporcionar su ID de especificación de conexión única como parte de la solicitud del POST. El identificador de especificación de conexión para [!DNL Oracle Object Storage] es `c85f9425-fb21-426c-ad0b-405e9bd8a46c`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Oracle Object Storage connection",
        "description": "Oracle Object Storage connection",
        "auth": {
            "specName": "Access Key",
            "params": {
                "serviceUrl": "{SERVICE_URL}",
                "accessKey": "{ACCESS_KEY}",
                "secretKey": "{SECRET_KEY}",
                "bucketName": "{BUCKET_NAME}",
                "folderPath", "{FOLDER_PATH}"
            }
        },
        "connectionSpec": {
            "id": "c85f9425-fb21-426c-ad0b-405e9bd8a46c",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUrl` | El extremo [!DNL Oracle Object Storage] requerido para la autenticación. |
| `auth.params.accessKey` | Se requiere el ID de la clave de acceso [!DNL Oracle Object Storage] para la autenticación. |
| `auth.params.secretKey` | La contraseña [!DNL Oracle Object Storage] requerida para la autenticación. |
| `auth.params.bucketName` | Se requiere el nombre del bloque permitido si el usuario tiene acceso restringido. |
| `auth.params.folderPath` | La ruta de la carpeta permitida que se requiere si el usuario tiene acceso restringido. |
| `connectionSpec.id` | El identificador de especificación de conexión [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de la conexión recién creada. Este ID es necesario para explorar los datos del almacenamiento de nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Oracle Object Storage] mediante la API [!DNL Flow Service] y ha obtenido su ID de conexión única. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md).