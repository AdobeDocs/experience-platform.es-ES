---
description: Esta página ejemplifica la llamada de API utilizada para recuperar detalles sobre una solicitud de publicación de destino a través del Adobe Experience Platform Destination SDK.
title: Recuperar una solicitud de publicación de destino
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 3%

---


# Recuperar una solicitud de publicación de destino

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

## Enumerar solicitudes de publicación de destino {#retrieve-list}

Puede recuperar una lista de todos los destinos enviados para su publicación en la organización IMS realizando una solicitud de GET al `/authoring/destinations/publish` punto final.

**Formato de API**

Utilice el siguiente formato de API para recuperar todas las solicitudes de publicación de su cuenta.

```http
GET /authoring/destinations/publish
```

Utilice el siguiente formato de API para recuperar una solicitud de publicación específica, definido por la variable `{DESTINATION_ID}` parámetro.

```http
GET /authoring/destinations/publish/{DESTINATION_ID}
```

**Solicitud**

Las dos solicitudes siguientes recuperan todas las solicitudes de publicación de su organización de IMS o una solicitud de publicación específica, en función de si pasa la variable `DESTINATION_ID` en la solicitud.

Seleccione cada pestaña a continuación para ver la carga útil correspondiente.

>[!BEGINTABS]

>[!TAB Recuperar todas las solicitudes de publicación]

+++Solicitud

La siguiente solicitud recuperará la lista de solicitudes de publicación que ha enviado, en función de [!DNL IMS Org ID] y configuración del entorno limitado.

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/destinations/publish \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Respuesta

La siguiente respuesta devuelve el estado HTTP 200 con una lista de todos los destinos enviados para publicación a los que tiene acceso, según el ID de organización de IMS y el nombre del simulador de pruebas que ha utilizado. One `configId` corresponde a la solicitud de publicación de un destino.

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
| `publishDetailsList.configId` | Cadena | El ID exclusivo de la solicitud de publicación de destino para el destino enviado. |
| `publishDetailsList.allowedOrgs` | Cadena | Devuelve las organizaciones de Experience Platform para las que está disponible el destino. <br> <ul><li> Para `"destinationType": "PUBLIC"`, este parámetro devuelve `"*"`, lo que significa que el destino está disponible para todas las organizaciones de Experience Platform.</li><li> Para `"destinationType": "DEV"`, este parámetro devuelve el ID de organización de la organización que utilizó para crear y probar el destino.</li></ul> |
| `publishDetailsList.status` | Cadena | El estado de la solicitud de publicación de destino. Los valores posibles son `TEST`, `REVIEW`, `APPROVED`, `PUBLISHED`, `DENIED`, `REVOKED`, `DEPRECATED`. Destinos con valor `PUBLISHED` están activas y pueden utilizarlas los clientes Experience Platform. |
| `publishDetailsList.destinationType` | Cadena | Tipo de destino. Los valores pueden `DEV` y `PUBLIC`. `DEV` corresponde al destino de su organización de Experience Platform. `PUBLIC` corresponde al destino que ha enviado para su publicación. Piense en estas dos opciones en términos de Git, donde la variable `DEV` representa su rama de creación local y la `PUBLIC` representa la rama principal remota. |
| `publishDetailsList.publishedDate` | Cadena | La fecha en la que se envió el destino para su publicación, en tiempo de época. |

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

Si ha pasado un `DESTINATION_ID` en la llamada de API, la respuesta devuelve el estado HTTP 200 con información detallada sobre la solicitud de publicación de destino especificada.

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

+++

>[!ENDTABS]

## Gestión de errores de API

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.