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
>Solo debe utilizar este punto final de API si envía un destino productizado (público) para que lo utilicen otros clientes de Experience Platform. Si está creando un destino privado para su propio uso, no necesita enviar formalmente el destino mediante la API de publicación.

>[!IMPORTANT]
>
>**Extremo de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Después de configurar y probar el destino, puede enviarlo al Adobe para que lo revise y publique. Leer [Enviar para revisión un destino creado en Destination SDK](../guides/submit-destination.md) para todos los demás pasos, debe realizar como parte del proceso de envío de destino.

Utilice el punto final de la API de destinos de publicación para enviar una solicitud de publicación cuando:

* Como socio Destination SDK, desea que el destino de productos esté disponible en todas las organizaciones de Experience Platform para que lo utilicen todos los clientes Experience Platform;
* Usted hace *cualquier actualización* a sus configuraciones de. Las actualizaciones de configuración se reflejan en el destino solo después de enviar una nueva solicitud de publicación, que es aprobada por el equipo de Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK son **distingue mayúsculas de minúsculas**. Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de publicación de destino {#get-started}

Antes de continuar, consulte la [guía de introducción](../getting-started.md) para obtener información importante que necesita conocer para realizar llamadas correctamente a la API, incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Enviar una configuración de destino para publicarla {#create}

Puede enviar una configuración de destino para publicarla realizando una solicitud de POST a `/authoring/destinations/publish` punto final.

**Formato de API**

```http
POST /authoring/destinations/publish
```

+++Solicitud

La siguiente solicitud envía un destino para la publicación, entre las organizaciones configuradas por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el `/authoring/destinations/publish` punto final.

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
| `destinationId` | Cadena | El ID de destino de la configuración de destino que envía para su publicación. Obtenga el ID de destino de una configuración de destino utilizando [recuperar una configuración de destino](../authoring-api/destination-configuration/retrieve-destination-configuration.md) Llamada de API. |
| `destinationAccess` | Cadena | Uso `ALL` para que el destino aparezca en el catálogo para todos los clientes de Experience Platform. |

{style="table-layout:auto"}

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la solicitud de publicación de destino.

## Administración de errores de API

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo enviar una solicitud de publicación para su destino. El equipo de Adobe Experience Platform revisará su solicitud de publicación y se pondrá en contacto con usted en un plazo de cinco días laborables.