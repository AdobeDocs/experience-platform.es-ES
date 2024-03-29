---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Creación de una conexión base de Zoho CRM mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Adobe Experience Platform a Zoho CRM mediante la API de Flow Service.
exl-id: 33995927-8f5e-44c5-b809-4db8706bbd34
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---

# Crear un [!DNL Zoho CRM] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Zoho CRM] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesita conocer para conectarse correctamente a [!DNL Zoho CRM] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Zoho CRM], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `endpoint` | El punto final del [!DNL Zoho CRM] servidor al que está realizando la solicitud. |
| `accountsUrl` | La dirección URL de cuentas se utiliza para generar los tokens de acceso y actualización. La dirección URL debe ser específica del dominio. |
| `clientId` | El ID de cliente que corresponde con su [!DNL Zoho CRM] cuenta de usuario. |
| `clientSecret` | El secreto de cliente que corresponde con su [!DNL Zoho CRM] cuenta de usuario. |
| `accessToken` | El token de acceso autoriza su acceso seguro y temporal a su [!DNL Zoho CRM] cuenta. |
| `refreshToken` | Un token de actualización es un token que se utiliza para generar un nuevo token de acceso, una vez que el token de acceso ha caducado. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Zoho CRM] es: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

Para obtener más información sobre estas credenciales, consulte la documentación sobre [[!DNL Zoho CRM] authentication](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Zoho CRM] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

>[!TIP]
>
>El dominio URL de las cuentas debe corresponder con la ubicación de dominio adecuada. A continuación se indican los distintos dominios y las direcciones URL de sus cuentas correspondientes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Australia: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>India: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

La siguiente solicitud crea una conexión base para [!DNL Zoho CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Zoho CRM base connection",
        "description": "Base Connection for Zoho CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "accountsUrl": "{ACCOUNTS_URL}",
                "clientId": "{CLIENT_ID}",
                "clientSecret": "{CLIENT_SECRET}",
                "accessToken": "{ACCESS_TOKEN}",
                "refreshToken": "{REFRESH_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "929e4450-0237-4ed2-9404-b7e1e0a00309",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | El nombre de su [!DNL Zoho CRM] conexión base. Puede utilizar este nombre para buscar su [!DNL Zoho CRM] conexión base. |
| `description` | Una descripción opcional para su [!DNL Zoho CRM] conexión base. |
| `auth.specName` | Tipo de autenticación utilizado para la conexión. |
| `auth.params.endpoint` | El punto final del [!DNL Zoho CRM] servidor al que está realizando la solicitud. |
| `auth.params.accountsUrl` | La dirección URL de cuentas se utiliza para generar los tokens de acceso y actualización. La dirección URL debe ser específica del dominio. |
| `auth.params.clientId` | El ID de cliente que corresponde con su [!DNL Zoho CRM] cuenta de usuario. |
| `auth.params.clientSecret` | El secreto de cliente que corresponde con su [!DNL Zoho CRM] cuenta de usuario. |
| `auth.params.accessToken` | El token de acceso autoriza su acceso seguro y temporal a su [!DNL Zoho CRM] cuenta. |
| `auth.params.refreshToken` | Un token de actualización es un token que se utiliza para generar un nuevo token de acceso, una vez que el token de acceso ha caducado. |
| `connectionSpec.id` | Identificador de especificación de conexión para [!DNL Zoho CRM]: `929e4450-0237-4ed2-9404-b7e1e0a00309`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Zoho] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos CRM a Platform mediante [!DNL Flow Service] API](../../collect/crm.md)
