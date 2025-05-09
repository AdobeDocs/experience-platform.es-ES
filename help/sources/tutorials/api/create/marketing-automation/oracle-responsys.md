---
keywords: Experience Platform;inicio;temas populares;oracle;
title: (Beta) Crear una conexión base de Oracle Responsys mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Oracle Responsys mediante la API de Flow Service.
hide: true
hidefromtoc: true
exl-id: 76659f5a-c923-488c-88f6-1919bc6a7bb5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 2%

---

# (Beta) Cree una conexión base [!DNL Oracle Responsys] mediante la API [!DNL Flow Service]

>[!NOTE]
>
>El origen [!DNL Oracle Responsys] está en la versión beta. Consulte [Resumen de fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL Oracle Responsys] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesita conocer para conectarse correctamente a [!DNL Oracle Responsys] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Oracle Responsys], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `endpoint` | La URL del extremo de autenticación REST de su instancia [!DNL Oracle Responsys]. |
| `clientId` | Identificador de cliente de su instancia [!DNL Oracle Responsys]. |
| `clientSecret` | El secreto de cliente de su instancia [!DNL Oracle Responsys]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El valor del id. de especificación de conexión del origen [!DNL Oracle Responsys] se ha corregido como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

Para obtener más información sobre las credenciales de autenticación de [!DNL Oracle Responsys], consulte la [[!DNL Oracle Responsys] guía de autenticación](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Oracle Responsys] como parte de los parámetros de solicitud.

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
| `name` | Nombre de su conexión base [!DNL Oracle Responsys]. Se recomienda proporcionar un nombre descriptivo, ya que puede utilizar este valor para buscar la conexión base. |
| `description` | (Opcional) Una propiedad que puede incluir para proporcionar información adicional sobre la conexión base. |
| `auth.specName` | Tipo de autenticación utilizado para la conexión. |
| `auth.params.endpoint` | URL del extremo de autenticación REST de su servidor [!DNL Oracle Responsys]. |
| `auth.params.clientId` | Identificador de cliente de su instancia [!DNL Oracle Responsys]. |
| `auth.params.clientSecret` | El secreto de cliente de su instancia [!DNL Oracle Responsys]. |
| `connectionSpec.id` | El valor del id. de especificación de conexión del origen [!DNL Oracle Responsys] se ha corregido como: `ff4274f2-c9a9-11eb-b8bc-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`). Este ID es necesario en el siguiente paso para crear una conexión de origen.

```json
{
    "id": "2484f2df-c057-4ab5-84f2-dfc0577ab592",
    "etag": "\"10033e77-0000-0200-0000-5e96785b0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Oracle Responsys] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
