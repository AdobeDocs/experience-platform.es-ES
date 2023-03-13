---
keywords: Experience Platform;inicio;temas populares;hubspot;hubspot
solution: Experience Platform
title: Creación de una conexión base de HubSpot mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Adobe Experience Platform a HubSpot mediante la API de Flow Service.
exl-id: a3e64215-a82d-4aa7-8e6a-48c84c056201
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 2%

---

# Crear un [!DNL HubSpot] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL HubSpot] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL HubSpot] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL HubSpot], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientId` | El ID de cliente asociado con su [!DNL HubSpot] aplicación. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL HubSpot] aplicación. |
| `accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `refreshToken` | El token de actualización obtenido al autenticar inicialmente la integración de OAuth. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL HubSpot] es: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

Para obtener más información sobre cómo empezar, consulte esta [Documento de HubSpot](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL HubSpot] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL HubSpot]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "connection for HubSpot",
        "description": "connection for HubSpot",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "cc6a4487-9e91-433e-a3a3-9cf6626c1806",
            "version": "1.0"
        }
    }
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.clientId` | El ID de cliente asociado con su [!DNL HubSpot] aplicación. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su [!DNL HubSpot] aplicación. |
| `auth.params.accessToken` | El token de acceso obtenido al autenticar inicialmente la integración de OAuth. |
| `auth.params.refreshToken` | El token de actualización obtenido al autenticar inicialmente la integración de OAuth. |
| `connectionSpec.id` | El [!DNL HubSpot] identificador de especificación de conexión: `cc6a4487-9e91-433e-a3a3-9cf6626c1806`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL HubSpot] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Platform mediante [!DNL Flow Service] API](../../collect/marketing-automation.md)
