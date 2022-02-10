---
keywords: Experience Platform;inicio;temas populares;Snowflake;snowflake
solution: Experience Platform
title: Creación de una conexión base del Snowflake mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform al Snowflake mediante la API de servicio de flujo.
exl-id: 0ef34d30-7b4c-43f5-8e2e-cde05da05aa5
source-git-commit: ac7910c971fbedf3afebd87633f814d597260cae
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 2%

---

# Cree un [!DNL Snowflake] conexión base utilizando [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL Snowflake] usando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

La siguiente sección proporciona información adicional que deberá conocer para conectarse correctamente a [!DNL Snowflake] usando la variable [!DNL Flow Service] API.

### Recopilar las credenciales necesarias

Para [!DNL Flow Service] para conectarse con [!DNL Snowflake], debe proporcionar las siguientes propiedades de conexión:

| Credencial | Descripción |
| --- | --- |
| `account` | El nombre de cuenta completo asociado con su [!DNL Snowflake] cuenta. Una [!DNL Snowflake] el nombre de cuenta incluye el nombre de su cuenta, su región y su plataforma de nube. Por ejemplo, `cj12345.east-us-2.azure`. Para obtener más información sobre los nombres de cuenta, consulte esta [[!DNL Snowflake document on account identifiers]](https://docs.snowflake.com/en/user-guide/admin-account-identifier.html). |
| `warehouse` | La variable [!DNL Snowflake] warehouse administra el proceso de ejecución de consultas para la aplicación. Cada [!DNL Snowflake] el almacén es independiente entre sí y se debe acceder a él de forma individual al llevar los datos a Platform. |
| `database` | La variable [!DNL Snowflake] base de datos contiene los datos que desea que sean compatibles con Platform. |
| `username` | El nombre de usuario de la variable [!DNL Snowflake] cuenta. |
| `password` | La contraseña de la variable [!DNL Snowflake] cuenta de usuario. |
| `connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] instancia. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}` |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL Snowflake] es `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

Para obtener más información sobre cómo empezar, consulte esta [[!DNL Snowflake] documento](https://docs.snowflake.com/en/user-guide/key-pair-auth.html).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` al proporcionar su [!DNL Snowflake] credenciales de autenticación como parte del cuerpo de la solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Snowflake]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Snowflake base connection",
        "description": "Snowflake base connection",
        "auth": {
            "specName": "Basic Authentication for Snowflake,
            "params": {
                "connectionString": "{CONNECTION_STRING}"
            }
        },
        "connectionSpec": {
            "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| -------- | ----------- |
| `auth.params.connectionString` | La cadena de conexión utilizada para conectarse a su [!DNL Snowflake] instancia. El patrón de cadena de conexión para [!DNL Snowflake] es `jdbc:snowflake://{ACCOUNT_NAME}.snowflakecomputing.com/?user={USERNAME}&password={PASSWORD}&db={DATABASE}&warehouse={WAREHOUSE}`. |
| `connectionSpec.id` | La variable [!DNL Snowflake] id. de especificación de conexión: `b2e08744-4f1a-40ce-af30-7abac3e23cf3`. |

**Respuesta**

Una respuesta correcta devuelve la conexión recién creada, incluido su identificador de conexión único (`id`). Este ID es necesario para explorar sus datos en el siguiente tutorial.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

Al seguir este tutorial, ha creado un [!DNL Snowflake] conexión mediante la función [!DNL Flow Service] y han obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión en el siguiente tutorial, mientras aprende a [explorar bases de datos mediante la API de servicio de flujo](../../explore/database-nosql.md).
