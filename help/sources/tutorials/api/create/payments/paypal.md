---
keywords: Experience Platform;inicio;temas populares;conector de PayPal;PayPal;PayPal
solution: Experience Platform
title: Creación de una conexión base de PayPal mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar PayPal a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 5e6ca7b4-5e2f-4706-a339-ac159e2e0938
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 5%

---

# Crear una conexión base [!DNL PayPal] mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL PayPal] quedará obsoleto a finales de mayo de 2025. Como alternativa, puede utilizar el origen [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md).

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL PayPal] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL PayPal] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL PayPal], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Dirección URL de la instancia [!DNL PayPal]. (valor predeterminado: api.sandbox.paypal.com). |
| `clientId` | Identificador de cliente asociado con la aplicación [!DNL PayPal]. |
| `clientSecret` | Secreto de cliente asociado a la aplicación [!DNL PayPal]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL PayPal] es: `221c7626-58f6-4eec-8ee2-042b0226f03b` |

Para obtener más información sobre cómo empezar, consulte [este documento de PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL PayPal] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL PayPal]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Paypal connection",
        "description": "Paypal connection",
        "auth": {
        "specName": "Client-Id-Secret Based Authentication",
        "params": {
            "host": "{HOST}",
            "clientId": "{CLIENT_ID}",
            "clientSecret": "{CLIENT_SECRET}"
            }
        },
        "connectionSpec": {
            "id": "221c7626-58f6-4eec-8ee2-042b0226f03b",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | Dirección URL de la instancia [!DNL PayPal]. |
| `auth.params.clientId` | El ID de cliente asociado con su instancia de [!DNL PayPal]. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su instancia de [!DNL PayPal]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL PayPal]: `221c7626-58f6-4eec-8ee2-042b0226f03b`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "24151d58-ffa7-4960-951d-58ffa7396097",
    "etag": "\"65015e9d-0000-0200-0000-5e89162d0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL PayPal] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de pagos a Platform mediante la API  [!DNL Flow Service] ](../../collect/payments.md)
