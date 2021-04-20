---
keywords: Experience Platform;inicio;temas populares;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Creación de una conexión de origen PostgreSQL mediante la API de servicio de flujo
topic: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a PostgreSQL mediante la API de servicio de flujo.
translation-type: tm+mt
source-git-commit: 8851e11e956b393e56714d4d48870b7f68947c18
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---


# Crear una conexión de origen [!DNL PostgreSQL] mediante la API [!DNL Flow Service]

[!DNL Flow Service] se utiliza para recopilar y centralizar datos de clientes de diferentes fuentes dentro de Adobe Experience Platform. El servicio proporciona una interfaz de usuario y una API RESTful desde las que se pueden conectar todas las fuentes admitidas.

Este tutorial utiliza la API [!DNL Flow Service] para guiarle por los pasos para conectar [!DNL Experience Platform] con [!DNL PostgreSQL] (en adelante denominada &quot;PSQL&quot;).

## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que debe conocer para conectarse correctamente a PSQL mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con PSQL, debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada a su cuenta PSQL. El patrón de cadena de conexión PSQL es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | ID utilizado para generar una conexión. El ID de especificación de conexión fija para PSQL es `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Para obtener más información sobre la obtención de una cadena de conexión, consulte [este documento PSQL](https://www.postgresql.org/docs/9.2/app-psql.html).

### Leer llamadas de API de ejemplo

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas [!DNL Experience Platform].

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

Una conexión especifica un origen y contiene sus credenciales para ese origen. Solo se requiere una conexión por cuenta PSQL, ya que se puede utilizar para crear varios conectores de origen para introducir datos diferentes.

**Formato de API**

```http
POST /connections
```

**Solicitud**

Para crear una conexión PSQL, su ID de especificación de conexión única debe proporcionarse como parte de la solicitud del POST. El ID de especificación de conexión para PSQL es `74a1c565-4e59-48d7-9d67-7c03b8a13137`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Test connection for PostgreSQL",
        "description": "Test connection for PostgreSQL",
        "auth": {
            "specName": "Connection String Based Authentication",
            "params": {
                "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| ------------- | --------------- |
| `auth.params.connectionString` | La cadena de conexión asociada a su cuenta PSQL. El patrón de cadena de conexión PSQL es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | El ID de especificación de conexión para PSQL es: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada. Este ID es necesario para explorar la base de datos PSQL en el siguiente tutorial.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión PSQL utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID único de la conexión. Puede utilizar este ID de conexión en el siguiente tutorial, mientras aprende a explorar las [bases de datos o los sistemas NoSQL mediante la API de servicio de flujo](../../explore/database-nosql.md).
