---
description: Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/Destinations/publish`.
title: Operaciones de extremo de la API de Publish Destinations
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 4%

---

# Operaciones de API de extremo de Destinos de publicación {#publish-destination}

>[!IMPORTANT]
>
>Solo debe utilizar este extremo de API si está enviando un destino producido (público) para que lo utilicen otros clientes Experience Platform. Si está creando un destino privado para su propio uso, no necesita enviar formalmente el destino mediante la API de publicación.

>[!IMPORTANT]
>
>**Punto de conexión de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

En esta página se enumeran y describen todas las operaciones de API que puede realizar mediante la `/authoring/destinations/publish` extremo de API.

Después de configurar y probar el destino, puede enviarlo a Adobe para su revisión y publicación. Lectura [Enviar para revisión un destino creado en Destination SDK](./submit-destination.md) para todos los demás pasos que debe realizar como parte del proceso de envío de destino.

Utilice el extremo de la API de destinos de publicación para enviar una solicitud de publicación cuando:

* Como socio Destination SDK, desea que el destino productivo esté disponible en todas las organizaciones de Experience Platform para que lo utilicen todos los clientes Experience Platform;
* Usted hace *cualquier actualización* a sus configuraciones. Las actualizaciones de configuración se reflejan en el destino solo después de enviar una nueva solicitud de publicación, que el equipo del Experience Platform aprueba.

<!-- * You want to make your custom destination available in your own Experience Platform organization, across all sandboxes. -->

## Introducción a las operaciones de API de publicación de destino {#get-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Enviar una configuración de destino para su publicación {#create}

Puede enviar una configuración de destino para su publicación realizando una solicitud de POST al `/authoring/destinations/publish` punto final.

**Formato de API**

```http
POST /authoring/destinations/publish
```

**Solicitud**

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
| `destinationId` | Cadena | El ID de destino de la configuración de destino que envía para su publicación. Obtenga el ID de destino de una configuración de destino utilizando la variable [referencia de la API de configuración de destino](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Cadena | Uso `ALL` para que su destino aparezca en el catálogo para todos los clientes Experience Platform. |

{style="table-layout:auto"}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la solicitud de publicación de destino.

## Enumerar solicitudes de publicación de destino {#retrieve-list}

Puede recuperar una lista de todos los destinos enviados para su publicación en la organización realizando una solicitud de GET al `/authoring/destinations/publish` punto final.

**Formato de API**

```http
GET /authoring/destinations/publish
```

**Solicitud**

La siguiente solicitud recupera la lista de destinos enviados para la publicación a los que tiene acceso, según la organización y la configuración del entorno limitado.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de destinos enviados para publicación a la que tiene acceso, en función del ID de organización y el nombre del simulador de pruebas que ha utilizado. One `configId` corresponde a la solicitud de publicación de un destino.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"123cs780-ce29-434f-921e-4ed6ec2a6c35",
         "allowedOrgs": [
            "*"
         ],    
         "status":"PUBLISHED",
         "destinationType": "PUBLIC",
         "publishedDate":"1630617746"
      }
   ]
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `destinationId` | Cadena | El ID de destino de la configuración de destino que ha enviado para su publicación. |
| `publishDetailsList.configId` | Cadena | El ID exclusivo de la solicitud de publicación de destino para el destino enviado. |
| `publishDetailsList.allowedOrgs` | Cadena | Devuelve las organizaciones de Experience Platform para las que está disponible el destino. <br> <ul><li> Para `"destinationType": "PUBLIC"`, este parámetro devuelve `"*"`, lo que significa que el destino está disponible para todas las organizaciones de Experience Platform.</li><li> Para `"destinationType": "DEV"`, este parámetro devuelve el ID de organización de la organización que utilizó para crear y probar el destino.</li></ul> |
| `publishDetailsList.status` | Cadena | El estado de la solicitud de publicación de destino. Los valores posibles son `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinos con valor `PUBLISHED` están activas y pueden utilizarlas los clientes Experience Platform. |
| `publishDetailsList.destinationType` | Cadena | Tipo de destino. Los valores pueden `DEV` y `PUBLIC`. `DEV` corresponde al destino de su organización de Experience Platform. `PUBLIC` corresponde al destino que ha enviado para su publicación. Piense en estas dos opciones en términos de Git, donde la variable `DEV` representa su rama de creación local y la `PUBLIC` representa la rama principal remota. |
| `publishDetailsList.publishedDate` | Cadena | La fecha en la que se envió el destino para su publicación, en tiempo de época. |

{style="table-layout:auto"}

## Obtener el estado de una solicitud de publicación de destino específica {#get}

Puede recuperar información detallada sobre una solicitud de publicación de destino específica realizando una solicitud de GET al `/authoring/destinations/publish` y proporcionando el ID del destino para el que desea recuperar el estado de publicación.

**Formato de API**

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID del destino para el que desea recuperar el estado de publicación. |

**Solicitud**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con información detallada sobre la solicitud de publicación de destino especificada.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"ab41387c0-4772-4709-a3ce-6d5fee654520",
         "allowedOrgs":[
            "716543205DB85F7F0A495E5B@AdobeOrg"
         ],
         "status":"TEST",
         "destinationType":"DEV"
      },
      {
         "configId":"cd568c67-f25e-47e4-b9a2-d79297a20b27",
         "allowedOrgs":[
            "*"
         ],
         "status":"DEPRECATED",
         "destinationType":"PUBLIC",
         "publishedDate":1630525501009
      },
      {
         "configId":"ef6f07154-09bc-4bee-8baf-828ea9c92fba",
         "allowedOrgs":[
            "*"
         ],
         "status":"PUBLISHED",
         "destinationType":"PUBLIC",
         "publishedDate":1630531586002
      }
   ]
}
```

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo enviar una solicitud de publicación para su destino. El equipo de Adobe Experience Platform revisará su solicitud de publicación y le responderá con cinco días hábiles.
