---
description: En esta página se explica cómo utilizar el extremo de API /sample-profiles de Destination SDK para generar perfiles de muestra basados en un esquema de origen. Puede utilizar estos perfiles de muestra para probar la configuración de destino basada en archivos.
title: Generar perfiles de muestra basados en un esquema de origen
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 2%

---


# Generar perfiles de muestra basados en un esquema de origen

El primer paso para probar el destino basado en archivos es usar el extremo `/sample-profiles` para generar un perfil de muestra basado en el esquema de origen existente.

Los perfiles de muestra pueden ayudarle a comprender la estructura JSON de un perfil. Además, le proporcionan un valor predeterminado que puede personalizar con sus propios datos de perfil para realizar más pruebas de destino.

## Introducción {#getting-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Requisitos previos {#prerequisites}

Antes de usar el extremo `/sample-profiles`, asegúrese de cumplir las siguientes condiciones:

* Ya tiene un destino basado en archivos creado mediante Destination SDK y puede verlo en su [catálogo de destinos](../../../ui/destinations-workspace.md).
* Ha creado al menos un flujo de activación para su destino en la interfaz de usuario de Experience Platform. El extremo `/sample-profiles` crea los perfiles en función del esquema de origen definido en el flujo de activación. Consulte el [tutorial de activación](../../../ui/activate-batch-profile-destinations.md) para obtener información sobre cómo crear un flujo de activación.
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debe utilizar en la llamada de API desde la dirección URL cuando busque una conexión con su destino en la interfaz de usuario de Experience Platform.

  ![Imagen de interfaz de usuario que muestra cómo obtener el identificador de instancia de destino de la dirección URL.](../../assets/testing-api/get-destination-instance-id.png)

## Generar perfiles de muestra para las pruebas de destino {#generate-sample-profiles}

Puede generar perfiles de muestra basados en el esquema de origen realizando una petición GET al extremo `/sample-profiles` con el ID de instancia de destino del destino que desea probar.

**Formato de API**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| Parámetros de consulta | Descripción |
| -------- | ----------- |
| `destinationInstanceId` | El ID de la instancia de destino para la que está generando perfiles de muestra. Consulte la sección [requisitos previos](#prerequisites) para obtener más información sobre cómo obtener este ID. |
| `count` | *Opcional*. El número de perfiles de muestra que desea generar. El parámetro puede tomar valores entre `1 - 1000`. Si esta propiedad no está definida, la API genera un solo perfil de muestra. |

**Solicitud**

La siguiente solicitud genera un perfil de muestra basado en el esquema de origen definido en la instancia de destino con el `destinationInstanceId` correspondiente.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 con el número especificado de perfiles de muestra, con pertenencia a audiencia, identidades y atributos de perfil que corresponden al esquema XDM de origen.

>[!NOTE]
>
> La respuesta solo devuelve la pertenencia a audiencias, identidades y atributos de perfil que se utilizan en la instancia de destino. Aunque el esquema de origen tenga otros campos, estos se ignoran.

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

![Imagen que muestra la asignación de la interfaz de usuario a los campos de la respuesta de API.](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| Propiedad | Descripción |
| -------- | ----------- |
| `segmentMembership` | Un objeto map que describe las pertenencias de audiencia del individuo. Para obtener más información sobre `segmentMembership`, lea [Detalles de pertenencia a audiencias](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | Una marca de tiempo de la última vez que este perfil se clasificó para el segmento. |
| `status` | Campo de cadena que indica si el abono a audiencia se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`realized`: el perfil forma parte del segmento.</li><li>`exited`: el perfil está saliendo de la audiencia como parte de la solicitud actual.</li></ul> |
| `identityMap` | Campo de tipo mapa que describe los distintos valores de identidad de un individuo, junto con sus áreas de nombres asociadas. Para obtener más información sobre `identityMap`, vea [base de la composición del esquema](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo generar perfiles de muestra basados en el esquema de origen que configuró en su [flujo de activación](../../../ui/activate-batch-profile-destinations.md) de destino.

Ahora puede personalizar estos perfiles o usarlos a medida que la API los devuelva para [probar la configuración de destino basada en archivos](file-based-destination-testing-api.md).
