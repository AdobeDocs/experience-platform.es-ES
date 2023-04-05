---
description: En esta página se explica cómo utilizar el extremo de la API /sample-profiles del Destination SDK para generar perfiles de muestra basados en un esquema de origen. Puede utilizar estos perfiles de ejemplo para probar la configuración de destino basada en archivos.
title: Generación de perfiles de muestra basados en un esquema de origen
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 3%

---

# Generación de perfiles de muestra basados en un esquema de origen

## Información general {#overview}

El primer paso para probar el destino basado en archivos es usar la variable `/sample-profiles` para generar un perfil de muestra basado en el esquema de origen existente.

Los perfiles de muestra pueden ayudarle a comprender la estructura JSON de un perfil. Además, le proporcionan un valor predeterminado que puede personalizar con sus propios datos de perfil para realizar más pruebas de destino.

## Primeros pasos {#getting-started}

Antes de continuar, revise la [guía de introducción](./getting-started.md) para obtener información importante que debe conocer para realizar llamadas correctamente a la API de , incluido cómo obtener el permiso de creación de destino requerido y los encabezados necesarios.

## Requisitos previos {#prerequisites}

Antes de usar la variable `/sample-profiles` , asegúrese de cumplir las siguientes condiciones:

* Tiene un destino basado en archivos creado mediante el Destination SDK y puede verlo en su [catálogo de destinos](../ui/destinations-workspace.md).
* Ha creado al menos un flujo de activación para el destino en la interfaz de usuario del Experience Platform. La variable `/sample-profiles` el extremo crea los perfiles en función del esquema de origen definido en el flujo de activación. Consulte la [tutorial de activación](../ui/activate-batch-profile-destinations.md) para aprender a crear un flujo de activación.
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debería usar en la llamada de API, desde la dirección URL, al examinar una conexión con su destino en la interfaz de usuario de Platform.

   ![Imagen de la interfaz de usuario que muestra cómo obtener el ID de instancia de destino desde la dirección URL.](assets/get-destination-instance-id.png)

## Generación de perfiles de muestra para pruebas de destino {#generate-sample-profiles}

Puede generar perfiles de ejemplo basados en el esquema de origen realizando una solicitud de GET al `/sample-profiles` extremo con el ID de instancia de destino del destino que desea probar.

**Formato de API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parámetros de consulta | Descripción |
| -------- | ----------- |
| `destinationInstanceId` | El ID de la instancia de destino para la que está generando perfiles de muestra. Consulte la [requisitos previos](#prerequisites) para obtener más información sobre cómo obtener este ID. |
| `count` | *Opcional*. Número de perfiles de muestra que desea generar. El parámetro puede tomar valores entre `1 - 1000`. Si no se define esta propiedad, la API genera un único perfil de muestra. |

**Solicitud**

La siguiente solicitud genera un perfil de muestra basado en el esquema de origen definido en la instancia de destino con el correspondiente `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el número especificado de perfiles de muestra, con pertenencia a segmentos, identidades y atributos de perfil que corresponden al esquema XDM de origen.

>[!NOTE]
>
> La respuesta solo devuelve la pertenencia a segmentos, las identidades y los atributos de perfil que se utilizan en la instancia de destino. Incluso si el esquema de origen tiene otros campos, estos se ignoran.

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![Imagen que muestra la asignación de la interfaz de usuario a los campos de la respuesta de API.](assets/sample-api-response-mapping.png)

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentMembership` | Un objeto map que describe las suscripciones a segmentos del individuo. Para obtener más información, consulte `segmentMembership`, leer [Detalles de pertenencia a segmentos](../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Marca de fecha y hora de la última vez que este perfil cumplía los requisitos para el segmento. |
| `status` | Campo de cadena que indica si la pertenencia al segmento se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`realized`: El perfil forma parte del segmento.</li><li>`exited`: El perfil sale del segmento como parte de la solicitud actual.</li></ul> |
| `identityMap` | Campo de tipo asignación que describe los distintos valores de identidad de un individuo, junto con sus áreas de nombres asociadas. Para obtener más información, consulte `identityMap`, consulte [base de la composición del esquema](../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## Gestión de errores de API {#api-error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo generar perfiles de muestra basados en el esquema de origen configurado en el destino [flujo de activación](../ui/activate-batch-profile-destinations.md).

Ahora puede personalizar estos perfiles o utilizarlos como la API los devuelve para [probar la configuración de destino basada en archivos](file-based-destination-testing-api.md).
