---
keywords: Experience Platform;inicio;temas populares;greenplum;Greenplum
solution: Experience Platform
title: Creación de una conexión base de GreenPlum mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar GreenPlum a Adobe Experience Platform mediante la API de Flow Service.
exl-id: c4ce452a-b4c5-46ab-83ab-61b296c271d0
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 2%

---

# Crear un [!DNL GreenPlum] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL GreenPlum] uso del [[!DNL Flow Service] API](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL GreenPlum] uso del [!DNL Flow Service] API.

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL GreenPlum] ejemplo. El patrón de cadena de conexión para [!DNL GreenPlum] es `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}` |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL GreenPlum] es `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

Para obtener más información sobre la adquisición de una cadena de conexión, consulte [este documento de GreenPlum](https://docs.greenplum.org/6-7/security-guide/topics/Authenticate.html).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL GreenPlum] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL GreenPlum]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "GreenPlum test connection",
        "description": "A test connection for a GreenPlum source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "connectionString": "HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "37b6bf40-d318-4655-90be-5cd6f65d334b",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión utilizada para conectarse a un [!DNL GreenPlum] cuenta. El patrón de cadena de conexión es: `HOST={SERVER};PORT={PORT};DB={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |
| `connectionSpec.id` | El [!DNL GreenPlum] identificador de especificación de conexión: `37b6bf40-d318-4655-90be-5cd6f65d334b`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL GreenPlum] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
