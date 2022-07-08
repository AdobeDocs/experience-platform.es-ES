---
description: En esta página se explica cómo utilizar el extremo /authoring/testing/template/render para visualizar el aspecto que tendrían los campos de datos del cliente con plantilla definidos en la configuración de destino.
title: Validación de campos de cliente con plantilla
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 3%

---


# Validación de campos de cliente con plantilla

## Información general {#overview}

La variable `/authoring/testing/template/render` el extremo le ayuda a visualizar cómo se le aplica la plantilla [campos de datos del cliente](file-based-destination-configuration.md#customer-data-fields) definido en la configuración de destino tendría el aspecto siguiente.

El extremo genera valores aleatorios para los campos de datos del cliente y los devuelve en la respuesta. Esto le ayuda a validar la estructura semántica de los campos de datos del cliente, como los nombres de bloque o las rutas de carpeta.

## Primeros pasos {#getting-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Requisitos previos {#prerequisites}

Antes de usar la variable `/template/render` , asegúrese de cumplir las siguientes condiciones:

* Tiene un destino basado en archivos creado mediante el Destination SDK y puede verlo en su [catálogo de destinos](../ui/destinations-workspace.md).
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debería usar en la llamada de API, desde la dirección URL, al examinar una conexión con su destino en la interfaz de usuario de Platform.

   ![Imagen de la interfaz de usuario que muestra cómo obtener el ID de instancia de destino desde la dirección URL.](assets/get-destination-instance-id.png)

## Procesar campos de cliente con plantilla {#render-customer-fields}

**Formato de API**

```http
POST /authoring/testing/template/render/destination
```

Para ilustrar el comportamiento de este extremo de API, consideremos un destino basado en archivos con la siguiente configuración de campos de datos de clientes:

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

La siguiente solicitud llama a la función `/authoring/testing/template/render` , que devuelve una respuesta con valores generados aleatoriamente para los dos campos de datos de cliente mencionados anteriormente.

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
| `destinationId` | El ID de la variable [configuración de destino](file-based-destination-configuration.md) que está probando. |
| `templates` | Los nombres de campo con plantilla definidos en el [configuración del servidor de destino](server-and-file-configuration.md). |

**Respuesta**

Una respuesta correcta devuelve un valor `HTTP 200 OK` y el cuerpo incluye valores generados aleatoriamente para los campos con plantilla.

Esta respuesta está pensada para ayudarle a validar la estructura correcta de los campos de datos del cliente, como los nombres de bloque o las rutas de acceso a las carpetas.


```json
{
    "results": {
        "bucket": "hfWpE-bucket",
        "path": "hfWpE-bucket/ceC"
    }
}
```

## Gestión de errores de API {#api-error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe cómo validar la configuración del campo de datos del cliente definida en su [servidor de destino](server-and-file-configuration.md).
