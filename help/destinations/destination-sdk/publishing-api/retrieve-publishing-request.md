---
description: Esta página ejemplifica la llamada de API utilizada para recuperar detalles acerca de una solicitud de publicación de destino mediante Adobe Experience Platform Destination SDK.
title: Recuperar una solicitud de publicación de destino
exl-id: fceef12d-a52c-4259-a91e-7af88b132800
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 2%

---

# Recuperar una solicitud de publicación de destino

>[!IMPORTANT]
>
>Solo debe utilizar este punto final de API si envía un destino productivo (público) para que lo utilicen otros clientes de Experience Platform. Si está creando un destino privado para su propio uso, no necesita enviar formalmente el destino mediante la API de publicación.

>[!IMPORTANT]
>
>**extremo de API**: `platform.adobe.io/data/core/activation/authoring/destinations/publish`

Después de configurar y probar el destino, puede enviarlo a Adobe para su revisión y publicación. Lea [Enviar para revisión un destino creado en Destination SDK](../guides/submit-destination.md) para todos los demás pasos que debe realizar como parte del proceso de envío de destino.

Utilice el punto final de la API de destinos de publicación para enviar una solicitud de publicación cuando:

* Como socio de Destination SDK, desea que el destino de productos esté disponible en todas las organizaciones de Experience Platform para que lo utilicen todos los clientes de Experience Platform;
* Haces *cualquier actualización* a tus configuraciones. Las actualizaciones de configuración se reflejan en el destino solo después de enviar una nueva solicitud de publicación, que es aprobada por el equipo de Experience Platform.

>[!IMPORTANT]
>
>Todos los nombres y valores de parámetro admitidos por Destination SDK distinguen entre mayúsculas y minúsculas **1}.** Para evitar errores de distinción entre mayúsculas y minúsculas, utilice los nombres y valores de los parámetros exactamente como se muestra en la documentación.

## Introducción a las operaciones de API de publicación de destino {#get-started}

Antes de continuar, revisa la [guía de introducción](../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Enumerar solicitudes de publicación de destino {#retrieve-list}

Puede recuperar una lista de todos los destinos enviados para su publicación para su organización IMS realizando una petición GET al extremo `/authoring/destinations/publish`.

**Formato de API**

Utilice el siguiente formato de API para recuperar todas las solicitudes de publicación de la cuenta.

```http
GET /authoring/destinations/publish
```

Utilice el siguiente formato de API para recuperar una solicitud de publicación específica, definida por el parámetro `{DESTINATION_ID}`.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Solicitud**

Las dos solicitudes siguientes recuperan todas las solicitudes de publicación de su organización de IMS o una solicitud de publicación específica, en función de si pasa el parámetro `DESTINATION_ID` en la solicitud.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente.

>[!BEGINTABS]

>[!TAB Recuperar todas las solicitudes de publicación]

+++Solicitud

La siguiente solicitud recuperará la lista de solicitudes de publicación que ha enviado, según la configuración de [!DNL IMS Org ID] y la zona protegida.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

La siguiente respuesta devuelve el estado HTTP 200 con una lista de todos los destinos enviados para la publicación a los que tiene acceso, en función del ID de organización de IMS y el nombre de la zona protegida que ha utilizado. Un(a) `configId` corresponde a la solicitud de publicación de un destino.

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

| Parámetro | Tipo | Descripción |
|---------|----------|------|
| `destinationId` | Cadena | El ID de destino de la configuración de destino que ha enviado para su publicación. |
| `publishDetailsList.configId` | Cadena | El ID único de la solicitud de publicación de destino del destino enviado. |
| `publishDetailsList.allowedOrgs` | Cadena | Devuelve las organizaciones de Experience Platform para las que el destino está disponible. <br> <ul><li> Para `"destinationType": "PUBLIC"`, este parámetro devuelve `"*"`, lo que significa que el destino está disponible para todas las organizaciones de Experience Platform.</li><li> Para `"destinationType": "DEV"`, este parámetro devuelve el identificador de organización de la organización que utilizó para crear y probar el destino.</li></ul> |
| `publishDetailsList.status` | Cadena | El estado de la solicitud de publicación de destino. Los valores posibles son `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Los destinos con el valor `PUBLISHED` están activos y los clientes de Experience Platform pueden utilizarlos. |
| `publishDetailsList.destinationType` | Cadena | El tipo de destino. Los valores pueden ser `DEV` y `PUBLIC`. `DEV` corresponde al destino en su organización de Experience Platform. `PUBLIC` corresponde al destino que ha enviado para su publicación. Piense en estas dos opciones en términos de Git, donde la versión `DEV` representa su rama de creación local y la versión `PUBLIC` representa la rama principal remota. |
| `publishDetailsList.publishedDate` | Cadena | La fecha en la que se envió el destino para su publicación, en tiempo récord. |

{style="table-layout:auto"}

+++

>[!TAB Recuperar una solicitud de publicación específica]

+++Solicitud

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish/{DESTINATION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{DESTINATION_ID}` | El ID del destino para el que desea recuperar el estado de publicación. |

+++

+++Respuesta

Si pasó `DESTINATION_ID` en la llamada de API, la respuesta devuelve el estado HTTP 200 con información detallada sobre la solicitud de publicación de destino especificada.

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
| `publishDetailsList.configId` | Cadena | El ID único de la solicitud de publicación de destino del destino enviado. |
| `publishDetailsList.allowedOrgs` | Cadena | Devuelve las organizaciones de Experience Platform para las que el destino está disponible. <br> <ul><li> Para `"destinationType": "PUBLIC"`, este parámetro devuelve `"*"`, lo que significa que el destino está disponible para todas las organizaciones de Experience Platform.</li><li> Para `"destinationType": "DEV"`, este parámetro devuelve el identificador de organización de la organización que utilizó para crear y probar el destino.</li></ul> |
| `publishDetailsList.status` | Cadena | El estado de la solicitud de publicación de destino. Los valores posibles son `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Los destinos con el valor `PUBLISHED` están activos y los clientes de Experience Platform pueden utilizarlos. |
| `publishDetailsList.destinationType` | Cadena | El tipo de destino. Los valores pueden ser `DEV` y `PUBLIC`. `DEV` corresponde al destino en su organización de Experience Platform. `PUBLIC` corresponde al destino que ha enviado para su publicación. Piense en estas dos opciones en términos de Git, donde la versión `DEV` representa su rama de creación local y la versión `PUBLIC` representa la rama principal remota. |
| `publishDetailsList.publishedDate` | Cadena | La fecha en la que se envió el destino para su publicación, en tiempo récord. |

{style="table-layout:auto"}

+++

>[!ENDTABS]

## Administración de errores de API

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.
