---
keywords: Experience Platform;home;popular topics;troubleshooting;access control
solution: Experience Platform
title: Guía de solución de problemas de control de acceso
topic: troubleshooting guide
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---


# Guía de solución de problemas de control de acceso

Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros [!DNL Platform] servicios, consulte la guía de solución de problemas del [Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aprovecha los perfiles de productos de [Adobe Admin Console](http://adminconsole.adobe.com) para proporcionar controles de acceso basados en roles, vinculando a los usuarios con permisos y entornos limitados.  Consulte la descripción general [del](home.md) control de acceso para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, administrador del producto o administrador del perfil del producto de su organización de IMS, puede realizar la vista del perfil del producto asignado y de los permisos que proporciona dentro del Adobe Admin Console. Consulte la guía [del usuario de](./ui/overview.md) control de acceso para obtener instrucciones sobre cómo desplazarse por la página [!DNL Admin Console] para vista de los permisos de un perfil de producto.

Si no es administrador, puede seguir enviando una solicitud al extremo de la API de Control de acceso para que realice la vista de los permisos de acceso actuales mediante el envío de una solicitud al `/acl/effective-policies` extremo. Consulte la sección &quot;Políticas eficaces para la Vista&quot; en la guía [para desarrolladores de](./api/effective-policies.md) control de acceso para obtener más información.

## Algunas funciones de la interfaz de usuario no están disponibles [!DNL Platform] . ¿Cómo se controla el acceso a estas funciones mediante permisos?

Si no dispone de permisos de acceso para una función determinada [!DNL Platform] , dicha función se ocultará o atenuará en la [!DNL Experience Platform] interfaz de usuario. Por ejemplo, para realizar la vista de la ficha &quot;[!UICONTROL Perfiles]&quot;, debe tener los permisos &quot;Perfiles[!UICONTROL de]Vista&quot; o &quot;[!UICONTROL Administrar Perfiles]&quot;. Póngase en contacto con el administrador si necesita permisos adicionales para [!DNL Experience Platform] funciones.

## ¿Cómo se agrupan los permisos y qué grupo contiene los permisos que deseo utilizar?

Los permisos se agrupan y clasifican según las [!DNL Platform] capacidades a las que se aplican (por ejemplo, [!DNL Data Management] y [!DNL Profile Management]). Para obtener una lista completa de los permisos disponibles y de los grupos a los que pertenecen, consulte la sección [](home.md#permissions) Permisos en la descripción general del control de acceso.

Consulte la descripción general [del](home.md) control de acceso para obtener más información sobre cómo proporcionar controles de acceso basados en roles.