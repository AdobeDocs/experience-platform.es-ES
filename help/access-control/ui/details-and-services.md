---
keywords: Experience Platform;inicio;temas populares;perfil de producto
solution: Experience Platform
title: Administración de detalles y servicios adicionales para un perfil de producto
description: Este documento cubre los pasos necesarios para administrar los detalles y servicios adicionales de un perfil de producto en Adobe Admin Console. Puede configurar los detalles de un perfil y acceder a servicios adicionales desde el menú Configuración de perfil.
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Administrar detalles y servicios adicionales para un perfil de producto

Puede configurar los detalles de un perfil y acceder a servicios adicionales desde el **[!UICONTROL Configuración de perfil]** menú. Para acceder al menú, seleccione **[!UICONTROL Configuración]** desde el **[!UICONTROL Perfil del producto]** página.

![configuración](../images/settings.png)

El **[!UICONTROL Editar perfil de producto]** menú aparece, empezando por **[!UICONTROL Editar detalles del perfil]** pestaña. Esta pestaña le permite introducir y editar el nombre y la descripción del perfil. También puede modificar su nombre para mostrar, así como la configuración de notificaciones por correo electrónico de su cuenta.

![edit-product-profile](../images/edit-product-profile.png)

Seleccionar **[!UICONTROL Siguiente]** para acceder a **[!UICONTROL Habilitar servicios]** página.

El **[!UICONTROL Habilitar servicios]** permite modificar el acceso de un perfil a opciones adicionales [!DNL Platform] servicios que se configuraron inicialmente cuando se creó el perfil. En función de su [!DNL Platform] suscripción, estos servicios pueden incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Adobe Real-Time Customer Data Platform] IU (solo para Real-Time CDP)
- IU B2B

Haga clic en el botón de alternancia situado en el lado derecho de un servicio en particular para habilitarlo o deshabilitarlo. También puede seleccionar la variable **[!UICONTROL Todo en]** casilla de verificación para activar o desactivar todos los servicios enumerados.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![enable-services](../images/enable-services.png)

Los clientes con derecho a B2B o B2P Edition tienen acceso a la interfaz de usuario de B2B. La interfaz de usuario B2B se puede aprovisionar para los usuarios a través del [!UICONTROL Habilitar menú de servicios]. Seleccione la opción junto a [!UICONTROL IU B2B] para habilitar el servicio para un perfil de producto en particular, y luego seleccione **[!UICONTROL Guardar]**.

La opción de IU B2B permite a los usuarios ver flujos de trabajo B2B en torno a la administración de cuentas y oportunidades, así como crear segmentos relacionados con B2B. Para obtener más información, consulte la documentación sobre [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)