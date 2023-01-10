---
keywords: Experience Platform;inicio;temas populares;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creación de una conexión de origen de Amazon Kinesis mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un origen de Amazon Kinesis mediante la API de servicio de flujo.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Cree un [!DNL Amazon Kinesis] conexión de origen mediante la API de servicio de flujo

Este tutorial le guía por los pasos para conectarse [!DNL Amazon Kinesis] (en lo sucesivo, &quot;el[!DNL Kinesis]&quot;) al Experience Platform, usando el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, a la vez que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL Kinesis] a Platform que utiliza la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con su [!DNL Amazon Kinesis] debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de clave de acceso es la mitad del par de clave de acceso utilizado para autenticar su [!DNL Kinesis] a Platform. |
| `secretKey` | La clave de acceso secreta es la otra mitad del par de claves de acceso que se utiliza para autenticar su [!DNL Kinesis] a Platform. |
| `region` | La región de [!DNL Kinesis] cuenta. Consulte la guía de [adición de direcciones IP a la lista de permitidos](../../../../ip-address-allow-list.md) para obtener más información sobre las regiones. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. La variable [!DNL Kinesis] el ID de especificación de conexión es: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Para obtener más información, consulte [!DNL Kinesis] acceder a las claves y cómo generarlas, consulte esta [[!DNL AWS] guía sobre la administración de claves de acceso para usuarios de IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

El primer paso para crear una conexión de origen es autenticar su [!DNL Kinesis] y genere un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Kinesis] credenciales de autenticación como parte de los parámetros de solicitud.

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
| `auth.params.accessKeyId` | El ID de clave de acceso para su [!DNL Kinesis] cuenta. |
| `auth.params.secretKey` | La clave de acceso secreta para su [!DNL Kinesis] cuenta. |
| `auth.params.region` | La región de [!DNL Kinesis] cuenta. |
| `connectionSpec.id` | La variable [!DNL Kinesis] id. de especificación de conexión: `86043421-563b-46ec-8e6c-e23184711bf6` |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"6507cfd8-0000-0200-0000-5e18fc600000\""
}
```

## Crear una conexión de origen {#source}

Una conexión de origen crea y administra la conexión con el origen externo desde el que se introducen los datos. Una conexión de origen consiste en información como el origen de datos, el formato de datos y el ID de conexión de origen necesario para crear un flujo de datos. Una instancia de conexión de origen es específica para un inquilino y una organización IMS.

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
| `baseConnectionId` | El ID de conexión base de su [!DNL Kinesis] fuente que se generó en el paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión fija para [!DNL Kinesis]. Este ID es: `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | El formato de la variable [!DNL Kinesis] datos que desea ingerir. Actualmente, el único formato de datos admitido es `json`. |
| `params.stream` | Nombre del flujo de datos desde el que se extraerán los registros. |
| `params.dataType` | Este parámetro define el tipo de datos que se están incorporando. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Uso `latest` para empezar a leer los datos más recientes y usar `earliest` para empezar a leer los primeros datos disponibles del flujo. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Kinesis] conexión de origen utilizando la variable [!DNL Flow Service] API. Puede utilizar este ID de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo mediante el [!DNL Flow Service] API](../../collect/streaming.md).
