---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;
title: Borrador de flujos de datos mediante la API de servicio de flujo
description: Aprenda a configurar los flujos de datos en estado borrador mediante la API de servicio de flujo.
badge: label="New Feature" type="Positive"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Borrador de flujos de datos mediante la API del servicio de flujo

Guarde los flujos de datos como borradores al utilizar la API de servicio de flujo suministrando la variable `mode=draft` durante la llamada de creación de flujo. Los borradores se pueden actualizar posteriormente con nueva información y luego publicar una vez que estén listos. Este tutorial trata los pasos para establecer los flujos de datos en estado de borrador mediante la API de servicio de flujo.

## Primeros pasos

Este tutorial requiere tener una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Sandboxes](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona entornos limitados virtuales que dividen un solo [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Requisitos previos

Este tutorial requiere que ya haya generado los recursos necesarios para crear un flujo de datos. Esto incluye lo siguiente:

* Una conexión base autenticada
* Una conexión de origen
* Un esquema XDM de destino
* Un conjunto de datos de destinatario
* Una conexión de destino
* Una asignación

Si todavía no tiene estos valores, seleccione una fuente de [el catálogo en la descripción general de las fuentes](../../home.md). A continuación, siga las instrucciones de esa fuente determinada para generar los recursos necesarios para crear un flujo de datos.

### Uso de las API de plataforma

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Establecer un flujo de datos en estado de borrador

Las siguientes secciones describen el proceso para establecer un flujo de datos como borrador, actualizar el flujo de datos, publicar el flujo de datos y, finalmente, eliminar el flujo de datos.

### Crear un flujo de datos

Para establecer un flujo de datos como borrador, realice una solicitud de POST a la variable `/flows` al agregar la variable `mode=draft` como parámetro de consulta. Esto le permite crear un flujo de datos y guardarlo como borrador.

**Formato de API**

```http
POST /flows?mode=draft
```

| Parámetro | Descripción |
| --- | --- |
| `mode` | Un parámetro de consulta proporcionado por el usuario que decide el estado del flujo de datos. Para establecer un flujo de datos como borrador, establezca `mode` a `draft`. |

**Solicitud**

La siguiente solicitud crea un flujo de datos borrador.

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**Respuesta**

Una respuesta correcta devuelve el valor `id` y el `etag` del flujo de datos.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Actualizar un flujo de datos

Para actualizar el borrador, realice una solicitud de PATCH al `/flows` al proporcionar el ID del flujo de datos que desea actualizar. Durante este paso, también debe proporcionar un `If-Match` parámetro header, que corresponde al parámetro `etag` del flujo de datos que desea actualizar.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

Las siguientes solicitudes añaden transformaciones de asignación al flujo de datos redactado.

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**Respuesta**

Una respuesta correcta devuelve su ID de flujo y `etag`. Para comprobar el cambio, puede realizar una solicitud de GET a la variable `/flows` al proporcionar su ID de flujo.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publicar un flujo de datos

Una vez que el borrador esté listo para publicarse, realice una solicitud de POST al `/flows` al proporcionar el ID del flujo de datos borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `op` | Operación de acción que actualiza el estado del flujo de datos consultado. Para publicar un flujo de datos de borrador, establezca `op` a `publish`. |

**Solicitud**

La siguiente solicitud publica el flujo de datos borrador.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el ID y el valor correspondiente `etag` del flujo de datos.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Eliminar un flujo de datos

Para eliminar el flujo de datos, realice una solicitud de DELETE al `/flows` al proporcionar el ID del flujo de datos que desea eliminar. Para ver los pasos detallados sobre cómo eliminar un flujo de datos mediante la API de servicio de flujo, consulte la guía de [eliminación de un flujo de datos en la API](./delete-dataflows.md).