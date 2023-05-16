---
description: Obtenga información sobre cómo dar formato a una llamada de API para enviar una solicitud de publicación de destino a través del Adobe Experience Platform Destination SDK.
title: Crear una solicitud de publicación de destino
source-git-commit: acb7075f49b4194c31371d2de63709eea7821329
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---


# Crear una solicitud de publicación de destino

>[!IMPORTANT]
>
>Solo debe utilizar este extremo de API si está enviando un destino producido (público) para que lo utilicen otros clientes Experience Platform. Si está creando un destino privado para su propio uso, no necesita enviar formalmente el destino mediante la API de publicación.

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Después de configurar y probar el destino, puede enviarlo a Adobe para su revisión y publicación. Lectura [Enviar para revisión un destino creado en Destination SDK](../guides/submit-destination.md) para todos los demás pasos que debe realizar como parte del proceso de envío de destino.

Utilice el extremo de la API de destinos de publicación para enviar una solicitud de publicación cuando:

* Como socio Destination SDK, desea que el destino productivo esté disponible en todas las organizaciones de Experience Platform para que lo utilicen todos los clientes Experience Platform;
* Usted hace *cualquier actualización* a sus configuraciones. Las actualizaciones de configuración se reflejan en el destino solo después de enviar una nueva solicitud de publicación, que el equipo del Experience Platform aprueba.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **con distinción de mayúsculas y minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los parámetros nombres y valores exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de publicación de destino {#get-started}

Antes de continuar, revise la [guía de introducción](../getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Enviar una configuración de destino para su publicación {#create}

Puede enviar una configuración de destino para su publicación realizando una solicitud de POST al `/authoring/destinations/publish` punto final.

**Formato de API**

```http
POST /authoring/destinations/publish
```

+++Solicitud

La siguiente solicitud envía un destino para su publicación en todas las organizaciones configuradas por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por la variable `/authoring/destinations/publish` punto final.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"ALL"
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `destinationId` | Cadena | El ID de destino de la configuración de destino que envía para su publicación. Obtenga el ID de destino de una configuración de destino utilizando la variable [recuperar una configuración de destino](../authoring-api/destination-configuration/retrieve-destination-configuration.md) Llamada de API. |
| `destinationAccess` | Cadena | Uso `ALL` para que su destino aparezca en el catálogo para todos los clientes Experience Platform. |

{style="table-layout:auto"}

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la solicitud de publicación de destino.

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo enviar una solicitud de publicación para su destino. El equipo de Adobe Experience Platform revisará su solicitud de publicación y le responderá con cinco días hábiles.