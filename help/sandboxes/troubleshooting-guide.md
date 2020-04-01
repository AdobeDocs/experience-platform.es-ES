---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de solución de problemas de Simuladores para pruebas
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: f15049ca917818d325b5783c70faaa53ba669aba

---


# Guía de solución de problemas de Simuladores para pruebas

Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros servicios de la plataforma, consulte la guía de solución de problemas de la plataforma de [experiencias](../landing/troubleshooting.md).

Los Simuladores de pruebas dividen una sola instancia de plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital. Consulte la descripción general [de los](home.md) entornos limitados para obtener más información.

## ¿Qué es un simulador de pruebas?

Los entornos limitados son particiones virtuales dentro de una sola instancia de la plataforma de experiencia. Cada simulador de pruebas mantiene su propia biblioteca independiente de recursos de la Plataforma (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas dentro de un entorno limitado solo se limitan a ese entorno limitado y no afectan a ningún otro entorno limitado. Consulte la descripción general [de los](home.md) entornos limitados para obtener más información.

## ¿Qué tipos de entornos limitados están disponibles y cuáles son sus diferencias?

Existen dos tipos de simulación de pruebas disponibles en la plataforma de experiencia:

* Simulador de pruebas de producción
* Simulador de pruebas que no son de producción

La plataforma de experiencias proporciona un solo simulador de pruebas **de** producción que no se puede eliminar ni restablecer. Sólo puede existir un entorno limitado de producción para una sola instancia de Plataforma.

Por el contrario, los administradores de simuladores de pruebas pueden crear varios entornos limitados **que no sean de producción** para una sola instancia de plataforma. Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. Además, los entornos limitados que no son de producción tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados que no son de producción no se pueden convertir en entornos limitados de producción.

Consulte la descripción general [de los](./home.md) entornos limitados para obtener más información.

## ¿Puedo acceder a un recurso desde más de un simulador de pruebas?

Los Simuladores de pruebas son particiones aisladas de una sola instancia de Plataforma, y cada simulador de pruebas mantiene su propia biblioteca independiente de recursos. No se puede acceder a un recurso que existe en un simulador para pruebas desde ningún otro simulador para pruebas, independientemente del tipo de simulador de pruebas (producción o no producción).

## ¿Cuántos entornos limitados de producción puedo tener?

La plataforma de experiencia solo admite un simulador de pruebas de producción por organización de IMS, que se proporciona de forma predeterminada. Aunque se puede cambiar el nombre del entorno limitado de producción, no se puede eliminar ni restablecer. Los usuarios con permisos de administración de Simuladores para pruebas solo pueden crear, restablecer y eliminar entornos limitados que no sean de producción.

## ¿Cuántos entornos limitados que no son de producción puedo tener?

La plataforma de experiencias permite que hasta 15 entornos limitados que no sean de producción estén activos en una única organización de IMS.

## Acabo de crear un simulador de pruebas. ¿Cómo puedo establecer permisos para los usuarios que trabajarán con este simulador para pruebas?

La Consola de administración de Adobe vincula a los usuarios con los entornos limitados y los permisos mediante el uso de perfiles **de** productos. Después de crear un nuevo simulador para pruebas, vaya a la ficha _Permisos_ del perfil del producto al que desea otorgar acceso y, a continuación, haga clic en **Entornos** para pruebas. Desde aquí, puede agregar o eliminar el acceso al nuevo simulador para pruebas de la misma manera que otros permisos.

Si desea agregar permisos únicos a los usuarios de un entorno limitado concreto, puede que tenga que crear un nuevo perfil de productos con los entornos limitados y los permisos correspondientes aplicados, y asignar esos usuarios a ese perfil.

Consulte la guía [del usuario de](../access-control/ui/overview.md) control de acceso para obtener más información sobre la administración de entornos limitados y permisos en Admin Console.