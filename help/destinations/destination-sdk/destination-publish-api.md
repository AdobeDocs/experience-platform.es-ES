---
description: Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/Destinations/publish`.
title: Operaciones de extremo de la API de Publish Destinations
exl-id: 0564a132-42f4-478c-9197-9b051acf093c
source-git-commit: 9be8636b02a15c8f16499172289413bc8fb5b6f0
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 5%

---

# Operaciones de API de extremo de Destinos de publicación {#publish-destination}

>[!IMPORTANT]
>
>**Punto final** de API:  `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Esta página enumera y describe todas las operaciones de API que puede realizar con el extremo de API `/authoring/destinations/publish` .

Después de configurar y probar el destino, puede enviarlo a Adobe para su revisión y publicación.

Utilice el extremo de la API de destinos de publicación para enviar una solicitud de publicación cuando:
* Como socio de SDK de destino, desea que el destino producido esté disponible en todas las organizaciones de Experience Platform para que lo utilicen todos los clientes Experience Platform;
* Desea que el destino personalizado esté disponible en su propia organización de Experience Platform, en todos los entornos limitados.

## Introducción a las operaciones de API de publicación de destino {#get-started}

Antes de continuar, consulte la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino necesario y los encabezados necesarios.

## Enviar una configuración de destino para su publicación {#create}

Puede enviar una configuración de destino para su publicación realizando una solicitud de POST al extremo `/authoring/destinations/publish` .

**Formato de API**


```http
POST /authoring/destinations/publish
```

**Solicitud**

La siguiente solicitud envía un destino para su publicación en todas las organizaciones configuradas por los parámetros proporcionados en la carga útil. La carga útil siguiente incluye todos los parámetros aceptados por el extremo `/authoring/destinations/publish` .

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "xyz@AdobeOrg",
      "lmn@AdobeOrg"
   ]
}
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `destinationId` | Cadena | El ID de destino de la configuración de destino que envía para su publicación. Obtenga el ID de destino de una configuración de destino mediante la [referencia de API de configuración de destino](./destination-configuration-api.md#retrieve-list). |
| `destinationAccess` | Cadena | `ALL` o `LIMITED`. Especifique si desea que el destino aparezca en el catálogo para todos los clientes Experience Platform o solo para determinadas organizaciones. <br> **Nota**: Si utiliza  `LIMITED`, el destino solo se publicará para su organización Experience Platform. Si desea publicar el destino en un subconjunto de organizaciones de Experience Platform con fines de prueba de clientes, póngase en contacto con el servicio de asistencia técnica de Adobe. |
| `allowedOrgs` | Cadena | Si utiliza `"destinationAccess":"LIMITED"`, especifique las organizaciones de Experience Platform para las que estará disponible el destino. |

{style=&quot;table-layout:auto&quot;}

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 201 con detalles de la solicitud de publicación de destino.

## Enumerar solicitudes de publicación de destino {#retrieve-list}

Puede recuperar una lista de todos los destinos enviados para su publicación en la organización IMS realizando una solicitud de GET al extremo `/authoring/destinations/publish` .

**Formato de API**


```http
GET /authoring/destinations/publish
```

**Solicitud**

La siguiente solicitud recuperará la lista de destinos enviados para publicación a la que tiene acceso, según la configuración de la organización y el simulador de pruebas de IMS.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Respuesta**

La siguiente respuesta devuelve el estado HTTP 200 con una lista de destinos enviados para publicación a la que tiene acceso, según el ID de organización de IMS y el nombre del simulador de pruebas que ha utilizado. Un `configId` corresponde a la solicitud de publicación de un destino.

```json
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "publishDetailsList":[
      {
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"1630617746"
      }
   ]
}
    
```

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `destinationId` | Cadena | El ID de destino de la configuración de destino que ha enviado para su publicación. |
| `publishDetailsList.configId` | Cadena | El ID exclusivo de la solicitud de publicación de destino para el destino enviado. |
| `publishDetailsList.allowedOrgs` | Cadena | Devuelve las organizaciones de Experience Platform para las que debe estar disponible el destino. |
| `publishDetailsList.status` | Cadena | El estado de la solicitud de publicación de destino. Los valores posibles son `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. |
| `publishDetailsList.publishedDate` | Cadena | La fecha en la que se envió el destino para su publicación, en tiempo de época. |

{style=&quot;table-layout:auto&quot;}

## Actualizar una solicitud de publicación de destino existente {#update}

Puede actualizar las organizaciones permitidas en una solicitud de publicación de destino existente realizando una solicitud de PUT al extremo `/authoring/destinations/publish` y proporcionando el ID del destino para el que desea actualizar las organizaciones permitidas. En el cuerpo de la llamada, proporcione las organizaciones permitidas actualizadas.

**Formato de API**


```http
PUT /authoring/destinations/publish/{DESTINATION_ID}
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID del destino para el que desea actualizar la solicitud de publicación. |

**Solicitud**

La siguiente solicitud actualiza una solicitud de publicación de destino existente, configurada por los parámetros proporcionados en la carga útil. En la llamada de ejemplo siguiente, actualizamos las organizaciones permitidas.

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destinations/publish/1230e5e4-4ab8-4655-ae1e-a6296b30f2ec \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "destinationId":"1230e5e4-4ab8-4655-ae1e-a6296b30f2ec",
   "destinationAccess":"LIMITED",
   "allowedOrgs":[
      "abc@AdobeOrg",
      "def@AdobeOrg"
   ]
}
```

## Obtener el estado de una solicitud de publicación de destino específica {#get}

Puede recuperar información detallada sobre una solicitud de publicación de destino específica realizando una solicitud de GET al extremo `/authoring/destinations/publish` y proporcionando el ID del destino para el que desea recuperar el estado de publicación.

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
         "configId":"string",
         "allowedOrgs":[
            "xyz@AdobeOrg",
            "lmn@AdobeOrg"
         ],
         "status":"TEST",
         "publishedDate":"string"
      }
   ]
}
```

## Gestión de errores de API

Los extremos de la API del SDK de destino siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte los [códigos de estado de API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) y [errores de encabezado de solicitud](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo enviar una solicitud de publicación para su destino. El equipo de Adobe Experience Platform revisará su solicitud de publicación y le responderá con cinco días hábiles.
