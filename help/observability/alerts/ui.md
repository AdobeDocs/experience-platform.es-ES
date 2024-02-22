---
keywords: Experience Platform;inicio;temas populares;intervalo de fechas
title: Guía de IU de alertas
description: Obtenga información sobre cómo administrar alertas en la interfaz de usuario del Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 8d63e9fa4c7eb09ffb90edca612a6e6d44dd18fa
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Guía de IU de alertas

La interfaz de usuario de Adobe Experience Platform le permite ver un historial de alertas recibidas en función de las métricas reveladas por Adobe Experience Platform Observability Insights. La IU también le permite ver, habilitar, deshabilitar y suscribirse a las reglas de alerta disponibles.

>[!NOTE]
>
>Para ver una introducción a las alertas en Experience Platform, consulte la [información general sobre alertas](./overview.md).

Para empezar, seleccione **[!UICONTROL Alertas]** en el panel de navegación izquierdo.

![Alertas resaltadas de página [!UICONTROL Alertas] en el panel de navegación izquierdo.](../images/alerts/ui/workspace.png)

## Administrar reglas de alerta

El **[!UICONTROL Examinar]** La pestaña enumera las reglas disponibles que pueden almacenar en déclencheur una alerta.

![Una lista de alertas disponibles que se muestran en la variable [!UICONTROL Examinar] pestaña.](../images/alerts/ui/rules.png)

Seleccione una regla de la lista para ver su descripción y sus parámetros de configuración en el carril derecho, incluidos el umbral y la gravedad.

![Una regla de alerta resaltada que muestra los detalles en el carril derecho.](../images/alerts/ui/rule-details.png)

Seleccione los puntos suspensivos (**...**) junto al nombre de una regla, y una lista desplegable muestra controles para habilitar o deshabilitar la alerta (según su estado actual), y para suscribirse o cancelar la suscripción a las notificaciones por correo electrónico de la alerta.

![Las elipses seleccionadas muestran el menú desplegable.](../images/alerts/ui/disable-subscribe.png)

## Administrar suscriptores de alerta

>[!NOTE]
>
> Para asignar una alerta a un ID de usuario de Adobe, una dirección de correo electrónico externa o una lista de grupos de correo electrónico, debe ser un administrador.

El **[!UICONTROL Examinar]** La pestaña enumera las reglas disponibles que pueden almacenar en déclencheur una alerta.

![Una lista de las reglas de alerta disponibles que se muestran en la [!UICONTROL Examinar] pestaña.](../images/alerts/ui/rules.png)

Seleccione los puntos suspensivos (**...**) junto al nombre de una regla, una lista desplegable muestra los controles. Seleccionar **[!UICONTROL Administrar suscriptores de alerta]**.

![Seleccione los puntos suspensivos para mostrar el menú desplegable. El [!UICONTROL Administrar suscriptores de alerta] opción está resaltada.](../images/alerts/ui/manage-alert-subscribers.png)

El [!UICONTROL Administrar suscriptores de alerta] página. Para asignar notificaciones a usuarios específicos, introduzca su ID de usuario de Adobe, su dirección de correo electrónico externa o una lista de grupos de correo electrónico y, a continuación, pulse Intro.

>[!NOTE]
>
>Para enviar este aviso a varios usuarios a la vez, proporcione una lista de ID de usuario o direcciones de correo electrónico separados por comas.

![La página Gestionar suscriptores de alertas muestra las direcciones de correo electrónico introducidas.](../images/alerts/ui/manage-alert-add-email.png)

Las direcciones de correo electrónico aparecen en la lista de suscriptores actuales enumerados. Seleccione **[!UICONTROL Actualizar]**.

![La página Administrar suscriptores de alerta resalta los suscriptores y [!UICONTROL Actualizar].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Ha agregado correctamente usuarios a su lista de notificaciones de alerta. Los usuarios enviados recibirán ahora notificaciones por correo electrónico para esta alerta, tal como se ve en la siguiente imagen.

![Ejemplo por correo electrónico de la notificación de alerta recibida.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Activar alertas de correo electrónico

Las notificaciones de alerta se pueden enviar directamente al correo electrónico.

Seleccione el icono de campana (![icono de campana](../images/alerts/ui/bell-icon.png)), que se encuentra en la cinta superior a la derecha, para mostrar las notificaciones y los anuncios. En la lista desplegable que aparece, seleccione el icono de engranaje (![icono de engranaje](../images/alerts/ui/cog-icon.png)) para acceder a la página preferencias de Experience Cloud.

![Una lista de alertas que se muestra resaltando el icono de campana y el icono de engranaje.](../images/alerts/ui/edit-preferences.png)

El **Perfil** se muestra la página. Seleccione el **[!UICONTROL Notificaciones]** en la navegación de la izquierda para acceder a las preferencias de alertas por correo electrónico.

![Resaltado de la página Perfil [!UICONTROL Notificaciones] en el panel de navegación izquierdo.](../images/alerts/ui/profile.png)

Desplácese hasta **Correos electrónicos** en la parte inferior de la página y seleccione **[!UICONTROL Notificaciones inmediatas]**

![La sección Correos electrónicos resaltada en la página Perfil.](../images/alerts/ui/notifications.png)

Las alertas a las que se haya suscrito ahora se enviarán a la dirección de correo electrónico conectada a la cuenta de Adobe ID.

## Ver historial de alertas

El **[!UICONTROL Historial]** Esta pestaña muestra el historial de alertas recibidas para su organización, incluida la regla que activó la alerta, la fecha activada y la fecha resuelta (si corresponde).

![Una lista de alertas recibidas que se muestran en la [!UICONTROL Historial] pestaña.](../images/alerts/ui/history.png)

Seleccione una alerta de la lista y aparecerán más detalles en el carril derecho, incluido un breve resumen del evento que activó la alerta.

![Una alerta resaltada que muestra los detalles en el carril derecho.](../images/alerts/ui/history-details.png)

## Pasos siguientes

Este documento proporciona información general sobre cómo ver y administrar alertas en la IU de Platform. Consulte la información general sobre [Observability Insights](../home.md) para obtener más información sobre las capacidades del servicio.
