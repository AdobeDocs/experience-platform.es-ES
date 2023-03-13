---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Resumen de alertas
description: Obtenga información sobre las alertas en Adobe Experience Platform, incluida la estructura de cómo se definen las reglas de alerta.
feature: Alerts
exl-id: c38a93c6-1618-4ef9-8f94-41c7ab4af43c
source-git-commit: b1c82169056e66b9cdcf99f73daa7d37a3a01600
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 3%

---

# Resumen de alertas

Adobe Experience Platform le permite suscribirse a alertas basadas en eventos relativas a actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear el [[!DNL Observability Insights] API](../api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Cuando se alcanza un determinado conjunto de condiciones en las operaciones de Platform (como un problema potencial cuando el sistema supera un umbral), Platform puede enviar mensajes de alerta a cualquier usuario de la organización que se haya suscrito a ellos. Estos mensajes se pueden repetir a lo largo de un intervalo de tiempo predefinido hasta que se haya resuelto la alerta.

Este documento proporciona información general sobre las alertas en Adobe Experience Platform, incluida la estructura de cómo se definen las reglas de alerta.

## Alertas únicas frente a alertas repetidas

Las alertas de plataforma se pueden enviar una vez o pueden repetirse a lo largo de un intervalo predefinido hasta que se resuelven. Los casos de uso de cada una de estas opciones están pensados para diferir de las siguientes maneras:

| Alerta única | Alerta repetida |
| --- | --- |
| No indica necesariamente un problema. | Indica un estado potencialmente no deseable. |
| No repetir. | Se puede repetir si la condición anómala persiste. |
| Algunos ejemplos son:<ul><li>La ingesta de datos se ha completado correctamente.</li><li>Ha finalizado la ejecución de una consulta.</li><li>Se han eliminado los datos.</li></ul> | Algunos ejemplos son:<ul><li>La duración de la ingesta supera el contrato de nivel de servicio (SLA).</li><li>La ingestión diaria no se ha producido en las últimas 24 horas.</li><li>La tasa de error del procesador de flujo está por encima del umbral configurado.</li><li>El número total de perfiles supera el derecho.</li></ul> |

{style="table-layout:auto"}

## Anatomía de una alerta

Una alerta se puede desglosar en los siguientes componentes:

| Componente | Descripción |
| --- | --- |
| **Métrica** | Una observabilidad [métrica](../api/metrics.md#available-metrics) cuyo valor almacena en déclencheur la alerta, como el número de eventos de ingesta por lotes fallidos (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condición** | Condición relacionada con la métrica que almacena en déclencheur la alerta si se resuelve en verdadera, como una métrica de recuento que supera un determinado número. Esta condición puede estar asociada a una ventana de tiempo predefinida. |
| **Ventana** | (Opcional) La condición de una alerta puede restringirse a una ventana de tiempo predefinida. Por ejemplo, una alerta puede tener un déclencheur en función del número de lotes fallidos en los últimos cinco minutos. |
| **Acción** | Cuando se activa una alerta, se realiza una acción. En concreto, los mensajes se envían a los destinatarios correspondientes a través de un canal de entrega, como un webhook preconfigurado o la interfaz de usuario del Experience Platform. |
| **Frecuencia** | (Opcional) Se puede configurar una alerta para que repita su acción a un intervalo definido si su condición sigue siendo verdadera o no se ha resuelto. |

{style="table-layout:auto"}

## Recepción y administración de alertas

Las alertas se pueden recibir y administrar a través de dos canales:

* [Eventos de Adobe I/O](#events)
* [IU de Platform](#ui)

### Eventos de E/S {#events}

Las alertas se pueden enviar a un webhook configurado para facilitar la automatización eficaz de la monitorización de la actividad. Para recibir alertas a través de un webhook, debe registrar su webhook para recibir alertas de Platform en la consola de Adobe Developer. Consulte la guía de [suscripción a notificaciones de eventos de Adobe I/O](./subscribe.md) para pasos específicos.

### IU de Platform {#ui}

La interfaz de usuario de Platform le permite ver las alertas recibidas y administrar las reglas de alerta. El siguiente vídeo ofrece una introducción a estas funciones.

>[!VIDEO](https://video.tv.adobe.com/v/336218?quality=12&learn=on)

Para trabajar con alertas en la IU de Platform, debe tener los siguientes permisos de control de acceso habilitados a través de Adobe Admin Console:

| Permiso | Descripción |
| --- | --- |
| Ver alertas | Permite ver los mensajes de alerta recibidos. |
| Ver historial de alertas* | Permite ver un historial de alertas recibidas a través del [!UICONTROL Alertas] pestaña. |
| Administrar alertas* | Permite activar y desactivar las reglas de alerta a través de [!UICONTROL Alertas] pestaña. |
| Resolver alertas* | Permite resolver alertas activadas mediante el [!UICONTROL Alertas] pestaña. |

{style="table-layout:auto"}

**Para acceder a la [!UICONTROL Alertas] , también se le debe otorgar el permiso Ver alertas en combinación con uno de los otros permisos.*

>[!NOTE]
>
>Para obtener más información sobre cómo administrar permisos en Platform, consulte la [documentación de control de acceso](../../access-control/ui/overview.md).

Con el permiso Ver alertas, puede ver las alertas recibidas seleccionando el icono de campana (![Icono de campana](../images/alerts/overview/icon.png)), en la esquina superior derecha.

![](../images/alerts/overview/ui.png)

>[!NOTE]
>
> Seleccione una alerta para navegar a un panel relacionado y obtener información más detallada sobre por qué se ha activado la alerta.

Además, la variable [!UICONTROL Alertas] La pestaña en la interfaz de usuario de permite a los usuarios individuales suscribirse a tipos de alerta específicos y a los administradores habilitar o deshabilitar por completo las reglas de alerta. Consulte la [Guía de IU](./ui.md) para obtener más información sobre la administración de alertas.

## Pasos siguientes

Al leer este documento, se le ha presentado las alertas de Platform y su función en el ecosistema de Platform. Consulte la documentación del proceso relacionada con esta descripción general para obtener información sobre cómo recibir y administrar alertas.
