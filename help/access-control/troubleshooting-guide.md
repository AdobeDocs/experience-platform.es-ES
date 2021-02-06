---
keywords: Experience Platform;inicio;temas populares;solución de problemas;control de acceso
solution: Experience Platform
title: Guía de solución de problemas de control de acceso
topic: troubleshooting guide
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Guía de solución de problemas de control de acceso

Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros [!DNL Platform] servicios, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aprovecha los perfiles de productos de  [Adobe Admin ](http://adminconsole.adobe.com) Consolation para proporcionar control de acceso basado en roles y vincular a los usuarios con permisos y entornos limitados.  Consulte la [información general del control de acceso](home.md) para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, administrador del producto o administrador del perfil del producto de su organización de IMS, puede realizar la vista del perfil del producto asignado y de los permisos que proporciona dentro del Adobe Admin Console. Consulte la [guía del usuario de control de acceso](./ui/overview.md) para obtener instrucciones sobre cómo desplazarse por [!DNL Admin Console] para vista de los permisos de un perfil de producto.

Si no es administrador, puede seguir enviando una solicitud al extremo `/acl/effective-policies` de la API de Control de acceso para que realice la vista de los permisos de acceso actuales. Consulte la sección &quot;Políticas eficaces para la Vista&quot; en [Guía para desarrolladores de control de acceso](./api/effective-policies.md) para obtener más información.

## Algunas funciones de la interfaz de usuario [!DNL Platform] no están disponibles. ¿Cómo se controla el acceso a estas funciones mediante permisos?

Si no tiene permisos de acceso para una función [!DNL Platform] en particular, dicha función se ocultará o atenuará en la interfaz de usuario de [!DNL Experience Platform]. Por ejemplo, para realizar la vista de la ficha &quot;[!UICONTROL Perfiles]&quot;, debe tener los permisos &quot;[!UICONTROL Perfiles de Vista]&quot; o &quot;[!UICONTROL Administrar Perfiles]&quot;. Póngase en contacto con el administrador si necesita permisos adicionales para [!DNL Experience Platform] capacidades.

## ¿Cómo se agrupan los permisos y qué grupo contiene los permisos que deseo utilizar?

Los permisos se agrupan y clasifican según las capacidades [!DNL Platform] a las que se aplican (como [!DNL Data Management] y [!DNL Profile Management]). Para obtener una lista completa de los permisos disponibles y los grupos a los que pertenecen, consulte la sección [permisos](home.md#permissions) en la información general de control de acceso.

Consulte la [información general de control de acceso](home.md) para obtener más información sobre cómo proporcionar control de acceso basado en roles.