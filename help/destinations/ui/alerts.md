---
keywords: Experience Platform;inicio;temas populares; alertas;destinos
description: Puede suscribirse a alertas al crear un flujo de datos para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.
title: Suscribirse a alertas de destino en contexto
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 8%

---

# Suscribirse a alertas de destino en contexto

Adobe Experience Platform le permite suscribirse a alertas basadas en eventos relativas a actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear la [[!DNL Observability Insights] API](../../observability/api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Puede suscribirse a alertas al crear un flujo de datos para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.

Este documento proporciona pasos sobre cómo suscribirse y recibir mensajes de alertas para los flujos de datos de destino.

## Introducción

Este documento requiere un entendimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.
* [Observabilidad](../../observability/home.md): [!DNL Observability Insights] le permite supervisar las actividades de Experience Platform mediante el uso de métricas estadísticas y notificaciones de eventos.
   * [Alertas](../../observability/alerts/overview.md): Cuando se alcanza un conjunto determinado de condiciones en las operaciones de Experience Platform (como un problema potencial cuando el sistema incumple un umbral), Experience Platform puede enviar mensajes de alerta a cualquier usuario de su organización que se haya suscrito a ellos.

## Suscripción a alertas en la IU {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Suscripción a alertas de destino"
>abstract="Las alertas permiten recibir notificaciones en función del estado de sus flujos de datos de destino. Puede configurar notificaciones de alerta para obtener actualizaciones si el flujo de datos se ha iniciado, ha fallado o no ha enviado datos a su destino."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Debe habilitar notificaciones instantáneas de correos electrónicos para su cuenta de Experience Platform a fin de recibir notificaciones de alerta basadas en correo electrónico para sus flujos de datos.

Puede habilitar alertas para sus flujos de datos durante el paso [!UICONTROL Configurar nuevo destino] del flujo de trabajo [conexión de destino](connect-destination.md).

![Imagen de la interfaz de usuario que muestra la sección de alertas de destino.](../assets/ui/alerts/destination-alerts.png)

Seleccione las alertas a las que desee suscribirse y, a continuación, seleccione **[!UICONTROL Siguiente]** para revisar y finalizar el flujo de datos.

Las alertas disponibles para los flujos de datos de destino se describen en la siguiente tabla.

* Para los destinos de flujo continuo, solo está disponible la alerta [!DNL Activation Skipped Rate Exceeded].
* Para destinos basados en archivos, todas las alertas están disponibles.

| Alertas | Descripción |
| --- | --- |
| Retraso de ejecución de flujo de destinos | Esta alerta le notifica cuando una ejecución de flujo de destino tarda más de 150 minutos en activar una audiencia. |
| Error de ejecución de flujo de destino | Esta alerta le avisa cuando se produce un error al activar una audiencia en un destino. |
| Ejecución correcta de flujo de destino | Esta alerta le notifica cuando una audiencia se activa correctamente en un destino. |
| Inicio de ejecución de flujo de destino | Esta alerta le avisa cuando una ejecución de flujo de destino comienza a activar una audiencia. |
| Tasa de activación omitida superada | Esta alerta le notifica cuando la tasa de omisión de activación ha superado el 1 % del total de activaciones. Las identidades se omiten durante la activación cuando faltan atributos o una infracción de consentimiento. |

## Recepción de alertas {#receiving-alerts}

Una vez que se ejecute el flujo de datos de destino, puede recibir alertas a través de la interfaz de usuario o por correo electrónico.

### Recepción de alertas en la IU {#receiving-alerts-in-ui}

Las alertas se representan en la interfaz de usuario mediante un icono de notificación en el encabezado superior de la interfaz de usuario de Experience Platform. Seleccione el icono de notificación para ver mensajes de alerta específicos relacionados con los flujos de datos.

![Imagen de interfaz de usuario que muestra el icono de notificación en Experience Platform](../assets/ui/alerts/notification.png)

Aparecerá el panel de notificaciones, que mostrará una lista de las actualizaciones de estado del flujo de datos que ha creado.

![Imagen de interfaz de usuario que muestra el panel de notificaciones](../assets/ui/alerts/alert-window.png)

Puede colocar el ratón encima de un mensaje de alerta para marcarlo como leído o seleccionar el icono del reloj para definir recordatorios futuros sobre el estado del flujo de datos.

![Imagen de la interfaz de usuario que muestra las opciones de recordatorio de notificación](../assets/ui/alerts/remind-me.png)

Seleccione el mensaje de alerta para ver información específica sobre el flujo de datos.

![Imagen de interfaz de usuario que muestra cómo seleccionar una notificación](../assets/ui/alerts/select-alert-message.png)

Aparecerá la página [!UICONTROL Detalles de ejecución del flujo de datos]. La mitad superior de la pantalla muestra una descripción general del flujo de datos, incluida información sobre sus atributos, el ID de ejecución del flujo de datos correspondiente y el resumen de errores de alto nivel.

![Imagen de interfaz de usuario que muestra la página de detalles de ejecución del flujo de datos.](../assets/ui/alerts/dataflow-overview.png)

La mitad inferior de la página muestra cualquier [!UICONTROL error de ejecución de flujo de datos] que se haya producido durante la fase de ejecución del flujo de datos. Desde aquí, puede obtener una vista previa de los diagnósticos de error o utilizar la [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) para descargar los diagnósticos de error o el manifiesto de archivo que corresponda a su flujo de datos.

![Imagen de la interfaz de usuario que muestra la página de detalles de ejecución del flujo de datos, con un resaltado en la sección de errores.](../assets/ui/alerts/dataflow-run-error.png)

Para obtener más información sobre la administración de errores de flujo de datos, consulte la guía sobre [supervisión de destinos y flujos de datos en la IU](../../dataflows/ui/monitor-destinations.md).

### Recibir alertas por correo electrónico {#receiving-alerts-by-email}

Las alertas de sus flujos de datos también se le envían por correo electrónico. Seleccione el nombre del flujo de datos en el cuerpo del correo electrónico para ver más información sobre el flujo de datos.

![Captura de pantalla de un correo electrónico de alerta](../assets/ui/alerts/email.png)

Similar a la alerta de interfaz de usuario, aparece la página [!UICONTROL Información general sobre la ejecución del flujo de datos], que le proporciona una interfaz para investigar cualquier error asociado con el flujo de datos.

![descripción general del flujo de datos](../assets/ui/alerts/dataflow-overview.png)

## Suscripción y cancelación de la suscripción a alertas {#subscribe-and-unsubscribe}

Puede suscribirse a más alertas o cancelar la suscripción a alertas establecidas para un flujo de datos de destino existente en la página [!UICONTROL Examinar] destinos.

![Imagen de IU que muestra la página de exploración de destinos](../assets/ui/alerts/destination-list.png)

Busque la conexión de destino para la que desea recibir alertas y seleccione los puntos suspensivos (`...`) para ver un menú desplegable de opciones. A continuación, seleccione **[!UICONTROL Suscribirse a alertas]** para modificar la configuración de alertas del flujo de datos de destino.

![Imagen de interfaz de usuario que muestra las opciones de destino](../assets/ui/alerts/destination-alerts-subscribe.png)

Aparece una ventana emergente que le proporciona una lista de alertas de destino. Seleccione las alertas a las que desee suscribirse o anule la selección de las alertas cuya suscripción desee cancelar. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Imagen de interfaz de usuario que muestra la página de suscripciones de alertas de destino](../assets/ui/alerts/destination-alerts-list.png)

## Pasos siguientes {#next-steps}

Este documento proporciona una guía paso a paso sobre cómo suscribirse a alertas en contexto para los flujos de datos de destino. Para obtener más información, consulte la [guía de la interfaz de usuario de alertas](../../observability/alerts/ui.md).
