---
keywords: Experience Platform;inicio;temas populares;PostgreSQL;postgresql;PSQL;psql
solution: Experience Platform
title: Crear una conexión base de PostgreSQL mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo conectar Adobe Experience Platform a PostgreSQL mediante la API de Flow Service.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 3%

---

# Crear un [!DNL PostgreSQL] conexión base mediante el [!DNL Flow Service] API

Una conexión base representa la conexión autenticada entre un origen y Adobe Experience Platform.

Este tutorial lo acompañará durante los pasos para crear una conexión base para [!DNL PostgreSQL] uso del [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).


## Primeros pasos

Esta guía requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para conectarse correctamente a [!DNL PostgreSQL] uso del [!DNL Flow Service] API.

### Recopilar credenciales necesarias

Para que [!DNL Flow Service] para conectar con [!DNL PostgreSQL], debe proporcionar la siguiente propiedad de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `connectionString` | La cadena de conexión asociada a su [!DNL PostgreSQL] cuenta. El [!DNL PostgreSQL] el patrón de cadena de conexión es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. Identificador de especificación de conexión para [!DNL PostgreSQL] es `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

Para obtener más información sobre la obtención de una cadena de conexión, consulte [[!DNL PostgreSQL] documento](https://www.postgresql.org/docs/9.2/app-psql.html).

#### Habilitar el cifrado SSL para la cadena de conexión

Puede habilitar el cifrado SSL para su [!DNL PostgreSQL] cadena de conexión adjuntando la cadena de conexión con las siguientes propiedades:

| Propiedad | Descripción | Ejemplo |
| --- | --- | --- |
| `EncryptionMethod` | Permite habilitar el cifrado SSL en su [!DNL PostgreSQL] datos. | <uL><li>`EncryptionMethod=0`(Desactivado)</li><li>`EncryptionMethod=1`(Habilitado)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valida el certificado enviado por su [!DNL PostgreSQL] base de datos cuando `EncryptionMethod` se aplica. | <uL><li>`ValidationServerCertificate=0`(Desactivado)</li><li>`ValidationServerCertificate=1`(Habilitado)</li></ul> |

El siguiente es un ejemplo de [!DNL PostgreSQL] cadena de conexión anexada con cifrado SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../../../landing/api-guide.md).

## Crear una conexión base

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un ID de conexión base, realice una solicitud de POST al `/connections` extremo al proporcionar su [!DNL PostgreSQL] credenciales de autenticación como parte de los parámetros de solicitud.

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
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.connectionString` | La cadena de conexión asociada a su [!DNL PostgreSQL] cuenta. El [!DNL PostgreSQL] el patrón de cadena de conexión es: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | El [!DNL PostgreSQL] ID de especificación de conexión: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

**Respuesta**

Una respuesta correcta devuelve el identificador único (`id`) de la conexión base recién creada. Este ID es necesario para explorar su [!DNL PostgreSQL] en el siguiente tutorial.

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

## Pasos siguientes

Al seguir este tutorial, ha creado un [!DNL PostgreSQL] conexión base utilizando el [!DNL Flow Service] API. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explorar la estructura y el contenido de las tablas de datos mediante [!DNL Flow Service] API](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante [!DNL Flow Service] API](../../collect/database-nosql.md)
