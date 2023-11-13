---
keywords: Experience Platform;inicio;temas populares;[!DNL Azure Table Storage];[!DNL Azure Table Storage];Azure Table Storage
solution: Experience Platform
title: Crear una conexión base de Azure Table Storage mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Azure Table Storage a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 8ebd5d77-ed1f-47e1-8212-efb6c5e84ec1
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 6%

---

# Crear un [!DNL Azure Table Storage] conexión base mediante el [!DNL Flow Service] API

>[!NOTE]
>
>El [!DNL Azure Table Storage] el conector está en versión beta. Consulte la [Resumen de orígenes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores etiquetados como beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Azure Table Storage] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Azure Table Storage] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Azure Table Storage], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión utilizada para conectarse a un [!DNL Azure Table Storage] ejemplo. El patrón de cadena de conexión para [!DNL Azure Table Storage] es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Azure Table Storage] es `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

Para obtener más información sobre la obtención de una cadena de conexión, consulte [esta [!DNL Azure Table Storage] documento](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Cree una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Azure Table Storage] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Azure Table Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Azure Table Storage connection",
        "description": "Azure Table Storage connection",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}"
            }
        },
        "connectionSpec": {
            "id": "ecde33f2-c56f-46cc-bdea-ad151c16cd69",
            "version": "1.0"
        }
    }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión utilizada para conectarse a un [!DNL Azure Table Storage] ejemplo. El patrón de cadena de conexión para [!DNL Azure Table Storage] es: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. |
| `connectionSpec.id` | El [!DNL Azure Table Storage] identificador de especificación de conexión: `ecde33f2-c56f-46cc-bdea-ad151c16cd69`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "82abddb3-d59a-436c-abdd-b3d59a436c21",
    "etag": "\"7d00fde3-0000-0200-0000-5e84d9430000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Azure Table Storage] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
