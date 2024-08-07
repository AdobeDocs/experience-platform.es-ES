---
title: Creación de una conexión base de Google BigQuery mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a Google BigQuery mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# Crear una conexión base [!DNL Google BigQuery] mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Google BigQuery] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL Google BigQuery] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): El Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Google BigQuery] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] conecte [!DNL Google BigQuery] a Platform, debe proporcionar los siguientes valores de autenticación OAuth 2.0:

| Credencial | Descripción |
| ---------- | ----------- |
| `project` | Identificador de proyecto del proyecto predeterminado [!DNL Google BigQuery] con el que se va a realizar la consulta. |
| `clientID` | El valor de ID utilizado para generar el token de actualización. |
| `clientSecret` | El valor secreto utilizado para generar el token de actualización. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] se usó para autorizar el acceso a [!DNL Google BigQuery]. |
| `largeResultsDataSetId` | El ID del conjunto de datos [!DNL Google BigQuery] creado previamente que es necesario para habilitar la compatibilidad con grandes conjuntos de resultados. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Google BigQuery] es: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

Para obtener más información sobre estos valores, consulte este [[!DNL Google BigQuery] documento](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL Google BigQuery] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Google BigQuery]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.project` | Identificador de proyecto del proyecto predeterminado [!DNL Google BigQuery] que se va a consultar. en contra. |
| `auth.params.clientId` | El valor de ID utilizado para generar el token de actualización. |
| `auth.params.clientSecret` | Valor de cliente utilizado para generar el token de actualización. |
| `auth.params.refreshToken` | El token de actualización obtenido de [!DNL Google] se usó para autorizar el acceso a [!DNL Google BigQuery]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Google BigQuery] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
