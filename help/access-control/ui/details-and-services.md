---
keywords: Experience Platform;inicio;temas populares;perfil de producto
solution: Experience Platform
title: Administración de detalles y servicios adicionales para un perfil de producto
description: Este documento cubre los pasos necesarios para administrar los detalles y servicios adicionales de un perfil de producto en Adobe Admin Console. Puede configurar los detalles de un perfil y acceder a servicios adicionales desde el menú Configuración de perfil.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Administrar detalles y servicios adicionales para un perfil de producto

Puede configurar los detalles de un perfil y acceder a servicios adicionales desde el menú **[!UICONTROL Configuración del perfil]**. Para obtener acceso al menú, seleccione **[!UICONTROL Configuración]** en la página **[!UICONTROL Perfil del producto]**.

![configuración](../images/settings.png)

Aparecerá el menú **[!UICONTROL Editar perfil de producto]**, a partir de la ficha **[!UICONTROL Editar detalles de perfil]**. Esta pestaña le permite introducir y editar el nombre y la descripción del perfil. También puede modificar su nombre para mostrar, así como la configuración de notificaciones por correo electrónico de su cuenta.

![edit-product-profile](../images/edit-product-profile.png)

Seleccione **[!UICONTROL Siguiente]** para acceder a la página **[!UICONTROL Habilitar servicios]**.

El menú **[!UICONTROL Habilitar servicios]** le permite modificar el acceso de un perfil a [!DNL Experience Platform] servicios adicionales que se configuraron inicialmente cuando se creó el perfil. En función de su suscripción de [!DNL Experience Platform], estos servicios pueden incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- IU [!DNL Adobe Real-Time Customer Data Platform] (solo para Real-Time CDP)
- IU B2B

Haga clic en el botón de alternancia situado en el lado derecho de un servicio en particular para habilitarlo o deshabilitarlo. También puede seleccionar la casilla de verificación **[!UICONTROL Todo en]** para habilitar o deshabilitar todos los servicios enumerados.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![enable-services](../images/enable-services.png)

Los clientes con derecho a B2B o B2P Edition tienen acceso a la interfaz de usuario de B2B. La interfaz de usuario B2B se puede aprovisionar para los usuarios mediante el [!UICONTROL menú Habilitar servicios]. Seleccione la opción junto a [!UICONTROL IU B2B] para habilitar el servicio para un perfil de producto en particular y, a continuación, seleccione **[!UICONTROL Guardar]**.

La opción de IU B2B permite a los usuarios ver flujos de trabajo B2B en torno a la administración de cuentas y oportunidades, así como crear segmentos relacionados con B2B. Para obtener más información, consulte la documentación de [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)