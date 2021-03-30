---
keywords: Experience Platform;inicio;temas populares;Shopify;shopify;comercio electrónico
solution: Experience Platform
title: Creación de una conexión de origen de conector Shopify mediante la API de servicio de flujo
topic: sobre validación
type: Tutorial
description: Obtenga información sobre cómo conectar Shopify a Adobe Experience Platform mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: cc23228cb410dc4c70a56c5142be00c2ca1c40d3
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL Shopify] mediante la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [[!DNL Flow Service]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) para guiarle por los pasos para conectar [!DNL Shopify] con [!DNL Experience Platform].

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [[!DNL Sources]](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL Shopify] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL Shopify], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El punto final del servidor [!DNL Shopify]. |
| `accessToken` | El token de acceso de su cuenta de usuario [!DNL Shopify]. |
| `connectionSpec` | Identificador único necesario para crear una conexión. El ID de especificación de conexión para [!DNL Shopify] es: `4f63aa36-bd48-4e33-bb83-49fbcd11c708` |

Para obtener más información sobre cómo empezar, consulte este [documento de autenticación Shopify](https://shopify.dev/concepts/about-apis/authentication).

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios

Para realizar llamadas a las API [!DNL Platform], primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API [!DNL Experience Platform], como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Todos los recursos de [!DNL Experience Platform], incluidos los que pertenecen a [!DNL Flow Service], están aislados en entornos limitados virtuales específicos. Todas las solicitudes a las API [!DNL Platform] requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Crear una conexión

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cada cuenta [!DNL Shopify], ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión [!DNL Shopify], su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para [!DNL Shopify] es `4f63aa36-bd48-4e33-bb83-49fbcd11c708`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Shopify source",
        "description": "Shopify source",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "host": "{HOST}",
                "accessToken": "{ACCCESS_TOKEN}"
            }
        },
        "connectionSpec": {
            "id": "4f63aa36-bd48-4e33-bb83-49fbcd11c708",
            "version": "1.0"
        }
    }
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.host` | El extremo del servidor [!DNL Shopify]. |
| `auth.params.accessToken` | El token de acceso de su cuenta de usuario [!DNL Shopify]. |
| `connectionSpec.id` | El ID de especificación de conexión [!DNL Shopify]: `4f63aa36-bd48-4e33-bb83-49fbcd11c708`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "582f4f8d-71e9-4a5c-a164-9d2056318d6c",
    "etag": "\"d600d3ae-0000-0200-0000-5fa99a3d0000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL Shopify] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID en el siguiente tutorial, mientras aprende a [explorar las conexiones de comercio electrónico mediante la API de servicio de flujo](../../explore/ecommerce.md).