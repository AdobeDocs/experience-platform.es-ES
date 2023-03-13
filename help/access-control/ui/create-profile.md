---
keywords: Experience Platform;inicio;temas populares;perfil de producto
solution: Experience Platform
title: Crear un nuevo perfil de producto en Adobe Admin Console
description: Este documento cubre los pasos necesarios para crear un nuevo perfil de producto en Adobe Admin Console. Para empezar a crear un nuevo perfil, vaya a la pestaña Perfiles de producto y haga clic en Nuevo perfil.
exl-id: 47558f03-c3f7-4ead-affb-fcbfd7f1e918
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 1%

---

# Creación de un nuevo perfil de producto en Adobe Admin Console

Para empezar a crear un nuevo perfil, vaya a **[!UICONTROL Perfiles de producto]** y seleccione **[!UICONTROL Nuevo perfil]**.

![new-profile](../images/new-profile.png)

El **[!UICONTROL Crear un nuevo perfil de producto]** aparece un cuadro de diálogo que le solicita que introduzca un perfil, un nombre para mostrar opcional y una descripción opcional. En **[!UICONTROL Notificaciones de usuario]**, puede alternar si se notificará por correo electrónico a los usuarios cuando se añadan o se eliminen del perfil.

Cuando termine, seleccione **[!UICONTROL Siguiente]**.

![create-new-product-profile](../images/create-new-product-profile.png)

La siguiente pantalla le solicita que elija qué servicios de Platform Services incluir en el perfil. Seleccione el botón de alternancia situado junto a un servicio para desactivarlo. Si se deshabilita un servicio, todas las funciones asociadas con ese servicio no estarán disponibles para los usuarios asignados a este perfil de producto. Cuando termine, seleccione **[!UICONTROL Guardar]**.

![enable-services](../images/enable-services.png)

Los clientes con derecho a B2B o B2P Edition tienen acceso a la interfaz de usuario de B2B. La interfaz de usuario B2B se puede aprovisionar para los usuarios a través del [!UICONTROL Habilitar menú de servicios]. Seleccione la opción junto a [!UICONTROL IU B2B] para habilitar el servicio para un perfil de producto en particular, y luego seleccione **[!UICONTROL Guardar]**.

La opción de IU B2B permite a los usuarios ver flujos de trabajo B2B en torno a la administración de cuentas y oportunidades, así como crear segmentos relacionados con B2B. Para obtener más información, consulte la documentación sobre [[!DNL Adobe Real-Time Customer Data Platform B2B Edition]](../../rtcdp/b2b-overview.md).

![enable-b2b](../images/enable-b2b.png)

El nuevo perfil de producto se ha creado correctamente y se le redirigirá al [página editar permisos](#edit-permissions). Consulte las secciones sobre [administración de permisos](#manage-permissions-for-a-product-profile) y [administrar usuarios](#manage-users-for-a-product-profile) para obtener más información sobre cómo administrar perfiles de producto una vez creados.

## Pasos siguientes

Con un nuevo perfil de producto creado, puede continuar con el siguiente paso para [administración de permisos para un perfil de producto](permissions.md)
