---
keywords: Experience Platform;inicio;temas populares;salesforce marketing cloud;Marketing Cloud de Salesforce
solution: Experience Platform
title: Creación de una conexión base de Marketing Cloud de Salesforce mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform al Marketing Cloud de Salesforce mediante la API de servicio de flujo.
source-git-commit: b4291b4f13918a1f85d73e0320c67dd2b71913fc
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 1%

---

# Crear una conexión base [!DNL Salesforce Marketing Cloud] utilizando la API [!DNL Flow Service]

>[!NOTE]
>
>El origen [!DNL Salesforce Marketing Cloud] está en versión beta. Consulte [sources overview](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Salesforce Marketing Cloud] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que deberá conocer para conectarse correctamente a [!DNL Salesforce Marketing Cloud] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Salesforce Marketing Cloud], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El servidor host de la aplicación. Este suele ser su subdominio. |
| `clientId` | El ID de cliente asociado con su aplicación [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | El secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Salesforce Marketing Cloud] es: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` mientras proporciona las credenciales de autenticación [!DNL Salesforce Marketing Cloud] como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Marketing Cloud base connection",
        "description": "Salesforce Marketing Cloud base connection",
        "auth": {
            "specName": "Client-Id-Secret Based Authentication",
            "params": {
                "host": "{HOST}"
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "cea1c2a08-b722-11eb-8529-0242ac130003",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.clientId` | El ID de cliente asociado con su aplicación [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | El secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Salesforce Marketing Cloud]: `cea1c2a08-b722-11eb-8529-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Siguiendo este tutorial, ha creado una conexión [!DNL Salesforce Marketing Cloud] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID de conexión en el siguiente tutorial, mientras aprende a explorar los [sistemas de automatización de marketing mediante la API de servicio de flujo](../../explore/marketing-automation.md).
