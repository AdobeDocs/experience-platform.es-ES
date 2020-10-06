---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform Noviembre de 2020
doc-type: release notes
last-update: November, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 39668013723dcda332558b74cf72b5f93db04461
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de versión: Noviembre de 2020**

Nuevas funciones de Adobe Experience Platform:

- [[!Control de acceso DNL]](#access-control)
- [[!Sandboxes de DNL]](#sandboxes)

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aprovecha los perfiles de productos de [Adobe Admin Console](https://adminconsole.adobe.com) para vincular a los usuarios con permisos y entornos limitados. Los permisos controlan el acceso a una variedad de funciones de la Plataforma, incluyendo modelado de datos, administración de perfiles y administración de simuladores de pruebas.

**Funciones principales**

| Función | Descripción |
|--- | ---|
| Permisos | En la ficha [!DNL Admin Console], dentro de un perfil de [!DNL Platform] producto, puede personalizar [!DNL Platform] las funciones disponibles para los usuarios conectados a ese perfil. Las categorías de permisos disponibles incluyen: [!UICONTROL Modelado]de datos, [!UICONTROL Gestión de datos], Administración [!UICONTROL de]Perfiles, [!UICONTROL Identidades], Monitoreo [!UICONTROL de]datos, Administración de Simuladores de pruebas , Destinaciones, Fuentes. |
| Acceso a los entornos limitados | La ficha **[!UICONTROL Permisos]** de un perfil [!DNL Platform] de producto puede otorgar a los usuarios acceso a entornos limitados específicos. Para obtener más información, consulte la sección sobre [entornos](#sandboxes) limitados más abajo. |

Para obtener más información, consulte la descripción general [del](../../access-control/home.md)control de acceso.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] está diseñada para enriquecer las aplicaciones de experiencia digital a escala global. Las compañías suelen ejecutar varias aplicaciones de experiencia digital en paralelo y deben encargarse del desarrollo, la prueba y la implementación de estas aplicaciones al mismo tiempo que garantizan el cumplimiento de normas operacionales. Para satisfacer esta necesidad, [!DNL Experience Platform] proporciona entornos limitados que dividen una sola [!DNL Platform] instancia en entornos virtuales independientes para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

**Funciones principales**

| Función | Descripción |
|--- | ---|
| Simulador de pruebas de producción | [!DNL Experience Platform] proporciona un solo entorno limitado de producción, que no se puede eliminar ni restablecer. |
| Entornos limitados que no son de producción | Se pueden crear varios entornos limitados que no sean de producción para una sola [!DNL Platform] instancia, lo que permite probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. |
| Mezclador de Simulador para pruebas | En la interfaz de usuario, el conmutador de simulador de pruebas situado en la esquina superior izquierda de la pantalla permite cambiar entre los entornos limitados disponibles mediante un menú desplegable. [!DNL Experience Platform] |
| `x-sandbox-name` header | Todas las llamadas a [!DNL Experience Platform] las API deben ahora incluir el nuevo `x-sandbox-name` encabezado, cuyo valor hace referencia al `name` atributo del simulador para pruebas en el que tendrá lugar la operación. |

Para obtener más información, consulte la descripción general [de los](../../sandboxes/home.md)entornos limitados.