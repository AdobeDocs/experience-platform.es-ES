---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Información general sobre alertas
description: Obtenga información sobre las alertas en Adobe Experience Platform, incluida la estructura de cómo se definen las reglas de alerta.
source-git-commit: 5fabf5fa12f0a117a50bf694dea5118e5ea03500
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---


# Información general sobre las alertas

Adobe Experience Platform le permite suscribirse a las alertas basadas en eventos relacionadas con las actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear la [[!DNL Observability Insights] API](../api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Cuando se alcanza un determinado conjunto de condiciones en las operaciones de Platform (como un problema potencial cuando el sistema supera un umbral), Platform puede enviar mensajes de alerta a cualquier usuario de su organización que se haya suscrito a ellos. Estos mensajes se pueden repetir durante un intervalo de tiempo predefinido hasta que se haya resuelto la alerta.

Este documento proporciona información general sobre las alertas en Adobe Experience Platform, incluida la estructura de cómo se definen las reglas de alerta.

## Alertas únicas frente a alertas repetidas

Las alertas de plataforma se pueden enviar una vez o pueden repetirse en un intervalo predefinido hasta que se resuelvan. Los casos de uso de cada una de estas opciones tienen la intención de diferir de las siguientes maneras:

| Alerta única | Alerta repetida |
| --- | --- |
| No necesariamente indica un problema. | Indica un estado potencialmente no deseado. |
| No se repite. | Se puede repetir si la condición anómala persiste. |
| Algunos ejemplos son:<ul><li>La ingesta de datos se ha completado correctamente.</li><li>Ha finalizado la ejecución de una consulta.</li><li>Se han eliminado los datos.</li></ul> | Algunos ejemplos son:<ul><li>La duración de la ingesta supera el acuerdo de nivel de servicio (SLA).</li><li>La ingestión diaria no se produjo en las últimas 24 horas.</li><li>La tasa de error del procesador de flujo está por encima del umbral configurado.</li><li>El número total de perfiles supera la asignación de derechos.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Anatomía de una alerta

Una alerta se puede desglosar en los siguientes componentes:

| Componente | Descripción |
| --- | --- |
| **Métrica** | Una métrica [de capacidad de observación](../api/metrics.md#available-metrics) cuyo valor déclencheur la alerta, como el número de eventos de ingesta por lotes fallidos (`timeseries.ingestion.dataset.batchfailed.count`). |
| **Condición** | Condición relacionada con la métrica que genera déclencheur para la alerta si se resuelve en verdadero, como una métrica de recuento que supera un determinado número. Esta condición puede asociarse con un periodo de tiempo predefinido. |
| **Ventana** | (Opcional) La condición para una alerta puede estar restringida a un periodo de tiempo predefinido. Por ejemplo, una alerta puede generar un déclencheur en función del número de lotes con errores de los últimos cinco minutos. |
| **Acción** | Cuando se activa una alerta, se realiza una acción. En concreto, los mensajes se envían a los destinatarios aplicables a través de un canal de envío, como un vínculo web preconfigurado o la interfaz de usuario del Experience Platform. |
| **Frecuencia** | (Opcional) Se puede configurar una alerta para que repita su acción a un intervalo definido si su condición sigue siendo verdadera o si, de lo contrario, no se resuelve. |

{style=&quot;table-layout:auto&quot;}

## Recibir y administrar alertas

Las alertas se pueden recibir y administrar a través de dos canales:

* [Eventos de Adobe I/O](#events)
* [Interfaz de usuario de Platform](#ui)

### Eventos de E/S {#events}

Las alertas se pueden enviar a un enlace web configurado para facilitar la automatización eficaz de la supervisión de actividades. Para recibir alertas a través de weblock, debe registrar el weblink para las alertas de Platform en Adobe Developer Console. Consulte la guía sobre [suscripción a notificaciones de eventos de Adobe I/O](./subscribe.md) para conocer los pasos específicos.

### Interfaz de usuario de Platform {#ui}

Para trabajar con alertas en la interfaz de usuario de Platform, debe tener activados los siguientes permisos de control de acceso mediante Adobe Admin Console:

| Permiso | Descripción |
| --- | --- |
| Ver alertas | Permite ver los mensajes de alerta recibidos. |
| Ver el historial de alertas* | Permite ver un historial de alertas recibidas a través de la pestaña [!UICONTROL Alerts]. |
| Administrar alertas* | Permite habilitar y deshabilitar las reglas de alerta a través de la pestaña [!UICONTROL Alerts]. |
| Resolver alertas* | Permite resolver alertas activadas mediante la pestaña [!UICONTROL Alerts]. |

{style=&quot;table-layout:auto&quot;}

**Para acceder a la pestaña [!UICONTROL Alerts], también se le debe otorgar el permiso Ver alertas en combinación con uno de los demás permisos.*

>[!NOTE]
>
>Para obtener más información sobre cómo administrar permisos en Platform, consulte la [documentación de control de acceso](../../access-control/ui/overview.md).

Con el permiso Ver alertas , puede ver las alertas recibidas seleccionando el icono de campana (![Bell Icon](../images/alerts/overview/icon.png)) en la esquina superior derecha.

![](../images/alerts/overview/ui.png)

Además, la pestaña [!UICONTROL Alerts] de la interfaz de usuario permite que los usuarios individuales se suscriban a tipos de alerta específicos y permite a los administradores habilitar o deshabilitar reglas de alerta por completo. Consulte la [guía de la interfaz de usuario](./ui.md) para obtener más información sobre la administración de alertas.

## Pasos siguientes

Al leer este documento, se le ha introducido a las alertas de Platform y su papel en el ecosistema de Platform. Consulte la documentación del proceso vinculada a esta descripción general para obtener información sobre cómo recibir y administrar alertas.