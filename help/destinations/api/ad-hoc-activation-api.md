---
keywords: Experience Platform;api de destino;activación ad hoc;activar segmentos ad hoc
solution: Experience Platform
title: (Beta) Activar segmentos de audiencia en destinos por lotes mediante la API de activación ad hoc
description: Este artículo ilustra el flujo de trabajo completo para activar segmentos de audiencia mediante la API de activación ad hoc, incluidos los trabajos de segmentación que se realizan antes de la activación.
topic-legacy: tutorial
type: Tutorial
source-git-commit: 749fa5dc1e8291382408d9b1a0391c4c7f2b2a46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 2%

---


# (Beta) Activar segmentos de audiencia en destinos por lotes mediante la API de activación ad hoc

>[!IMPORTANT]
>
>La variable [!DNL ad-hoc activation API] en Platform se encuentra en versión beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

The ad-hoc activation API allows marketers to programmatically activate audience segments to destinations, in a fast and efficient manner, for situations where immediate activation is required.

The diagram below illustrates the end-to-end workflow for activating segments via the ad-hoc activation API, including the segmentation jobs that take place in Platform every 24 hours.

![ad-hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>La activación de audiencias ad-hoc solo es compatible con [destinos basados en archivos por lotes](../destination-types.md#file-based).

## Casos de uso {#use-cases}

### Ventas o promociones de Flashes

Un minorista en línea está preparando una venta flash limitada y quiere notificar a los clientes con un breve aviso. A través de la API de activación ad hoc del Experience Platform, el equipo de marketing puede exportar segmentos bajo demanda y enviar rápidamente correos electrónicos promocionales a la base de clientes.


### Current events or breaking news

A hotel expects inclement weather over the following days, and the team wants to inform the arriving guests quickly, so they can plan accordingly. The marketing team can use the Experience Platform ad-hoc activation API to export segments on-demand, and notify the guests.

### Pruebas de integración

Los administradores de TI pueden utilizar la API de activación ad hoc del Experience Platform para exportar segmentos bajo demanda, de modo que puedan probar su integración personalizada con Adobe Experience Platform y asegurarse de que todo funciona correctamente.


## Seguridad {#guardrails}

Tenga en cuenta las siguientes limitaciones al utilizar la API de activación ad hoc.

* Actualmente, cada trabajo de activación ad-hoc puede activar hasta 20 segmentos. Attempting to activate more than 20 segments per job will cause the job to fail. This behavior is subject to change in future releases.
* Ad-hoc activation jobs cannot run in parallel with scheduled [segment export jobs](../../segmentation/api/export-jobs.md). Before running an ad-hoc activation job, make sure the scheduled segment export job has finished. See [destination dataflow monitoring](../../dataflows/ui/monitor-destinations.md) for information on how to monitor the status of activation flows. Por ejemplo, si el flujo de datos de activación muestra un **[!UICONTROL Procesamiento]** espera a que finalice antes de ejecutar el trabajo de activación ad hoc.
* No ejecute más de un trabajo de activación ad hoc concurrente por segmento.

## Consideraciones sobre la segmentación {#segmentation-considerations}

Adobe Experience Platform ejecuta trabajos de segmentación programados una vez cada 24 horas. The ad-hoc activation API runs based on the latest segmentation results.

## Paso 1: Requisitos previos {#prerequisites}

Antes de realizar llamadas a las API de Adobe Experience Platform, asegúrese de cumplir los siguientes requisitos previos:

* Tiene una cuenta de organización de IMS con acceso a Adobe Experience Platform.
* Su cuenta de Experience Platform tiene la variable `developer` y `user` funciones habilitadas para el perfil de producto de la API de Adobe Experience Platform. Contact your [Admin Console](../../access-control/home.md) administrator to enable these roles for your account.
* You have an Adobe ID. Si no tiene un Adobe ID, vaya a la sección [Adobe Developer Console](https://developer.adobe.com/console) y cree una cuenta nueva.

## Paso 2: Recopilar credenciales {#credentials}

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Los recursos del Experience Platform se pueden aislar en entornos limitados virtuales específicos. En las solicitudes a las API de plataforma, puede especificar el nombre y el ID del simulador de pruebas en el que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en el Experience Platform, consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Paso 3: Crear flujo de activación en la interfaz de usuario de Platform {#activation-flow}

Para poder activar segmentos a través de la API de activación ad hoc, primero debe tener configurado un flujo de activación en la interfaz de usuario de Platform para el destino elegido.

Esto incluye entrar en el flujo de trabajo de activación, seleccionar los segmentos, configurar una programación y activarlos.

Consulte el siguiente tutorial para obtener instrucciones detalladas sobre cómo configurar un flujo de activación para los destinos de lote: [Activar datos de audiencia en destinos de exportación de perfiles en lote](../ui/activate-batch-profile-destinations.md).

## Paso 4: Obtenga el último ID de trabajo de exportación de segmentos {#segment-export-id}

After you configure an activation flow for your batch destination, scheduled segmentation jobs start running automatically every 24 hours.

Para poder ejecutar el trabajo de activación ad-hoc, debe obtener el ID del trabajo de exportación de segmentos más reciente. You must pass this ID in the ad-hoc activation job request.

Follow the instructions described [here](../../segmentation/api/export-jobs.md#retrieve-list) to retrieve a list of all the segment export jobs.

En la respuesta, busque el primer registro que incluye la propiedad schema a continuación.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

El ID del trabajo de exportación de segmentos se encuentra en la variable `id` como se muestra a continuación.

![ID de trabajo de exportación de segmentos](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Paso 5: Ejecutar el trabajo de activación ad hoc {#activation-job}

Adobe Experience Platform ejecuta trabajos de segmentación programados una vez cada 24 horas. La API de activación ad hoc se ejecuta en función de los resultados de segmentación más recientes.

Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que el trabajo de exportación de segmentos programado para sus segmentos haya finalizado. Consulte [control de flujo de datos de destino](../../dataflows/ui/monitor-destinations.md) para obtener información sobre cómo monitorizar el estado de los flujos de activación. Por ejemplo, si el flujo de datos de activación muestra un **[!UICONTROL Procesamiento]** espera a que finalice antes de ejecutar el trabajo de activación ad hoc.

Una vez completado el trabajo de exportación de segmentos, puede almacenar en déclencheur la activación.

>[!NOTE]
>
>Actualmente, cada trabajo de activación ad-hoc puede activar hasta 20 segmentos. Si se intentan activar más de 20 segmentos por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones.

### Solicitud

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | The IDs of the destination instances to which you want to activate segments. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | The IDs of the segments that you want to activate to the selected destination. |
| <ul><li>`exportId1`</li></ul> | El ID devuelto en la respuesta del [exportación de segmentos](../../segmentation/api/export-jobs.md#retrieve-list) trabajo. Consulte [Paso 4: Obtenga el último ID de trabajo de exportación de segmentos](#segment-export-id) para obtener instrucciones sobre cómo encontrar este ID. |

### Respuesta

Una respuesta correcta devuelve el estado HTTP 200.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `segment` | ID del segmento activado. |
| `order` | The ID of the destination to which the segment was activated. |
| `statusURL` | La URL de estado del flujo de activación. You can track the flow progress using the [Flow Service API](../../sources/tutorials/api/monitor.md). |


## API error handling

Destination SDK API endpoints follow the general Experience Platform API error message principles. Refer to [API status codes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) and [request header errors](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in the Platform troubleshooting guide.
