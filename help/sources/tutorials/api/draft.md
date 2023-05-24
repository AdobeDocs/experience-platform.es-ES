---
keywords: Experience Platform;inicio;temas populares;servicio de flujo;
title: Borradores de flujos de datos mediante la API de Flow Service
description: Obtenga información sobre cómo establecer los flujos de datos en estado de borrador mediante la API de Flow Service.
badge: label="Nueva función" type="Positiva"
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 3%

---

# Borradores de flujos de datos mediante la API de Flow Service

Guarde los flujos de datos como borradores al utilizar la API de Flow Service suministrando la variable `mode=draft` parámetro de consulta durante la llamada de creación de flujo. Los borradores se pueden actualizar más tarde con información nueva y, a continuación, publicar una vez que estén listos. Este tutorial cubre los pasos para establecer los flujos de datos en estado de borrador mediante la API de Flow Service.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Zonas protegidas](../../../sandboxes/home.md): [!DNL Experience Platform] proporciona zonas protegidas virtuales que dividen una sola [!DNL Platform] en entornos virtuales independientes para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

### Requisitos previos

Este tutorial requiere que ya haya generado los recursos necesarios para crear un flujo de datos. Esto incluye lo siguiente:

* Una conexión base autenticada
* Una conexión de origen
* Un esquema XDM de destino
* Un conjunto de datos de destinatario
* Una conexión de destino
* Una asignación

Si todavía no tiene estos valores, seleccione un origen de [información general sobre el catálogo en orígenes](../../home.md). A continuación, siga las instrucciones de esa fuente para generar los recursos necesarios para redactar un flujo de datos.

### Uso de API de Platform

Para obtener información sobre cómo realizar llamadas correctamente a las API de Platform, consulte la guía de [introducción a las API de Platform](../../../landing/api-guide.md).

## Definir un flujo de datos en estado de borrador

En las siguientes secciones se describe el proceso para establecer un flujo de datos como borrador, actualizarlo, publicarlo y, finalmente, eliminarlo.

### Borrador de un flujo de datos

Para establecer un flujo de datos como borrador, realice una solicitud de POST a `/flows` al añadir el `mode=draft` como parámetro de consulta. Esto le permite crear un flujo de datos y guardarlo como borrador.

**Formato de API**

```http
POST /flows?mode=draft
```

| Parámetro | Descripción |
| --- | --- |
| `mode` | Parámetro de consulta proporcionado por el usuario que decide el estado del flujo de datos. Para establecer un flujo de datos como borrador, establezca `mode` hasta `draft`. |

**Solicitud**

La siguiente solicitud crea un flujo de datos de borrador.

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

Una respuesta correcta devuelve el valor `id` y el correspondiente `etag` del flujo de datos.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Actualización de un flujo de datos

Para actualizar el borrador, realice una solicitud de PATCH a `/flows` al proporcionar el ID del flujo de datos que desea actualizar. Durante este paso, también debe proporcionar un `If-Match` parámetro de encabezado, que corresponde a la variable `etag` del flujo de datos que desea actualizar.

**Formato de API**

```http
PATCH /flows/{FLOW_ID}
```

**Solicitud**

Las siguientes solicitudes añaden transformaciones de asignación al flujo de datos esbozado.

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

Una respuesta correcta devuelve su ID de flujo y `etag`. Para comprobar el cambio, puede realizar una solicitud de GET al `/flows` al proporcionar su ID de flujo.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Publicación de un flujo de datos

Una vez que el borrador esté listo para publicarse, realice una solicitud de POST al `/flows` al proporcionar el ID del flujo de datos de borrador que desea publicar, así como una operación de acción para la publicación.

**Formato de API**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parámetro | Descripción |
| --- | --- |
| `op` | Operación de acción que actualiza el estado del flujo de datos consultado. Para publicar un flujo de datos de borrador, establezca `op` hasta `publish`. |

**Solicitud**

La siguiente solicitud publica el flujo de datos de borrador.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el ID y el correspondiente `etag` del flujo de datos.

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### Eliminación de un flujo de datos

Para eliminar el flujo de datos, realice una solicitud de DELETE a `/flows` al proporcionar el ID del flujo de datos que desea eliminar. Para ver los pasos detallados sobre cómo eliminar un flujo de datos mediante la API de Flow Service, lea la guía sobre [eliminación de un flujo de datos en la API](./delete-dataflows.md).
