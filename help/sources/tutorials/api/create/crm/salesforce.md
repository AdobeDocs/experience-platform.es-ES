---
keywords: Experience Platform;inicio;temas populares;Salesforce;salesforce
solution: Experience Platform
title: Creación de una conexión base de Salesforce mediante la API de Flow Service
type: Tutorial
description: Aprenda a conectar Adobe Experience Platform a una cuenta de Salesforce mediante la API de Flow Service.
exl-id: 43dd9ee5-4b87-4c8a-ac76-01b83c1226f6
source-git-commit: 57cdcbd5018e7f57261f09c6bddf5e2a8dcfd0d5
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 5%

---

# Crear un [!DNL Salesforce] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL Salesforce] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente [!DNL Platform] a un [!DNL Salesforce] cuenta que utiliza [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectarse a [!DNL Salesforce], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | La dirección URL del [!DNL Salesforce] instancia de origen. |
| `username` | El nombre de usuario de [!DNL Salesforce] cuenta de usuario. |
| `password` | La contraseña para el [!DNL Salesforce] cuenta de usuario. |
| `securityToken` | El token de seguridad para [!DNL Salesforce] cuenta de usuario. |
| `apiVersion` | (Opcional) La versión de la API de REST de [!DNL Salesforce] instancia de que está utilizando. Si este campo se deja en blanco, el Experience Platform utilizará automáticamente la última versión disponible. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL Salesforce] es: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

Para obtener más información sobre cómo empezar, visite [este documento de Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Cree una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` y proporcione su [!DNL Salesforce] credenciales de autenticación en el cuerpo de la solicitud.

**Formato de API**

```http
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Salesforce]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Salesforce Connection",
      "description": "Connection for Salesforce account",
      "auth": {
          "specName": "Basic Authentication",
          "params": {****
              "username": "{USERNAME}",
              "password": "{PASSWORD}",
              "securityToken": "{SECURITY_TOKEN}"
          }
      },
      "connectionSpec": {
          "id": "cfc0fee1-7dc0-40ef-b73e-d8b134c436f5",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.username` | El nombre de usuario asociado con su [!DNL Salesforce] cuenta. |
| `auth.params.password` | La contraseña asociada a su [!DNL Salesforce] cuenta. |
| `auth.params.securityToken` | El token de seguridad asociado con su [!DNL Salesforce] cuenta. |
| `connectionSpec.id` | El [!DNL Salesforce] identificador de especificación de conexión: `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el siguiente paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL Salesforce] conexión base mediante el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar datos CRM a Platform mediante [!DNL Flow Service] API](../../collect/crm.md)
