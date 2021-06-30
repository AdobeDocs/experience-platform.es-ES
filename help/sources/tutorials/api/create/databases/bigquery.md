---
keywords: Experience Platform;inicio;temas populares;bigquery;Google;google;Google BigQuery
solution: Experience Platform
title: Creación de una conexión base de Google BigQuery mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Google BigQuery mediante la API de servicio de flujo.
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: e8c6620a6d2447a577bd56192030ff4353c62c62
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# Crear una conexión base [!DNL Google BigQuery] utilizando la API [!DNL Flow Service]

>[!NOTE]
>
>El conector [!DNL Google BigQuery] está en versión beta. Consulte la [información general sobre fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Google BigQuery] (en adelante denominada &quot;[!DNL BigQuery]&quot;) mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL BigQuery] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte [!DNL BigQuery] a Platform, debe proporcionar los siguientes valores de autenticación de OAuth 2.0:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | El ID del proyecto predeterminado [!DNL BigQuery] con el que realizar la consulta. |
| `clientID` | El valor de ID utilizado para generar el token de actualización. |
| `clientSecret` | El valor secreto utilizado para generar el token de actualización. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] utilizado para autorizar el acceso a [!DNL BigQuery]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL BigQuery] es: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Para obtener más información sobre estos valores, consulte este [[!DNL BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL BigQuery] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection",
        "description": "Google BigQuery connection",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.project` | El ID del proyecto predeterminado [!DNL BigQuery] que se va a consultar. en contra. |
| `auth.params.clientId` | El valor de ID utilizado para generar el token de actualización. |
| `auth.params.clientSecret` | El valor de cliente utilizado para generar el token de actualización. |
| `auth.params.refreshToken` | El token de actualización obtenido de [!DNL Google] utilizado para autorizar el acceso a [!DNL BigQuery]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL BigQuery] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID de conexión en el siguiente tutorial, mientras aprende a explorar las [bases de datos o los sistemas NoSQL mediante la API de servicio de flujo](../../explore/database-nosql.md).
