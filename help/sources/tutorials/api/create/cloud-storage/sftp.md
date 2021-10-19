---
keywords: Experience Platform;inicio;temas populares;SFTP;sftp;Protocolo seguro de transferencia de archivos;protocolo seguro de transferencia de archivos
solution: Experience Platform
title: Creación de una conexión base SFTP mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor SFTP (Protocolo seguro de transferencia de archivos) mediante la API de servicio de flujo.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 2%

---

# Cree una conexión base SFTP usando la variable [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL SFTP] (Protocolo seguro de transferencia de archivos) utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

>[!IMPORTANT]
>
>Se recomienda evitar nuevas líneas o retornos de carro al introducir objetos JSON con un [!DNL SFTP] conexión de origen. Para solucionar la limitación, utilice un único objeto JSON por línea y utilice líneas múltiples para los archivos posteriores.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a un [!DNL SFTP] servidor que utiliza la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse a [!DNL SFTP], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con su [!DNL SFTP] servidor. |
| `port` | Puerto del servidor SFTP al que se está conectando. Si no se proporciona, el valor predeterminado es `22`. |
| `username` | El nombre de usuario con acceso a su [!DNL SFTP] servidor. |
| `password` | La contraseña de su [!DNL SFTP] servidor. |
| `privateKeyContent` | El contenido de clave privada SSH codificada Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `passPhrase` | La frase de contraseña o contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si la variable `privateKeyContent` está protegido con contraseña, este parámetro debe utilizarse con la frase de contraseña del contenido de clave privada como valor. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL SFTP] es: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL SFTP] credenciales de autenticación como parte de los parámetros de solicitud.

### Cree un [!DNL SFTP] conexión base con autenticación básica

Para crear un [!DNL SFTP] conexión base usando autenticación básica, realice una solicitud de POST al [!DNL Flow Service] API mientras proporciona valores para la `host`, `userName`y `password`.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL SFTP] mediante autenticación básica:

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
| `connectionSpec.id` | El ID de especificación de conexión del servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor SFTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### Cree un [!DNL SFTP] conexión base mediante autenticación de clave pública SSH

Para crear un [!DNL SFTP] conexión base usando autenticación de clave pública SSH, realice una solicitud de POST al [!DNL Flow Service] API mientras proporciona valores para la `host`, `userName`, `privateKeyContent`y `passPhrase`.

>[!IMPORTANT]
>
>La variable [!DNL SFTP] El conector admite una clave OpenSSH de tipo RSA o DSA. Asegúrese de que el contenido del archivo clave comience por `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` y termina con `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir del formato PPK al formato OpenSSH.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL SFTP] mediante autenticación de clave pública SSH:

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
| `auth.params.host` | El nombre de host de su [!DNL SFTP] servidor. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL SFTP] servidor. |
| `auth.params.privateKeyContent` | El contenido de clave privada SSH codificada Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `auth.params.passPhrase` | La frase de contraseña o contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido por contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como valor. |
| `connectionSpec.id` | La variable [!DNL SFTP] ID de especificación de conexión del servidor: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar su [!DNL SFTP] en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL SFTP] conexión mediante la función [!DNL Flow Service] y han obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión para [explorar las tiendas en la nube mediante la API de servicio de flujo](../../explore/cloud-storage.md).
