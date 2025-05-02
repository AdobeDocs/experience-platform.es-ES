---
title: Conectar Azure Databricks A Experience Platform Mediante La API De Flow Service
description: Obtenga información sobre cómo conectar Azure Databricks a Experience Platform mediante API.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
exl-id: c3974bab-8e67-49a1-b1a5-d453cf7bfd1d
source-git-commit: 5637a12d5f9cc14b6cf3d88f018aa92de06ab739
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# Conectar [!DNL Azure Databricks] a Experience Platform mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Azure Databricks] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time CDP Ultimate.

Lea esta guía para aprender a conectar su cuenta de [!DNL Azure Databricks] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Lea la guía de [introducción a las API de Experience Platform](../../../../../landing/api-guide.md) para obtener información sobre cómo realizar llamadas a las API de Experience Platform correctamente.

### Configuración de requisitos previos

Lea la [[!DNL Databricks] descripción general](../../../../connectors/databases/databricks.md) para obtener información sobre las configuraciones de requisitos previos que deben completarse primero para poder conectar su cuenta a Experience Platform.

### Recopilar credenciales necesarias

Proporcione valores para las siguientes credenciales a fin de conectar [!DNL Databricks] a Experience Platform.

| Credencial | Descripción |
| --- | --- |
| `domain` | La URL de su área de trabajo [!DNL Databricks]. Por ejemplo, `https://adb-1234567890123456.7.azuredatabricks.net`. |
| `clusterId` | El identificador de su clúster en [!DNL Databricks]. Este clúster ya debe ser un clúster existente y debe ser un clúster interactivo. |
| `accessToken` | El token de acceso que autentica su cuenta de [!DNL Databricks]. Puede generar el token de acceso mediante el área de trabajo [!DNL Databricks]. |
| `database` | Nombre de la base de datos en el lago delta. |
| `connectionSpec.Id` | El ID de especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y fuente. El id. de especificación de conexión para [!DNL Databricks] es `e9d7ec6b-0873-4e57-ad21-b3a7c65e310b`. |

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione las credenciales de autenticación adecuadas para su cuenta de [!DNL Databricks].

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para un origen de [!DNL Databricks] mediante la autenticación de token de acceso.

+++Ver ejemplo de solicitud

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/connections' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d '{
    "name": "Databricks connection to Experience Platform",
    "description": "A Databricks base connection to Experience Platform",
    "auth": {
        "specName": "Access Token Authentication",
        "params": {
          "domain": "https://adb-1234567890123456.7.azuredatabricks.net",
          "clusterId": "xxxx",
          "accessToken": "xxxx",
          "database": "acme-db"
        }
    },
    "connectionSpec": {
        "id": "e9d7ec6b-0873-4e57-ad21-b3a7c65e310b",
        "version": "1.0"
    }
}'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.domain` | La URL de su área de trabajo [!DNL Databricks]. |
| `auth.params.clusterId` | El identificador de su clúster en [!DNL Databricks]. Este clúster ya debe ser uno existente y debe ser interactivo |
| `auth.params.accessToken` | El token de acceso que autentica su cuenta de [!DNL Databricks]. |
| `auth.params.database` | Nombre de la base de datos en el lago delta. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Databricks]. |

+++

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido el ID de la conexión base.

+++Ver ejemplo de respuesta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++

## Pasos siguientes

Al seguir este tutorial, ha creado correctamente una conexión entre su cuenta de [!DNL Databricks] y Experience Platform. Puede utilizar el ID de conexión base recién generado en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
