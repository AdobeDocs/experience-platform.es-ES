---
title: Creación de una conexión base de Salesforce Marketing Cloud mediante la API de Flow Service
description: Obtenga información sobre cómo autenticar su cuenta de Salesforce Marketing Cloud con Experience Platform mediante la API de Flow Service.
exl-id: fbf68d3a-f8b1-4618-bd56-160cc6e3346d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 4%

---

# Crear una conexión base [!DNL Salesforce Marketing Cloud] mediante la API [!DNL Flow Service]

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto a finales de junio de 2025.

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo guiará para crear una conexión base para [!DNL Salesforce Marketing Cloud] mediante la [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que necesitará conocer para conectarse correctamente a [!DNL Salesforce Marketing Cloud] mediante la API [!DNL Flow Service].

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Salesforce Marketing Cloud], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | Servidor host de la aplicación. Este suele ser su subdominio. **Nota:** Al escribir el valor `host`, debe especificar `{subdomain}.rest.marketingcloudapis.com`. Por ejemplo, si la dirección URL de host es `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, debe escribir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` como valor de host. |
| `clientId` | Identificador de cliente asociado con la aplicación [!DNL Salesforce Marketing Cloud]. |
| `clientSecret` | Secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Salesforce Marketing Cloud] es: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

Para obtener más información sobre cómo empezar, consulte este [[!DNL Salesforce Marketing Cloud] documento](<https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm>).

## Crear una conexión base

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.

Una conexión base retiene información entre el origen y Experience Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el identificador único de la conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Salesforce Marketing Cloud] como parte del cuerpo de la solicitud.

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
| `auth.params.clientId` | Identificador de cliente asociado con la aplicación [!DNL Salesforce Marketing Cloud]. |
| `auth.params.clientSecret` | Secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Salesforce Marketing Cloud]: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Salesforce Marketing Cloud] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de automatización de marketing a Experience Platform mediante la API  [!DNL Flow Service] ](../../collect/marketing-automation.md)
