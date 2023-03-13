---
keywords: Experience Platform;inicio;temas populares;veeva crm;Veeva CRM;Veeva CRM;
solution: Experience Platform
title: Creación de una conexión base de Veeva CRM mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Adobe Experience Platform a Veeva CRM mediante la API de Flow Service.
exl-id: e1aea5a2-a247-43eb-8252-2e2ed96b82a1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 2%

---

# Crear un [!DNL Veeva CRM] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Veeva CRM] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesita conocer para conectarse correctamente a [!DNL Veeva CRM] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Veeva CRM], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | La URL de su [!DNL Veeva CRM] ejemplo. |
| `username` | El valor de nombre de usuario de su [!DNL Veeva CRM] cuenta. |
| `password` | El valor de contraseña de su [!DNL Veeva CRM] cuenta. |
| `securityToken` | El token de seguridad de su [!DNL Veeva CRM] ejemplo. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Veeva CRM] es: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

Para obtener más información sobre estos valores, consulte [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Veeva CRM] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Veeva CRM]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json'
    -d '{
        "name": "Veeva CRM base connection",
        "description": "Base Connection for Veeva CRM",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "environmentUrl": "{ENVIRONMENT_URL}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}",
                "securityToken": "{SECURITY_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "fcad62f3-09b0-41d3-be11-449d5a621b69",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | El nombre de su [!DNL Veeva CRM] conexión base. Puede utilizar este nombre para buscar su [!DNL Veeva CRM] conexión base. |
| `description` | Una descripción opcional para su [!DNL Veeva CRM] conexión base. |
| `auth.specName` | Tipo de autenticación utilizado para la conexión. |
| `auth.params.environmentUrl` | La URL de su [!DNL Veeva CRM] ejemplo. |
| `auth.params.username` | El valor de nombre de usuario de su [!DNL Veeva CRM] cuenta. |
| `auth.params.password` | El valor de contraseña de su [!DNL Veeva CRM] cuenta. |
| `auth.params.securityToken` | El token de seguridad de su [!DNL Veeva CRM] ejemplo. |
| `connectionSpec.id` | Identificador de especificación de conexión para [!DNL Veeva CRM]: `fcad62f3-09b0-41d3-be11-449d5a621b69`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Veeva CRM] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos CRM a Platform mediante [!DNL Flow Service] API](../../collect/crm.md)
