---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de solución de problemas de Control de acceso
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# Guía de solución de problemas de Control de acceso

Este documento proporciona respuestas a las preguntas más frecuentes sobre el control de acceso en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros servicios de la plataforma, consulte la guía de solución de problemas de la plataforma de [experiencias](../landing/troubleshooting.md).

La plataforma de experiencia aprovecha los perfiles de productos de [Adobe Admin Console](http://adminconsole.adobe.com) para proporcionar un **control de acceso** basado en roles, vinculando a los usuarios con permisos y entornos limitados.  Consulte la descripción general [del](home.md) control de acceso para obtener más información.

## ¿Dónde puedo encontrar mis permisos de acceso actuales?

Si es administrador del sistema, administrador del producto o administrador del perfil del producto de su organización de IMS, puede realizar la vista del perfil del producto asignado y de los permisos que proporciona en Adobe Admin Console. Consulte la guía [del usuario de](./ui/overview.md) control de acceso para obtener instrucciones sobre cómo navegar por Admin Console para vista de los permisos de un perfil de producto.

Si no es administrador, puede seguir enviando una solicitud al extremo de la API de Control de acceso para que realice la vista de los permisos de acceso actuales mediante el envío de una solicitud al `/acl/effective-policies` extremo. Consulte la sección &quot;Políticas eficaces para la Vista&quot; en la guía [para desarrolladores de](./api/effective-policies.md) control de acceso para obtener más información.

## Algunas funciones de la interfaz de usuario de la plataforma no están disponibles. ¿Cómo se controla el acceso a estas funciones mediante permisos?

Si no tiene permisos de acceso para una función de plataforma en particular, dicha función se ocultará o atenuará en la interfaz de usuario de la plataforma de experiencia. Por ejemplo, para poder vista de la ficha &quot;Perfiles&quot;, debe tener los permisos &quot;Perfiles de Vista&quot; o &quot;Administrar Perfiles&quot;. Póngase en contacto con el administrador si necesita permisos adicionales para las funciones de la plataforma de experiencia.

## ¿Cómo se agrupan los permisos y qué grupo contiene los permisos que deseo utilizar?

Los permisos se agrupan y clasifican según las funciones de plataforma a las que se aplican (como la administración de Gestiones de datos y Perfiles). Para obtener una lista completa de los permisos disponibles y de los grupos a los que pertenecen, consulte la sección [](home.md#permissions) Permisos en la descripción general del control de acceso.

Consulte la descripción general [del](home.md) control de acceso para obtener más información sobre cómo proporcionar controles de acceso basados en roles.