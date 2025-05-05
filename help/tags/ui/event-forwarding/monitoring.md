---
title: Supervisar actividades en el reenvío de eventos
description: Obtenga información sobre cómo monitorizar el uso, los errores y calcular la hora en las propiedades de reenvío de eventos.
feature: Event Forwarding
exl-id: 9d8572a3-816e-4b66-afe6-344fe8a15f22
source-git-commit: f8988d08e7009cc613a00f34e8151e8560c479d4
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Monitorización de actividades en el reenvío de eventos (Beta)

>[!IMPORTANT]
>
>Esta función se encuentra actualmente en la versión beta y es posible que su organización aún no tenga acceso a ella. La funcionalidad y la documentación están sujetas a cambios.

La ficha **[!UICONTROL Supervisión]** de la IU de recopilación de datos le permite supervisar los patrones de uso, los errores y calcular la hora de las propiedades de reenvío de eventos. Esta guía proporciona información general de alto nivel sobre cómo ver y comprender los informes que se muestran en la pestaña.

![Imagen que muestra la ficha de supervisión en la IU de recopilación de datos](../../images/ui/event-forwarding/monitoring/monitoring-tab.png)

## Requisitos previos

En esta guía se da por hecho que ha adquirido el reenvío de eventos y que tiene una comprensión práctica de cómo funciona dicho reenvío. Consulte la [descripción general del reenvío de eventos](./overview.md) para obtener más información.

## Vídeo introductorio

Vea el siguiente vídeo para obtener información general de alto nivel sobre la función de monitorado:

>[!VIDEO](https://video.tv.adobe.com/v/3411266?quality=12&learn=on&captions=spa)

## Selección de propiedades y entornos

Puede ver métricas dentro de un entorno y una propiedad individuales, o en todas las propiedades y entornos propiedad de su organización.

Para mostrar las métricas de una sola propiedad, seleccione el menú desplegable de propiedades y elija la propiedad de interés en la lista. Una vez que haya elegido una propiedad, también puede utilizar la lista desplegable de entornos para seleccionar un entorno de interés.

![Imagen que muestra los menús desplegables del entorno de propiedades en la interfaz de usuario](../../images/ui/event-forwarding/monitoring/property-environment.png)

## [!UICONTROL Uso]

>[!NOTE]
>
>Los datos de uso se actualizan cada mes después de que finalice el mes anterior.

El informe **[!UICONTROL Uso]** muestra las llamadas entrantes y salientes durante un período de tiempo determinado. Las llamadas entrantes representan datos enviados al reenvío de eventos. Las llamadas salientes representan datos enviados desde el reenvío de eventos. El número **[!UICONTROL Total de eventos]** del panel izquierdo es la suma de las llamadas entrantes y salientes durante un período determinado.

## [!UICONTROL Eventos de error]

El informe **[!UICONTROL Eventos de error]** muestra errores en suma y desglosados por código de respuesta HTTP cuando pasa el cursor sobre el gráfico de líneas. Los errores mostrados proceden de llamadas salientes y los códigos de respuesta proceden del extremo con el que interactúa el reenvío de eventos.

Los errores se muestran para un período de tiempo determinado, que se puede ajustar desde el menú desplegable proporcionado.

![Imagen que muestra el menú desplegable de período de tiempo para el informe de eventos de error](../../images/ui/event-forwarding/monitoring/error-time.png)

El cuadro de búsqueda para el evento de error permite consultar el reenvío de eventos para comprender los errores de un dominio de extremo determinado. Debe introducir el dominio exacto, ya que la función de búsqueda no acepta aproximaciones ni coincidencias &quot;difusas&quot;. Una vez proporcionado un dominio exacto para el que hay datos de error salientes, pulse Intro y el informe se actualiza para mostrar los errores salientes de ese dominio. Por ejemplo, para ver errores del extremo de la API de conversiones de Facebook, el dominio debe escribirse como `https://graph.facebook.com`.

## [!UICONTROL Tiempo de cómputo]

El informe **[!UICONTROL Calcular tiempo]** muestra el tiempo de cálculo de todas las reglas en los servidores de reenvío de eventos.

>[!NOTE]
>
>Los tiempos mostrados no representan una latencia de extremo a extremo. El reenvío de eventos tiene una limitación de tiempo de cálculo de 50 milisegundos. Si se supera este límite, se perderán los datos relacionados.

Los siguientes factores afectan al tiempo de cálculo:

1. El número de reglas
2. La complejidad de las reglas, generalmente impulsada por la cantidad de JavaScript personalizado que se ejecuta

Por ejemplo, si una acción en el reenvío de eventos afecta a un extremo y este tarda dos segundos en responder, esta latencia de dos segundos no se contará en el tiempo de cálculo porque el reenvío de eventos solo está esperando y no calcula nada de forma activa. El tiempo de respuesta no puede ser superior a 30 segundos; de lo contrario, se perderán datos.
