---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Suscripción a las notificaciones de eventos de Adobe I/O
description: Este documento proporciona los pasos sobre cómo suscribirse a las notificaciones de eventos de Adobe I/O para los servicios de Adobe Experience Platform. También se proporciona información de referencia sobre los tipos de eventos disponibles, junto con vínculos a documentación adicional sobre cómo interpretar los datos de eventos devueltos para cada tipo aplicable [!DNL Platform] servicio.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 3%

---

# Suscripción a las notificaciones de eventos de Adobe I/O

[!DNL Observability Insights] le permite suscribirse a las notificaciones de eventos de Adobe I/O relacionadas con las actividades de Adobe Experience Platform. Estos eventos se envían a un enlace web configurado para facilitar la automatización eficaz de la supervisión de actividades.

Este documento proporciona los pasos sobre cómo suscribirse a las notificaciones de eventos de Adobe I/O para los servicios de Adobe Experience Platform. También se proporciona información de referencia sobre los tipos de eventos disponibles, junto con vínculos a documentación adicional sobre cómo interpretar los datos de eventos devueltos para cada tipo aplicable [!DNL Platform] servicio.

## Primeros pasos

Este documento requiere una comprensión práctica de los enlaces web y cómo conectar un enlace web de una aplicación a otra. Consulte la [[!DNL I/O Events] documentación](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) para una introducción a los webhooks.

## Creación de un vínculo web

Para recibir [!DNL I/O Event] notificaciones, debe registrar un enlace web especificando una URL de enlace web única como parte de los detalles de registro de eventos.

Puede configurar su weblink utilizando el cliente de su elección. Para que una dirección temporal de enlace web se utilice como parte de este tutorial, visite [Sitio web.sitio](https://webhook.site/) y copie la dirección URL única proporcionada.

![](../images/notifications/webhook-url.png)

Durante el proceso de validación inicial, [!DNL I/O Events] envía un `challenge` parámetro de consulta en una solicitud de GET al weblink. Debe configurar el enlace web para que devuelva el valor de este parámetro en la carga útil de respuesta. Si está utilizando Weblock.site, seleccione **[!DNL Edit]** en la esquina superior derecha, luego introduzca `$request.query.challenge$` under **[!DNL Response body]** antes de seleccionar **[!DNL Save]**.

![](../images/notifications/response-challenge.png)

## Crear un nuevo proyecto en la consola de Adobe Developer

Vaya a la [consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial en [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de Adobe Developer Console.

## Suscripción a eventos

Una vez que haya creado un nuevo proyecto, vaya a la pantalla de información general de ese proyecto. Desde aquí, seleccione **[!UICONTROL Agregar evento]**.

![](../images/notifications/add-event-button.png)

Aparece un cuadro de diálogo que le permite agregar un proveedor de eventos al proyecto:

* Si está suscrito a alertas de Experience Platform, seleccione **[!UICONTROL Notificaciones de la plataforma]**
* Si está suscrito a Adobe Experience Platform [!DNL Privacy Service] notificaciones, seleccionar **[!UICONTROL Eventos de Privacy Service]**

Una vez que haya elegido un proveedor de eventos, seleccione **[!UICONTROL Siguiente]**.

![](../images/notifications/event-provider.png)

La siguiente pantalla muestra una lista de tipos de eventos a los que suscribirse. Seleccione los eventos a los que desee suscribirse y, a continuación, seleccione **[!UICONTROL Siguiente]**.

>[!NOTE]
>
>Si no está seguro de a qué eventos suscribirse para el servicio con el que está trabajando, consulte la siguiente documentación:
>
>* [Notificaciones de la plataforma](./rules.md)
>* [notificaciones del Privacy Service](../../privacy-service/privacy-events.md)


![](../images/notifications/choose-event-subscriptions.png)

La siguiente pantalla le solicita que cree un token web JSON (JWT). Se le da la opción de generar automáticamente un par de claves o cargar su propia clave pública generada en el terminal.

Para los fines de este tutorial, se sigue la primera opción. Seleccione el cuadro de opciones de **[!UICONTROL Generación de un par de claves]** y, a continuación, seleccione **[!UICONTROL Generar par de teclas]** en la esquina inferior derecha.

![](../images/notifications/generate-keypair.png)

Cuando se genera el par de claves, el explorador la descarga automáticamente. Debe almacenar el archivo usted mismo, ya que no se conserva en Developer Console.

La siguiente pantalla le permite revisar los detalles del par de claves recién generado. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![](../images/notifications/keypair-generated.png)

En la siguiente pantalla, proporcione un nombre y una descripción para el registro de evento en la [!UICONTROL Detalles de registro de eventos] para obtener más información. Una práctica recomendada es crear un nombre único y fácilmente identificable para ayudar a diferenciar este registro de evento de otros en el mismo proyecto.

![](../images/notifications/registration-details.png)

Más abajo en la misma pantalla debajo de la [!UICONTROL Cómo recibir eventos] , si lo desea, puede configurar cómo recibir eventos. **[!UICONTROL Weblock]** permite proporcionar una dirección de enlace web personalizada para recibir eventos, mientras que **[!UICONTROL Acción en tiempo de ejecución]** le permite hacer lo mismo con [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html).

Para este tutorial, seleccione **[!UICONTROL Weblock]** y proporcione la URL del vínculo web que creó anteriormente. Una vez finalizado, seleccione **[!UICONTROL Guardar eventos configurados]** para completar el registro de eventos.

![](../images/notifications/receive-events.png)

Se abre la página de detalles del registro de eventos recién creado, donde puede editar su configuración, revisar los eventos recibidos, realizar el seguimiento de la depuración y agregar nuevos proveedores de eventos.

![](../images/notifications/registration-complete.png)

## Pasos siguientes

Siguiendo este tutorial, ha registrado un enlace web para recibir [!DNL I/O Event] notificaciones para [!DNL Experience Platform] y/o [!DNL Privacy Service]. Para obtener más información sobre los eventos disponibles y cómo interpretar las cargas de notificación para cada servicio, consulte la siguiente documentación:

* [[!DNL Privacy Service] notificaciones](../../privacy-service/privacy-events.md)
* [[!DNL Data Ingestion] notificaciones](../../ingestion/quality/subscribe-events.md)
* [[!DNL Flow Service] (fuentes) notificaciones](../../sources/notifications.md)

Consulte la [[!DNL Observability Insights] información general](../home.md) para obtener más información sobre cómo supervisar las actividades en [!DNL Experience Platform] y [!DNL Privacy Service].
