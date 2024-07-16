---
solution: Experience Platform
title: Editar conexiones de destino mediante la API de Flow Service
type: Tutorial
description: Obtenga información sobre cómo editar varios componentes de una conexión de destino mediante la API de Flow Service.
exl-id: d6d27d5a-e50c-4170-bb3a-c4cbf2b46653
source-git-commit: 2a72f6886f7a100d0a1bf963eedaed8823a7b313
workflow-type: tm+mt
source-wordcount: '1605'
ht-degree: 5%

---

# Editar conexiones de destino mediante la API de Flow Service

Este tutorial trata los pasos para editar varios componentes de una conexión de destino. Obtenga información sobre cómo actualizar las credenciales de autenticación, la ubicación de exportación y mucho más usando la [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Actualmente, las operaciones de edición descritas en este tutorial solo se admiten a través de la API de Flow Service.

## Introducción {#get-started}

Este tutorial requiere que tenga un ID de flujo de datos válido. Si no tiene un ID de flujo de datos válido, seleccione el destino que elija en el [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectarse al destino](../ui/connect-destination.md) y [activar los datos](../ui/activation-overview.md) antes de intentar este tutorial.

>[!NOTE]
>
> Los términos *flow* y *dataflow* se usan indistintamente en este tutorial. En el contexto de este tutorial, tienen el mismo significado.

Este tutorial también requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
* [Zonas protegidas](../../sandboxes/home.md): El Experience Platform proporciona zonas protegidas virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para actualizar correctamente el flujo de datos mediante la API [!DNL Flow Service].

### Lectura de llamadas de API de muestra {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas, encabezados obligatorios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de la API. Para obtener información sobre las convenciones utilizadas en la documentación de las llamadas de API de ejemplo, consulte la sección sobre [cómo leer las llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilación de valores para los encabezados obligatorios {#gather-values-for-required-headers}

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos del Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aislados en zonas protegidas virtuales específicas. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre de la zona protegida en la que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si no se especifica el encabezado `x-sandbox-name`, las solicitudes se resuelven en la zona protegida `prod`.

Todas las solicitudes que contienen una carga útil (`POST`, `PUT`, `PATCH`) requieren un encabezado de tipo multimedia adicional:

* `Content-Type: application/json`

## Búsqueda de detalles de flujo de datos {#look-up-dataflow-details}

El primer paso para editar la conexión de destino es recuperar los detalles del flujo de datos con el ID de flujo. Puede ver los detalles actuales de un flujo de datos existente realizando una solicitud de GET al extremo `/flows`.

>[!TIP]
>
>Puede utilizar la interfaz de usuario del Experience Platform para obtener el ID de flujo de datos deseado de un destino. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]**, seleccione el flujo de datos de destino deseado y busque el ID de destino en el carril derecho. El ID de destino es el valor que utilizará como ID de flujo en el siguiente paso.
>
> ![Obtener el identificador de destino mediante la interfaz de usuario del Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El valor `id` único del flujo de datos de destino que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información sobre el ID de flujo.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales del flujo de datos, incluida su versión, el identificador único (`id`) y otra información relevante. Los más relevantes para este tutorial son la conexión de destino y los ID de conexión base resaltados en la respuesta que aparece a continuación. Utilizará estos ID en las secciones siguientes para actualizar varios componentes de la conexión de destino.

```json {line-numbers="true" start-line="1" highlight="27,38"}
{
   "items":[
      {
         "id":"226fb2e1-db69-4760-b67e-9e671e05abfc",
         "createdAt":"{CREATED_AT}",
         "updatedAt":"{UPDATED_BY}",
         "createdBy":"{CREATED_BY}",
         "updatedBy":"{UPDATED_BY}",
         "createdClient":"{CREATED_CLIENT}",
         "updatedClient":"{UPDATED_CLIENT}",
         "sandboxId":"{SANDBOX_ID}",
         "sandboxName":"prod",
         "imsOrgId":"{ORG_ID}",
         "name":"2021 winter campaign",
         "description":"ACME company holiday campaign for high fidelity customers",
         "flowSpec":{
            "id":"71471eba-b620-49e4-90fd-23f1fa0174d8",
            "version":"1.0"
         },
         "state":"enabled",
         "version":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "etag":"\"8b0351ca-0000-0200-0000-61c4d6700000\"",
         "sourceConnectionIds":[
            "5e45582a-5336-4ea1-9ec9-d0004a9f344a"
         ],
         "targetConnectionIds":[
            "8ce3dc63-3766-4220-9f61-51d2f8f14618"
         ],
         "inheritedAttributes":{
            "sourceConnections":[
               {
                  "id":"5e45582a-5336-4ea1-9ec9-d0004a9f344a",
                  "connectionSpec":{
                     "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"0a82f29f-b457-47f7-bb30-33856e2ae5aa",
                     "connectionSpec":{
                        "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1",
                        "version":"1.0"
                     }
                  },
                  "typeInfo":{
                     "type":"ProfileFragments",
                     "id":"ups"
                  }
               }
            ],
            "targetConnections":[
               {
                  "id":"8ce3dc63-3766-4220-9f61-51d2f8f14618",
                  "connectionSpec":{
                     "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                     "version":"1.0"
                  },
                  "baseConnection":{
                     "id":"7fbf542b-83ed-498f-8838-8fde0c4d4d69",
                     "connectionSpec":{
                        "id":"0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
                        "version":"1.0"
                     }
                  }
               }
            ]
         },
         "transformations":[
            "shortened for brevity"
         ]
      }
   ]
```

>[!ENDSHADEBOX]

## Editar componentes de conexión de destino (ubicación de almacenamiento y otros componentes) {#patch-target-connection}

Los componentes de una conexión de destino difieren según el destino. Por ejemplo, para [!DNL Amazon S3] destinos, puede actualizar el bloque y la ruta donde se exportan los archivos. Para [!DNL Pinterest] destinos, puede actualizar su [!DNL Pinterest Advertiser ID] y para [!DNL Google Customer Match], puede actualizar su [!DNL Pinterest Account ID].

Para actualizar los componentes de una conexión de destino, realice una solicitud `PATCH` al extremo `/targetConnections/{TARGET_CONNECTION_ID}` y proporcione el identificador, la versión y los nuevos valores de conexión de destino que desee utilizar. Recuerde que obtuvo el ID de conexión de Target en el paso anterior, cuando inspeccionó un flujo de datos existente en el destino deseado.

>[!IMPORTANT]
>
>Se requiere el encabezado `If-Match` al realizar una solicitud `PATCH`. El valor de este encabezado es la versión única de la conexión de destino que desea actualizar. El valor de la etiqueta se actualiza con cada actualización correcta de una entidad de flujo, como flujo de datos, conexión de destino y otras.
>
> Para obtener la última versión del valor de etiqueta, realice una solicitud de GET al extremo `/targetConnections/{TARGET_CONNECTION_ID}`, donde `{TARGET_CONNECTION_ID}` es el identificador de conexión de destino que desea actualizar.
>
> Asegúrese de encerrar el valor del encabezado `If-Match` entre comillas dobles, como en los ejemplos siguientes, al realizar `PATCH` solicitudes.

A continuación se muestran algunos ejemplos de actualización de parámetros en la especificación de conexión de destino para diferentes tipos de destinos. Sin embargo, la regla general para actualizar los parámetros de cualquier destino es la siguiente:

Obtenga el ID de flujo de datos de la conexión > obtenga el ID de conexión de destino > `PATCH` de la conexión de destino con valores actualizados para los parámetros deseados.

>[!BEGINSHADEBOX]

**Formato de API**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

La siguiente solicitud actualiza los parámetros `bucketName` y `path` de una conexión de destino [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "bucketName": "newBucketName",
      "path": "updatedPath"
    }
  }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de destino y una etiqueta electrónica actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de conexión de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager y Google Ad Manager 360]

**Solicitud**

La siguiente solicitud actualiza los parámetros de una conexión [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) o [[!DNL Google Ad Manager 360] destino](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) para agregar el nuevo campo [**[!UICONTROL Anexar ID de audiencia al nombre de audiencia]**](/help/release-notes/2023/april-2023.md#destinations).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/params/appendSegmentId",
    "value": true
  }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de destino y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de conexión de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Solicitud**

La siguiente solicitud actualiza el parámetro `advertiserId` de una [[!DNL Pinterest] conexión de destino](/help/destinations/catalog/advertising/pinterest.md#parameters).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "replace",
    "path": "/params",
    "value": {
      "advertiser_id": "1234567890"
    }
  }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión de destino y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de conexión de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Editar componentes de conexión base (parámetros de autenticación y otros componentes) {#patch-base-connection}

Edite la conexión base cuando desee actualizar las credenciales de un destino. Los componentes de una conexión base difieren según el destino. Por ejemplo, para [!DNL Amazon S3] destinos, puede actualizar la clave de acceso y la clave secreta a su ubicación [!DNL Amazon S3].

Para actualizar los componentes de una conexión base, realice una solicitud `PATCH` al extremo `/connections` y proporcione el identificador, la versión y los nuevos valores de la conexión base que desee utilizar.

Recuerde que obtuvo el identificador de conexión base en un [paso anterior](#look-up-dataflow-details), cuando inspeccionó un flujo de datos existente en el destino deseado para el parámetro `baseConnection`.

>[!IMPORTANT]
>
>Se requiere el encabezado `If-Match` al realizar una solicitud `PATCH`. El valor de este encabezado es la versión única de la conexión base que desea actualizar. El valor de la etiqueta se actualiza con cada actualización correcta de una entidad de flujo, como flujo de datos, conexión base y otras.
>
> Para obtener la última versión del valor Etag, realice una solicitud de GET al extremo `/connections/{BASE_CONNECTION_ID}`, donde `{BASE_CONNECTION_ID}` es el identificador de conexión base que desea actualizar.
>
> Asegúrese de encerrar el valor del encabezado `If-Match` entre comillas dobles, como en los ejemplos siguientes, al realizar `PATCH` solicitudes.

A continuación se muestran algunos ejemplos de actualización de parámetros en la especificación de conexión base para diferentes tipos de destinos. Sin embargo, la regla general para actualizar los parámetros de cualquier destino es la siguiente:

Obtenga el ID de flujo de datos de la conexión > obtenga el ID de conexión base > `PATCH` de la conexión base con valores actualizados para los parámetros deseados.

>[!BEGINSHADEBOX]

**Formato de API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

La siguiente solicitud actualiza los parámetros `accessId` y `secretKey` de una conexión de destino [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details).

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "accessId": "exampleAccessId",
      "secretKey": "exampleSecretKey"
    }
  }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión base y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de conexión base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB blob de Azure]

**Solicitud**

La siguiente solicitud actualiza los parámetros de una conexión [[!DNL Azure Blob] destination](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) para actualizar la cadena de conexión necesaria para conectarse a una instancia de Azure Blob.

```shell
curl -X PATCH \
    'https://platform.adobe.io/data/foundation/flowservice/targetConnections/b2cb1407-3114-441c-87ea-2c1a3c84d0b0' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
    -H 'If-Match: "1a0037e4-0000-0200-0000-602e06f60000"' \
    -d '[
  {
    "op": "add",
    "path": "/auth/params",
    "value": {
      "connectionString": "updatedString"
    }
  }
]'
```

| Propiedad | Descripción |
| --------- | ----------- |
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace` y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve el ID de conexión base y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la API [!DNL Flow Service], al tiempo que proporciona su ID de conexión base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Administración de errores de API {#api-error-handling}

Los extremos de la API en este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](/help/landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](/help/landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform para obtener más información sobre la interpretación de respuestas de error.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha aprendido a actualizar varios componentes de una conexión de destino mediante la API [!DNL Flow Service]. Para obtener más información sobre los destinos, consulte la [descripción general de los destinos](../home.md).
