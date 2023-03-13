---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: Crear una conexión base de Microsoft Dynamics mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Platform a una cuenta de Microsoft Dynamics mediante la API de Flow Service.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 2%

---

# Crear un [!DNL Microsoft Dynamics] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Microsoft Dynamics] (en lo sucesivo, &quot;[!DNL Dynamics]&quot;) utilizando el [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectar correctamente Platform a una cuenta de Dynamics mediante [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse a [!DNL Dynamics], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La URL de servicio de su [!DNL Dynamics] ejemplo. |
| `username` | El nombre de usuario de su [!DNL Dynamics] cuenta de usuario. |
| `password` | La contraseña de su [!DNL Dynamics] cuenta. |
| `servicePrincipalId` | El ID de cliente de su [!DNL Dynamics] cuenta. Este ID es necesario cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `servicePrincipalKey` | La clave secreta principal de servicio. Esta credencial es necesaria cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Dynamics] es: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Para obtener más información sobre cómo empezar, visite [esta [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Dynamics] credenciales de autenticación como parte de los parámetros de solicitud.

### Crear un [!DNL Dynamics] conexión base mediante autenticación básica

Para crear un [!DNL Dynamics] conexión base mediante autenticación básica, realice una solicitud de POST al [!DNL Flow Service] API, al tiempo que proporciona valores para el `serviceUri`, `username`, y `password`.

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
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUri` | El URI de servicio asociado con su [!DNL Dynamics] ejemplo. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Dynamics] cuenta. |
| `auth.params.password` | La contraseña asociada a su [!DNL Dynamics] cuenta. |
| `connectionSpec.id` | El [!DNL Dynamics] identificador de especificación de conexión: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Crear un [!DNL Dynamics] conexión base mediante autenticación basada en claves principales de servicio

Para crear un [!DNL Dynamics] conexión base mediante autenticación basada en claves principales de servicio, realice una solicitud de POST al [!DNL Flow Service] API, al tiempo que proporciona valores para el `serviceUri`, `servicePrincipalId`, y `servicePrincipalKey`.

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
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.serviceUri` | El URI de servicio asociado con su [!DNL Dynamics] ejemplo. |
| `auth.params.servicePrincipalId` | El ID de cliente de su [!DNL Dynamics] cuenta. Este ID es necesario cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `auth.params.servicePrincipalKey` | La clave secreta principal de servicio. Esta credencial es necesaria cuando se utiliza la autenticación principal del servicio y basada en claves. |
| `connectionSpec.id` | El [!DNL Dynamics] identificador de especificación de conexión: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Microsoft Dynamics] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos CRM a Platform mediante [!DNL Flow Service] API](../../collect/crm.md)
