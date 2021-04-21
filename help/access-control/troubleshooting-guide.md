---
keywords: Experience Platform;inicio;temas populares;solución de problemas;control de acceso
solution: Experience Platform
title: Guía de solución de problemas de control de acceso
topic-legacy: troubleshooting guide
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Guía de solución de problemas del control de acceso

Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros [!DNL Platform] servicios, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aprovecha los perfiles de producto de  [Adobe Admin ](http://adminconsole.adobe.com) Console para proporcionar control de acceso basado en funciones y vincular usuarios con permisos y entornos limitados.  Consulte la [descripción general del control de acceso](home.md) para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, administrador de productos o administrador de perfiles de producto de su organización de IMS, puede ver el perfil de producto asignado y los permisos que proporciona en Adobe Admin Console. Consulte la [guía del usuario de control de acceso](./ui/overview.md) para obtener instrucciones sobre cómo navegar por [!DNL Admin Console] para ver los permisos de un perfil de producto.

Si no es administrador, aún puede ver los permisos de acceso actuales enviando una solicitud al extremo `/acl/effective-policies` en la API de control de acceso. Para obtener más información, consulte la sección &quot;Ver políticas efectivas&quot; en [guía para desarrolladores de control de acceso](./api/effective-policies.md).

## Algunas funciones de la interfaz de usuario [!DNL Platform] no están disponibles. ¿Cómo controla el acceso a estas funciones los permisos?

Si no tiene permisos de acceso para una función [!DNL Platform] concreta, dicha función se ocultará o atenuará en la interfaz de usuario de [!DNL Experience Platform]. Por ejemplo, para poder ver la pestaña &quot;[!UICONTROL Profiles]&quot;, debe tener los permisos &quot;[!UICONTROL View Profiles]&quot; o &quot;[!UICONTROL Manage Profiles]&quot;. Póngase en contacto con su administrador si necesita permisos adicionales para las capacidades de [!DNL Experience Platform] .

## ¿Cómo se agrupan los permisos y qué grupo contiene el permiso que deseo usar?

Los permisos se agrupan y clasifican según las [!DNL Platform] capacidades a las que se aplican (como [!DNL Data Management] y [!DNL Profile Management]). Para obtener una lista completa de los permisos disponibles y los grupos a los que pertenecen, consulte la sección [permisos](home.md#permissions) en la descripción general del control de acceso.

Consulte la [información general del control de acceso](home.md) para obtener más información sobre cómo proporcionar control de acceso basado en roles.
