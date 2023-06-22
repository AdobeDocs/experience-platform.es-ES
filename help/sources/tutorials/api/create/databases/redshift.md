---
title: Creación de una conexión base de Amazon Redshift mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a Amazon Redshift mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 2728ce08-05c9-4dca-af1d-d2d1b266c5d9
source-git-commit: a7c2c5e4add5c80e0622d5aeb766cec950d79dbb
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# Crear un [!DNL Amazon Redshift] conexión base mediante el [!DNL Flow Service] API

>[!IMPORTANT]
>
>El [!DNL Amazon Redshift] La fuente de está disponible en el catálogo de fuentes de para los usuarios que han adquirido Real-time Customer Data Platform Ultimate.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Amazon Redshift] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Amazon Redshift] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Amazon Redshift], debe proporcionar las siguientes propiedades de conexión:

| **Credencial** | **Descripción** |
| -------------- | --------------- |
| `server` | El servidor asociado con su [!DNL Amazon Redshift] cuenta. |
| `port` | El puerto TCP que un [!DNL Amazon Redshift] El servidor de utiliza para detectar conexiones de cliente. |
| `username` | El nombre de usuario asociado con su [!DNL Amazon Redshift] cuenta. |
| `password` | La contraseña asociada a su [!DNL Amazon Redshift] cuenta. |
| `database` | El [!DNL Amazon Redshift] base de datos a la que accede. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Amazon Redshift] es `3416976c-a9ca-4bba-901a-1f08f66978ff`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Amazon Redshift] documento](https://docs.aws.amazon.com/redshift/latest/gsg/getting-started.html).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

>[!NOTE]
>
>El estándar de codificación predeterminado para [!DNL Redshift] es Unicode. Esto no se puede cambiar.

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Amazon Redshift] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Amazon Redshift]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "amazon-redshift base connection",
      "description": "base connection for amazon-redshift,
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "{SERVER}",
              "port": "{PORT},
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "database": "{DATABASE}"
          }
      },
      "connectionSpec": {
          "id": "3416976c-a9ca-4bba-901a-1f08f66978ff",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| ------------- | --------------- |
| `auth.params.server` | Su [!DNL Amazon Redshift] servidor. |
| `auth.params.port` | El puerto TCP en el que [!DNL Amazon Redshift] El servidor de utiliza para detectar conexiones de cliente. |
| `auth.params.database` | La base de datos asociada a su [!DNL Amazon Redshift] cuenta. |
| `auth.params.password` | La contraseña asociada a su [!DNL Amazon Redshift] cuenta. |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Amazon Redshift] cuenta. |
| `connectionSpec.id` | El [!DNL Amazon Redshift] identificador de especificación de conexión: `3416976c-a9ca-4bba-901a-1f08f66978ff` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "373e88fc-43da-4e3c-be88-fc43da3e3c0f",
    "etag": "\"1700ce7b-0000-0200-0000-5e3b405e0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Amazon Redshift] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
