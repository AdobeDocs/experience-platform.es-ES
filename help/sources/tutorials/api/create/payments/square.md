---
keywords: Experience Platform;inicio;temas populares;cuadrado;cuadrado
title: Creación de una conexión base cuadrada mediante la API de servicio de flujo
description: Obtenga información sobre cómo conectar Square a Adobe Experience Platform mediante la API de servicio de flujo.
exl-id: 82c1d513-3b06-4ce9-b637-2c5a268da506
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 2%

---

# Cree un [!DNL Square] conexión base utilizando [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Square] usando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Square] usando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL Square], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `host` | La dirección URL del [!DNL Square] instancia. |
| `clientId` | El ID de cliente asociado con su [!DNL Square] cuenta. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL Square] cuenta. |
| `accessToken` | El token de acceso se utiliza para autenticar su [!DNL Square] cuenta con autenticación OAuth 2.0. El token de acceso se puede obtener de [!DNL Square]. |
| `refreshToken` | El token de actualización se utiliza para generar nuevos tokens de acceso una vez que caduca el token de acceso actual. El token de actualización se puede obtener de [!DNL Square]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Square] es: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5` |

Para obtener más información sobre estas credenciales y cómo obtenerlas, consulte la [[!DNL Square] documentación sobre OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Square] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Square]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Square Base Connection",
        "description": "Square Base Connection",
        "auth": {
        "specName": "OAuth2 Refresh Code",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            "accessToken": "{ACCESS_TOKEN}"
            "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "2acf109f-9b66-4d5e-bc18-ebb2adcff8d5",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | La dirección URL del [!DNL Square] instancia. |
| `auth.params.clientId` | El ID de cliente asociado con su [!DNL Square] cuenta. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su [!DNL Square] cuenta. |
| `auth.params.accessToken` | El token de acceso se utiliza para autenticar su [!DNL Square] cuenta con autenticación OAuth 2.0. El token de acceso se puede obtener de [!DNL Square]. |
| `auth.params.refreshToken` | El token de actualización se utiliza para generar nuevos tokens de acceso una vez que caduca el token de acceso actual. El token de actualización se puede obtener de [!DNL Square]. |
| `connectionSpec.id` | La variable [!DNL Square] id. de especificación de conexión: `2acf109f-9b66-4d5e-bc18-ebb2adcff8d5`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Square] conexión mediante la función [!DNL Flow Service] y han obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial mientras aprende a [explorar la aplicación de pagos mediante la API de servicio de flujo](../../explore/payments.md).
