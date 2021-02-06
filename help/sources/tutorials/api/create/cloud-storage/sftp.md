---
keywords: Experience Platform;inicio;temas populares;SFTP;sftp;Protocolo seguro de transferencia de archivos;protocolo seguro de transferencia de archivos
solution: Experience Platform
title: Creación de una conexión de origen SFTP mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor SFTP (Protocolo seguro de transferencia de archivos) mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 1%

---


# Creación de una conexión de origen SFTP mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector SFTP está en versión beta. Las funciones y la documentación están sujetas a cambios. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar al Experience Platform a un servidor SFTP (Protocolo seguro de transferencia de archivos).

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde diversas fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de plataforma.
* [Simuladores](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

>[!IMPORTANT]
>
>Se recomienda evitar nuevas líneas o retornos de carro al ingerir objetos JSON con una conexión de origen SFTP. Para evitar la limitación, utilice un único objeto JSON por línea y varias líneas para los archivos posteriores.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un servidor SFTP mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a SFTP, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con el servidor SFTP. |
| `username` | El nombre de usuario con acceso al servidor SFTP. |
| `password` | La contraseña del servidor SFTP. |
| `privateKeyContent` | Contenido de clave privada SSH codificada en Base64. Formato SSH de clave privada OpenSSH (RSA/DSA). |
| `passPhrase` | La frase de contraseña o la contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido con contraseña, este parámetro debe usarse con la frase de contraseña de PrivateKeyContent como valor. |

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión, ya que se puede utilizar para crear varios flujos de datos para introducir datos diferentes.

### Creación de una conexión SFTP mediante autenticación básica

Para crear una conexión SFTP mediante autenticación básica, realice una solicitud de POST a la API [!DNL Flow Service] mientras proporciona valores para las `host`, `userName` y `password` de la conexión.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión SFTP, debe proporcionarse su ID de especificación de conexión única como parte de la solicitud del POST. El ID de especificación de conexión para SFTP es `b7bf2577-4520-42c9-bae9-cad01560f7bc`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.host` | El nombre de host del servidor SFTP. |
| `auth.params.username` | El nombre de usuario asociado al servidor SFTP. |
| `auth.params.password` | La contraseña asociada al servidor SFTP. |
| `connectionSpec.id` | ID de especificación de conexión del servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor SFTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Creación de una conexión SFTP mediante autenticación de clave pública SSH

Para crear una conexión SFTP mediante autenticación de clave pública SSH, realice una solicitud de POST a la API [!DNL Flow Service] mientras proporciona valores para las `host`, `userName`, `privateKeyContent` y `passPhrase` de la conexión.

**Formato API**

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
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
            }
        },
        "connectionSpec": {
            "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.host` | El nombre de host del servidor SFTP. |
| `auth.params.username` | El nombre de usuario asociado al servidor SFTP. |
| `auth.params.privateKeyContent` | Contenido de clave privada SSH codificada en base64. Formato SSH de clave privada OpenSSH (RSA/DSA). |
| `auth.params.passPhrase` | La frase de contraseña o la contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido con contraseña, este parámetro debe usarse con la frase de contraseña de PrivateKeyContent como valor. |
| `connectionSpec.id` | ID de especificación de conexión del servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor SFTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión SFTP mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión para [explorar almacenamientos en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md) o [ingestar datos de parquet mediante la API de servicio de flujo](../../cloud-storage-parquet.md).
