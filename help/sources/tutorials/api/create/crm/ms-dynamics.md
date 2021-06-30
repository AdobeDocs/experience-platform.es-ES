---
keywords: Experience Platform;inicio;temas populares;Microsoft Dynamics;microsoft dynamics;dinámica;Dynamics
solution: Experience Platform
title: Crear una conexión de Microsoft Dynamics Base mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Platform a una cuenta de Microsoft Dynamics mediante la API de servicio de flujo.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: 8035539321f5016521208aa110a4ee2881cb5d1e
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Crear una conexión base [!DNL Microsoft Dynamics] utilizando la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Microsoft Dynamics] (en adelante denominada &quot;[!DNL Dynamics]&quot;) mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al mismo tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Simuladores para pruebas](../../../../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectar correctamente Platform a una cuenta de Dynamics mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL Dynamics], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `serviceUri` | La URL de servicio de su instancia [!DNL Dynamics]. |
| `username` | El nombre de usuario de su cuenta de usuario [!DNL Dynamics]. |
| `password` | La contraseña de su cuenta [!DNL Dynamics]. |
| `servicePrincipalId` | El ID de cliente de su cuenta [!DNL Dynamics]. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `servicePrincipalKey` | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Dynamics] es: `38ad80fe-8b06-4938-94f4-d4ee80266b07`. |

Para obtener más información sobre cómo empezar, visite [este [!DNL Dynamics] documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL Dynamics] como parte de los parámetros de solicitud.

### Crear una conexión base [!DNL Dynamics] utilizando autenticación básica

Para crear una conexión base [!DNL Dynamics] utilizando autenticación básica, realice una solicitud de POST a la API [!DNL Flow Service] mientras proporciona valores para las `serviceUri`, `username` y `password` de la conexión.

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
| `auth.params.serviceUri` | El URI de servicio asociado a su instancia [!DNL Dynamics]. |
| `auth.params.username` | El nombre de usuario asociado a su cuenta [!DNL Dynamics]. |
| `auth.params.password` | La contraseña asociada a su cuenta [!DNL Dynamics]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Crear una conexión base [!DNL Dynamics] mediante autenticación basada en claves de servicio principal

Para crear una conexión base [!DNL Dynamics] utilizando autenticación basada en claves principales de servicio, realice una solicitud de POST a la API [!DNL Flow Service] mientras proporciona valores para las `serviceUri`, `servicePrincipalId` y `servicePrincipalKey` de la conexión.

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
| `auth.params.serviceUri` | El URI de servicio asociado a su instancia [!DNL Dynamics]. |
| `auth.params.servicePrincipalId` | El ID de cliente de su cuenta [!DNL Dynamics]. Este ID es necesario cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `auth.params.servicePrincipalKey` | La clave secreta principal del servicio. Esta credencial es necesaria cuando se utiliza la entidad de seguridad del servicio y la autenticación basada en claves. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Dynamics]: `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Dynamics] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial, mientras aprende a [explorar los sistemas CRM mediante la API de servicio de flujo](../../explore/crm.md).
