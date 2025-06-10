---
title: Creación de una conexión de Amazon Kinesis Source mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a una fuente de Amazon Kinesis mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 4%

---

# Crear una conexión de origen [!DNL Amazon Kinesis] mediante la API de Flow Service

>[!IMPORTANT]
>
>El origen [!DNL Amazon Kinesis] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Este tutorial lo guiará para conectar [!DNL Amazon Kinesis] (denominado en adelante &quot;[!DNL Kinesis]&quot;) a Experience Platform mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectar correctamente [!DNL Kinesis] a Experience Platform mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con su cuenta de [!DNL Amazon Kinesis], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El identificador de clave de acceso es la mitad del par de claves de acceso que se utilizó para autenticar la cuenta de [!DNL Kinesis] en Experience Platform. |
| `secretKey` | La clave secreta de acceso es la otra mitad del par de claves de acceso que se utilizó para autenticar la cuenta de [!DNL Kinesis] en Experience Platform. |
| `region` | Región de su cuenta de [!DNL Kinesis]. Consulte la guía de [adición de direcciones IP a su lista de permitidos](../../../../ip-address-allow-list.md) para obtener más información sobre las regiones. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión [!DNL Kinesis] es: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Para obtener más información sobre [!DNL Kinesis] claves de acceso y cómo generarlas, consulte esta [[!DNL AWS] guía sobre la administración de claves de acceso para usuarios de IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

El primer paso para crear una conexión de origen es autenticar el origen de [!DNL Kinesis] y generar un identificador de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Kinesis] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Amazon Kinesis connection",
        "description": "Connector for Amazon Kinesis",
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "auth": {
            "specName": "Aws Kinesis authentication credentials",
            "params": {
                "accessKeyId": "{ACCESS_KEY_ID}",
                "secretKey": "{SECRET_KEY}",
                "region": "{REGION}"
            }
        },
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.accessKeyId` | Identificador de clave de acceso de su cuenta de [!DNL Kinesis]. |
| `auth.params.secretKey` | La clave secreta de acceso para su cuenta de [!DNL Kinesis]. |
| `auth.params.region` | Región de su cuenta de [!DNL Kinesis]. |
| `connectionSpec.id` | Id. de especificación de conexión [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Crear una conexión de origen {#source}

Una conexión de origen crea y administra la conexión con el origen externo desde el que se incorporan los datos. Una conexión de origen consta de información como el origen de datos, el formato de datos y el ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica de un inquilino y una organización.

Para crear una conexión de origen, realice una petición POST al extremo `/sourceConnections` de la API [!DNL Flow Service].

**Formato de API**

```http
POST /sourceConnections
```

**Solicitud**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "AWS Kinesis source connection",
        "description": "A source connection for AWS Kinesis",
        "baseConnectionId": "4cb0c374-d3bb-4557-b139-5712880adc55",
        "connectionSpec": {
            "id": "86043421-563b-46ec-8e6c-e23184711bf6",
            "version": "1.0"
        },
        "data": {
            "format": "json"
        },
        "params": {
            "stream": "{STREAM}",
            "dataType": "raw",
            "reset": "latest"
        }
    }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Nombre de la conexión de origen. Asegúrese de que el nombre de la conexión de origen sea descriptivo, ya que puede utilizarlo para buscar información sobre la conexión de origen. |
| `description` | Un valor opcional que puede proporcionar para incluir más información sobre la conexión de origen. |
| `baseConnectionId` | Identificador de conexión base del origen [!DNL Kinesis] que se generó en el paso anterior. |
| `connectionSpec.id` | Identificador de especificación de conexión fija para [!DNL Kinesis]. Este identificador es: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | Formato de los datos de [!DNL Kinesis] que desea introducir. Actualmente, el único formato de datos compatible es `json`. |
| `params.stream` | Nombre del flujo de datos desde el que se extraen registros. |
| `params.dataType` | Este parámetro define el tipo de datos que se están introduciendo. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Use `latest` para comenzar a leer los datos más recientes y use `earliest` para comenzar a leer los primeros datos disponibles en el flujo. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

>[!NOTE]
>
>Después de crear o actualizar un flujo de datos de flujo continuo, se requiere una breve pausa de 5 minutos en la ingesta de datos para evitar cualquier posible instancia de pérdida o caída de datos.

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de origen [!DNL Kinesis] mediante la API [!DNL Flow Service]. Puede usar este identificador de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo usando la [!DNL Flow Service] API](../../collect/streaming.md).
