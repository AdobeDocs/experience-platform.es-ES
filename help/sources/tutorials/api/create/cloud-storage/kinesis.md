---
title: Creación de una conexión de origen de Amazon Kinesis mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una fuente de Kinesis de Amazon mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 4%

---

# Crear un [!DNL Amazon Kinesis] conexión de origen mediante la API de Flow Service

>[!IMPORTANT]
>
>El [!DNL Amazon Kinesis] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Este tutorial lo acompañará durante los pasos para conectarse [!DNL Amazon Kinesis] (en lo sucesivo, &quot;[!DNL Kinesis]&quot;) al Experience Platform, utilizando [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): el Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): el Experience Platform proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL Kinesis] a Platform mediante el [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse con su [!DNL Amazon Kinesis] En su cuenta de, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de clave de acceso es la mitad del par de claves de acceso que se utiliza para autenticar su [!DNL Kinesis] a Platform. |
| `secretKey` | La clave secreta de acceso es la otra mitad del par de claves de acceso que se utiliza para autenticar su [!DNL Kinesis] a Platform. |
| `region` | La región para su [!DNL Kinesis] cuenta. Consulte la guía de [adición de direcciones IP a la lista de permitidos](../../../../ip-address-allow-list.md) para obtener más información sobre las regiones. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El [!DNL Kinesis] ID de especificación de conexión: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Para obtener más información sobre [!DNL Kinesis] las claves de acceso y cómo generarlas, consulte esta sección [[!DNL AWS] guía sobre administración de claves de acceso para usuarios de IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Cree una conexión base

El primer paso para crear una conexión de origen es autenticar su [!DNL Kinesis] y generar un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Kinesis] credenciales de autenticación como parte de los parámetros de solicitud.

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
| `auth.params.accessKeyId` | El ID de la clave de acceso de su [!DNL Kinesis] cuenta. |
| `auth.params.secretKey` | La clave secreta de acceso para su [!DNL Kinesis] cuenta. |
| `auth.params.region` | La región para su [!DNL Kinesis] cuenta. |
| `connectionSpec.id` | El [!DNL Kinesis] identificador de especificación de conexión: `86043421-563b-46ec-8e6c-e23184711bf6` |

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

Para crear una conexión de origen, realice una solicitud de POST al `/sourceConnections` punto final del [!DNL Flow Service] API.

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
| `baseConnectionId` | El ID de conexión base de su [!DNL Kinesis] origen que se generó en el paso anterior. |
| `connectionSpec.id` | Identificador de especificación de conexión fija para [!DNL Kinesis]. Este ID es: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | El formato del [!DNL Kinesis] datos que desea introducir. Actualmente, el único formato de datos admitido es `json`. |
| `params.stream` | Nombre del flujo de datos desde el que se extraen registros. |
| `params.dataType` | Este parámetro define el tipo de datos que se están introduciendo. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Uso `latest` para empezar a leer los datos más recientes, y utilice `earliest` para comenzar a leer los primeros datos disponibles en la secuencia. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Kinesis] conexión de origen mediante [!DNL Flow Service] API. Puede utilizar este ID de conexión de origen en el siguiente tutorial para lo siguiente [crear un flujo de datos de flujo continuo utilizando [!DNL Flow Service] API](../../collect/streaming.md).
