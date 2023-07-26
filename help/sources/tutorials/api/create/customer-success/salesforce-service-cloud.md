---
keywords: Experience Platform;inicio;temas populares;Salesforce Service Cloud;Salesforce service cloud
solution: Experience Platform
title: Creación de una conexión de origen de Salesforce Cloud mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a Salesforce Service Cloud mediante la API de Flow Service.
exl-id: ed133bca-8e88-4c85-ae52-c3269b6bf3c9
source-git-commit: 5d28db34edd377269e8710b1741098a08616ae5f
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 2%

---

# Crear un [!DNL Salesforce Service Cloud] conexión de origen mediante [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Salesforce Service Cloud] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Salesforce Service Cloud] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL Salesforce Service Cloud], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `username` | El nombre de usuario de su [!DNL Salesforce Service Cloud] cuenta de usuario. |
| `password` | La contraseña de su [!DNL Salesforce Service Cloud] cuenta. |
| `securityToken` | El token de seguridad de su [!DNL Salesforce Service Cloud] cuenta. |
| `apiVersion` | (Opcional) La versión de la API de REST de [!DNL Salesforce Service Cloud] instancia de que está utilizando. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Salesforce Service Cloud] es: `b66ab34-8619-49cb-96d1-39b37ede86ea`. |

Para obtener más información sobre cómo empezar, consulte [este documento de Salesforce Service Cloud](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL Salesforce Service Cloud] credenciales de autenticación como parte de los parámetros de solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Salesforce Service Cloud]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for salesforce service cloud",
      "description": "Base connection for salesforce service cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "b66ab34-8619-49cb-96d1-39b37ede86ea",
          "version": "1.0"
      }
  }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Salesforce Service Cloud] cuenta. |
| `auth.params.password` | La contraseña asociada a su [!DNL Salesforce Service Cloud] cuenta. |
| `auth.params.securityToken` | El token de seguridad asociado con su [!DNL Salesforce Service Cloud] cuenta. |
| `connectionSpec.id` | El [!DNL Salesforce Service Cloud] identificador de especificación de conexión: `b66ab34-8619-49cb-96d1-39b37ede86ea` |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Salesforce Service Cloud] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de éxito de los clientes a Platform mediante [!DNL Flow Service] API](../../collect/customer-success.md)
