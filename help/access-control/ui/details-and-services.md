---
keywords: Experience Platform;inicio;temas populares;perfil de producto
solution: Experience Platform
title: Administrar detalles y servicios adicionales para un perfil de producto
topic-legacy: user guide
description: Este documento cubre los pasos necesarios para administrar los detalles y los servicios adicionales para un perfil de producto en Adobe Admin Console. Puede configurar los detalles de un perfil y el acceso a servicios adicionales desde el menú Configuración de perfil .
exl-id: ac9c2213-f2fb-44be-9334-87fada8a4717
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Administrar detalles y servicios adicionales para un perfil de producto

Puede configurar los detalles de un perfil y el acceso a servicios adicionales desde el **[!UICONTROL Configuración de perfil]** para abrir el Navegador. Para acceder al menú , seleccione **[!UICONTROL Configuración]** de la variable **[!UICONTROL Perfil del producto]** página.

![configuración](../images/settings.png)

La variable **[!UICONTROL Editar perfil de producto]** aparece, empezando en el **[!UICONTROL Editar detalles de perfil]** pestaña . Esta pestaña le permite introducir y editar su nombre de perfil y descripción. También puede modificar el nombre para mostrar y la configuración de notificación por correo electrónico de la cuenta.

![edit-product-profile](../images/edit-product-profile.png)

Select **[!UICONTROL Siguiente]** para acceder a la **[!UICONTROL Habilitar servicios]** página.

La variable **[!UICONTROL Habilitar servicios]** permite modificar el acceso de un perfil a [!DNL Platform] servicios que se configuraron inicialmente cuando se creó el perfil. Según el [!DNL Platform] suscripción, estos servicios pueden incluir:

- [!DNL Data Science Workspace]
- [!DNL Query Service]
- [!DNL Adobe Real-Time Customer Data Platform] IU (solo para Real-Time CDP)
- IU B2B

Haga clic en el botón de alternancia de la derecha de un servicio concreto para habilitarlo o deshabilitarlo. También puede seleccionar el **[!UICONTROL Todo en]** para activar o desactivar todos los servicios enumerados.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![enable-services](../images/enable-services.png)

Los clientes con derecho a la edición B2B o B2P tienen acceso a la IU B2B. La interfaz de usuario B2B se puede aprovisionar para los usuarios a través del [!UICONTROL Habilitar menú de servicios]. Seleccione la opción que aparece junto a [!UICONTROL IU B2B] para habilitar el servicio para un perfil de producto determinado y, a continuación, seleccione **[!UICONTROL Guardar]**.

La opción B2B UI permite a los usuarios ver flujos de trabajo B2B sobre la administración de cuentas y oportunidades, así como crear segmentos relacionados con B2B. Para obtener más información, consulte la documentación de [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)