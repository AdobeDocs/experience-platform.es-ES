---
keywords: Experience Platform;inicio;temas populares;google adwords;Google AdWords;adwords
solution: Experience Platform
title: Creación de una conexión base de Google AdWords mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Google AdWords mediante la API de servicio de flujo.
exl-id: 4658e392-1bd9-4e74-aa05-96109f9b62a0
source-git-commit: 17055f76800deadacf435970a691cec79c9f1d17
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 2%

---

# Cree un [!DNL Google AdWords] conexión base utilizando [!DNL Flow Service] API

>[!NOTE]
>
>La variable [!DNL Google AdWords] El conector está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Google AdWords] (en lo sucesivo, &quot;el[!DNL AdWords]&quot;) usando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL AdWords] usando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL AdWords], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `clientCustomerId` | El ID de cliente de la variable [!DNL AdWords] cuenta. |
| `developerToken` | El token de desarrollador asociado a la cuenta de administrador. |
| `refreshToken` | El token de actualización obtenido de [!DNL Google] para autorizar el acceso a [!DNL AdWords]. |
| `clientId` | El ID de cliente de la variable [!DNL Google] aplicación utilizada para adquirir el token de actualización. |
| `clientSecret` | El secreto de cliente del [!DNL Google] aplicación utilizada para adquirir el token de actualización. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL AdWords] es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

Para obtener más información sobre estos valores, consulte esta [Documento de Google AdWords](https://developers.google.com/adwords/api/docs/guides/authentication).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL AdWords] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL AdWords]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "google-AdWords connection",
        "description": "Connection for google-AdWords",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "clientCustomerID": "{CLIENT_CUSTOMER_ID}",
                "developerToken": "{DEVELOPER_TOKEN}",
                "authenticationType": "{AUTHENTICATION_TYPE}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "d771e9c1-4f26-40dc-8617-ce58c4b53702",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.clientCustomerID` | El ID de cliente de su [!DNL AdWords] cuenta. |
| `auth.params.developerToken` | El token de desarrollador de su [!DNL AdWords] cuenta. |
| `auth.params.refreshToken` | El token de actualización de su [!DNL AdWords] cuenta. |
| `auth.params.clientID` | El ID de cliente de su [!DNL AdWords] cuenta. |
| `auth.params.clientSecret` | El secreto de cliente de su [!DNL AdWords] cuenta. |
| `connectionSpec.id` | La variable [!DNL Google AdWords] id. de especificación de conexión: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Google AdWords] conexión base utilizando [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante el [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para incluir datos publicitarios en Platform mediante la variable [!DNL Flow Service] API](../../collect/advertising.md)
