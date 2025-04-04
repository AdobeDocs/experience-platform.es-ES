---
keywords: Experience Platform;inicio;temas populares;Apache Hadoop Distributed File System;Apache hadoop;hdfs;HDFS
solution: Experience Platform
title: Creación de una conexión base de Apache HDFS mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar un sistema de archivos distribuido de Apache Hadoop a Adobe Experience Platform mediante la API de Flow Service.
exl-id: 04fa65db-073c-48e1-b981-425185ae08aa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 5%

---

# Crear una conexión base de HDFS [!DNL Apache] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El conector Apache HDFS está en versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Apache Hadoop Distributed File System] (denominada en adelante como &quot;[!DNL HDFS]&quot;) mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL HDFS] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

| Credencial | Descripción |
| ---------- | ----------- |
| `url` | La dirección URL define los parámetros de autenticación necesarios para conectarse a [!DNL HDFS] de forma anónima. Para obtener más información sobre cómo obtener este valor, consulte [este [!DNL HDFS] documento](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL AdWords] es: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL HDFS] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL HDFS]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "HDFS test connection",
        "description": "A test connection for an HDFS source",
        "auth": {
            "specName": "Anonymous Authentication",
            "params": {
                "url": "{URL}"
                }
        },
        "connectionSpec": {
            "id": "54e221aa-d342-4707-bcff-7a4bceef0001",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.url` | Dirección URL que define los parámetros de autenticación necesarios para conectarse a [!DNL HDFS] de forma anónima |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL HDFS]: `54e221aa-d342-4707-bcff-7a4bceef0001`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "6a6a880a-2b15-4051-aa88-0a2b1570516d",
    "etag": "\"1801bb7d-0000-0200-0000-5ed6ad580000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL HDFS] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede usar este identificador en el siguiente tutorial mientras aprende a [explorar un almacenamiento de nube de terceros mediante la API de Flow Service](../../explore/cloud-storage.md).
