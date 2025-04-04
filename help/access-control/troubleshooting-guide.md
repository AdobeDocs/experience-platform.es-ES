---
keywords: Experience Platform;inicio;temas populares;resolución de problemas;control de acceso
solution: Experience Platform
title: Guía de resolución de problemas de control de acceso
description: Este documento proporciona respuestas a las preguntas frecuentes acerca del control de acceso en Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Guía de solución de problemas de control de acceso

Este documento proporciona respuestas a las preguntas frecuentes acerca del control de acceso en Adobe Experience Platform. Si tiene alguna pregunta o solución de problemas relacionada con otros servicios de [!DNL Experience Platform], consulte la [Guía de solución de problemas de Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aprovecha los perfiles de producto en [Adobe Admin Console](https://adminconsole.adobe.com) para proporcionar un control de acceso basado en roles que vincula a los usuarios con permisos y zonas protegidas.  Consulte la [descripción general del control de acceso](home.md) para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, administrador de productos o administrador de perfiles de productos de su organización, puede ver el perfil de productos asignado y los permisos que proporciona en Adobe Admin Console. Consulte la [guía del usuario de control de acceso](./ui/overview.md) para obtener instrucciones sobre cómo navegar por [!DNL Admin Console] para ver los permisos de un perfil de producto.

Si no es administrador, puede seguir viendo sus permisos de acceso actuales enviando una solicitud al extremo `/acl/effective-policies` en la API de control de acceso. Consulte la sección &quot;Ver directivas efectivas&quot; en [Guía para desarrolladores de control de acceso](./api/effective-policies.md) para obtener más información.

## Algunas características de la interfaz de usuario de [!DNL Experience Platform] no están disponibles. ¿Cómo controla los permisos el acceso a estas funciones?

Si no tiene permisos de acceso para una característica de [!DNL Experience Platform] en particular, esa característica estará oculta o atenuada en la interfaz de usuario de [!DNL Experience Platform]. Por ejemplo, para ver la ficha &quot;[!UICONTROL Perfiles]&quot;, debe tener los permisos &quot;[!UICONTROL Ver perfiles]&quot; o &quot;[!UICONTROL Administrar perfiles]&quot;. Póngase en contacto con el administrador si necesita permisos adicionales para las capacidades de [!DNL Experience Platform].

## ¿Cómo se agrupan los permisos y qué grupo contiene los permisos que deseo utilizar?

Los permisos se agrupan y clasifican según las capacidades de [!DNL Experience Platform] a las que se aplican (como [!DNL Data Management] y [!DNL Profile Management]). Para obtener una lista completa de los permisos disponibles y los grupos a los que pertenecen, consulte la [sección de permisos](home.md#permissions) en la descripción general del control de acceso.

Consulte la [descripción general del control de acceso](home.md) para obtener más información sobre cómo proporcionar control de acceso basado en roles.

## ¿Qué les sucede a los permisos después de migrar de Adobe IO a Business ID?

El control de acceso utiliza un ID de usuario (un ID único interno asignado a un usuario) para conceder permisos. Cuando se migra una organización de Adobe ID a un ID empresarial, se perderán todos los permisos establecidos para sus usuarios, ya que el ID de usuario cambia y el control de acceso utiliza el ID de usuario recién generado. Si su organización se migra a un ID empresarial, póngase en contacto con su representante de Adobe para migrar su ID de usuario de Adobe ID a un ID empresarial.
