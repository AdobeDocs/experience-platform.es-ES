---
keywords: Experience Platform;inicio;temas populares;oracle;
title: (Beta) Crear una conexión base de Responsys de Oracle mediante la API de servicio de flujo
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Responsys de Oracle mediante la API de servicio de flujo.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 1%

---

# (Beta) Cree un [!DNL Oracle Responsys] conexión base utilizando [!DNL Flow Service] API

>[!NOTE]
>
>La variable [!DNL Oracle Responsys] el origen está en versión beta. Consulte la [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Oracle Responsys] usando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Platform:

* [Fuentes](../../../../home.md): Platform permite la ingesta de datos de varias fuentes, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): Platform proporciona entornos limitados virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a [!DNL Oracle Responsys] usando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL Oracle Responsys], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `endpoint` | La dirección URL de extremo de autenticación REST de su [!DNL Oracle Responsys] instancia. |
| `clientId` | El ID de cliente de su [!DNL Oracle Responsys] instancia. |
| `clientSecret` | El secreto de cliente de su [!DNL Oracle Responsys] instancia. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El valor del ID de especificación de conexión de la variable [!DNL Oracle Responsys] el origen se fija como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Para obtener más información sobre las credenciales de autenticación para [!DNL Oracle Responsys], consulte la [[!DNL Oracle Responsys] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Oracle Responsys] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Oracle Responsys]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "name": "Oracle Responsys Base Connection",
      "description": "Base Connection for Oracle Responsys",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "endpoint": "{ENDPOINT}",
              "clientId": "{CLIENT_ID}",
              "clientSecret": "{CLIENT_SECRET}"
          }
      },
      "connectionSpec": {
          "id": "ff4274f2-c9a9-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Parámetro | Descripción |
| --- | --- |
| `name` | El nombre de su [!DNL Oracle Responsys] conexión base. Se recomienda proporcionar un nombre descriptivo, ya que puede utilizar este valor para buscar la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar información adicional sobre la conexión base. |
| `auth.specName` | El tipo de autenticación utilizado para la conexión. |
| `auth.params.endpoint` | La dirección URL de extremo de autenticación REST de su [!DNL Oracle Responsys] servidor. |
| `auth.params.clientId` | El ID de cliente de su [!DNL Oracle Responsys] instancia. |
| `auth.params.clientSecret` | El secreto de cliente de su [!DNL Oracle Responsys] instancia. |
| `connectionSpec.id` | El valor del ID de especificación de conexión de la variable [!DNL Oracle Responsys] el origen se fija como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el paso siguiente para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Oracle Responsys] conexión base utilizando [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante el [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Platform mediante la variable [!DNL Flow Service] API](../../collect/marketing-automation.md)
