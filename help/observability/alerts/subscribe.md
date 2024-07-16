---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Suscribirse a notificaciones de eventos de Adobe I/O
description: Este documento proporciona pasos sobre cómo suscribirse a las notificaciones de eventos de Adobe I/O para los servicios de Adobe Experience Platform. También se proporciona información de referencia sobre los tipos de eventos disponibles, junto con vínculos a documentación adicional sobre cómo interpretar los datos de eventos devueltos para cada servicio  [!DNL Platform] aplicable.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 06ea57d41269e98ddd984c898f41c478ddefc618
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# Suscribirse a las notificaciones de eventos de Adobe I/O

[!DNL Observability Insights] le permite suscribirse a las notificaciones de eventos de Adobe I/O relacionados con las actividades de Adobe Experience Platform. Estos eventos se envían a un webhook configurado para facilitar la automatización eficaz de la monitorización de la actividad.

Este documento proporciona pasos sobre cómo puede suscribirse a las notificaciones de eventos de Adobe I/O para los servicios de Adobe Experience Platform. También se proporciona información de referencia sobre los tipos de eventos disponibles, junto con vínculos a documentación adicional sobre cómo interpretar los datos de eventos devueltos para cada servicio [!DNL Platform] aplicable.

## Introducción

Este documento requiere una comprensión práctica de los webhooks y cómo conectar un webhook de una aplicación a otra. Consulte la [[!DNL I/O Events] documentación](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para ver una introducción a los webhooks.

## Crear un webhook

Para recibir notificaciones de [!DNL I/O Event], debe registrar un webhook especificando una URL de webhook única como parte de los detalles de registro del evento.

Puede configurar su webhook usando el cliente de su elección. Para que una dirección de webhook temporal se use como parte de este tutorial, visite [Webhook.site](https://webhook.site/) y copie la dirección URL única proporcionada.

![](../images/notifications/webhook-url.png)

Durante el proceso de validación inicial, [!DNL I/O Events] envía un parámetro de consulta `challenge` en una solicitud de GET al webhook. Debe configurar el webhook para que devuelva el valor de este parámetro en la carga útil de respuesta. Si usa Webhook.site, seleccione **[!DNL Edit]** en la esquina superior derecha y, a continuación, escriba `$request.query.challenge$` en **[!DNL Response body]** antes de seleccionar **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Creación de un nuevo proyecto en Adobe Developer Console

Vaya a la [consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de Adobe Developer Console.

## Suscribirse a eventos

>[!NOTE]
>
>El evento de notificación de ingesta de datos se ha quedado obsoleto en el Adobe I/O. En su lugar, debería usar el evento de E/S **Información de ejecución de flujo de fuentes**.

Una vez creado un nuevo proyecto, vaya a la pantalla de información general de ese proyecto. Aquí, seleccione **[!UICONTROL Agregar evento]**.

![](../images/notifications/add-event-button.png)

Aparece un cuadro de diálogo que le permite agregar un proveedor de eventos al proyecto:

* Si se está suscribiendo a las alertas de Experience Platform, seleccione **[!UICONTROL Notificaciones de plataforma]**
* Si se está suscribiendo a las notificaciones de Adobe Experience Platform [!DNL Privacy Service], seleccione **[!UICONTROL Eventos de Privacy Service]**

Cuando haya elegido un proveedor de eventos, seleccione **[!UICONTROL Siguiente]**.

![](../images/notifications/event-provider.png)

La siguiente pantalla muestra una lista de tipos de eventos a los que suscribirse. Seleccione los eventos a los que desea suscribirse y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!NOTE]
>
>Si no está seguro de a qué eventos suscribirse para el servicio con el que está trabajando, consulte la siguiente documentación:
>
>* [Notificaciones de plataforma](./rules.md)
>* [Notificaciones al Privacy Service](../../privacy-service/privacy-events.md)

![](../images/notifications/choose-event-subscriptions.png)

La siguiente pantalla le solicita que cree un token web JSON (JWT). Se le da la opción de generar automáticamente un par de claves o cargar su propia clave pública generada en el terminal.

A los efectos de este tutorial, se sigue la primera opción. Seleccione el cuadro de opción para **[!UICONTROL Generar un par de claves]** y, a continuación, seleccione el botón **[!UICONTROL Generar par de claves]** en la esquina inferior derecha.

![](../images/notifications/generate-keypair.png)

Cuando se genera el par de claves, el explorador lo descarga automáticamente. Debe almacenar este archivo, ya que no persiste en Developer Console.

La siguiente pantalla le permite revisar los detalles del par de claves recién generado. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![](../images/notifications/keypair-generated.png)

En la siguiente pantalla, proporcione un nombre y una descripción para el registro del evento en la sección [!UICONTROL Detalles de registro del evento]. Una práctica recomendada es crear un nombre único y fácilmente identificable para ayudar a diferenciar este registro de evento de otros en el mismo proyecto.

![](../images/notifications/registration-details.png)

Más abajo en la misma pantalla, en la sección [!UICONTROL Cómo recibir eventos], puede configurar de forma opcional cómo recibir eventos. **[!UICONTROL Webhook]** le permite proporcionar una dirección de webhook personalizada para recibir eventos, mientras que **[!UICONTROL Acción en tiempo de ejecución]** le permite hacer lo mismo con [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Para este tutorial, seleccione **[!UICONTROL Webhook]** y proporcione la URL del webhook que creó anteriormente. Una vez finalizado, seleccione **[!UICONTROL Guardar eventos configurados]** para completar el registro de eventos.

![](../images/notifications/receive-events.png)

Aparece la página de detalles del registro de eventos recién creado, donde puede editar su configuración, revisar los eventos recibidos, realizar un seguimiento de la depuración y agregar nuevos proveedores de eventos.

![](../images/notifications/registration-complete.png)

## Pasos siguientes

Siguiendo este tutorial, ha registrado un webhook para recibir [!DNL I/O Event] notificaciones para [!DNL Experience Platform] y/o [!DNL Privacy Service]. Para obtener más información sobre los eventos disponibles y cómo interpretar las cargas útiles de notificación para cada servicio, consulte la siguiente documentación:

* [[!DNL Privacy Service] notificaciones](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notificaciones](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] notificaciones (fuentes)](../../sources/notifications.md)

Consulte la [[!DNL Observability Insights] descripción general](../home.md) para obtener más información sobre cómo supervisar las actividades de [!DNL Experience Platform] y [!DNL Privacy Service].
