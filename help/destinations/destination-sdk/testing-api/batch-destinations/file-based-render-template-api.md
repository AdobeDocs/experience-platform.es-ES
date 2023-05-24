---
description: En esta página se explica cómo utilizar el extremo /authoring/testing/template/render para visualizar el aspecto que tendrían los campos de datos del cliente con plantillas definidos en la configuración de destino.
title: Validar campos de cliente con plantilla
exl-id: 8ed93f0c-3439-4d11-bb2f-d417a1e0b6a8
source-git-commit: 6bd169075cd3826ae2a0907e6e624fd901076a4a
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---


# Validar campos de cliente con plantilla

## Información general {#overview}

El `/authoring/testing/template/render` El punto de conexión le ayuda a visualizar cómo se personalizan las plantillas [campos de datos del cliente](../../functionality/destination-configuration/customer-data-fields.md) definido en la configuración de destino tendría el siguiente aspecto:.

El extremo genera valores aleatorios para los campos de datos del cliente y los devuelve en la respuesta. Esto le ayuda a validar la estructura semántica de los campos de datos del cliente, como los nombres de los bloques o las rutas de carpetas.

## Primeros pasos {#getting-started}

Antes de continuar, consulte la [guía de introducción](../../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Requisitos previos {#prerequisites}

Antes de usar el `/template/render` extremo, asegúrese de cumplir las siguientes condiciones:

* Tiene un destino basado en archivos existente creado mediante el Destination SDK y puede verlo en su [catálogo de destinos](../../../ui/destinations-workspace.md).
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debe utilizar en la llamada a la API, desde la dirección URL, al examinar una conexión con su destino en la interfaz de usuario de Platform.

   ![Imagen de la interfaz de usuario que muestra cómo obtener el ID de instancia de destino desde la URL.](../../assets/testing-api/get-destination-instance-id.png)

## Procesar campos de cliente con plantillas {#render-customer-fields}

**Formato de API**

```http
POST /authoring/testing/template/render/destination
```

Para ilustrar el comportamiento de este extremo de API, consideremos un destino basado en archivos con la siguiente configuración de campos de datos del cliente:

```json
"fileBasedS3Destination":{
   "bucket":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.bucket}}"
   },
   "path":{
      "templatingStrategy":"PEBBLE_V1",
      "value":"{{customerData.path}}"
   }
}
```

**Solicitud**

La solicitud siguiente llama a `/authoring/testing/template/render` extremo, que devuelve una respuesta con valores generados aleatoriamente para los dos campos de datos del cliente mencionados anteriormente.

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/template/render/destination' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
    "destinationId": "{DESTINATION_CONFIGURATION_ID}",
    "templates": {
        "bucket": "{{customerData.bucket}}",
        "path": "{{customerData.bucket}}/{{customerData.path}}"
    }
}'
```

| Parámetros | Descripción |
| -------- | ----------- |
| `destinationId` | El ID del [configuración de destino](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) que está probando. |
| `templates` | Los nombres de los campos con plantillas definidos en su [configuración del servidor de destino](../../authoring-api/destination-server/create-destination-server.md). |

**Respuesta**

Una respuesta correcta devuelve un `HTTP 200 OK` estado y el cuerpo incluye valores generados aleatoriamente para los campos con plantilla.

Esta respuesta puede ayudarle a validar la estructura correcta de los campos de datos del cliente, como los nombres de los bloques o las rutas de carpetas.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo validar la configuración del campo de datos del cliente definida en su [servidor de destino](../../authoring-api/destination-server/create-destination-server.md).
