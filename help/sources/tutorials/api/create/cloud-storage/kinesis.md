---
keywords: Experience Platform;inicio;temas populares;Kinesis;kinesis;Amazon Kinesis;amazon kinesis
solution: Experience Platform
title: Creación de una conexión de origen de Amazon Kinesis mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a un origen de Amazon Kinesis mediante la API de servicio de flujo.
exl-id: 64da8894-12ac-45a0-b03e-fe9b6aa435d3
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 2%

---

# Creación de una conexión de origen [!DNL Amazon Kinesis] mediante la API de servicio de flujo

Este tutorial le guía por los pasos para conectar [!DNL Amazon Kinesis] (en adelante denominado &quot;[!DNL Kinesis]&quot;) con el Experience Platform, utilizando la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectar correctamente [!DNL Kinesis] a Platform mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con su cuenta [!DNL Amazon Kinesis], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `accessKeyId` | El ID de clave de acceso es la mitad del par de clave de acceso utilizado para autenticar su cuenta [!DNL Kinesis] en Platform. |
| `secretKey` | La clave de acceso secreta es la otra mitad del par de claves de acceso utilizado para autenticar su cuenta [!DNL Kinesis] en Platform. |
| `region` | Región de la cuenta [!DNL Kinesis]. Consulte la guía [adición de direcciones IP a la lista de permitidos](../../../../ip-address-allow-list.md) para obtener más información sobre las regiones. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión [!DNL Kinesis] es: `86043421-563b-46ec-8e6c-e23184711bf6`. |

Para obtener más información sobre las claves de acceso [!DNL Kinesis] y cómo generarlas, consulte esta [[!DNL AWS] guía sobre la administración de claves de acceso para los usuarios de IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

El primer paso para crear una conexión de origen es autenticar el origen [!DNL Kinesis] y generar un ID de conexión base. Un ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar elementos específicos que desee introducir, incluida información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL Kinesis] como parte de los parámetros de solicitud.

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `auth.params.accessKeyId` | El ID de clave de acceso para su cuenta [!DNL Kinesis]. |
| `auth.params.secretKey` | La clave de acceso secreta para su cuenta [!DNL Kinesis]. |
| `auth.params.region` | Región de la cuenta [!DNL Kinesis]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Kinesis]: `86043421-563b-46ec-8e6c-e23184711bf6` |

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

Para crear una conexión de origen, realice una solicitud de POST al extremo `/sourceConnections` de la API [!DNL Flow Service].

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
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `baseConnectionId` | El ID de conexión base del origen [!DNL Kinesis] que se generó en el paso anterior. |
| `connectionSpec.id` | El ID de especificación de conexión fija para [!DNL Kinesis]. Este ID es : `86043421-563b-46ec-8e6c-e23184711bf6` |
| `data.format` | El formato de los datos [!DNL Kinesis] que desea introducir. Actualmente, el único formato de datos admitido es `json`. |
| `params.stream` | Nombre del flujo de datos desde el que se extraerán los registros. |
| `params.dataType` | Este parámetro define el tipo de datos que se están incorporando. Los tipos de datos admitidos son: `raw` y `xdm`. |
| `params.reset` | Este parámetro define cómo se leerán los datos. Utilice `latest` para empezar a leer los datos más recientes y utilice `earliest` para comenzar a leer los primeros datos disponibles del flujo. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión de origen recién creada. Este ID es necesario en el siguiente tutorial para crear un flujo de datos.

```json
{
    "id": "e96d6135-4b50-446e-922c-6dd66672b6b2",
    "etag": "\"66013508-0000-0200-0000-5f6e2ae70000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión de origen [!DNL Kinesis] utilizando la API [!DNL Flow Service]. Puede utilizar este ID de conexión de origen en el siguiente tutorial para [crear un flujo de datos de flujo continuo mediante la [!DNL Flow Service] API](../../collect/streaming.md).
