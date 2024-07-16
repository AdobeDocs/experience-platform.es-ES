---
title: Punto final de API de contenido
description: Obtenga información sobre cómo recuperar los datos de acceso mediante la API de Privacy Service.
role: Developer
badgePrivateBeta: label="Private Beta" type="Informative"
exl-id: b3b7ea0f-957d-4e51-bf92-121e9ae795f5
source-git-commit: e3a453ad166fe244b82bd1f90e669579fcf09d17
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# Extremo de contenido

>[!IMPORTANT]
>
>El extremo `/content` se encuentra actualmente en la versión beta y es posible que su organización aún no tenga acceso a él. La funcionalidad y la documentación están sujetas a cambios.

Use el extremo `/content` para recuperar de forma segura *información de acceso* (la información a la que un sujeto de privacidad puede solicitar acceso con razón) para sus clientes. La URL de descarga proporcionada en la respuesta a una solicitud de GET de `/jobs/{JOB_ID}` apunta a un extremo de servicio de Adobe. Luego puede realizar una solicitud de GET a `/jobs/:JOB_ID/content` para que devuelva los datos de sus clientes en formato JSON. Este método de acceso implementa varias capas de autenticación y control de acceso para mejorar la seguridad.

Antes de usar esta guía, consulte la [guía de introducción](./getting-started.md) para obtener información sobre los encabezados de autenticación requeridos que se presentan en el ejemplo de llamada de API a continuación.

>[!TIP]
>
>Si actualmente no conoce el identificador de trabajo para la información de acceso que necesita, realice una llamada al extremo `/jobs` y use parámetros de consulta adicionales para filtrar los resultados. Encontrará una lista completa de los parámetros de consulta disponibles en la [guía de extremo de trabajos de privacidad](./privacy-jobs.md).

## Recuperar información de trabajo de privacidad

Para recuperar información sobre un trabajo específico, como su estado de procesamiento actual, incluya el `jobId` de ese trabajo en la ruta de una solicitud de GET al extremo `/jobs`.

**Formato de API**

```http
GET /jobs/{JOB_ID}
```

**Solicitud**

La siguiente solicitud recupera los detalles del trabajo cuyo `jobId` se ha proporcionado en la ruta de solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve los detalles del trabajo especificado.

>[!NOTE]
>
>Los trabajos de privacidad deben tener el estado `complete` para contener `downloadUrl`.

```json
{
    "jobId":"dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5",
    "requestId":"17129380910360540RX-753",
    "userKey":"1234",
    "action":"access",
    "status":"complete",
    "submittedBy":"jsnow@adobe.com",
    "createdDate":"04/12/2024 04:08 PM GMT",
    "lastModifiedDate":"04/12/2024 04:08 PM GMT",
    "userIds":[{
        "namespace":"ECID",
        "value":"1234",
        "type":"standard",
        "namespaceId":4,
        "isDeletedClientSide":false
        }],
    "productResponses":[{
        "product":"Identity",
        "retryCount":0,
        "processedDate":"04/12/2024 04:08 PM GMT",
        "productStatusResponse":{"status":"submitted"
        }}],
    "downloadUrl":"https://platform.adobe.io/data/core/privacy/jobs/dbe3a6a6-f8e6-11ee-a365-8d1d6df81cc5/content",
    "regulation":"gdpr"
}
```

| Propiedad | Descripción |
|----------------------|---------------------------------------------------------------------------------------------------------------|
| `jobId` | Un identificador único del trabajo de privacidad. |
| `requestId` | Un identificador único para la solicitud específica realizada al Privacy Service. |
| `userKey` | `userKey` es el valor `key` que proporcionó al enviar la solicitud de privacidad. El valor `key` es su oportunidad de proporcionar un identificador para el interesado que le resulte más adecuado. Suele ser un identificador único que el sistema crea para realizar el seguimiento de ese interesado. SUGERENCIA: puede enumerar todos los trabajos de privacidad activos y comparar su `key` con cada trabajo. |
| `action` | El tipo de acción solicitada. Los valores aceptados son `access` y `delete`. |
| `status` | El estado actual del trabajo de privacidad. |
| `submittedBy` | La dirección de correo electrónico de la persona que envió el trabajo de privacidad. |
| `createdDate` | La fecha y la hora en que se creó el trabajo de privacidad. |
| `lastModifiedDate` | La fecha y la hora en que se modificó el trabajo de privacidad por última vez. |
| `userIds` | Matriz que contiene identificadores de usuario e información relacionada. |
| `userIds.namespace` | El área de nombres utilizada para el identificador de usuario. |
| `userIds.value` | El valor real del identificador de usuario. |
| `userIds.type` | El tipo de identificador (por ejemplo `standard` o `custom`). |
| `userIds.namespaceId` | Identificador del área de nombres que se utiliza para categorizar y administrar las identidades de usuario. |
| `userIds.isDeletedClientSide` | Un booleano que indica si el identificador se ha eliminado en el lado del cliente. |
| `productResponses` | Matriz que contiene respuestas de diferentes productos o servicios relacionados con el trabajo de privacidad. |
| `productResponses.product` | El nombre del producto o servicio que se utilizó para obtener información sobre el interesado. |
| `productResponses.retryCount` | El número de veces que se ha reintentado la solicitud. |
| `productResponses.processedDate` | La fecha y hora en que se procesó la respuesta del producto. |
| `productResponses.productStatusResponse` | Un objeto que contiene el estado de la respuesta del producto. |
| `productResponses.productStatusResponse.status` | El estado de la respuesta del producto. |
| `downloadURL` | Este atributo proporciona un extremo que está disponible para llamar a durante 60 días después de que se complete el trabajo. El estado del trabajo debe ser `complete` y `action` debe ser `access`. De lo contrario, este campo está ausente. |
| `regulation` | Marco normativo en el que se está procesando la solicitud de privacidad, como `gdpr`, `ccpa`, `lgpd_bra`, `pdpa_tha`, etc. |

{style="table-layout:auto"}

## Recuperar información de acceso del cliente {#retrieve-access-data}

Para obtener la &quot;información de acceso&quot; generada en respuesta a la consulta del interesado, realice una solicitud de GET al extremo `/jobs/{JOB_ID}/content`. La respuesta es un archivo zip (*.zip) que contiene una carpeta con subcarpetas para cada producto que contiene datos del interesado.

>[!TIP]
>
>Necesita un ID de trabajo específico para realizar esta solicitud. Si necesita recuperar el id. de trabajo específico, primero realice una solicitud de GET al extremo `/jobs` y use parámetros de consulta adicionales para filtrar los resultados. Encontrará información detallada, incluidos los parámetros de consulta permitidos, en la [guía de extremo de trabajos de privacidad](./privacy-jobs.md).

**Formato de API**

```http
GET /jobs/{JOB_ID}/content
```

**Solicitud**

La siguiente solicitud devuelve la &quot;información de acceso&quot; para el ID de trabajo proporcionado en la solicitud.

```shell
curl -X GET \
  https://platform.adobe.io/data/core/privacy/jobs/32d429b1-f7f4-11ee-a365-574bcf5a525d/content \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'Accept: application/json`
```

**Respuesta**

La respuesta es un archivo zip (*.zip). La información generalmente se devuelve en formato JSON, aunque esto no se puede garantizar. Los datos extraídos se pueden devolver en cualquier formato.

