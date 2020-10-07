---
keywords: Experience Platform;home;popular topics;sandbox troubleshooting
solution: Experience Platform
title: Guía de solución de problemas de Simuladores para pruebas
topic: troubleshooting guide
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9bd893820c7ab60bf234456fdd110fb2fbe6697c
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---


# Guía de solución de problemas de Simuladores para pruebas

Este documento proporciona respuestas a las preguntas más frecuentes sobre los entornos limitados de Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otros servicios de plataforma, consulte la guía de solución de problemas del [Experience Platform](../landing/troubleshooting.md).

Los Simuladores de pruebas dividen una sola instancia de plataforma en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital. See the [sandboxes overview](home.md) for more information.

## ¿Qué es un simulador de pruebas?

Los Simuladores de pruebas son particiones virtuales dentro de una sola instancia de Experience Platform. Cada simulador de pruebas mantiene su propia biblioteca independiente de recursos de la Plataforma (incluidos esquemas, conjuntos de datos, perfiles, etc.). Todo el contenido y las acciones realizadas dentro de un entorno limitado solo se limitan a ese entorno limitado y no afectan a ningún otro entorno limitado. See the [sandboxes overview](home.md) for more information.

## ¿Qué tipos de entornos limitados están disponibles y cuáles son sus diferencias?

Hay dos tipos de simulación de pruebas disponibles en Experience Platform:

* Simulador de pruebas de producción
* Simulador de pruebas que no son de producción

Experience Platform proporciona un solo simulador para pruebas de producción, que no se puede eliminar ni restablecer. Sólo puede existir un entorno limitado de producción para una sola instancia de Plataforma.

Por el contrario, los administradores de entornos limitados pueden crear varios entornos limitados que no sean de producción para una única instancia de plataforma. Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. Además, los entornos limitados que no son de producción tienen una función de restablecimiento que elimina todos los recursos creados por el cliente del entorno limitado. Los entornos limitados que no son de producción no se pueden convertir en entornos limitados de producción. Una licencia de Experience Platform predeterminada le otorga cinco entornos limitados (una producción y cuatro no producción). Puede agregar paquetes de diez entornos limitados sin producción hasta un máximo de 75 entornos limitados en total. Póngase en contacto con el administrador de la organización IMS o con el representante de ventas de Adobe para obtener más información.

See the [sandboxes overview](./home.md) for more information.

## ¿Puedo acceder a un recurso desde más de un simulador de pruebas?

Los Simuladores de pruebas son particiones aisladas de una sola instancia de Plataforma, y cada simulador de pruebas mantiene su propia biblioteca independiente de recursos. No se puede acceder a un recurso que existe en un simulador para pruebas desde ningún otro simulador para pruebas, independientemente del tipo de simulador para pruebas (producción o no producción).

## ¿Cuántos entornos limitados de producción puedo tener?

El Experience Platform solo admite un simulador para pruebas de producción por organización de IMS, que se proporciona de forma predeterminada. Aunque se puede cambiar el nombre del entorno limitado de producción, no se puede eliminar ni restablecer. Los usuarios con permisos de administración de Simuladores para pruebas solo pueden crear, restablecer y eliminar entornos limitados que no sean de producción.

## ¿Cuántos entornos limitados que no son de producción puedo tener?

Actualmente, el Experience Platform permite que un máximo de 15 entornos limitados que no sean de producción estén activos dentro de una única organización de IMS.

## Acabo de crear un simulador de pruebas. ¿Cómo puedo establecer permisos para los usuarios que trabajarán con este simulador para pruebas?

Adobe Admin Console vincula a los usuarios con los entornos limitados y los permisos mediante el uso de perfiles de productos. Después de crear un nuevo simulador para pruebas, vaya a la ficha **Permisos** del perfil del producto al que desea otorgar acceso y, a continuación, haga clic en **Entornos** para pruebas. Desde aquí, puede agregar o eliminar el acceso al nuevo simulador para pruebas de la misma manera que otros permisos.

Si desea agregar permisos únicos a los usuarios de un entorno limitado concreto, puede que tenga que crear un nuevo perfil de productos con los entornos limitados y los permisos correspondientes aplicados, y asignar esos usuarios a ese perfil.

Consulte la guía [del usuario de](../access-control/ui/overview.md) control de acceso para obtener más información sobre la administración de entornos limitados y permisos en el Admin Console.