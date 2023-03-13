---
keywords: Experience Platform;inicio;temas populares;Azure Data Lake Storage Gen2;Azure Data Lake Storage;Azure Data Lake Storage;Azure
solution: Experience Platform
title: Crear una conexión base de Azure Data Lake Storage Gen2 mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Azure Data Lake Storage Gen2 mediante la API de Flow Service.
exl-id: cad5e2a0-e27c-4130-9ad8-888352c92f04
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---

# Crear un [!DNL Azure Data Lake Storage Gen2] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Azure Data Lake Storage Gen2] (en lo sucesivo, &quot;ADLS Gen2&quot;) utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para crear correctamente una conexión de origen ADLS Gen2 utilizando [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse a ADLS Gen2, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | Extremo de ADLS Gen2. El patrón de extremo es: `https://<accountname>.dfs.core.windows.net`. |
| `servicePrincipalId` | ID de cliente de la aplicación. |
| `servicePrincipalKey` | La clave de la aplicación. |
| `tenant` | La información del inquilino que contiene su aplicación. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El ID de especificación de conexión para ADLS Gen2 es: `b3ba5556-48be-44b7-8b85-ff2b69b46dc4`. |

Para obtener más información, consulte [este documento ADLS Gen2](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar sus credenciales de autenticación ADLS Gen2 como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para ADLS Gen2:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "adls-gen2",
        "description": "Connection for adls-gen2",
        "auth": {
            "specName": "Basic Authentication for adls-gen2",
            "params": {
                "url": "{URL}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}",
                "tenant": "{TENANT}"
            }
        },
        "connectionSpec": {
            "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.url` | Punto final de URL de la cuenta ADLS Gen2. |
| `auth.params.servicePrincipalId` | El ID principal de servicio de su cuenta ADLS Gen2. |
| `auth.params.servicePrincipalKey` | La clave principal de servicio de su cuenta de ADLS Gen2. |
| `auth.params.tenant` | La información de inquilino de su cuenta de ADLS Gen2. |
| `connectionSpec.id` | ID de especificación de conexión ADLS Gen2: `b3ba5556-48be-44b7-8b85-ff2b69b46dc41`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "7497ad71-6d32-4973-97ad-716d32797304",
    "etag": "\"23005f80-0000-0200-0000-5e1d00a20000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado una conexión ADLS Gen2 mediante API y se ha obtenido un ID único como parte del cuerpo de respuesta. Puede usar este ID de conexión para lo siguiente [explore los almacenes en la nube mediante la API de Flow Service](../../explore/cloud-storage.md).
