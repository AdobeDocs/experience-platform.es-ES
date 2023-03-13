---
keywords: Experience Platform;inicio;temas populares;Azure;Azure File Storage;Azure file storage
solution: Experience Platform
title: Crear una conexión base de Azure File Storage mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Azure File Storage a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Crear un [!DNL Azure File Storage] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Azure File Storage] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Azure File Storage] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Azure File Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El punto final del [!DNL Azure File Storag]Instancia a la que accede. |
| `userId` | El usuario con acceso suficiente al [!DNL Azure File Storage] punto final. |
| `password` | La contraseña de su [!DNL Azure File Storage] instancia |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Azure File Storage] es: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Azure File Storage](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Azure File Storage] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | El punto final del [!DNL Azure File Storage] instancia a la que accede.. |
| `auth.params.userId` | El usuario con acceso suficiente al [!DNL Azure File Storage] punto final. |
| `auth.params.password` | El [!DNL Azure File Storage] clave de acceso. |
| `connectionSpec.id` | El [!DNL Azure File Storage] identificador de especificación de conexión: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Azure File Storage] conexión mediante el [!DNL Flow Service] y han obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial mientras aprende a hacer lo siguiente [explore un almacenamiento en la nube de terceros mediante la API de Flow Service](../../explore/cloud-storage.md).
