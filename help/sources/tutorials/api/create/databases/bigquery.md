---
title: Conexión de Google BigQuery a Experience Platform mediante la API de Flow Service
description: Aprenda a conectar Adobe Experience Platform a Google BigQuery mediante la API de Flow Service.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 51f90366-7a0e-49f1-bd57-b540fa1d15af
source-git-commit: 1900a8c6a3f3119c8b9049b12f5660cc9fd181a2
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---

# Conectar [!DNL Google BigQuery] a Experience Platform mediante la API [!DNL Flow Service]

>[!IMPORTANT]
>
>El origen [!DNL Google BigQuery] está disponible en el catálogo de orígenes para los usuarios que han adquirido Real-Time Customer Data Platform Ultimate.

Lea esta guía para aprender a conectar su base de datos de [!DNL Google BigQuery] a Adobe Experience Platform mediante la [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introducción 

Esta guía requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [Fuentes](../../../../home.md): Experience Platform permite la ingesta de datos de varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform.
* [Zonas protegidas](../../../../../sandboxes/home.md): Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía sobre [introducción a las API de Platform](../../../../../landing/api-guide.md).

### Recopilar credenciales necesarias

Lea la [[!DNL Google BigQuery] guía de autenticación](../../../../connectors/databases/bigquery.md#prerequisites) para ver los pasos detallados sobre cómo recuperar sus credenciales de [!DNL Google BigQuery].

## Conectar [!DNL Google BigQuery] a Experience Platform en Azure {#azure}

Lea los pasos siguientes para obtener información sobre cómo conectar su origen de [!DNL Google BigQuery] a Experience Platform en Azure.

### Crear una conexión base para [!DNL Google BigQuery] en Experience Platform en Azure {#azure-base}

Una conexión base retiene información entre el origen y Platform, incluidas las credenciales de autenticación del origen, el estado actual de la conexión y el ID único de conexión base. El ID de conexión base le permite explorar y navegar por archivos desde el origen e identificar los elementos específicos que desea introducir, incluida la información sobre sus tipos de datos y formatos.

Para crear un identificador de conexión base, realice una petición POST al extremo `/connections` y proporcione sus credenciales de autenticación [!DNL Google BigQuery] como parte de los parámetros de solicitud.

**Formato de API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Usar autenticación básica]

+++Solicitud

La siguiente solicitud crea una conexión base para [!DNL Google BigQuery] mediante autenticación básica.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Google BigQuery connection with basic authentication",
        "description": "Google BigQuery connection with basic authentication",
        "auth": {
            "specName": "Basic Authentication",
            "type": "OAuth2.0",
            "params": {
                    "project": "{PROJECT}",
                    "clientId": "{CLIENT_ID},
                    "clientSecret": "{CLIENT_SECRET}",
                    "refreshToken": "{REFRESH_TOKEN}"
                }
        },
        "connectionSpec": {
            "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
            "version": "1.0"
        }
    }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.project` | Identificador de proyecto del proyecto predeterminado [!DNL Google BigQuery] que se va a consultar. en contra. |
| `auth.params.clientId` | El valor de ID utilizado para generar el token de actualización. |
| `auth.params.clientSecret` | Valor de cliente utilizado para generar el token de actualización. |
| `auth.params.refreshToken` | El token de actualización obtenido de [!DNL Google] se usó para autorizar el acceso a [!DNL Google BigQuery]. |
| `connectionSpec.id` | Identificador de especificación de conexión [!DNL Google BigQuery]: `3c9b37f8-13a6-43d8-bad3-b863b941fedd`. |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!TAB Usar autenticación de servicio]


+++Solicitud

La siguiente solicitud crea una conexión base para [!DNL Google BigQuery] mediante la autenticación de servicio:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection with service account",
      "description": "Google BigQuery connection with service account",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "largeResultsDataSetId": "{LARGE_RESULTS_DATASET_ID}"
              }
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `auth.params.projectId` | Identificador de proyecto del proyecto predeterminado [!DNL Google BigQuery] que se va a consultar. en contra. |
| `auth.params.keyFileContent` | El archivo de clave que se utiliza para autenticar la cuenta de servicio. Debe codificar el contenido del archivo de claves en [!DNL Base64]. |
| `auth.params.largeResultsDataSetId` | (Opcional) El ID del conjunto de datos [!DNL Google BigQuery] creado previamente que es necesario para habilitar la compatibilidad con grandes conjuntos de resultados. |

+++

+++Respuesta

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar los datos en el siguiente tutorial.

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

>[!ENDTABS]

## Conectar [!DNL Google BigQuery] a Experience Platform en Amazon Web Service (AWS) {#aws}

Lea los pasos siguientes para obtener información sobre cómo conectar su base de datos de [!DNL Google BigQuery] a Experience Platform en AWS.

### Crear una conexión base para [!DNL Google BigQuery] en Experience Platform en AWS

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../../../landing/multi-cloud.md).

**Formato de API**

```https
POST /connections
```

**Solicitud**

La siguiente solicitud crea una conexión base para conectar [!DNL Google BigQuery] a Experience Platform en AWS.

+++Seleccione para ver el ejemplo

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Google BigQuery base connection on AWS",
      "description": "Google BigQuery base connection on AWS",
      "auth": {
          "specName": "Service Authentication",
          "params": {
                  "projectId": "{PROJECT_ID}",
                  "keyFileContent": "{KEY_FILE_CONTENT},
                  "datasetId": "{DATASET_ID}"
      },
      "connectionSpec": {
          "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
          "version": "1.0"
      }
  }'
```

| Propiedad | Descripción |
| --- | --- |
| `auth.params.projectId` | Identificador de proyecto del proyecto predeterminado [!DNL Google BigQuery] que se va a consultar. en contra. |
| `auth.params.keyFileContent` | El archivo de clave que se utiliza para autenticar la cuenta de servicio. Debe codificar el contenido del archivo de claves en [!DNL Base64]. |
| `auth.params.datasetId` | ID del conjunto de datos que corresponde con el origen [!DNL Google BigQuery]. Este ID representa la ubicación de las tablas de datos. |

+++

**Respuesta**

Una respuesta correcta devuelve detalles de la conexión recién creada, incluido su identificador único (`id`). Este ID es necesario para explorar el almacenamiento en el siguiente tutorial.

+++Seleccione para ver el ejemplo

```json
{
    "id": "6990abad-977d-41b9-a85d-17ea8cf1c0e4",
    "etag": "\"ca00acbf-0000-0200-0000-60149e1e0000\""
}
```

+++

## Pasos siguientes

Siguiendo este tutorial, ha creado una conexión base [!DNL Google BigQuery] mediante la API [!DNL Flow Service]. Puede utilizar este ID de conexión base en los siguientes tutoriales:

* [Explore la estructura y el contenido de las tablas de datos mediante la API  [!DNL Flow Service] B](../../explore/tabular.md)
* [Cree un flujo de datos para llevar los datos de la base de datos a Platform mediante la API  [!DNL Flow Service] ](../../collect/database-nosql.md)
