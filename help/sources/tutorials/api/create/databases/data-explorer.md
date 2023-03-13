---
keywords: Experience Platform;inicio;temas populares;Data Explorer de Azure;Data Explorer de Azure;Data Explorer de Azure
solution: Experience Platform
title: Crear una conexión de base de Data Explorer de Azure mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar la Data Explorer de Azure a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 2%

---

# Crear un [!DNL Azure Azure Data Explorer] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Azure Data Explorer] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Azure Data Explorer] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Azure Data Explorer], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | El punto final del [!DNL Azure Data Explorer] servidor. |
| `database` | El nombre del [!DNL Azure Data Explorer] base de datos. |
| `tenant` | ID único de inquilino utilizado para conectarse a [!DNL Azure Data Explorer] base de datos. |
| `servicePrincipalId` | El ID principal de servicio único utilizado para conectarse a [!DNL Azure Data Explorer] base de datos. |
| `servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse al [!DNL Azure Data Explorer] base de datos. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Azure Data Explorer] es `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Azure Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Azure Data Explorer] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Azure Data Explorer]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Azure Data Explorer connection",
        "description": "A connection for Azure Azure Data Explorer",
        "auth": {
            "specName": "Service Principal Based Authentication",
            "params": {
                    "endpoint": "{ENDPOINT}",
                    "database": "{DATABASE}",
                    "tenant": "{TENANT}",
                    "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                    "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
                }
        },
        "connectionSpec": {
            "id": "0479cc14-7651-4354-b233-7480606c2ac3",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.endpoint` | El punto final del [!DNL Azure Data Explorer] servidor. |
| `auth.params.database` | El nombre del [!DNL Azure Data Explorer] base de datos. |
| `auth.params.tenant` | ID único de inquilino utilizado para conectarse a [!DNL Azure Data Explorer] base de datos. |
| `auth.params.servicePrincipalId` | El ID principal de servicio único utilizado para conectarse a [!DNL Azure Data Explorer] base de datos. |
| `auth.params.servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse al [!DNL Azure Data Explorer] base de datos. |
| `connectionSpec.id` | El [!DNL Azure Data Explorer] identificador de especificación de conexión: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Azure Data Explorer] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
