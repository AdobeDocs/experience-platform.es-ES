---
keywords: Experience Platform;inicio;temas populares;IBM [!DNL IBM DB2];IBM;ibm [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: Creación de una IBM [!DNL IBM DB2] Conexión base mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar IBM [!DNL IBM DB2] a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 2%

---

# Creación de una IBM [!DNL IBM DB2] conexión base mediante el [!DNL Flow Service] API

>[!NOTE]
>
>El IBM [!DNL IBM DB2] el conector está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL IBM DB2] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL IBM DB2] uso del [!DNL Flow Service] API.

| Credencial | Descripción |
| ---------- | ----------- |
| `server` | El nombre del [!DNL IBM DB2] servidor. Puede especificar el número de puerto después del nombre del servidor delimitado por dos puntos. Por ejemplo: server:port. |
| `database` | El nombre del [!DNL IBM DB2] base de datos. |
| `username` | El nombre de usuario utilizado para conectarse a [!DNL IBM DB2] base de datos. |
| `password` | Contraseña de la cuenta de usuario especificada para el nombre de usuario. |
| `connectionSpec.id` | El identificador único necesario para crear una conexión. Identificador de especificación de conexión para [!DNL IBM DB2] es `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

Para obtener más información sobre cómo empezar, consulte [esta [!DNL IBM DB2] documento](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL IBM DB2] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL IBM DB2]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión asociada a su [!DNL IBM DB2] cuenta. |
| `connectionSpec.id` | El [!DNL IBM DB2] identificador de especificación de conexión: `09182899-b429-40c9-a15a-bf3ddbc8ced7`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL IBM DB2] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)

