---
title: Creación de una conexión base SFTP mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un servidor SFTP (Protocolo seguro de transferencia de archivos) mediante la API de Flow Service.
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: a826bda356a7205f3d4c0e0836881530dbaaf54e
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 3%

---

# Cree una conexión base SFTP con el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL SFTP] (Protocolo seguro de transferencia de archivos) utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

>[!IMPORTANT]
>
>Se recomienda evitar líneas nuevas o retornos de carro al ingerir objetos JSON con un [!DNL SFTP] conexión de origen. Para solucionar la limitación, utilice un solo objeto JSON por línea y utilice varias líneas para los archivos siguientes.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a un [!DNL SFTP] servidor que utiliza el [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse a [!DNL SFTP], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con su [!DNL SFTP] servidor. |
| `port` | El puerto del servidor SFTP al que se está conectando. Si no se proporciona, el valor predeterminado es `22`. |
| `username` | El nombre de usuario con acceso a su [!DNL SFTP] servidor. |
| `password` | La contraseña de su [!DNL SFTP] servidor. |
| `privateKeyContent` | El contenido de clave privada SSH codificado en Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `passPhrase` | La contraseña o frase de paso para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de paso. Si la variable `privateKeyContent` Si está protegido con contraseña, este parámetro debe utilizarse con la frase de contraseña del contenido de la clave privada como valor. |
| `maxConcurrentConnections` | Este parámetro le permite especificar un límite máximo para el número de conexiones simultáneas que Platform creará al conectarse al servidor SFTP. Debe configurar este valor para que sea inferior al límite establecido por SFTP. **Nota**: Cuando esta configuración está habilitada para una cuenta SFTP existente, solo afectará a flujos de datos futuros y no a flujos de datos existentes. |
| `folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. [!DNL SFTP] origen, puede proporcionar la ruta de la carpeta para especificar el acceso del usuario a la subcarpeta que elija. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL SFTP] es: `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Cree una conexión base

>[!TIP]
>
>Una vez creado, no se puede cambiar el tipo de autenticación de una [!DNL Dynamics] conexión base. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

El [!DNL SFTP] source admite la autenticación básica y la autenticación mediante clave pública SSH. Durante este paso, también puede designar la ruta a la subcarpeta a la que desea proporcionar acceso.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL SFTP] credenciales de autenticación como parte de los parámetros de solicitud.

>[!IMPORTANT]
>
>El [!DNL SFTP] El conector admite una clave OpenSSH de tipo RSA o DSA. Asegúrese de que el contenido del archivo de claves comience por `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` y termina por `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir de formato PPK a formato OpenSSH.

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.maxConcurrentConnections` | Número máximo de conexiones simultáneas especificadas al conectar Platform a SFTP. Cuando está habilitado, este valor debe establecerse en al menos 1. |
| `auth.params.folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `connectionSpec.id` | ID de especificación de conexión del servidor SFTP: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

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
              "folderPath": "acme/business/customers/holidaySales"
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
| `auth.params.port` | El puerto del servidor SFTP. El valor predeterminado de este entero es 22. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL SFTP] servidor. |
| `auth.params.privateKeyContent` | El contenido de clave privada SSH codificado en Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `auth.params.passPhrase` | La contraseña o frase de paso para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de paso. Si PrivateKeyContent está protegido con contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como valor. |
| `auth.params.maxConcurrentConnections` | Número máximo de conexiones simultáneas especificadas al conectar Platform a SFTP. Cuando está habilitado, este valor debe establecerse en al menos 1. |
| `auth.params.folderPath` | La ruta a la carpeta a la que desea proporcionar acceso. |
| `connectionSpec.id` | El [!DNL SFTP] Id. de especificación de conexión de servidor: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

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

Al seguir este tutorial, ha creado un [!DNL SFTP] conexión mediante el [!DNL Flow Service] API y han obtenido el valor de ID único de la conexión. Puede usar este ID de conexión para lo siguiente [explore los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
