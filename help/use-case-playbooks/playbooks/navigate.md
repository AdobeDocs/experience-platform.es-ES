---
solution: Experience Platform
title: Navegar a los manuales de casos de uso
description: Aprenda a navegar por una galería de libros de reproducción y a empezar con una zona protegida inspiradora.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Navegar a los manuales de casos de uso

Los manuales de casos de uso están disponibles sin coste adicional para todos los clientes de Adobe Experience Platform. Para acceder a una amplia galería de libros de casos de uso en la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Manuales]** en el panel de navegación izquierdo.

![Caso de uso: galería de libros.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Acceso directo a los libros de reproducción de casos de uso en la barra de navegación izquierda.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Seleccione cualquier manual para ir a la página de detalles y, a continuación, seleccione **[!UICONTROL Vaya a una zona protegida inspiradora]**. Aparecerá un modal de confirmación. Seleccionar **Confirmar** para ir al simulador para pruebas inspiracional, donde puede explorar y experimentar con los diferentes casos de uso.

Si no tiene permiso para crear zonas protegidas, póngase en contacto con el administrador para obtener ayuda sobre la creación de una zona protegida inspiradora.

>[!TIP]
>
>Un simulador para pruebas inspiracional es un simulador para pruebas de desarrollo dentro de Adobe Experience Platform en el que puede crear, probar y experimentar con diferentes casos de uso antes de implementarlos en un entorno de producción en directo.

![Vaya a la zona protegida inspiradora.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Si aún no ha configurado ninguna zona protegida inspiradora, seleccione **[!UICONTROL Crear una zona protegida inspiradora]**. Aparecerá un modal. Introduzca el **Nombre** y **Título** en los cuadros de campo obligatorios y seleccione **Crear**. Una vez creado el simulador para pruebas inspiracional, asegúrese de lo siguiente [definir permisos](/help/access-control/home.md) antes de volver a la página de detalles de libros de reproducción de casos de uso para crear una instancia.

![Cree una zona protegida inspiradora.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Introduzca un nombre y un título para crear una zona protegida inspiradora.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Si selecciona una guía de casos de uso desde fuera de una zona protegida inspiradora, no podrá crear una instancia. En la página de detalles, seleccione **Ir a zona protegida inspiracional** para ir a una zona protegida inspiracional existente y, a continuación, seleccione **[!UICONTROL Crear instancia]**.

Si no tiene permiso para crear zonas protegidas, póngase en contacto con el administrador para obtener ayuda sobre la creación de una zona protegida inspiradora.

![No tiene permisos para crear una zona protegida.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Si ha alcanzado el límite del número de zonas protegidas asignadas, aparece un mensaje que le solicita que se ponga en contacto con el administrador de la organización para aumentar el límite o desactivar o eliminar algunas zonas protegidas activas. Una vez ajustado el límite de la zona protegida o reducido el número de zonas protegidas activas, puede continuar con la creación de la zona protegida inspiradora.

![Límite de zona protegida alcanzado.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Tenga en cuenta que cuando crea un simulador para pruebas inspiracional, las superficies de canal para las notificaciones por correo electrónico, push y SMS no se configuran automáticamente. Póngase en contacto con el administrador de TI para configurarlos manualmente o la creación de la instancia podría fallar.

![Configure los ajustes preestablecidos de canal.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Configuración de zonas protegidas y superficies de canal en Journey Optimizer {#configure-channel-surfaces}

Si su organización tiene licencia para [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=es)Además, y si desea utilizar los libros de reproducción diseñados para Journey Optimizer, deberá configurar los ajustes preestablecidos de canal en su zona protegida, que definen los parámetros técnicos necesarios para sus mensajes. [Obtenga información sobre cómo configurar superficies de canal en Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=es).

Para crear instancias de libros de reproducción en Journey Optimizer, debe configurar las superficies de canal para las notificaciones por correo electrónico, push y SMS.

### Superficie del canal de correo electrónico

Ir a `Channels` en la interfaz de Journey Optimizer. Configure subdominios y grupos de IP independientes para los correos electrónicos de marketing y la mensajería transaccional, si no están configurados ya. Estas son las prácticas recomendadas para garantizar que los mensajes transaccionales, como los correos electrónicos de confirmación de pedidos, lleguen a sus clientes. Escriba nombres, direcciones de correo electrónico y configuraciones adicionales. Seleccionar **Enviar** en la parte superior derecha de la página para crear la superficie del canal de marketing. Lea la documentación sobre [configuración de superficies de canal de correo electrónico](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### Superficie del canal SMS

Para crear una superficie de canal SMS, primero cree una credencial de API de SMS y seleccione el proveedor preferido (por ejemplo, Sinch). Asigne un nombre a la superficie del canal SMS (por ejemplo, Marketing SMS), seleccione la configuración e introduzca un número de remitente. Seleccionar **Enviar** en la parte superior derecha de la página para guardar la superficie del canal SMS. Lea la documentación sobre [Cómo configurar superficies de canal SMS](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=es#message-preset-sms).

Configure también canales para libros de reproducción que contengan mensajes transaccionales como confirmaciones de pedidos.

### Superficie del canal push

Confirme que las superficies de la aplicación estén configuradas desde la interfaz de Experience Platform o de Recopilación de datos. Este es el aspecto de las superficies de aplicación en el entorno de recopilación de datos.

## Pasos siguientes {#next-steps}

Ahora que ha leído este documento, debe saber cómo configurar una zona protegida inspiradora y familiarizarse con las diferentes formas de acceder a los libros de casos de uso dentro de Platform. Como paso siguiente, obtenga información sobre cómo [escoger](/help/use-case-playbooks/playbooks/choose.md) el manual correcto.
