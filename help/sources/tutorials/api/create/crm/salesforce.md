---
keywords: Experience Platform;inicio;temas populares;Salesforce;Salesforce
solution: Experience Platform
title: Creación de una conexión de origen de Salesforce mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a una cuenta de Salesforce mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL Salesforce] mediante la API [!DNL Flow Service]

El servicio de flujo se utiliza para recopilar y centralizar datos de clientes de diversas fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde la que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Platform] a una cuenta [!DNL Salesforce] mediante la API de servicio de flujo.

## Primeros pasos

Esta guía requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las siguientes secciones proporcionan información adicional que deberá conocer para conectar [!DNL Platform] correctamente a una cuenta [!DNL Salesforce] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte a [!DNL Salesforce], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `environmentUrl` | Dirección URL de la instancia de origen [!DNL Salesforce]. |
| `username` | El nombre de usuario de la cuenta de usuario [!DNL Salesforce]. |
| `password` | La contraseña de la cuenta de usuario [!DNL Salesforce]. |
| `securityToken` | El distintivo de seguridad para la cuenta de usuario [!DNL Salesforce]. |

Para obtener más información sobre cómo empezar, visite [este documento de Salesforce](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm).

### Leer llamadas de API de muestra

Este tutorial proporciona ejemplos de llamadas a API para mostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados requeridos y cargas de solicitud con el formato adecuado. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener más información sobre las convenciones utilizadas en la documentación de las llamadas de API de muestra, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

### Recopilar valores para encabezados necesarios

Para realizar llamadas a [!DNL Platform] API, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas [!DNL Experience Platform] API, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del entorno limitado en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta [!DNL Salesforce], ya que se puede utilizar para crear varios conectores de origen para traer datos diferentes.

**Formato API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Salesforce], se debe proporcionar su ID de especificación de conexión única como parte de la solicitud del POST. El identificador de especificación de conexión para [!DNL Salesforce] es `cfc0fee1-7dc0-40ef-b73e-d8b134c436f5`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Salesforce Connection",
        "description": "Connection for Salesforce account",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
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
| `auth.params.username` | El nombre de usuario asociado a su cuenta [!DNL Salesforce]. |
| `auth.params.password` | La contraseña asociada a su cuenta [!DNL Salesforce]. |
| `auth.params.securityToken` | El token de seguridad asociado a su cuenta [!DNL Salesforce]. |
| `connectionSpec.id` | La especificación de conexión `id` de su cuenta [!DNL Salesforce] recuperada en el paso anterior. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el sistema CRM en el próximo paso.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"1700df7b-0000-0200-0000-5e3b424f0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Salesforce] mediante la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial cuando aprenda a [explorar sistemas CRM mediante la API de servicio de flujo](../../explore/crm.md).