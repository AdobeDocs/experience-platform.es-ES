---
keywords: Experience Platform;api de destino;activación ad hoc;activar segmentos ad hoc
solution: Experience Platform
title: Activar segmentos de audiencia en destinos por lotes mediante la API de activación ad hoc
description: Este artículo ilustra el flujo de trabajo completo para activar segmentos de audiencia mediante la API de activación ad hoc, incluidos los trabajos de segmentación que se realizan antes de la activación.
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 8d67d89db6a8c179935b4fe709f91279860d464e
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 2%

---

# Activar segmentos de audiencia según demanda en destinos por lotes mediante la API de activación ad hoc

>[!IMPORTANT]
>
>Después de completar la fase beta, la variable [!DNL ad-hoc activation API] ahora está disponible de forma general (GA) para todos los clientes Experience Platform. En la versión GA, la API se ha actualizado a la versión 2. Paso 4 ([Obtenga el último ID de trabajo de exportación de segmentos](#segment-export-id)) ya no es obligatorio, ya que la API ya no requiere el ID de exportación.
>
>Consulte [Ejecutar el trabajo de activación ad hoc](#activation-job) más abajo en este tutorial para obtener más información.

## Información general {#overview}

La API de activación ad hoc permite a los especialistas en marketing activar mediante programación segmentos de audiencia en destinos de forma rápida y eficaz en situaciones en las que se requiera una activación inmediata.

El diagrama siguiente ilustra el flujo de trabajo completo para activar segmentos mediante la API de activación ad hoc, incluidos los trabajos de segmentación que se realizan en Platform cada 24 horas.

![activación ad hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>La activación de audiencias ad-hoc solo es compatible con [destinos basados en archivos por lotes](../destination-types.md#file-based).

## Casos de uso {#use-cases}

### Ventas o promociones de Flashes

Un minorista en línea está preparando una venta flash limitada y quiere notificar a los clientes con un breve aviso. A través de la API de activación ad hoc del Experience Platform, el equipo de marketing puede exportar segmentos bajo demanda y enviar rápidamente correos electrónicos promocionales a la base de clientes.

### Eventos actuales o noticias de último minuto

Un hotel espera que el tiempo sea inclemente en los próximos días, y el equipo quiere informar a los clientes rápidamente, para que puedan planear en consecuencia. El equipo de marketing puede utilizar la API de activación ad hoc de Experience Platform para exportar segmentos bajo demanda y notificar a los clientes.

### Pruebas de integración

Los administradores de TI pueden utilizar la API de activación ad hoc del Experience Platform para exportar segmentos bajo demanda, de modo que puedan probar su integración personalizada con Adobe Experience Platform y asegurarse de que todo funciona correctamente.

## Límites de protección  {#guardrails}

Tenga en cuenta las siguientes limitaciones al utilizar la API de activación ad hoc.

* Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 segmentos. Si se intentan activar más de 80 segmentos por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones.
* Los trabajos de activación específicos no se pueden ejecutar en paralelo con los programados [trabajos de exportación de segmentos](../../segmentation/api/export-jobs.md). Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que el trabajo de exportación de segmentos programado haya finalizado. Consulte [control de flujo de datos de destino](../../dataflows/ui/monitor-destinations.md) para obtener información sobre cómo monitorizar el estado de los flujos de activación. Por ejemplo, si el flujo de datos de activación muestra un **[!UICONTROL Procesamiento]** espera a que finalice antes de ejecutar el trabajo de activación ad hoc.
* No ejecute más de un trabajo de activación ad hoc concurrente por segmento.

## Consideraciones sobre la segmentación {#segmentation-considerations}

Adobe Experience Platform ejecuta trabajos de segmentación programados una vez cada 24 horas. La API de activación ad hoc se ejecuta en función de los resultados de segmentación más recientes.

## Paso 1: Requisitos previos {#prerequisites}

Antes de realizar llamadas a las API de Adobe Experience Platform, asegúrese de cumplir los siguientes requisitos previos:

* Tiene una cuenta de organización de IMS con acceso a Adobe Experience Platform.
* Su cuenta de Experience Platform tiene la variable `developer` y `user` funciones habilitadas para el perfil de producto de la API de Adobe Experience Platform. Póngase en contacto con su [Admin Console](../../access-control/home.md) para habilitar estas funciones en su cuenta.
* Tiene un Adobe ID. Si no tiene un Adobe ID, vaya a la sección [Consola de Adobe Developer](https://developer.adobe.com/console) y cree una cuenta nueva.

## Paso 2: Recopilar credenciales {#credentials}

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Los recursos del Experience Platform se pueden aislar en entornos limitados virtuales específicos. En las solicitudes a las API de plataforma, puede especificar el nombre y el ID del simulador de pruebas en el que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en el Experience Platform, consulte la [documentación general de entorno limitado](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Paso 3: Crear flujo de activación en la interfaz de usuario de Platform {#activation-flow}

Para poder activar segmentos a través de la API de activación ad hoc, primero debe tener configurado un flujo de activación en la interfaz de usuario de Platform para el destino elegido.

Esto incluye entrar en el flujo de trabajo de activación, seleccionar los segmentos, configurar una programación y activarlos. Puede utilizar la interfaz de usuario o la API para crear un flujo de activación:

* [Utilice la interfaz de usuario de Platform para crear un flujo de activación para los destinos de exportación de perfiles en lote](../ui/activate-batch-profile-destinations.md)
* [Utilice la API de servicio de flujo para conectarse a destinos de exportación de perfiles en lote y activar datos](../api/connect-activate-batch-destinations.md)

## Paso 4: Obtenga el último ID de trabajo de exportación de segmentos (no obligatorio en la versión 2) {#segment-export-id}

>[!IMPORTANT]
>
>En la versión 2 de la API de activación ad hoc, no es necesario obtener el ID de trabajo de exportación de segmentos más reciente. Puede omitir este paso y continuar con el siguiente.

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

>[!IMPORTANT]
>
>Tenga en cuenta la siguiente restricción de una sola vez: Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que hayan transcurrido al menos 20 minutos desde el momento en que se activó el segmento por primera vez según la programación que configuró [Paso 3: Creación del flujo de activación en la interfaz de usuario de Platform](#activation-flow).

Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que el trabajo de exportación de segmentos programado para sus segmentos haya finalizado. Consulte [control de flujo de datos de destino](../../dataflows/ui/monitor-destinations.md) para obtener información sobre cómo monitorizar el estado de los flujos de activación. Por ejemplo, si el flujo de datos de activación muestra un **[!UICONTROL Procesamiento]** espera a que finalice antes de ejecutar el trabajo de activación ad hoc.

Una vez completado el trabajo de exportación de segmentos, puede almacenar en déclencheur la activación.

>[!NOTE]
>
>Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 segmentos. Si se intentan activar más de 80 segmentos por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones.

### Solicitud {#request}

>[!IMPORTANT]
>
>Es obligatorio incluir el `Accept: application/vnd.adobe.adhoc.activation+json; version=2` en la solicitud para utilizar la versión 2 de la API de activación ad hoc.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| Propiedad | Descripción |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | ID de las instancias de destino en las que desea activar segmentos. Puede obtener estos ID desde la interfaz de usuario de Platform, navegando hasta **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y haciendo clic en la fila de destino que desee para que aparezca el ID de destino en el carril derecho. Para obtener más información, lea la [documentación del espacio de trabajo de destinos](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | ID de los segmentos que desea activar en el destino seleccionado. |

{style=&quot;table-layout:auto&quot;}

### Solicitud con ID de exportación (pendiente de finalización) {#request-deprecated}

>[!IMPORTANT]
>
>**Tipo de solicitud obsoleta**. Este tipo de ejemplo describe el tipo de solicitud para la versión 1 de la API. En la versión 2 de la API de activación ad hoc, no es necesario incluir el ID de trabajo de exportación de segmentos más reciente.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | ID de las instancias de destino en las que desea activar segmentos. Puede obtener estos ID desde la interfaz de usuario de Platform, navegando hasta **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y haciendo clic en la fila de destino que desee para que aparezca el ID de destino en el carril derecho. Para obtener más información, lea la [documentación del espacio de trabajo de destinos](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | ID de los segmentos que desea activar en el destino seleccionado. |
| <ul><li>`exportId1`</li></ul> | El ID devuelto en la respuesta del [exportación de segmentos](../../segmentation/api/export-jobs.md#retrieve-list) trabajo. Consulte [Paso 4: Obtenga el último ID de trabajo de exportación de segmentos](#segment-export-id) para obtener instrucciones sobre cómo encontrar este ID. |

{style=&quot;table-layout:auto&quot;}

### Respuesta {#response}

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
| `order` | ID del destino en el que se activó el segmento. |
| `statusURL` | La URL de estado del flujo de activación. Puede realizar un seguimiento del progreso del flujo mediante la [API del servicio de flujo](../../sources/tutorials/api/monitor.md). |

{style=&quot;table-layout:auto&quot;}

## Gestión de errores de API {#api-error-handling}

Los extremos de la API del Destination SDK siguen los principios generales del mensaje de error de la API del Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores en el encabezado de la solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

### Códigos de error de API y mensajes específicos de la API de activación ad hoc {#specific-error-messages}

Al utilizar la API de activación ad-hoc, puede encontrar mensajes de error específicos de este extremo de API. Revise la tabla para comprender cómo abordarlos cuando aparecen.

| Mensaje de error | Resolución |
|---------|----------|
| Ejecutar ya en curso para el segmento `segment ID` para pedido `dataflow ID` con id de ejecución `flow run ID` | Este mensaje de error indica que un flujo de activación ad hoc está actualmente en curso para un segmento. Espere a que finalice el trabajo antes de activar de nuevo el trabajo de activación. |
| Segmentos `<segment name>` no forman parte de este flujo de datos ni están fuera del intervalo de programación. | Este mensaje de error indica que los segmentos que ha seleccionado para activar no están asignados al flujo de datos o que la programación de activación configurada para los segmentos ha caducado o aún no se ha iniciado. Compruebe si el segmento está asignado al flujo de datos y compruebe que la programación de activación de segmentos se superponga con la fecha actual. |

## Información relacionada {#related-information}

* [Conectarse a destinos por lotes y activar datos mediante la API de servicio de flujo](/help/destinations/api/connect-activate-batch-destinations.md)