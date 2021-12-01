---
keywords: Experience Platform;inicio;temas populares; alertas
description: Al crear un flujo de datos, puede suscribirse a las alertas para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.
title: Suscripción a alertas en contexto en la interfaz de usuario
hide: true
hidefromtoc: true
source-git-commit: a81d21f615206e644044c2f0f546a458d1aebbf3
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Suscríbase a los mensajes de alerta para monitorizar los flujos de datos de origen en la interfaz de usuario

Adobe Experience Platform le permite suscribirse a las alertas basadas en eventos relacionadas con las actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear el [[!DNL Observability Insights] API](../../../observability/api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Al crear un flujo de datos, puede suscribirse a las alertas para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.

Este documento proporciona los pasos sobre cómo suscribirse a alertas y recibir mensajes de alerta para sus ejecuciones de flujo.

## Primeros pasos

Este documento requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Fuentes](../../home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
* [Observabilidad](../../../observability/home.md): [!DNL Observability Insights] le permite supervisar las actividades de Platform mediante el uso de métricas estadísticas y notificaciones de eventos.
   * [Alertas](../../../observability/alerts/overview.md): Cuando se alcanza un determinado conjunto de condiciones en las operaciones de Platform (como un problema potencial cuando el sistema supera un umbral), Platform puede enviar mensajes de alerta a cualquier usuario de su organización que se haya suscrito a ellos.

## Suscripción a alertas en la interfaz de usuario {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Suscripción a las alertas de fuentes"
>abstract="Las alertas le permiten recibir notificaciones en función del estado de sus flujos de datos de origen. Puede establecer notificaciones de alerta para obtener actualizaciones si el flujo de datos se ha iniciado, se ha realizado correctamente, ha fallado o no ha introducido ningún dato."
>text="Learn more in documentation"
