---
keywords: Experience Platform;inicio;temas populares;solución de problemas de entornos limitados
solution: Experience Platform
title: Guía de solución de problemas de entornos limitados
topic-legacy: troubleshooting guide
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform.
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Guía de solución de problemas de los Simuladores para pruebas

Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros servicios de Platform, consulte la [guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

Los entornos limitados dividen una sola instancia de Platform en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital. Consulte la [información general de los entornos limitados](home.md) para obtener más información.

## ¿Qué es un simulador de pruebas?

Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform. Cada simulador para pruebas mantiene su propia biblioteca independiente de recursos de Platform (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas dentro de un simulador de pruebas solo se limitan a ese simulador de pruebas y no afectan a ningún otro simulador de pruebas. Consulte la [información general de los entornos limitados](home.md) para obtener más información.

## ¿Qué tipos de entornos limitados están disponibles y cuáles son sus diferencias?

Hay dos tipos de entornos limitados disponibles en el Experience Platform:

* Espacio aislado de producción
* Simulador para pruebas que no son de producción

Experience Platform proporciona un solo simulador para pruebas de producción, que no se puede eliminar ni restablecer. Solo puede existir un simulador para pruebas de producción para una única instancia de Platform.

Por el contrario, los administradores de entornos limitados para una única instancia de Platform pueden crear varios entornos limitados que no sean de producción. Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a su entorno limitado de producción. Además, los entornos limitados que no son de producción tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados que no sean de producción no se pueden convertir en entornos limitados de producción. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados que no sean de producción hasta un máximo de 75 entornos limitados totales. Póngase en contacto con su administrador de organización de IMS o con su representante de ventas de Adobe para obtener más información.

Consulte la [información general de los entornos limitados](./home.md) para obtener más información.

## ¿Puedo acceder a un recurso desde más de un simulador para pruebas?

Los entornos limitados son particiones aisladas de una sola instancia de Platform, y cada entorno limitado mantiene su propia biblioteca de recursos independiente. No se puede acceder a un recurso que existe en un simulador de pruebas desde ningún otro simulador de pruebas, independientemente del tipo de simulación de pruebas (de producción o sin producción).

## ¿Cuántos entornos limitados de producción puedo tener?

El Experience Platform solo admite un simulador para pruebas de producción por cada organización de IMS, que se proporciona de forma predeterminada. Aunque se puede cambiar el nombre del simulador para pruebas de producción, no se puede eliminar ni restablecer. Los usuarios con permisos de administración de entornos limitados solo pueden crear, restablecer y eliminar entornos limitados que no sean de producción.

## ¿Cuántos entornos limitados que no sean de producción puedo tener?

Actualmente, el Experience Platform permite que hasta 15 entornos limitados que no sean de producción estén activos dentro de una única organización de IMS.

## Acabo de crear un simulador de pruebas. ¿Cómo establezco permisos para los usuarios que trabajarán con este simulador para pruebas?

Adobe Admin Console vincula a los usuarios con entornos limitados y permisos mediante el uso de perfiles de producto. Después de crear un nuevo entorno limitado, vaya a la pestaña **Permisos** del perfil de producto al que desea conceder acceso y, a continuación, haga clic en **Entornos aislados**. Desde aquí, puede agregar o eliminar el acceso al nuevo simulador de pruebas del mismo modo que con otros permisos.

Si desea agregar permisos únicos a los usuarios de un entorno limitado concreto, es posible que tenga que crear un nuevo perfil de producto con los entornos limitados y permisos adecuados aplicados y asignar esos usuarios a ese perfil.

Consulte la [guía del usuario de control de acceso](../access-control/ui/overview.md) para obtener más información sobre la administración de entornos limitados y permisos en el Admin Console.
