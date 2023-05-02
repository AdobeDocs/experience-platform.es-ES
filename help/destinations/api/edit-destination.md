---
solution: Experience Platform
title: Edición de conexiones de destino mediante la API de servicio de flujo
type: Tutorial
description: Obtenga información sobre cómo editar varios componentes de una conexión de destino mediante la API de servicio de flujo.
source-git-commit: 956ac5d210d54526e886e57b8ea37ab4b3fbab8a
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 2%

---

# Edición de conexiones de destino mediante la API de servicio de flujo

Este tutorial trata los pasos para editar los distintos componentes de una conexión de destino. Obtenga información sobre cómo actualizar las credenciales de autenticación, la ubicación de exportación y mucho más utilizando la variable [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

>[!NOTE]
>
> Actualmente, las operaciones de edición descritas en este tutorial solo se admiten a través de la API de servicio de flujo.

## Primeros pasos {#get-started}

Este tutorial requiere que tenga un ID de flujo de datos válido. Si no tiene un ID de flujo de datos válido, seleccione el destino que elija en el [catálogo de destinos](../catalog/overview.md) y siga los pasos descritos para [conectarse al destino](../ui/connect-destination.md) y [activar datos](../ui/activation-overview.md) antes de intentar este tutorial.

>[!NOTE]
>
> Los términos *flujo* y *dataflow* se utilizan de forma intercambiable en este tutorial. En el contexto de este tutorial, tienen el mismo significado.

Este tutorial también requiere que tenga una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): [!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
* [Sandboxes](../../sandboxes/home.md): Experience Platform proporciona entornos limitados virtuales que dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

Las secciones siguientes proporcionan información adicional que deberá conocer para actualizar correctamente el flujo de datos mediante el [!DNL Flow Service] API.

### Leer llamadas de API de ejemplo {#reading-sample-api-calls}

Este tutorial proporciona llamadas de API de ejemplo para demostrar cómo dar formato a las solicitudes. Estas incluyen rutas de acceso, encabezados necesarios y cargas de solicitud con el formato correcto. También se proporciona el JSON de muestra devuelto en las respuestas de API. Para obtener información sobre las convenciones utilizadas en la documentación para las llamadas de API de ejemplo, consulte la sección sobre [cómo leer llamadas de API de ejemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) en la guía de solución de problemas del Experience Platform.

### Recopilar valores para encabezados necesarios {#gather-values-for-required-headers}

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Todos los recursos del Experience Platform, incluidos los que pertenecen a [!DNL Flow Service], están aisladas para entornos limitados virtuales específicos. Todas las solicitudes a las API de Platform requieren un encabezado que especifique el nombre del simulador para pruebas en el que se realizará la operación:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Si la variable `x-sandbox-name` no se ha especificado, las solicitudes se resuelven en la sección `prod` simulador de pruebas.

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* `Content-Type: application/json`

## Buscar detalles de flujo de datos {#look-up-dataflow-details}

El primer paso para editar la conexión de destino es recuperar los detalles del flujo de datos mediante su ID de flujo. Puede ver los detalles actuales de un flujo de datos existente realizando una solicitud de GET al `/flows` punto final.

>[!TIP]
>
>Puede utilizar la interfaz de usuario del Experience Platform para obtener el ID de flujo de datos deseado de un destino. Vaya a **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]**, seleccione el flujo de datos de destino deseado y busque el ID de destino en el carril derecho. El ID de destino es el valor que utilizará como ID de flujo en el siguiente paso.
>
> ![Obtención del ID de destino mediante la interfaz de usuario del Experience Platform](/help/destinations/assets/api/edit-destination/get-destination-id.png)

>[!BEGINSHADEBOX]

**Formato de API**

```http
GET /flows/{FLOW_ID}
```

| Parámetro | Descripción |
| --------- | ----------- |
| `{FLOW_ID}` | El único `id` para el flujo de datos de destino que desea recuperar. |

**Solicitud**

La siguiente solicitud recupera información sobre su ID de flujo.

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/flows/226fb2e1-db69-4760-b67e-9e671e05abfc' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles actuales del flujo de datos, incluida su versión, el identificador único (`id`) y otra información pertinente. Los más relevantes para este tutorial son los ID de conexión de destino y de conexión de base resaltados en la respuesta a continuación. Estos ID se utilizan en las secciones siguientes para actualizar los distintos componentes de la conexión de destino.

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

Los componentes de una conexión de destino difieren según el destino. Por ejemplo, para [!DNL Amazon S3] destinos, puede actualizar el bloque y la ruta de acceso donde se exportan los archivos. Para [!DNL Pinterest] destinos, puede actualizar su [!DNL Pinterest Advertiser ID] y para [!DNL Google Customer Match] puede actualizar su [!DNL Pinterest Account ID].

Para actualizar componentes de una conexión de destino, realice una solicitud de PATCH a la `/targetConnections/{TARGET_CONNECTION_ID}` al proporcionar el ID de conexión de destino, la versión y los nuevos valores que desea utilizar. Recuerde que obtuvo su ID de conexión de destino en el paso anterior, cuando inspeccionó un flujo de datos existente en el destino deseado.

>[!IMPORTANT]
>
>La variable `If-Match` es obligatorio cuando se realiza una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión de destino que desea actualizar. El valor de etiqueta se actualiza con cada actualización correcta de una entidad de flujo, como dataflow, target connection, etc.
>
> Para obtener la versión más reciente del valor de etiqueta, realice una solicitud de GET a la variable `/targetConnections/{TARGET_CONNECTION_ID}` punto final, donde `{TARGET_CONNECTION_ID}` es el ID de conexión de destino que desea actualizar.

A continuación se presentan algunos ejemplos de actualización de parámetros en la especificación de conexión de destino para diferentes tipos de destinos. Sin embargo, la regla general para actualizar parámetros para cualquier destino es la siguiente:

Obtenga el ID de flujo de datos de la conexión > obtenga el ID de conexión de destino > PATCH de la conexión de destino con valores actualizados para los parámetros deseados.

>[!BEGINSHADEBOX]

**Formato de API**

```http
PATCH /targetConnections/{TARGET_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

La siguiente solicitud actualiza el `bucketName` y `path` parámetros de un [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) conexión de destino.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión de destino y una etiqueta Etag actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Google Ad Manager y Google Ad Manager 360]

**Solicitud**

La siguiente solicitud actualiza los parámetros de un [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md) o [[!DNL Google Ad Manager 360] destino](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) conexión para agregar la nueva [**[!UICONTROL Anexar ID de segmento al nombre del segmento]**](/help/release-notes/2023/april-2023.md#destinations) campo .

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión de destino y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Pinterest]

**Solicitud**

La siguiente solicitud actualiza el `advertiserId` parámetro de [[!DNL Pinterest] conexión de destino](/help/destinations/catalog/advertising/pinterest.md#parameters).

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión de destino y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión de destino.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Editar componentes de conexión base (parámetros de autenticación y otros componentes) {#patch-base-connection}

Los componentes de una conexión base difieren según el destino. Por ejemplo, para [!DNL Amazon S3] destinos, puede actualizar la clave de acceso y la clave secreta a su [!DNL Amazon S3] ubicación.

Para actualizar los componentes de una conexión base, realice una solicitud de PATCH al `/connections` al proporcionar el ID de conexión base, la versión y los nuevos valores que desea utilizar.

Recuerde que obtuvo su ID de conexión base en un paso anterior, cuando inspeccionó un flujo de datos existente hasta el destino deseado.

>[!IMPORTANT]
>
>La variable `If-Match` es obligatorio cuando se realiza una solicitud de PATCH. El valor de este encabezado es la versión única de la conexión base que desea actualizar. El valor de etiqueta se actualiza con cada actualización correcta de una entidad de flujo, como el flujo de datos, la conexión base y otros.
>
> Para obtener la versión más reciente del valor Etag , realice una solicitud de GET a la variable `/connections/{BASE_CONNECTION_ID}` punto final, donde `{BASE_CONNECTION_ID}` es el ID de conexión base que desea actualizar.

A continuación se presentan algunos ejemplos de actualización de parámetros en la especificación de conexión base para diferentes tipos de destinos. Sin embargo, la regla general para actualizar parámetros para cualquier destino es la siguiente:

Obtenga el ID de flujo de datos de la conexión > obtenga el ID de conexión base > PATCH de la conexión base con valores actualizados para los parámetros deseados.

>[!BEGINSHADEBOX]

**Formato de API**

```http
PATCH /connections/{BASE_CONNECTION_ID}
```

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitud**

La siguiente solicitud actualiza el `accessId` y `secretKey` parámetros de un [[!DNL Amazon S3]](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) conexión de destino.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión base y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!TAB Azure Blob]

**Solicitud**

La siguiente solicitud actualiza los parámetros de un [[!DNL Azure Blob] destino](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) para actualizar la cadena de conexión necesaria para conectarse a una instancia de Azure Blob.

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
| `op` | La llamada de operación utilizada para definir la acción necesaria para actualizar el flujo de datos. Las operaciones incluyen: `add`, `replace`y `remove`. |
| `path` | Define la parte del flujo que se va a actualizar. |
| `value` | El nuevo valor con el que desea actualizar el parámetro. |

**Respuesta**

Una respuesta correcta devuelve su ID de conexión base y una etiqueta actualizada. Puede comprobar la actualización realizando una solicitud de GET a la variable [!DNL Flow Service] al proporcionar su ID de conexión base.

```json
{
    "id": "b2cb1407-3114-441c-87ea-2c1a3c84d0b0",
    "etag": "\"50014cc8-0000-0200-0000-6036eb720000\""
}
```

>[!ENDTABS]

>[!ENDSHADEBOX]

## Gestión de errores de API {#api-error-handling}

Los extremos de API de este tutorial siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](/help/landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](/help/landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform para obtener más información sobre la interpretación de las respuestas de error.

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha aprendido a actualizar varios componentes de una conexión de destino mediante el [!DNL Flow Service] API. Para obtener más información sobre los destinos, consulte la [información general sobre destinos](../home.md).
