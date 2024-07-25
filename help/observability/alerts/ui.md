---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Guía de IU de alertas
description: Obtenga información sobre cómo administrar alertas en la interfaz de usuario del Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Guía de IU de alertas

La interfaz de usuario de Adobe Experience Platform le permite ver un historial de alertas recibidas en función de las métricas reveladas por Adobe Experience Platform Observability Insights. La IU también le permite ver, habilitar, deshabilitar y suscribirse a las reglas de alerta disponibles.

>[!NOTE]
>
>Para ver una introducción a las alertas en Experience Platform, consulte la [descripción general de las alertas](./overview.md).

Para empezar, seleccione **[!UICONTROL Alertas]** en el panel de navegación izquierdo.

![Alertas que resaltan la página [!UICONTROL Alertas] en la navegación izquierda.](../images/alerts/ui/workspace.png)

## Administrar reglas de alerta

La ficha **[!UICONTROL Examinar]** enumera las reglas disponibles que pueden almacenar en déclencheur una alerta.

![Se muestra una lista de las alertas disponibles en la ficha [!UICONTROL Examinar].](../images/alerts/ui/rules.png)

Seleccione una regla de la lista para ver su descripción y sus parámetros de configuración en el carril derecho, incluidos el umbral y la gravedad.

![Se resaltó una regla de alerta que muestra detalles en el carril derecho.](../images/alerts/ui/rule-details.png)

Seleccione los puntos suspensivos (**...**) junto al nombre de una regla y aparecerá un menú desplegable con controles para habilitar o deshabilitar la alerta (según su estado actual) y para suscribirse o cancelar la suscripción a las notificaciones por correo electrónico de la alerta.

![Los puntos suspensivos seleccionados muestran el menú desplegable.](../images/alerts/ui/disable-subscribe.png)

## Administrar suscriptores de alertas

>[!NOTE]
>
> Para asignar una alerta a un ID de usuario de Adobe, una dirección de correo electrónico externa o una lista de grupos de correo electrónico, debe ser un administrador.

La ficha **[!UICONTROL Examinar]** enumera las reglas disponibles que pueden almacenar en déclencheur una alerta.

![Lista de reglas de alerta disponibles que se muestran en la ficha [!UICONTROL Examinar].](../images/alerts/ui/rules.png)

Seleccione los puntos suspensivos (**...**) junto al nombre de una regla y aparecerá un menú desplegable con los controles. Seleccione **[!UICONTROL Administrar suscriptores de alertas]**.

![Seleccione los puntos suspensivos para mostrar el menú desplegable. La opción [!UICONTROL Administrar suscriptores de alerta] está resaltada.](../images/alerts/ui/manage-alert-subscribers.png)

Aparecerá la página [!UICONTROL Administrar suscriptores de alertas]. Para asignar notificaciones a usuarios específicos, introduzca su ID de usuario de Adobe, su dirección de correo electrónico externa o una lista de grupos de correo electrónico y, a continuación, pulse Intro.

>[!NOTE]
>
>Para enviar este aviso a varios usuarios a la vez, proporcione una lista de ID de usuario o direcciones de correo electrónico separados por comas.

![Página de administración de suscriptores de alertas que muestra las direcciones de correo electrónico ingresadas.](../images/alerts/ui/manage-alert-add-email.png)

Las direcciones de correo electrónico aparecen en la lista de suscriptores actuales enumerados. Seleccione **[!UICONTROL Actualizar]**.

![La página de administración de suscriptores de alertas resalta a los suscriptores y [!UICONTROL actualiza].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Ha agregado correctamente usuarios a su lista de notificaciones de alerta. Los usuarios enviados recibirán ahora notificaciones por correo electrónico para esta alerta, tal como se ve en la siguiente imagen.

![Ejemplo de correo electrónico de la notificación de alerta recibida.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Activar alertas de correo electrónico

Las notificaciones de alerta se pueden enviar directamente al correo electrónico.

Seleccione el icono de campana (![icono de campana](/help/images/icons/bell.png)) ubicado en la cinta superior a la derecha para mostrar notificaciones y anuncios. En el menú desplegable que aparece, seleccione el icono de engranaje (![icono de engranaje](/help/images/icons/settings.png)) para acceder a la página de preferencias de Experience Cloud.

![Se muestra una lista de alertas resaltando el icono de campana y el icono de engranaje.](../images/alerts/ui/edit-preferences.png)

Se muestra la página **Perfil**. Seleccione **[!UICONTROL Notificaciones]** en el panel de navegación izquierdo para acceder a las preferencias de alertas por correo electrónico.

![La página Perfil que resalta [!UICONTROL Notificaciones] en la navegación izquierda.](../images/alerts/ui/profile.png)

Desplácese a la sección **Correos electrónicos** en la parte inferior de la página y seleccione **[!UICONTROL Notificaciones inmediatas]**

![La sección Correos electrónicos resaltada en la página Perfil.](../images/alerts/ui/notifications.png)

Las alertas a las que se haya suscrito ahora se enviarán a la dirección de correo electrónico conectada a la cuenta de Adobe ID.

## Ver historial de alertas

La ficha **[!UICONTROL Historial]** muestra el historial de alertas recibidas para su organización, incluida la regla que activó la alerta, la fecha desencadenada y la fecha resuelta (si corresponde).

![Se muestra una lista de las alertas recibidas en la ficha [!UICONTROL Historial].](../images/alerts/ui/history.png)

Seleccione una alerta de la lista y aparecerán más detalles en el carril derecho, incluido un breve resumen del evento que activó la alerta.

![Alerta resaltada que muestra detalles en el carril derecho.](../images/alerts/ui/history-details.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo ver y administrar alertas en la IU de Platform. Consulte la descripción general de [Observability Insights](../home.md) para obtener más información sobre las capacidades del servicio.
