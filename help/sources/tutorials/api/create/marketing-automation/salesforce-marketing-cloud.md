---
title: Creación de una conexión base de Marketing Cloud de Salesforce mediante la API de Flow Service
description: Obtenga información sobre cómo autenticar su cuenta de Salesforce Marketing Cloud con Experience Platform mediante la API de Flow Service.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: 997a9dc70145a8cfd5d6da20ba788a4610e5c257
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 2%

---

# Crear un [!DNL Salesforce Marketing Cloud] conexión base mediante el [!DNL Flow Service] API

>[!IMPORTANT]
>
>La ingesta de objetos personalizados no es compatible actualmente con [!DNL Salesforce Marketing Cloud] integración de origen.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Salesforce Marketing Cloud] uso del [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos desde varias fuentes y, al mismo tiempo, le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): El Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL Salesforce Marketing Cloud] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Salesforce Marketing Cloud], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Servidor host de la aplicación. Este suele ser su subdominio. **Nota:** Al introducir su `host` , solo necesita especificar el subdominio y no la dirección URL completa. Por ejemplo, si la dirección URL del host es `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, entonces solo necesita introducir `acme-ab12c3d4e5fg6hijk7lmnop8qrst` como valor de host. |
| `clientId` | El ID de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |
| `clientSecret` | El secreto de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Salesforce Marketing Cloud] es: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Salesforce Marketing Cloud] documento](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Salesforce Marketing Cloud] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Salesforce Marketing Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Marketing Cloud base connection",
      "description": "Salesforce Marketing Cloud base connection",
      "auth": {
          "specName": "Client-Id-Secret Based Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "acme-salesforce-marketing-cloud",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.clientId` | El ID de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |
| `auth.params.clientSecret` | El secreto de cliente asociado con su [!DNL Salesforce Marketing Cloud] aplicación. |
| `connectionSpec.id` | El [!DNL Salesforce Marketing Cloud] identificador de especificación de conexión: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Salesforce Marketing Cloud] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Platform mediante [!DNL Flow Service] API](../../collect/marketing-automation.md)
