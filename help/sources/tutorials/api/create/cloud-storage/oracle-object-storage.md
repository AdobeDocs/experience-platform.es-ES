---
keywords: Experience Platform;inicio;temas populares;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Creación de una conexión base de Oracle Object Storage mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Object Storage mediante la API de Flow Service.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 4%

---

# Crear una conexión base [!DNL Oracle Object Storage] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL Oracle Object Storage] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Oracle Object Storage] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | Extremo [!DNL Oracle Object Storage] necesario para la autenticación. El formato del extremo es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | La clave de acceso [!DNL Oracle Object Storage] necesaria para la autenticación. |
| `secretKey` | Se requiere la contraseña [!DNL Oracle Object Storage] para la autenticación. |
| `bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y finalizar con una letra o un número, y solo puede contener letras minúsculas, números o guiones (`-`). El nombre del contenedor no puede tener el formato de una dirección IP. |
| `folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Oracle Object Storage] es: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Para obtener más información sobre cómo obtener estos valores, consulte la [guía de autenticación de Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Oracle Object Storage] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Oracle Object Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.serviceUrl` | Extremo [!DNL Oracle Object Storage] necesario para la autenticación. |
| `auth.params.accessKey` | La clave de acceso [!DNL Oracle Object Storage] necesaria para la autenticación. |
| `auth.params.secretKey` | Se requiere la contraseña [!DNL Oracle Object Storage] para la autenticación. |
| `auth.params.bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. |
| `auth.params.folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL Oracle Object Storage]: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de la conexión recién creada. Este ID es necesario para explorar los datos de almacenamiento en la nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Oracle Object Storage] mediante la API [!DNL Flow Service] y ha obtenido su identificador de conexión único. Puede usar este identificador de conexión para [explorar los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
