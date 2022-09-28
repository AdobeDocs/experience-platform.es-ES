---
keywords: Experience Platform;inicio;temas populares; alertas
description: Al crear un flujo de datos, puede suscribirse a las alertas para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.
title: Suscripción a alertas en contexto en la interfaz de usuario
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: d450dc7b0dc0303c9d33c3e8e003659e3140cf5b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Suscripción a alertas para flujos de datos de fuentes en la interfaz de usuario

Adobe Experience Platform le permite suscribirse a las alertas basadas en eventos relacionadas con las actividades de Adobe Experience Platform. Las alertas reducen o eliminan la necesidad de sondear el [[!DNL Observability Insights] API](../../../observability/api/overview.md) para comprobar si un trabajo se ha completado, si se ha alcanzado un hito determinado dentro de un flujo de trabajo o si se ha producido algún error.

Puede suscribirse a las alertas al crear un flujo de datos para recibir mensajes de alerta sobre el estado, el éxito o el error de la ejecución del flujo.

Este documento proporciona los pasos sobre cómo suscribirse para recibir mensajes de alerta para sus flujos de datos de origen.

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

>[!IMPORTANT]
>
>Debe activar notificaciones instantáneas de correos electrónicos para su cuenta de Platform para recibir notificaciones de alerta por correo electrónico para sus flujos de datos.

Puede activar las alertas para los flujos de datos durante el [!UICONTROL Detalles de flujo de datos] paso del flujo de trabajo de orígenes en el espacio de trabajo de orígenes.

![dataflow-detail](../../images/tutorials/alerts/dataflow-detail.png)

Las alertas disponibles para los flujos de datos de origen son:

| Alertas | Descripción |
| --- | --- |
| Inicio de ejecución del flujo de datos de fuentes | Esta alerta le envía un mensaje cuando se ha iniciado el flujo de datos de origen. |
| Éxito de ejecución del flujo de datos de fuentes | Esta alerta le envía un mensaje cuando los datos de su origen se incorporan correctamente en Platform. |
| Error de ejecución del flujo de datos de origen | Esta alerta le envía un mensaje si se produce un error en el flujo de datos. |
| ~~Fuentes: flujo de datos: falta de ingesta~~ | ~~Esta alerta le envía un mensaje si la ingesta se retrasa más de siete horas y no se introducen datos en Platform.~~ <br>**Nota:** Ya no recibirá alertas, ya que esta alerta está en desuso. |

Seleccione las alertas a las que desee suscribirse y, a continuación, seleccione **[!UICONTROL Siguiente]** para revisar y finalizar su flujo de datos.

![select-alert](../../images/tutorials/alerts/select-alerts.png)

Consulte las siguientes guías para ver los pasos detallados sobre la creación de un flujo de datos de fuentes en la interfaz de usuario:

* [Advertising](./dataflow/advertising.md)
* [Almacenamiento en la nube](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Database](./dataflow/databases.md)
* [Comercio electrónico](./dataflow/ecommerce.md)
* [Archivos locales](./create/local-system/local-file-upload.md)
* [Automatización de marketing](./dataflow/marketing-automation.md)
* [Pagos](./dataflow/payments.md)
* [Protocolos](./dataflow/protocols.md)

## Recibir alertas

Una vez que se ejecute el flujo de datos, puede recibir alertas a través de la interfaz de usuario o por correo electrónico.

### En la interfaz de usuario

Las alertas se representan en la interfaz de usuario mediante un icono de notificación en el encabezado superior de la interfaz de usuario de Platform. Seleccione el icono de notificación para ver mensajes de alerta específicos relacionados con sus flujos de datos.

![notificación](../../images/tutorials/alerts/notification.png)

Aparece el panel de notificaciones, que muestra una lista de actualizaciones de estado en el flujo de datos que ha creado.

![alert-window](../../images/tutorials/alerts/alert-window.png)

Puede situar el cursor sobre un mensaje de alerta para marcarlos como leídos o seleccionar el icono de reloj para establecer recordatorios futuros sobre el estado del flujo de datos.

![recordarme](../../images/tutorials/alerts/remind-me.png)

Seleccione el mensaje de alerta para ver información específica sobre su flujo de datos.

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

La variable [!UICONTROL Resumen de ejecución de flujo de datos] se abre. La mitad superior de la pantalla muestra información general sobre el flujo de datos, incluida información sobre sus atributos, el ID de ejecución del flujo de datos correspondiente y el resumen de errores de alto nivel.

![información general de dataflow](../../images/tutorials/alerts/dataflow-overview.png)

La mitad inferior de la página muestra cualquier [!UICONTROL Errores de ejecución del flujo de datos] que se produjo durante la fase de ejecución del flujo de datos. Desde aquí puede obtener una vista previa de los diagnósticos de error o utilizar la variable [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) para descargar diagnósticos de error o el manifiesto de archivo que corresponde a su flujo de datos.

![dataflow run-errors](../../images/tutorials/alerts/dataflow-run-error.png)

Para obtener más información sobre la gestión de errores de flujo de datos, consulte la guía de [control de flujos de datos de fuentes en la interfaz de usuario](../../../dataflows/ui/monitor-sources.md).

### Por correo electrónico

Las alertas para los flujos de datos también se le envían por correo electrónico. Seleccione el nombre del flujo de datos en el cuerpo del correo electrónico para ver más información sobre el flujo de datos.

![email](../../images/tutorials/alerts/email.png)

De forma similar a la alerta de interfaz de usuario, la variable [!UICONTROL Resumen de ejecución de flujo de datos] , lo que le proporciona una interfaz para investigar cualquier error asociado con su flujo de datos.

![información general de dataflow](../../images/tutorials/alerts/dataflow-overview.png)

## Suscribirse y cancelar la suscripción a alertas

Puede suscribirse a más alertas o cancelar la suscripción de alertas establecidas para un flujo de datos existente en la [!UICONTROL Flujos de datos] página. Busque el flujo de datos que cree a partir de la lista y seleccione los puntos suspensivos (`...`) para ver un menú desplegable de opciones. A continuación, seleccione **[!UICONTROL Suscribirse alertas]** para modificar la configuración de alerta del flujo de datos.

![opciones](../../images/tutorials/alerts/options.png)

Aparece una ventana emergente que proporciona una lista de alertas de fuentes. Seleccione las alertas a las que desee suscribirse o deseleccione las alertas de las que desee cancelar la suscripción. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![guardar](../../images/tutorials/alerts/save.png)

## Pasos siguientes

Este documento proporciona una guía paso a paso sobre cómo suscribirse a alertas en contexto para sus flujos de datos de origen. Para obtener más información, consulte la [guía de la interfaz de usuario de alertas](../../../observability/alerts/ui.md).