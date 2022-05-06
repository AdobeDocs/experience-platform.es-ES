---
keywords: Experience Platform;inicio;temas populares;oracle;eloqua;elocua de oracle
solution: Experience Platform
title: Creación de una conexión base de Eloqua de Oracle mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Eloqua mediante la API de servicio de flujo.
exl-id: 866e408f-6e0b-4e81-9ad8-9d74c485c89a
source-git-commit: 93061c84639ca1fdd3f7abb1bbd050eb6eebbdd6
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 1%

---

# Cree un [!DNL Oracle Eloqua] conexión base utilizando [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Oracle Eloqua] usando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): Platform proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a [!DNL Oracle Eloqua] usando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL Oracle Eloqua], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `endpoint` | El punto final de su [!DNL Oracle Eloqua]. |
| `username` | El nombre de usuario de su [!DNL Oracle Eloqua] cuenta. El nombre de usuario debe tener el formato `siteName + \\ + username`, donde `siteName` es el nombre de empresa que utilizó para iniciar sesión en [!DNL Oracle Eloqua] y `username` es su nombre de usuario. Por ejemplo, el nombre de usuario de inicio de sesión puede ser: `adobe\\emily`. |
| `password` | La contraseña correspondiente a su [!DNL Oracle Eloqua] nombre de usuario. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El valor del ID de especificación de conexión de la variable [!DNL Oracle Eloqua] el origen se fija como: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

Para obtener más información sobre las credenciales de autenticación para [!DNL Oracle Eloqua], consulte la [[!DNL Oracle Eloqua] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Oracle Eloqua] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Oracle Eloqua]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Eloqua Base Connection",
      "description": "Base Connection for Oracle Eloqua",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "35d6c4d8-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | El nombre de su [!DNL Oracle Eloqua] conexión base. Se recomienda proporcionar un nombre descriptivo, ya que puede utilizar este valor para buscar la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar información adicional sobre la conexión base. |
| `auth.specName` | El tipo de autenticación utilizado para la conexión. |
| `auth.params.endpoint` | El punto final de su [!DNL Oracle Eloqua] servidor. |
| `auth.params.username` | La credencial concatenada que incluye el nombre de sitio y el nombre de usuario que se corresponden con su [!DNL Oracle Eloqua] cuenta. |
| `auth.params.password` | La contraseña que corresponde a su [!DNL Oracle Eloqua] cuenta. |
| `connectionSpec.id` | El valor del ID de especificación de conexión de la variable [!DNL Oracle Eloqua] el origen se fija como: `35d6c4d8-c9a9-11eb-b8bc-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Oracle Eloqua] conexión base utilizando [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante el [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Platform mediante la variable [!DNL Flow Service] API](../../collect/marketing-automation.md)
