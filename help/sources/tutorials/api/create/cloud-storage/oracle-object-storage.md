---
keywords: Experience Platform;inicio;temas populares;Almacenamiento de objetos de Oracle;almacenamiento de objetos de oracle
solution: Experience Platform
title: Creación de una conexión base de almacenamiento de objetos de Oracle mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform al almacenamiento de objetos de Oracle mediante la API de Flow Service.
exl-id: a85faa44-7d5a-42a2-9052-af01744e13c9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Crear un [!DNL Oracle Object Storage] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Oracle Object Storage] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Oracle Object Storage] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse a [!DNL Oracle Object Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUrl` | El [!DNL Oracle Object Storage] extremo requerido para la autenticación. El formato del punto de conexión es: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | El [!DNL Oracle Object Storage] identificador de clave de acceso necesario para la autenticación. |
| `secretKey` | El [!DNL Oracle Object Storage] contraseña necesaria para la autenticación. |
| `bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. El nombre del contenedor debe tener entre tres y 63 caracteres, debe comenzar y finalizar con una letra o un número, y solo puede contener letras minúsculas, números o guiones (`-`). El nombre del contenedor no puede tener el formato de una dirección IP. |
| `folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Oracle Object Storage] es: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

Para obtener más información sobre cómo obtener estos valores, consulte la [Guía de autenticación de oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Oracle Object Storage] credenciales de autenticación como parte de los parámetros de solicitud.

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
| `auth.params.serviceUrl` | El [!DNL Oracle Object Storage] extremo requerido para la autenticación. |
| `auth.params.accessKey` | El [!DNL Oracle Object Storage] identificador de clave de acceso necesario para la autenticación. |
| `auth.params.secretKey` | El [!DNL Oracle Object Storage] contraseña necesaria para la autenticación. |
| `auth.params.bucketName` | Se requiere el nombre de contenedor permitido si el usuario tiene acceso restringido. |
| `auth.params.folderPath` | La ruta de carpeta permitida requerida si el usuario tiene acceso restringido. |
| `connectionSpec.id` | El [!DNL Oracle Object Storage] ID de especificación de conexión: `c85f9425-fb21-426c-ad0b-405e9bd8a46c`. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de la conexión recién creada. Este ID es necesario para explorar los datos de almacenamiento en la nube en el siguiente tutorial.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Oracle Object Storage] conexión mediante el [!DNL Flow Service] API y han obtenido su ID de conexión único. Puede usar este ID de conexión para lo siguiente [explore los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
