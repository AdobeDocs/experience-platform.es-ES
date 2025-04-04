---
title: Creación de una conexión base SFTP mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor SFTP (Protocolo seguro de transferencia de archivos) mediante la API de Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 3%

---

# Crear una conexión base SFTP mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL SFTP] (Protocolo seguro de transferencia de archivos) mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

>[!IMPORTANT]
>
>Se recomienda evitar líneas nuevas o retornos de carro al ingerir objetos JSON con una conexión de origen [!DNL SFTP]. Para solucionar la limitación, utilice un solo objeto JSON por línea y utilice varias líneas para los archivos siguientes.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a un servidor [!DNL SFTP] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [[!DNL SFTP] guía de autenticación](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) para ver los pasos detallados sobre cómo recuperar sus credenciales de autenticación.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

>[!TIP]
>
>Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL SFTP]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

El origen [!DNL SFTP] admite la autenticación básica y la autenticación mediante clave pública SSH. Durante este paso, también puede designar la ruta a la subcarpeta a la que desea proporcionar acceso.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL SFTP] como parte de los parámetros de solicitud.

>[!IMPORTANT]
>
>El conector [!DNL SFTP] admite una clave OpenSSH de tipo RSA o DSA. Asegúrese de que el contenido del archivo de claves comience por `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` y termine por `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir de formato PPK a formato OpenSSH.

**Formato de API**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticación básica]

+++Solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.port` | El puerto del servidor SFTP. El valor predeterminado de este entero es 22. |
| `auth.params.username` | El nombre de usuario asociado con el servidor SFTP. |
| `auth.params.password` | La contraseña asociada a su servidor SFTP. |
| `auth.params.maxConcurrentConnections` | Número máximo de conexiones simultáneas especificadas al conectar Experience Platform a SFTP. Cuando está habilitado, este valor debe establecerse en al menos 1. |
| `auth.params.folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `auth.params.disableChunking` | Un valor booleano que se utiliza para determinar si el servidor SFTP admite o no la fragmentación. |
| `connectionSpec.id` | Identificador de especificación de conexión del servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Respuesta

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor SFTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB Autenticación de clave pública SSH]

+++Solicitud

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales",
              "disableChunking": "true"
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
| `auth.params.host` | El nombre de host del servidor [!DNL SFTP]. |
| `auth.params.port` | El puerto del servidor SFTP. El valor predeterminado de este entero es 22. |
| `auth.params.username` | El nombre de usuario asociado con su servidor [!DNL SFTP]. |
| `auth.params.privateKeyContent` | El contenido de clave privada SSH codificado en Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `auth.params.passPhrase` | La contraseña o frase de paso para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de paso. Si PrivateKeyContent está protegido con contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como valor. |
| `auth.params.maxConcurrentConnections` | Número máximo de conexiones simultáneas especificadas al conectar Experience Platform a SFTP. Cuando está habilitado, este valor debe establecerse en al menos 1. |
| `auth.params.folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `auth.params.disableChunking` | Un valor booleano que se utiliza para determinar si el servidor SFTP admite o no la fragmentación. |
| `connectionSpec.id` | Id. de especificación de conexión de servidor [!DNL SFTP]: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++Respuesta

Una respuesta correcta devuelve el identificador único (`id`) de la conexión recién creada. Este ID es necesario para explorar el servidor SFTP en el siguiente tutorial.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL SFTP] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede usar este identificador de conexión para [explorar los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
