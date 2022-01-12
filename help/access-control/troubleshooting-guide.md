---
keywords: Experience Platform;inicio;temas populares;solución de problemas;control de acceso
solution: Experience Platform
title: Guía de solución de problemas de control de acceso
topic-legacy: troubleshooting guide
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Guía de solución de problemas del control de acceso

Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otras [!DNL Platform] servicios, consulte la [Guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aprovecha los perfiles de producto en la variable [Adobe Admin Console](https://adminconsole.adobe.com) para proporcionar control de acceso basado en roles, vinculando a los usuarios con permisos y entornos limitados.  Consulte la [información general sobre el control de acceso](home.md) para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, administrador de productos o administrador de perfiles de producto de su organización de IMS, puede ver el perfil de producto asignado y los permisos que proporciona en Adobe Admin Console. Consulte la [guía del usuario de control de acceso](./ui/overview.md) para obtener instrucciones sobre cómo navegar por la [!DNL Admin Console] para ver los permisos de un perfil de producto.

Si no es administrador, puede ver los permisos de acceso actuales enviando una solicitud a la `/acl/effective-policies` en la API de control de acceso. Consulte la sección &quot;Ver políticas efectivas&quot; en [guía para desarrolladores de control de acceso](./api/effective-policies.md) para obtener más información.

## Algunas funciones de la sección [!DNL Platform] La interfaz de usuario no está disponible. ¿Cómo controla el acceso a estas funciones los permisos?

Si no tiene permisos de acceso para una [!DNL Platform] , esa función estará oculta o atenuada en la función [!DNL Experience Platform] IU. Por ejemplo, para ver el &quot;[!UICONTROL Perfiles]&quot;, debe tener la pestaña &quot;[!UICONTROL Ver perfiles]&quot; o &quot;[!UICONTROL Administrar perfiles]&quot;. Póngase en contacto con el administrador si necesita permisos adicionales para [!DNL Experience Platform] capacidades.

## ¿Cómo se agrupan los permisos y qué grupo contiene el permiso que deseo usar?

Los permisos se agrupan y categorizan según la variable [!DNL Platform] funcionalidades a las que se aplican (por ejemplo, [!DNL Data Management] y [!DNL Profile Management]). Para obtener una lista completa de los permisos disponibles y los grupos a los que pertenecen, consulte la [sección de permisos](home.md#permissions) en la descripción general del control de acceso.

Consulte la [información general sobre el control de acceso](home.md) para obtener más información sobre cómo proporcionar control de acceso basado en roles.
