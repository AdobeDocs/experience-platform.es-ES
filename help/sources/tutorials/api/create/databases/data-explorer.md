---
keywords: Experience Platform;inicio;temas populares;Data Explorer de Azure;Data Explorer de Azure;Data Explorer de Azure
solution: Experience Platform
title: Creación de una conexión base de Data Explorer de Azure mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar la Data Explorer de Azure a Adobe Experience Platform mediante la API de servicio de flujo.
exl-id: 1b17bbb0-1f7b-4d89-a158-ad269e6edf30
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Crear una conexión base [!DNL Azure Azure Data Explorer] utilizando la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL Azure Azure Data Explorer] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Azure Data Explore] mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).


## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Azure Data Explorer] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Azure Data Explorer], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `endpoint` | El extremo del servidor [!DNL Azure Data Explorer]. |
| `database` | Nombre de la base de datos [!DNL Azure Data Explorer]. |
| `tenant` | ID de inquilino único que se utiliza para conectarse a la base de datos [!DNL Azure Data Explorer]. |
| `servicePrincipalId` | ID de entidad de seguridad de servicio único utilizado para conectarse a la base de datos [!DNL Azure Data Explorer]. |
| `servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse a la base de datos [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Azure Data Explorer] es `0479cc14-7651-4354-b233-7480606c2ac3`. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Azure Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL Azure Data Explorer] como parte de los parámetros de solicitud.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.endpoint` | El extremo del servidor [!DNL Azure Data Explorer]. |
| `auth.params.database` | Nombre de la base de datos [!DNL Azure Data Explorer]. |
| `auth.params.tenant` | ID de inquilino único que se utiliza para conectarse a la base de datos [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalId` | ID de entidad de seguridad de servicio único utilizado para conectarse a la base de datos [!DNL Azure Data Explorer]. |
| `auth.params.servicePrincipalKey` | La clave principal de servicio única utilizada para conectarse a la base de datos [!DNL Azure Data Explorer]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Azure Data Explorer]: `0479cc14-7651-4354-b233-7480606c2ac3`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Azure Data Explorer] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial, mientras aprende a explorar las [bases de datos mediante la API de servicio de flujo](../../explore/database-nosql.md).
