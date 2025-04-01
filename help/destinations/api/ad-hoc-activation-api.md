---
keywords: Experience Platform;api de destino;activación ad hoc;activar audiencias ad hoc
solution: Experience Platform
title: Activar audiencias en destinos por lotes mediante la API de activación ad hoc
description: Este artículo ilustra el flujo de trabajo completo para activar audiencias a través de la API de activación ad-hoc, incluidos los trabajos de segmentación que se realizan antes de la activación.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: f01a044d3d12ef457c6242a0b93acbfeeaf48588
workflow-type: tm+mt
source-wordcount: '1612'
ht-degree: 0%

---

# Activar audiencias bajo demanda en destinos por lotes mediante la API de activación ad hoc

>[!IMPORTANT]
>
>Después de completar la fase de Beta, [!DNL ad-hoc activation API] ahora está disponible de forma general (GA) para todos los clientes de Experience Platform. En la versión de GA, la API se ha actualizado a la versión 2. El paso 4 ([Obtener la última ID de trabajo de exportación de audiencia](#segment-export-id)) ya no es necesario, ya que la API ya no requiere la ID de exportación.
>
>Consulte [Ejecutar el trabajo de activación ad-hoc](#activation-job) más abajo en este tutorial para obtener más información.

## Información general {#overview}

La API de activación ad-hoc permite a los especialistas en marketing activar audiencias de audiencia a destinos mediante programación de forma rápida y eficaz en situaciones en las que se requiera la activación inmediata.

Utilice la API de activación ad-hoc para exportar archivos completos al sistema de recepción de archivos deseado. La activación de audiencias ad hoc solo es compatible con [destinos basados en archivos por lotes](../destination-types.md#file-based).

El diagrama siguiente ilustra el flujo de trabajo completo para activar audiencias a través de la API de activación ad-hoc, incluidos los trabajos de segmentación que se realizan en Platform cada 24 horas.

![activación-ad-hoc](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## Casos de uso {#use-cases}

### Ventas o promociones Flash

Un retailer en línea está preparando una venta flash limitada y quiere notificar a los clientes con un breve aviso. A través de la API de activación ad-hoc de Experience Platform, el equipo de marketing puede exportar audiencias bajo demanda y enviar rápidamente correos electrónicos promocionales a la base de clientes.

### Eventos actuales o noticias de última hora

Un hotel espera un tiempo inclemente en los próximos días, y el equipo quiere informar a los huéspedes que llegan rápidamente, para que puedan planificar en consecuencia. El equipo de marketing puede utilizar la API de activación ad-hoc de Experience Platform para exportar audiencias bajo demanda y notificar a los invitados.

### Pruebas de integración

Los administradores de TI pueden utilizar la API de activación ad hoc de Experience Platform para exportar audiencias bajo demanda, de modo que puedan probar su integración personalizada con Adobe Experience Platform y asegurarse de que todo funciona correctamente.

## Mecanismos de protección {#guardrails}

Tenga en cuenta las siguientes protecciones al utilizar la API de activación ad-hoc.

* Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 audiencias. Si se intentan activar más de 80 audiencias por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones.
* Los trabajos de activación específicos no se pueden ejecutar en paralelo con los [trabajos de exportación de audiencias](../../segmentation/api/export-jobs.md) programados. Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que el trabajo de exportación de audiencia programado haya finalizado. Consulte [supervisión del flujo de datos de destino](../../dataflows/ui/monitor-destinations.md) para obtener información sobre cómo supervisar el estado de los flujos de activación. Por ejemplo, si el flujo de datos de activación muestra el estado **[!UICONTROL Procesando]**, espere a que finalice antes de ejecutar el trabajo de activación ad-hoc.
* No ejecute más de un trabajo de activación ad hoc simultáneo por audiencia.

## Consideraciones de segmentación {#segmentation-considerations}

Adobe Experience Platform ejecuta trabajos de segmentación programados una vez cada 24 horas. La API de activación ad hoc se ejecuta en función de los resultados de segmentación más recientes.

## Paso 1: Requisitos previos {#prerequisites}

Para poder realizar llamadas a las API de Adobe Experience Platform, asegúrese de cumplir los siguientes requisitos previos:

* Tiene una cuenta de organización con acceso a Adobe Experience Platform.
* Su cuenta de Experience Platform tiene habilitados los roles `developer` y `user` para el perfil de producto de la API de Adobe Experience Platform. Póngase en contacto con su administrador de [Admin Console](../../access-control/home.md) para habilitar estos roles en su cuenta.
* Tiene un Adobe ID. Si no tienes un Adobe ID, ve a [Adobe Developer Console](https://developer.adobe.com/console) y crea una nueva cuenta.

## Paso 2: Recopilar credenciales {#credentials}

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](https://www.adobe.com/go/platform-api-authentication-en). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Los recursos de Experience Platform se pueden aislar para crear zonas protegidas virtuales específicas. En las solicitudes a las API de Platform, puede especificar el nombre y el ID de la zona protegida en la que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en Experience Platform, consulte la [documentación de información general sobre las zonas protegidas](../../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* Tipo de contenido: `application/json`

## Paso 3: Crear un flujo de activación en la interfaz de usuario de Platform {#activation-flow}

Para poder activar audiencias a través de la API de activación ad-hoc, primero debe tener configurado un flujo de activación en la interfaz de usuario de Platform para el destino elegido.

Esto incluye entrar en el flujo de trabajo de activación, seleccionar las audiencias, configurar una programación y activarlas. Puede utilizar la interfaz de usuario o la API de para crear un flujo de activación:

* [Utilice la interfaz de usuario de Platform para crear un flujo de activación para los destinos de exportación de perfiles por lotes](../ui/activate-batch-profile-destinations.md)
* [Utilice la API de Flow Service para conectarse a destinos de exportación de perfiles por lotes y activar datos](../api/connect-activate-batch-destinations.md)

## Paso 4: Obtener el ID de trabajo de exportación de audiencia más reciente (no obligatorio en la versión 2) {#segment-export-id}

>[!IMPORTANT]
>
>En la versión 2 de la API de activación ad-hoc, no es necesario obtener el ID de trabajo de exportación de audiencia más reciente. Puede omitir este paso y continuar con el siguiente.

Después de configurar un flujo de activación para el destino del lote, los trabajos de segmentación programados comienzan a ejecutarse automáticamente cada 24 horas.

Para poder ejecutar el trabajo de activación ad-hoc, debe obtener el ID del último trabajo de exportación de audiencias. Debe pasar este ID en la solicitud de trabajo de activación ad-hoc.

Siga las instrucciones descritas [aquí](../../segmentation/api/export-jobs.md#retrieve-list) para recuperar una lista de todos los trabajos de exportación de audiencias.

En la respuesta, busque el primer registro que incluya la propiedad de esquema a continuación.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

El identificador del trabajo de exportación de audiencias se encuentra en la propiedad `id`, como se muestra a continuación.

![ID de trabajo de exportación de audiencia](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Paso 5: Ejecutar el trabajo de activación ad-hoc {#activation-job}

Adobe Experience Platform ejecuta trabajos de segmentación programados una vez cada 24 horas. La API de activación ad hoc se ejecuta en función de los resultados de segmentación más recientes.

>[!IMPORTANT]
>
>Tenga en cuenta la siguiente restricción de una sola vez: antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que haya transcurrido al menos una hora desde el momento en que la audiencia se activó por primera vez según la programación establecida en [Paso 3: crear flujo de activación en la interfaz de usuario de Platform](#activation-flow).

Antes de ejecutar un trabajo de activación ad-hoc, asegúrese de que el trabajo de exportación de audiencias programado para sus audiencias haya finalizado. Consulte [supervisión del flujo de datos de destino](../../dataflows/ui/monitor-destinations.md) para obtener información sobre cómo supervisar el estado de los flujos de activación. Por ejemplo, si el flujo de datos de activación muestra el estado **[!UICONTROL Procesando]**, espere a que finalice antes de ejecutar el trabajo de activación ad-hoc para exportar un archivo completo.

Una vez completado el trabajo de exportación de audiencias, puede almacenar la activación en déclencheur.

>[!NOTE]
>
>Actualmente, cada trabajo de activación ad-hoc puede activar hasta 80 audiencias. Si se intentan activar más de 80 audiencias por trabajo, el trabajo fallará. Este comportamiento está sujeto a cambios en futuras versiones.

### Solicitud {#request}

>[!IMPORTANT]
>
>Es obligatorio incluir el encabezado `Accept: application/vnd.adobe.adhoc.activation+json; version=2` en su solicitud para utilizar la versión 2 de la API de activación ad-hoc.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Los ID de las instancias de destino en las que desea activar audiencias. Puede obtener estos identificadores desde la interfaz de usuario de Platform; para ello, vaya a la pestaña **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y haga clic en la fila de destino que desee para que aparezca el identificador de destino en el carril derecho. Para obtener más información, lea la [documentación del área de trabajo de destinos](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Los ID de las audiencias que desea activar en el destino seleccionado. Puede utilizar la API específica para exportar audiencias generadas por Platform, así como audiencias externas (carga personalizada). Cuando active audiencias externas, utilice el ID generado por el sistema en lugar del ID de audiencia. Puede encontrar el ID generado por el sistema en la vista Resumen de audiencias de la interfaz de usuario de audiencias. <br> ![Vista del ID de audiencia que no debería estar seleccionado.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "Vista del ID de audiencia que no debería seleccionarse."){width="100" zoomable="yes"} <br> ![Vista del ID de audiencia generado por el sistema que se debe usar.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "Vista del ID de audiencia generado por el sistema que se debe usar."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Solicitud con ID de exportación {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | Los ID de las instancias de destino en las que desea activar audiencias. Puede obtener estos identificadores desde la interfaz de usuario de Platform; para ello, vaya a la pestaña **[!UICONTROL Destinos]** > **[!UICONTROL Examinar]** y haga clic en la fila de destino que desee para que aparezca el identificador de destino en el carril derecho. Para obtener más información, lea la [documentación del área de trabajo de destinos](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | Los ID de las audiencias que desea activar en el destino seleccionado. |
| <ul><li>`exportId1`</li></ul> | El identificador devuelto en la respuesta del trabajo [exportación de audiencia](../../segmentation/api/export-jobs.md#retrieve-list). Consulte [Paso 4: Obtenga la última ID de trabajo de exportación de audiencias](#segment-export-id) para obtener instrucciones sobre cómo encontrar esta ID. |

{style="table-layout:auto"}

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
| `segment` | El ID de la audiencia activada. |
| `order` | El ID del destino en el que se activó la audiencia. |
| `statusURL` | La URL de estado del flujo de activación. Puede realizar un seguimiento del progreso del flujo mediante la [API de Flow Service](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## Administración de errores de API {#api-error-handling}

Los extremos de la API de Destination SDK siguen los principios generales del mensaje de error de la API de Experience Platform. Consulte [Códigos de estado de API](../../landing/troubleshooting.md#api-status-codes) y [errores de encabezado de solicitud](../../landing/troubleshooting.md#request-header-errors) en la guía de solución de problemas de Platform.

### Códigos de error de API y mensajes específicos de la API de activación ad hoc {#specific-error-messages}

Al utilizar la API de activación ad hoc, puede encontrar mensajes de error específicos de este extremo de API. Revise la tabla para comprender cómo abordarlos cuando aparecen.

| Mensaje de error | Resolución |
|---------|----------|
| La ejecución ya está en curso para la audiencia `segment ID` del pedido `dataflow ID` con el id. de ejecución `flow run ID` | Este mensaje de error indica que hay un flujo de activación ad-hoc en curso para una audiencia. Espere a que finalice el trabajo antes de volver a activar el trabajo de activación. |
| Los segmentos `<segment name>` no forman parte de este flujo de datos o están fuera del intervalo programado. | Este mensaje de error indica que las audiencias que seleccionó para activar no están asignadas al flujo de datos o que la programación de activación configurada para las audiencias ha caducado o aún no se ha iniciado. Compruebe si la audiencia está realmente asignada al flujo de datos y que la programación de activación de audiencia se superpone con la fecha actual. |

## Información relacionada {#related-information}

* [Conéctese a destinos por lotes y active los datos mediante la API de Flow Service](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform](/help/destinations/ui/export-file-now.md)