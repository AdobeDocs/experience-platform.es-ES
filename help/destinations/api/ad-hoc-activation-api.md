---
keywords: Experience Platform;api de destino;activación ad hoc;activar segmentos ad hoc
solution: Experience Platform
title: (Beta) Activar segmentos de audiencia mediante la API de activación ad hoc del Experience Platform
description: Este artículo ilustra el flujo de trabajo completo para activar segmentos mediante la API de activación ad hoc, incluidos los trabajos de segmentación que se realizan antes de la activación.
topic-legacy: tutorial
type: Tutorial
source-git-commit: d5b383ec4e9f6e2f05a0e5834e3998789a67ce32
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 2%

---


# (Beta) Activar segmentos de audiencia mediante la API de activación ad hoc del Experience Platform

>[!IMPORTANT]
>
>La variable [!DNL ad-hoc activation API] en Platform se encuentra en versión beta. La documentación y las funciones están sujetas a cambios.

## Información general {#overview}

La API de activación ad hoc permite a los especialistas en marketing activar mediante programación segmentos de audiencia en destinos de forma rápida y eficaz en situaciones en las que se requiera una activación inmediata.

El diagrama siguiente ilustra el flujo de trabajo completo para activar segmentos mediante la API de activación ad hoc, incluidos los trabajos de segmentación que se realizan en Platform cada 24 horas.

![activación ad hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>La activación de audiencias ad-hoc solo es compatible con [destinos basados en archivos por lotes](../destination-types.md#file-based).

## Casos de uso {#use-cases}

### Ventas o promociones de Flashes

Un minorista en línea está preparando una venta flash limitada y quiere notificar a los clientes con un breve aviso. A través de la API de activación ad-hoc del Experience Platform, el equipo de marketing puede exportar segmentos de audiencia bajo demanda y enviar rápidamente correos electrónicos promocionales a la base de clientes.


### Eventos actuales o noticias de último minuto

Un hotel espera que el tiempo sea inclemente en los próximos días, y el equipo quiere informar a los clientes rápidamente, para que puedan planear en consecuencia. El equipo de marketing puede utilizar la API de activación ad hoc de Experience Platform para exportar segmentos de audiencia bajo demanda y notificarlos a los clientes.

### Pruebas de integración

Los administradores de TI pueden utilizar la API de activación ad hoc del Experience Platform para exportar segmentos de audiencia bajo demanda, de modo que puedan probar su integración personalizada con Adobe Experience Platform y asegurarse de que todo funciona correctamente.


## Seguridad {#guardrails}

Tenga en cuenta las siguientes limitaciones al utilizar la API de activación ad hoc.

* Cada trabajo de activación ad hoc puede activar hasta 20 segmentos. Si se intentan activar más de 20 segmentos por trabajo, el trabajo fallará.
* Los trabajos de activación específicos no se pueden ejecutar en paralelo con los programados [trabajos de exportación de segmentos](../../segmentation/api/export-jobs.md). Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que el trabajo de exportación de segmentos programado haya finalizado. Consulte [control de flujo de datos de destino](../../dataflows/ui/monitor-destinations.md) para obtener información sobre cómo monitorizar el estado de los flujos de activación. Por ejemplo, si el flujo de datos de activación muestra un **[!UICONTROL Procesamiento]** espera a que finalice antes de ejecutar el trabajo de activación ad hoc.
* No ejecute más de un trabajo de activación ad hoc concurrente por segmento.

## Consideraciones sobre la segmentación {#segmentation-considerations}

Adobe Experience Platform ejecuta trabajos de segmentación programados una vez cada 24 horas. La API de activación ad hoc se ejecuta en función de los resultados de segmentación más recientes.

## Paso 1: Requisitos previos {#prerequisites}

Antes de realizar llamadas a las API de Adobe Experience Platform, asegúrese de cumplir los siguientes requisitos previos:

* Tiene una cuenta de organización de IMS con acceso a Adobe Experience Platform.
* Su cuenta de Experience Platform tiene la variable `developer` y `user` funciones habilitadas para el perfil de producto de la API de Adobe Experience Platform. Póngase en contacto con su [Admin Console](../../access-control/home.md) para habilitar estas funciones en su cuenta.
* Tiene un Adobe ID. Si no tiene un Adobe ID, vaya a la sección [Adobe Developer Console](https://developer.adobe.com/console) y cree una cuenta nueva.

## Paso 2: Recopilar credenciales {#credentials}

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
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

Después de configurar el flujo de activación para el destino por lotes, los trabajos de segmentación programados empiezan a ejecutarse automáticamente cada 24 horas.

Para poder ejecutar el trabajo de activación ad-hoc, debe obtener el ID del trabajo de exportación de segmentos más reciente. Debe pasar este ID en la solicitud de trabajo de activación ad hoc.

Siga las instrucciones descritas [here](../../segmentation/api/export-jobs.md#retrieve-list) para recuperar una lista de todos los trabajos de exportación de segmentos.

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

>[!WARNING]
>
>Puede activar un máximo de 50 segmentos por cada trabajo de activación ad-hoc. Si intenta activar más segmentos, el trabajo fallará.

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
   "exportId":[
      "exportId1"
   ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Los ID de las instancias de destino en las que desea activar los segmentos de audiencia. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | ID de los segmentos de audiencia que desea activar en el destino seleccionado. |
| <ul><li>`exportId1`</li></ul> | El ID devuelto en la respuesta del [exportación de segmentos](../../segmentation/api/export-jobs.md#retrieve-list) trabajo. Consulte [Paso 4: Obtenga el último ID de trabajo de exportación de segmentos](#segment-export-id) para obtener instrucciones sobre cómo encontrar este ID. |

### Respuesta

Una respuesta correcta devuelve el estado HTTP 200.

```shell
{
   "code":"DEST-ADH-200",
   "message":"Adhoc run triggered successfully",
   "statusURLs":[
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-1",
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-2"
   ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `code` | El código de respuesta de API. Una llamada correcta devuelve `DEST-ADH-200` (código de estado 200), mientras que devuelve un formato incorrecto `DEST-ADH-400` (código de estado 400). |
| `message` | El mensaje de error o éxito devuelto por la API. |
| `statusURLs` | La URL de estado del flujo de activación. Puede realizar un seguimiento del progreso del flujo mediante la [API del servicio de flujo](../../sources/tutorials/api/monitor.md). |


## Gestión de errores de API

Los extremos de la API del SDK de destino siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) y [errores en el encabezado de la solicitud](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) en la guía de solución de problemas de Platform.
