---
title: Creación de una conexión de Salesforce Service Cloud Source mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Salesforce Service Cloud mediante la API de Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 5%

---

# Crear una conexión de origen [!DNL Salesforce Service Cloud] mediante la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Lea este tutorial para aprender a crear una conexión base para [!DNL Salesforce Service Cloud] mediante la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform].
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de [!DNL Experience Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Salesforce Service Cloud] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Lea la [guía de autenticación](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials) para obtener más información sobre cómo recuperar sus credenciales.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Salesforce Service Cloud] como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Salesforce Service Cloud] mediante la credencial de cliente de OAuth 2:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "description": "Salesforce Service Cloud account for ACME data (OAuth2)",
      "auth": {
          "specName": "OAuth2 Client Credential",
          "params":
            "environmentUrl": "https://acme-enterprise-3126.my.salesforce.com",
            "clientId": "xxxx",
            "clientSecret": "xxxx",
            "apiVersion": "60.0"
        }
      },
      "connectionSpec": {
          "id": "cb66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.environmentUrl` | La URL de su instancia [!DNL Salesforce Service Cloud]. |
| `auth.params.clientId` | Identificador de cliente asociado con su cuenta de [!DNL Salesforce Service Cloud]. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su cuenta de [!DNL Salesforce Service Cloud]. |
| `auth.params.apiVersion` | La versión de la API de REST de la instancia [!DNL Salesforce Service Cloud] que está utilizando. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Salesforce Service Cloud]: `cb66ab34-8619-49cb-96d1-39b37ede86ea`. |

**Respuesta**

Una respuesta correcta devuelve la conexión base recién creada junto con su ID único.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Próximos pasos

Siguiendo este tutorial, ha creado una conexión base [!DNL Salesforce Service Cloud] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de éxito de los clientes a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/customer-success.md)
