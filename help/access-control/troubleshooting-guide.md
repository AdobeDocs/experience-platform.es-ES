---
keywords: Experience Platform;inicio;temas populares;resolución de problemas;control de acceso
solution: Experience Platform
title: Guía de resolución de problemas de control de acceso
description: Este documento proporciona respuestas a las preguntas frecuentes acerca del control de acceso en Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Guía de solución de problemas de control de acceso

Este documento proporciona respuestas a las preguntas frecuentes acerca del control de acceso en Adobe Experience Platform. Para preguntas y resolución de problemas relacionados con otros [!DNL Platform] servicios, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aprovecha los perfiles de producto en [Adobe Admin Console](https://adminconsole.adobe.com) para proporcionar control de acceso basado en funciones, vinculando usuarios con permisos y zonas protegidas.  Consulte la [información general de control de acceso](home.md) para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, de producto o de perfil de producto de su organización IMS, puede ver el perfil de producto asignado y los permisos que proporciona en Adobe Admin Console. Consulte la [guía del usuario de control de acceso](./ui/overview.md) para obtener instrucciones sobre cómo navegar por la [!DNL Admin Console] para ver los permisos de un perfil de producto.

Si no es administrador, puede seguir viendo sus permisos de acceso actuales enviando una solicitud a `/acl/effective-policies` en la API de control de acceso. Consulte la sección &quot;Ver directivas efectivas&quot; en [guía para desarrolladores de control de acceso](./api/effective-policies.md) para obtener más información.

## Algunas funciones de la [!DNL Platform] La interfaz de usuario no está disponible. ¿Cómo controla los permisos el acceso a estas funciones?

Si no tiene permisos de acceso para un en particular [!DNL Platform] función, dicha función estará oculta o atenuada en la [!DNL Experience Platform] IU. Por ejemplo, para ver el &quot;[!UICONTROL Perfiles]&quot;, debe tener el &quot;[!UICONTROL Ver perfiles]&quot; o &quot;[!UICONTROL Administrar perfiles]&quot; permisos. Póngase en contacto con el administrador si necesita permisos adicionales para [!DNL Experience Platform] funciones.

## ¿Cómo se agrupan los permisos y qué grupo contiene los permisos que deseo utilizar?

Los permisos se agrupan y clasifican según la variable [!DNL Platform] funciones a las que se aplican (como [!DNL Data Management] y [!DNL Profile Management]). Para obtener una lista completa de los permisos disponibles y los grupos a los que pertenecen, consulte la [sección de permisos](home.md#permissions) en la información general de control de acceso.

Consulte la [información general de control de acceso](home.md) para obtener más información sobre cómo proporcionar control de acceso basado en roles.

## ¿Qué les sucede a los permisos después de migrar de E/S de Adobe a ID empresarial?

El control de acceso utiliza un ID de usuario (un ID único interno asignado a un usuario) para conceder permisos. Cuando se migra una organización de Adobe ID a un ID empresarial, se perderán todos los permisos establecidos para sus usuarios, ya que el ID de usuario cambia y el control de acceso utiliza el ID de usuario recién generado. Si su organización se migra a un ID empresarial, póngase en contacto con su representante de Adobe para migrar su ID de usuario de Adobe ID a un ID empresarial.
