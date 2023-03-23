---
keywords: Experience Platform;inicio;temas populares; alertas;destinos
description: Al crear un flujo de datos, puede suscribirse a las alertas para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.
title: Suscripción a alertas de destino en contexto
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: 3bb9858c236c91e1567fd8e78988f4049537ffe3
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Suscripción a alertas de destino en contexto

Adobe Experience Platform le permite suscribirse a las alertas basadas en eventos relacionadas con las actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear el [[!DNL Observability Insights] API](../../observability/api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Puede suscribirse a las alertas al crear un flujo de datos para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.

Este documento proporciona pasos sobre cómo suscribirse para recibir mensajes de alerta para sus flujos de datos de destino.

## Primeros pasos

Este documento requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Destinos](../home.md): Integraciones creadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.
* [Observabilidad](../../observability/home.md): [!DNL Observability Insights] le permite supervisar las actividades de Platform mediante el uso de métricas estadísticas y notificaciones de eventos.
   * [Alertas](../../observability/alerts/overview.md): Cuando se alcanza un determinado conjunto de condiciones en las operaciones de Platform (como un problema potencial cuando el sistema supera un umbral), Platform puede enviar mensajes de alerta a cualquier usuario de su organización que se haya suscrito a ellos.

## Suscripción a alertas en la interfaz de usuario {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Suscripción a alertas de destino"
>abstract="Las alertas le permiten recibir notificaciones en función del estado de sus flujos de datos de destino. Puede configurar notificaciones de alerta para obtener actualizaciones si el flujo de datos se ha iniciado, ha fallado o no ha enviado datos a su destino."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>Debe activar notificaciones instantáneas de correos electrónicos para su cuenta de Platform para recibir notificaciones de alerta por correo electrónico para sus flujos de datos.

Puede activar las alertas para los flujos de datos durante el [!UICONTROL Configurar nuevo destino] del [conexión de destino](connect-destination.md) flujo de trabajo.

![Imagen de la interfaz de usuario que muestra la sección de alertas de destino.](../assets/ui/alerts/destination-alerts.png)

Seleccione las alertas a las que desee suscribirse y, a continuación, seleccione **[!UICONTROL Siguiente]** para revisar y finalizar su flujo de datos.

Las alertas disponibles para flujos de datos de destino se describen en la siguiente tabla.

* Para los destinos de flujo continuo, solo la variable [!DNL Activation Skipped Rate Exceeded] alerta está disponible.
* Para destinos basados en archivos, todas las alertas están disponibles.

| Alertas | Descripción |
| --- | --- |
| Retraso de ejecución del flujo de destino | Esta alerta le avisa cuando la ejecución de un flujo de destino tarda más de 150 minutos en activar un segmento. |
| Error de ejecución del flujo de destino | Esta alerta le avisa cuando se produce un error al activar un segmento en un destino. |
| Éxito de ejecución del flujo de destino | Esta alerta le avisa cuando un segmento se activa correctamente en un destino. |
| Inicio de la ejecución del flujo de destino | Esta alerta le avisa cuando una ejecución de flujo de destino comienza a activar un segmento. |
| Se ha superado la tasa de activación omitida | Esta alerta le avisa cuando la tasa de omisión de activación ha superado el 1 % de las activaciones totales. Las identidades se omiten durante la activación cuando faltan atributos o una infracción de consentimiento. |

## Recibir alertas {#receiving-alerts}

Una vez que se ejecute el flujo de datos de destino, puede recibir alertas a través de la interfaz de usuario o por correo electrónico.

### Recibir alertas en la interfaz de usuario {#receiving-alerts-in-ui}

Las alertas se representan en la interfaz de usuario mediante un icono de notificación en el encabezado superior de la interfaz de usuario de Platform. Seleccione el icono de notificación para ver mensajes de alerta específicos relacionados con sus flujos de datos.

![Imagen de la interfaz de usuario que muestra el icono de notificación en el Experience Platform](../assets/ui/alerts/notification.png)

Aparece el panel de notificaciones, que muestra una lista de actualizaciones de estado en el flujo de datos que ha creado.

![Imagen de la interfaz de usuario que muestra el panel de notificaciones](../assets/ui/alerts/alert-window.png)

Puede situar el cursor sobre un mensaje de alerta para marcarlos como leídos o seleccionar el icono de reloj para establecer recordatorios futuros sobre el estado del flujo de datos.

![Imagen de la interfaz de usuario que muestra las opciones de recordatorio de notificación](../assets/ui/alerts/remind-me.png)

Seleccione el mensaje de alerta para ver información específica sobre su flujo de datos.

![Imagen de la interfaz de usuario que muestra cómo seleccionar una notificación](../assets/ui/alerts/select-alert-message.png)

La variable [!UICONTROL Detalles de ejecución de flujo de datos] se abre. La mitad superior de la pantalla muestra información general sobre el flujo de datos, incluida información sobre sus atributos, el ID de ejecución del flujo de datos correspondiente y el resumen de errores de alto nivel.

![Imagen de interfaz de usuario que muestra la página de detalles de ejecución del flujo de datos.](../assets/ui/alerts/dataflow-overview.png)

La mitad inferior de la página muestra cualquier [!UICONTROL Errores de ejecución del flujo de datos] que se produjo durante la fase de ejecución del flujo de datos. Desde aquí puede obtener una vista previa de los diagnósticos de error o utilizar la variable [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) para descargar diagnósticos de error o el manifiesto de archivo que corresponde a su flujo de datos.

![La imagen de la interfaz de usuario muestra la página de detalles de ejecución del flujo de datos, con un resaltado en la sección de errores.](../assets/ui/alerts/dataflow-run-error.png)

Para obtener más información sobre la gestión de errores de flujo de datos, consulte la guía de [monitorización de flujos de datos de destinos en la interfaz de usuario](../../dataflows/ui/monitor-destinations.md).

### Recibir alertas por correo electrónico {#receiving-alerts-by-email}

Las alertas para los flujos de datos también se le envían por correo electrónico. Seleccione el nombre del flujo de datos en el cuerpo del correo electrónico para ver más información sobre el flujo de datos.

![Captura de pantalla de un correo electrónico de alerta](../assets/ui/alerts/email.png)

De forma similar a la alerta de interfaz de usuario, la variable [!UICONTROL Resumen de ejecución de flujo de datos] , lo que le proporciona una interfaz para investigar cualquier error asociado con su flujo de datos.

![información general de dataflow](../assets/ui/alerts/dataflow-overview.png)

## Suscribirse y cancelar la suscripción a alertas {#subscribe-and-unsubscribe}

Puede suscribirse a más alertas o cancelar la suscripción de alertas establecidas para un flujo de datos de destino existente en los destinos [!UICONTROL Examinar] página.

![Imagen de la interfaz de usuario que muestra la página de exploración de destinos](../assets/ui/alerts/destination-list.png)

Busque la conexión de destino para la que desea recibir alertas y seleccione los puntos suspensivos (`...`) para ver un menú desplegable de opciones. A continuación, seleccione **[!UICONTROL Suscripción a alertas]** para modificar la configuración de alerta del flujo de datos de destino.

![Imagen de la interfaz de usuario que muestra las opciones de destino](../assets/ui/alerts/destination-alerts-subscribe.png)

Aparece una ventana emergente que proporciona una lista de alertas de destino. Seleccione las alertas a las que desee suscribirse o deseleccione las alertas de las que desee cancelar la suscripción. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![Imagen de interfaz de usuario que muestra la página de suscripciones de alertas de destino](../assets/ui/alerts/destination-alerts-list.png)

## Pasos siguientes {#next-steps}

Este documento proporciona una guía paso a paso sobre cómo suscribirse a las alertas en contexto para los flujos de datos de destino. Para obtener más información, consulte la [guía de la interfaz de usuario de alertas](../../observability/alerts/ui.md).
