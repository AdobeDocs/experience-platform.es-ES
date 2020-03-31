---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 8 de abril de 2020
doc-type: release notes
last-update: March 4, 2020
author: ens71067
translation-type: tm+mt
source-git-commit: 38acbb4a0130763fe0c565215eda7c0713e1ff6e

---


# Notas de la versión de Adobe Experience Platform

## Fecha de publicación: 8 de abril de 2020

## Control de acceso

La plataforma de experiencia aprovecha los perfiles de productos de [Adobe Admin Console](https://adminconsole.adobe.com) para vincular a los usuarios con permisos y entornos limitados. Los permisos controlan el acceso a una variedad de funciones de la Plataforma, incluyendo modelado de datos, administración de perfiles y administración de simuladores de pruebas.

### Funciones principales

| Función | Descripción |
|--- | ---|
| Permisos | En Admin Console, la ficha _Permisos_ de un perfil de producto Plataforma permite personalizar las funciones de plataforma disponibles para los usuarios conectados a ese perfil. Las categorías de permisos disponibles incluyen: Modelado de datos, Gestión de datos, Administración de Perfiles, Identidades, Monitoreo de datos, Administración de Simulador para pruebas, Destinos, Fuentes. |
| Acceso a los entornos limitados | La ficha _Permisos_ de un perfil de producto Plataforma puede otorgar a los usuarios acceso a entornos limitados específicos. Para obtener más información, consulte la sección sobre [entornos](#sandboxes) limitados más abajo. |

Para obtener más información, consulte la descripción general [del](../../access-control/home.md)control de acceso.

## Sandboxes

La plataforma de experiencia está diseñada para enriquecer las aplicaciones de experiencia digital a escala global. Las Compañías suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, la prueba y la implementación de estas aplicaciones al mismo tiempo que garantizan el cumplimiento de normas operacionales. Para satisfacer esta necesidad, la plataforma de experiencia proporciona entornos limitados que dividen una instancia de plataforma única en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

### Funciones principales

| Función | Descripción |
|--- | ---|
| Simulador de pruebas de producción | La plataforma de experiencia proporciona un solo simulador para pruebas de producción, que no se puede eliminar ni restablecer. |
| Entornos limitados que no son de producción | Se pueden crear varios entornos limitados que no sean de producción para una sola instancia de Plataforma, lo que le permite probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. |
| Mezclador de Simulador para pruebas | En la interfaz de usuario de la plataforma de experiencia, el conmutador de simulador de pruebas situado en la esquina superior izquierda de la pantalla le permite cambiar entre los entornos limitados disponibles a través de un menú desplegable. |
| `x-sandbox-name` header | Todas las llamadas a las API de la plataforma de experiencia ahora deben incluir el nuevo `x-sandbox-name` encabezado, cuyo valor hace referencia al `name` atributo del entorno limitado en el que tendrá lugar la operación. |

Para obtener más información, consulte la descripción general [de los](../../sandboxes/home.md)entornos limitados.