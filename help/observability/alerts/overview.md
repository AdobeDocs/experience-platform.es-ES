---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Resumen de alertas
description: Obtenga información sobre las alertas en Adobe Experience Platform, incluida la estructura de cómo se definen las reglas de alerta.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 3%

---

# Resumen de alertas

>[!NOTE]
>
>Dado que las alertas son compatibles con los entornos limitados de producción y desarrollo, puede suscribirse a ellas en cualquier entorno limitado. Cuando se restablece una zona protegida, también se restablecen todas las alertas de suscripción y, cuando se elimina una zona protegida, se eliminan todas las alertas de suscripción.

Adobe Experience Platform le permite suscribirse a alertas basadas en eventos relativas a actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear la [[!DNL Observability Insights] API](../api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Cuando se alcanza un determinado conjunto de condiciones en las operaciones de Experience Platform (como un posible problema cuando el sistema supera un umbral), Experience Platform puede enviar mensajes de alerta a cualquier usuario de su organización que se haya suscrito a ellos. Estos mensajes se pueden repetir a lo largo de un intervalo de tiempo predefinido hasta que se haya resuelto la alerta.

Este documento proporciona información general sobre las alertas en Adobe Experience Platform, incluida la estructura de cómo se definen las reglas de alerta.

## Alertas únicas frente a alertas repetidas

Las alertas de Experience Platform se pueden enviar una vez o pueden repetirse a lo largo de un intervalo predefinido hasta que se resuelven. Los casos de uso de cada una de estas opciones están pensados para diferir de las siguientes maneras:

| Alerta única | Alerta repetida |
| --- | --- |
| No indica necesariamente un problema. | Indica un estado potencialmente no deseable. |
| No repetir. | Se puede repetir si la condición anómala persiste. |
| Algunos ejemplos son:<ul><li>La ingesta de datos se ha completado correctamente.</li><li>Ha finalizado la ejecución de una consulta.</li><li>Se han eliminado los datos.</li></ul> | Algunos ejemplos son:<ul><li>La duración de la ingesta supera el acuerdo de nivel de servicio (SLA).</li><li>La ingestión diaria no se ha producido en las últimas 24 horas.</li><li>La tasa de error del procesador de flujo está por encima del umbral configurado.</li><li>El número total de perfiles supera el derecho.</li></ul> |

{style="table-layout:auto"}

## Anatomía de una alerta

Una alerta se puede desglosar en los siguientes componentes:

| Componente | Descripción |
| --- | --- |
| **Métrica** | Una observabilidad [metric](../api/metrics.md#available-metrics) cuyo valor almacena en déclencheur la alerta, como el número de eventos de ingesta por lotes con errores (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condición** | Condición relacionada con la métrica que almacena en déclencheur la alerta si se resuelve en verdadera, como una métrica de recuento que supera un determinado número. Esta condición puede estar asociada a una ventana de tiempo predefinida. |
| **Ventana** | (Opcional) La condición de una alerta puede restringirse a una ventana de tiempo predefinida. Por ejemplo, una alerta puede tener un déclencheur en función del número de lotes fallidos en los últimos cinco minutos. |
| **Acción** | Cuando se activa una alerta, se realiza una acción. En concreto, los mensajes se envían a los destinatarios correspondientes a través de un canal de entrega, como un webhook preconfigurado o la interfaz de usuario de Experience Platform. |
| **Frecuencia** | (Opcional) Se puede configurar una alerta para que repita su acción a un intervalo definido si su condición sigue siendo verdadera o no se ha resuelto. |

{style="table-layout:auto"}

## Recepción y administración de alertas

Las alertas se pueden recibir y administrar a través de dos canales:

* [Adobe I/O Events](#events)
* [IU de Experience Platform](#ui)

### Eventos de E/S {#events}

Las alertas se pueden enviar a un webhook configurado para facilitar la automatización eficaz de la monitorización de la actividad. Para recibir alertas a través de webhook, debe registrar su webhook para recibir alertas de Experience Platform en Adobe Developer Console. Consulte la guía [suscripción a notificaciones de eventos de Adobe I/O](./subscribe.md) para ver los pasos específicos.

### IU de Experience Platform {#ui}

La interfaz de usuario de Experience Platform permite ver las alertas recibidas y administrar las reglas de alerta. El siguiente vídeo ofrece una introducción a estas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Para trabajar con alertas en la interfaz de usuario de Experience Platform, debe tener los siguientes permisos de control de acceso habilitados a través de Adobe Admin Console:

| Permiso | Descripción |
| --- | --- |
| Ver alertas | Permite ver los mensajes de alerta recibidos. |
| Ver historial de alertas* | Permite ver un historial de alertas recibidas a través de la ficha [!UICONTROL Alertas]. |
| Administrar alertas* | Permite habilitar y deshabilitar reglas de alerta a través de la ficha [!UICONTROL Alertas]. |
| Resolver alertas* | Permite resolver alertas activadas mediante la ficha [!UICONTROL Alertas]. |

{style="table-layout:auto"}

**Para tener acceso a la ficha [!UICONTROL Alertas], también se le debe otorgar el permiso Ver alertas en combinación con uno de los demás permisos.*

>[!NOTE]
>
>Para obtener más información sobre cómo administrar permisos en Experience Platform, consulte la [documentación de control de acceso](../../access-control/ui/overview.md).

Con el permiso Ver alertas, puede ver las alertas recibidas seleccionando el icono de campana (![Icono de campana](/help/images/icons/bell.png)) en la esquina superior derecha.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Seleccione una alerta para navegar a un panel relacionado y obtener información más detallada sobre por qué se ha activado la alerta.

Además, la ficha [!UICONTROL Alertas] de la interfaz de usuario permite que los usuarios individuales se suscriban a tipos de alerta específicos y que los administradores habiliten o deshabiliten por completo las reglas de alerta. Consulte la [guía de la interfaz de usuario](./ui.md) para obtener más información sobre la administración de alertas.

## Pasos siguientes

Al leer este documento, se le ha presentado a las alertas de Experience Platform y su función en el ecosistema de Experience Platform. Consulte la documentación del proceso relacionada con esta descripción general para obtener información sobre cómo recibir y administrar alertas.
