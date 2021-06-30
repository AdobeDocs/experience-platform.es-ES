---
keywords: Experience Platform;inicio;temas populares;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Creación de una conexión base PostgreSQL mediante la API de servicio de flujo
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a PostgreSQL mediante la API de servicio de flujo.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 5fb5f0ce8bd03ba037c6901305ba17f8939eb9ce
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 2%

---

# Crear una conexión base [!DNL PostgreSQL] utilizando la API [!DNL Flow Service]

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial le guía por los pasos para crear una conexión base para [!DNL PostgreSQL] mediante la [[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml).


## Primeros pasos

Esta guía requiere conocer los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md):  [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante  [!DNL Platform] servicios.
* [Simuladores para pruebas](../../../../../sandboxes/home.md):  [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen una sola  [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL PostgreSQL] mediante la API [!DNL Flow Service].

### Recopilar las credenciales necesarias

Para que [!DNL Flow Service] se conecte con [!DNL PostgreSQL], debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada a su cuenta [!DNL PostgreSQL]. El patrón de cadena de conexión [!DNL PostgreSQL] es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de un origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y de origen. El ID de especificación de conexión para [!DNL PostgreSQL] es `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Para obtener más información sobre la obtención de una cadena de conexión, consulte este [[!DNL PostgreSQL] documento](https://www.postgresql.org/docs/9.2/app-psql.html).

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Creación de una conexión base

Una conexión base retiene información entre la fuente y la plataforma, incluidas las credenciales de autenticación de la fuente, el estado actual de la conexión y el ID de conexión base único. El ID de conexión base le permite explorar y navegar archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al extremo `/connections` y proporcione las credenciales de autenticación [!DNL PostgreSQL] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL PostgreSQL]:

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
| `auth.params.connectionString` | La cadena de conexión asociada a su cuenta [!DNL PostgreSQL]. El patrón de cadena de conexión [!DNL PostgreSQL] es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Los ID de especificación de conexión [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada. Este ID es necesario para explorar la base de datos [!DNL PostgreSQL] en el siguiente tutorial.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión [!DNL PostgreSQL] utilizando la API [!DNL Flow Service] y ha obtenido el valor de ID exclusivo de la conexión. Puede utilizar este ID de conexión en el siguiente tutorial, mientras aprende a explorar las [bases de datos o los sistemas NoSQL mediante la API de servicio de flujo](../../explore/database-nosql.md).
