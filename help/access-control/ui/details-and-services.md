---
keywords: Experience Platform;inicio;temas populares;perfil de producto
solution: Experience Platform
title: Administrar detalles y servicios adicionales para un perfil de producto
topic-legacy: user guide
description: Este documento cubre los pasos necesarios para administrar los detalles y los servicios adicionales para un perfil de producto en Adobe Admin Console. Puede configurar los detalles de un perfil y el acceso a servicios adicionales desde el menú Configuración de perfil .
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 6228f499a42e61583abd1f7ff1e1af1fb90640c6
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Administrar detalles y servicios adicionales para un perfil de producto

Puede configurar los detalles de un perfil y el acceso a servicios adicionales desde el menú **[!UICONTROL Configuración de perfil]**. Para acceder al menú, seleccione **[!UICONTROL Settings]** en la página **[!UICONTROL Product Profile]**.

![configuración](../images/settings.png)

Aparece el menú **[!UICONTROL Editar perfil de producto]**, empezando en la pestaña **[!UICONTROL Editar detalles de perfil]**. Esta pestaña le permite introducir y editar su nombre de perfil y descripción. También puede modificar el nombre para mostrar y la configuración de notificación por correo electrónico de la cuenta.

![edit-product-profile](../images/edit-product-profile.png)

Seleccione **[!UICONTROL Next]** para acceder a la página **[!UICONTROL Enable services]**.

El menú **[!UICONTROL Enable services]** permite modificar el acceso de un perfil a servicios [!DNL Platform] adicionales que se configuraron inicialmente cuando se creó el perfil. Según su suscripción [!DNL Platform], estos servicios pueden incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Real-Time Customer Data Platform] IU (solo para CDP en tiempo real)
- IU B2B

Haga clic en el botón de alternancia de la derecha de un servicio concreto para habilitarlo o deshabilitarlo. También puede seleccionar la casilla **[!UICONTROL All on]** para habilitar o deshabilitar todos los servicios enumerados.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![enable-services](../images/enable-services.png)

Los clientes con derecho a la edición B2B o B2P tienen acceso a la IU B2B. La interfaz de usuario B2B se puede aprovisionar para los usuarios mediante el [!UICONTROL menú Enable services]. Seleccione el botón situado junto a [!UICONTROL B2B UI] para habilitar el servicio para un perfil de producto determinado y, a continuación, seleccione **[!UICONTROL Guardar]**.

La opción de IU B2B permite a los usuarios ver los flujos de trabajo B2B en la administración de cuentas y oportunidades, así como crear segmentos relacionados con B2B.

![enable-b2b](../images/enable-b2b.png)