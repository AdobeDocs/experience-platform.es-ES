---
description: En esta página se explica cómo utilizar el extremo de la API /testing/destinationInstance para probar si el destino basado en archivos está configurado correctamente y para comprobar la integridad de los flujos de datos al destino configurado.
title: Prueba del destino basado en archivos con perfiles de muestra
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 2%

---

# Prueba del destino basado en archivos con perfiles de muestra

## Información general {#overview}

En esta página se explica cómo usar el extremo de API `/testing/destinationInstance` para probar si el destino basado en archivos está configurado correctamente y comprobar la integridad de los flujos de datos al destino configurado.

Puede realizar solicitudes al extremo de prueba con o sin agregar [perfiles de muestra](file-based-sample-profile-generation-api.md) a la llamada. Si no envía ningún perfil en la solicitud, la API genera un perfil de muestra automáticamente y lo añade a la solicitud.

Los perfiles de muestra generados automáticamente contienen datos genéricos. Si desea probar el destino con datos de perfil personalizados e intuitivos, use la [API de generación de perfiles de muestra](file-based-sample-profile-generation-api.md) para generar un perfil de muestra, luego personalice su respuesta e inclúyala en la solicitud al extremo `/testing/destinationInstance`.

## Introducción {#getting-started}

Antes de continuar, revisa la [guía de introducción](../../getting-started.md) para obtener información importante que necesitas conocer para poder realizar llamadas a la API correctamente, incluyendo cómo obtener el permiso de creación de destino requerido y los encabezados requeridos.

## Requisitos previos {#prerequisites}

Antes de usar el extremo `/testing/destinationInstance`, asegúrese de cumplir las siguientes condiciones:

* Ya tiene un destino basado en archivos creado mediante Destination SDK y puede verlo en su [catálogo de destinos](../../../ui/destinations-workspace.md).
* Ha creado al menos un flujo de activación para su destino en la interfaz de usuario de Experience Platform.
* Para realizar correctamente la solicitud de API, necesita el ID de instancia de destino correspondiente a la instancia de destino que va a probar. Obtenga el ID de instancia de destino que debe utilizar en la llamada de API desde la dirección URL cuando busque una conexión con su destino en la interfaz de usuario de Experience Platform.

  ![Imagen de interfaz de usuario que muestra cómo obtener el identificador de instancia de destino de la dirección URL.](../../assets/testing-api/get-destination-instance-id.png)
* *Opcional*: Si desea probar la configuración de destino con un perfil de muestra agregado a la llamada de API, use el extremo [/sample-profiles](file-based-sample-profile-generation-api.md) para generar un perfil de muestra basado en el esquema de origen existente. Si no proporciona un perfil de muestra, la API generará uno y lo devolverá en la respuesta.

## Pruebe la configuración de destino sin añadir perfiles a la llamada {#test-without-adding-profiles}

**Formato de API**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Solicitud**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Parámetros de ruta | Descripción |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | El ID de la instancia de destino para la que está generando perfiles de muestra. Consulte la sección [requisitos previos](#prerequisites) para obtener más información sobre cómo obtener este ID. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con la carga útil de respuesta.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
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
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `activations` | Devuelve el ID de audiencia y el ID de ejecución de flujo para cada audiencia activada. El número de entradas de activación (y archivos generados asociados) es igual al número de audiencias asignadas en la instancia de destino. <br><br> Ejemplo: Si asignó dos audiencias a la instancia de destino, la matriz `activations` contendrá dos entradas. Cada audiencia activada corresponde a un archivo exportado. |
| `results` | Devuelve el identificador de instancia de destino y los identificadores de ejecución de flujo que puede usar para llamar a la API de [resultados](file-based-destination-results-api.md), con el fin de probar aún más la integración. |
| `inputProfiles` | Devuelve los perfiles de muestra generados automáticamente por la API. |

{style="table-layout:auto"}

## Pruebe la configuración de destino con perfiles añadidos a la llamada {#test-with-added-profiles}

Para probar el destino con datos de perfil personalizados y más intuitivos, puede personalizar la respuesta obtenida del extremo [/sample-profiles](file-based-sample-profile-generation-api.md) con los valores de su elección e incluir el perfil personalizado en la solicitud al extremo `/testing/destinationInstance`.

**Formato de API**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Solicitud**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
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
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Parámetro | Descripción |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | El ID de instancia de destino del destino que está probando.  El ID de la instancia de destino para la que está generando perfiles de muestra. Consulte la sección [requisitos previos](#prerequisites) para obtener más información sobre cómo obtener este ID. |
| `profiles` | Matriz que puede incluir uno o varios perfiles. Use [extremo de API de perfil de muestra](file-based-sample-profile-generation-api.md) para generar perfiles que se usarán en esta llamada de API. |

**Respuesta**

Una respuesta correcta devuelve el estado HTTP 200 junto con la carga útil de respuesta.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
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
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `activations` | Devuelve el ID de audiencia y el ID de ejecución de flujo para cada audiencia activada. El número de entradas de activación (y archivos generados asociados) es igual al número de audiencias asignadas en la instancia de destino. <br><br> Ejemplo: Si asignó dos audiencias a la instancia de destino, la matriz `activations` contendrá dos entradas. Cada audiencia activada corresponde a un archivo exportado. |
| `results` | Devuelve el identificador de instancia de destino y los identificadores de ejecución de flujo que puede usar para llamar a la API de [resultados](file-based-destination-results-api.md), con el fin de probar aún más la integración. |
| `inputProfiles` | Devuelve los perfiles de ejemplo personalizados que ha pasado en la solicitud de API. |

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Experience Platform.

## Pasos siguientes

Después de leer este documento, ahora sabe cómo probar la configuración de destino basada en archivos.

Si ha recibido una respuesta de API válida, el destino funciona correctamente. Si desea ver información más detallada sobre el flujo de activación, puede usar la propiedad `results` de la respuesta a [ver resultados detallados de la activación](file-based-destination-results-api.md).

Si estás creando un destino público, ahora puedes [enviar tu configuración de destino](../../guides/submit-destination.md) a Adobe para que la revisen.
