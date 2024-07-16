---
description: Obtenga información sobre cómo dar formato a una llamada de API para enviar una solicitud de publicación de destino a través del Adobe Experience Platform Destination SDK.
title: Crear una solicitud de publicación de destino
exl-id: 913be9de-a699-4756-885d-b3761ec729cb
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 2%

---

# Crear una solicitud de publicación de destino

>[!IMPORTANT]
>
>Solo debe utilizar este punto final de API si envía un destino productizado (público) para que lo utilicen otros clientes de Experience Platform. Si está creando un destino privado para su propio uso, no necesita enviar formalmente el destino mediante la API de publicación.

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Después de configurar y probar el destino, puede enviarlo al Adobe para que lo revise y publique. Lea [Enviar para revisión un destino creado en el Destination SDK](../guides/submit-destination.md) para todos los demás pasos que debe realizar como parte del proceso de envío de destino.

Utilice el punto final de la API de destinos de publicación para enviar una solicitud de publicación cuando:

* Como socio Destination SDK, desea que el destino de productos esté disponible en todas las organizaciones de Experience Platform para que lo utilicen todos los clientes Experience Platform;
* Haces *cualquier actualización* a tus configuraciones. Las actualizaciones de configuración se reflejan en el destino solo después de enviar una nueva solicitud de publicación, que es aprobada por el equipo de Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por el Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de publicación de destino {#get-started}

Antes de continuar, revisa la [guía de introducción](../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Enviar una configuración de destino para publicarla {#create}

Puede enviar una configuración de destino para publicarla realizando una solicitud de POST al extremo `/authoring/destinations/publish`.

**Formato de API**

```http
POST /authoring/destinations/publish
```

+++Solicitud

La siguiente solicitud envía un destino para la publicación, entre las organizaciones configuradas por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el extremo `/authoring/destinations/publish`.

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
| `destinationId` | Cadena | El ID de destino de la configuración de destino que envía para su publicación. Obtenga el identificador de destino de una configuración de destino mediante la llamada a la API [recuperar una configuración de destino](../authoring-api/destination-configuration/retrieve-destination-configuration.md). |
| `destinationAccess` | Cadena | Use `ALL` para que el destino aparezca en el catálogo para todos los clientes de Experience Platform. |

{style="table-layout:auto"}

+++

+++Respuesta

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la solicitud de publicación de destino.

+++

## Administración de errores de API

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo enviar una solicitud de publicación para su destino. El equipo de Adobe Experience Platform revisará su solicitud de publicación y se pondrá en contacto con usted en un plazo de cinco días laborables.
