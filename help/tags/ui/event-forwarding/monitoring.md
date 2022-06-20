---
title: Monitorizar actividades en el reenvío de eventos
description: Obtenga información sobre cómo monitorizar el uso, los errores y el tiempo de cálculo en las propiedades de reenvío de eventos.
feature: Event Forwarding
exl-id: 9d8572a3-816e-4b66-afe6-344fe8a15f22
source-git-commit: 9313ebe6d51d5ef42915d154def9cb0612407439
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# Monitorización de actividades en el reenvío de eventos (Beta)

>[!IMPORTANT]
>
>Esta función está actualmente en fase beta y es posible que su organización no tenga acceso a ella aún. La funcionalidad y la documentación están sujetas a cambios.

La variable **[!UICONTROL Monitorización]** en la interfaz de usuario de la recopilación de datos le permite supervisar los patrones de uso, los errores y calcular el tiempo de sus propiedades de reenvío de eventos. Esta guía proporciona información general de alto nivel sobre cómo ver y comprender los informes que se muestran en la pestaña .

![Imagen que muestra la pestaña de monitorización en la interfaz de usuario de la recopilación de datos](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Requisitos previos

En esta guía se da por hecho que ha comprado el reenvío de eventos y que tiene una comprensión práctica del funcionamiento del reenvío de eventos. Consulte la [información general sobre el reenvío de eventos](./overview.md) para obtener más información.

## Información general del vídeo

Vea el siguiente vídeo para obtener una descripción general de alto nivel de la función de monitorización:

>[!VIDEO](https://video.tv.adobe.com/v/343999?quality=12&learn=on)

## Selección de propiedades y entornos

Puede ver las métricas dentro de un entorno y una propiedad individuales, o en todas las propiedades y entornos que sean propiedad de su organización.

Para mostrar las métricas de una sola propiedad, seleccione el menú desplegable de propiedades y elija la propiedad de interés en la lista. Una vez que haya elegido una propiedad, también puede utilizar el menú desplegable de entorno para seleccionar un entorno de interés.

![Imagen que muestra los menús desplegables de entorno de propiedad en la interfaz de usuario](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Uso]

La variable **[!UICONTROL Uso]** muestra las llamadas entrantes y salientes durante un período de tiempo determinado. Las llamadas entrantes representan datos enviados al reenvío de eventos. Las llamadas salientes representan datos enviados desde el reenvío de eventos. La variable **[!UICONTROL Eventos totales]** número en el panel izquierdo es la suma de las llamadas entrantes y salientes para el período de tiempo determinado.

## [!UICONTROL Eventos de error]

La variable **[!UICONTROL Eventos de error]** el informe muestra errores en suma y desglosados por código de respuesta HTTP cuando pasa el cursor por encima del gráfico de líneas. Los errores mostrados proceden de llamadas salientes y los códigos de respuesta proceden del punto final con el que interactúa el reenvío de eventos.

Los errores se muestran durante un período de tiempo determinado, que se puede ajustar desde el menú desplegable proporcionado.

![Imagen que muestra el menú desplegable de período de tiempo para el informe Eventos de error](../../images/ui/event-forwarding/monitoring/error-time.png)

El cuadro de búsqueda del evento de error le permite consultar el reenvío de eventos para comprender los errores de un dominio de extremo determinado. Debe especificar el dominio exacto, ya que la función de búsqueda no acepta aproximaciones o coincidencias &quot;difusas&quot;. Una vez que proporcione un dominio exacto para el que hay datos de error salientes, pulse Intro y el informe se actualizará para mostrar los errores salientes para ese dominio. Por ejemplo, para ver los errores del extremo de la API de conversiones de Facebook, el dominio debe escribirse como `https://graph.facebook.com`.

## [!UICONTROL Tiempo de cómputo]

La variable **[!UICONTROL Tiempo de cómputo]** muestra la hora de cálculo de todas las reglas en los servidores de reenvío de eventos.

>[!NOTE]
>
>Los tiempos mostrados no representan latencia de extremo a extremo. El reenvío de eventos tiene una limitación de tiempo de cálculo de 50 milisegundos. Si se supera este límite, se perderán los datos relacionados.

Los siguientes factores afectan al tiempo de cálculo:

1. El número de reglas
2. Complejidad de las reglas, generalmente dada la cantidad de JavaScript personalizado que se está ejecutando

Por ejemplo, si una acción en el reenvío de eventos llega a un punto final y ese punto final tarda dos segundos en responder, esta latencia de dos segundos no se contará en el tiempo de cálculo porque el reenvío de eventos solo está esperando y no está calculando nada de forma activa. El tiempo de respuesta no puede ser superior a 30 segundos; de lo contrario, se perderán datos.
