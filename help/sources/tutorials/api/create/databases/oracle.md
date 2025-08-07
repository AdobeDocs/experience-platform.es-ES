---
title: Conexión de Oracle DB a Experience Platform mediante la API de Flow Service
description: Obtenga información sobre cómo conectar Oracle DB a Experience Platform mediante API.
exl-id: b1cea714-93ff-425f-8e12-6061da97d094
source-git-commit: aa5496be968ee6f117649a6fff2c9e83a4ed7681
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Conectar [!DNL Oracle DB] a Experience Platform mediante la API [!DNL Flow Service]

Lea esta guía para aprender a conectar su cuenta de [!DNL Oracle DB] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Experience Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que necesitará conocer para conectarse correctamente a [!DNL Oracle] mediante la API [!DNL Flow Service].

### Uso de API de Experience Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Experience Platform, consulte la guía sobre [introducción a las API de Experience Platform](../../../../../landing/api-guide.md).

### Recopilar credenciales necesarias

Lea la [[!DNL Oracle DB] descripción general](../../../../connectors/databases/oracle.md#prerequisites) para obtener información sobre la autenticación.

## Conectar [!DNL Oracle DB] a Experience Platform en Azure {#azure}

Lea los pasos a continuación para obtener información sobre cómo conectar su cuenta de [!DNL Oracle DB] a Experience Platform en Azure.

### Crear una conexión base para [!DNL Oracle DB] en Experience Platform en Azure {#azure-base}

Una conexión base vincula el origen a Experience Platform y almacena los detalles de autenticación, el estado de la conexión y un ID único. Utilice este ID para examinar los archivos de origen e identificar elementos específicos que se van a introducir, incluidos sus tipos de datos y formatos.

**Formato de API**

```https
POST /connections
```

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Oracle DB] como parte de los parámetros de solicitud.

**Solicitud**

La siguiente solicitud crea una conexión base para [!DNL Oracle DB] mediante la autenticación de cadena de conexión.

+++Solicitud de vista


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Oracle DB base connection",
    "description": "A base connection to connect Oracle DB to Experience Platform on Azure",
    "auth": {
      "specName": "ConnectionString",
      "params": {
        "connectionString": "Host={HOST};Port={PORT};Sid={SID};UserId={USERNAME};Password={PASSWORD}"
      }
    },
    "connectionSpec": {
      "id": "d6b52d86-f0f8-475f-89d4-ce54c8527328",
      "version": "1.0"
    }
  }'
```

| Parámetro | Descripción |
| --------- | ----------- |
| `auth.params.connectionString` | Cadena de conexión utilizada para conectarse a [!DNL Oracle DB]. El patrón de cadena de conexión [!DNL Oracle DB] es: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Oracle]: `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`).

+++Ver respuesta

```json
{
    "id": "f088e4f2-2464-480c-88e4-f22464b80c90",
    "etag": "\"43011faa-0000-0200-0000-5ea740cd0000\""
}
```

+++

## Conectar [!DNL Oracle DB] a Experience Platform en Amazon Web Service {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

Lea los pasos a continuación para obtener información sobre cómo conectar su cuenta de [!DNL Oracle DB] a Experience Platform en AWS.

### Crear una conexión base para [!DNL Oracle DB] en Experience Platform en AWS {#aws-base}

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para que [!DNL Oracle DB] se conecte a Experience Platform en AWS.

+++Solicitud de vista

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Oracle DB on Experience Platform AWS",
      "description": "Oracle DB on Experience Platform AWS",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "diy.us-dawkins-1.oraclecloud.com",
              "port": "1521",
              "database": "mcmg_profits_diy.oraclecloud.com",
              "username": "Admin",
              "password": "xxxx",
              "schema": "ADMIN",
              "sslMode": "true"
          }
      },
      "connectionSpec": {
          "id": "26d738e0-8963-47ea-aadf-c60de735468a",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.server` | La dirección IP o el nombre de host de su servidor [!DNL Oracle DB]. |
| `auth.params.port` | Número de puerto del servidor [!DNL Oracle DB]. |
| `auth.params.database` | Nombre de la instancia [!DNL Oracle DB] a la que se está conectando. |
| `auth.params.username` | La cuenta de usuario asociada con su instancia de [!DNL Oracle DB]. |
| `auth.prams.password` | La contraseña que corresponde con su cuenta de usuario [!DNL Oracle DB]. |
| `auth.params.schema` | Esquema que contiene los objetos de base de datos. |
| `auth.params.sslMode` | Un valor booleano que indica si se aplican o no medidas SSL. |
| `connectionSpec.id` | Id. de especificación de conexión que corresponde al origen [!DNL Oracle DB]. Este valor de identificador se corrigió como: `d6b52d86-f0f8-475f-89d4-ce54c8527328.` |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión base recién creada, incluido su identificador único (`id`) y sus correspondientes. Puede usar la ID para [crear conexión de origen](../../collect/database-nosql.md#create-a-source-connection) y la `etag` para [actualizar su cuenta](../../update.md).

+++Ver respuesta

```json
{
    "id": "f847950c-1c12-4568-a550-d5312b16fdb8",
    "etag": "\"0c0099f4-0000-0200-0000-67da91710000\""
}
```

+++


## Crear un flujo de datos para [!DNL Oracle DB] datos

Ahora que ha conectado correctamente su cuenta de [!DNL Oracle DB], puede [crear un flujo de datos e introducir datos de su base de datos en Experience Platform](../../collect/database-nosql.md).