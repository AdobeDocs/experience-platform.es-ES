---
title: Notas de la versión de Adobe Experience Platform Debugger
description: Las notas de la versión más recientes de Adobe Experience Platform Debugger.
keywords: debugger;extensión de experience Platform Debugger;chrome;extensión;notas de la versión
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: 28e54656fcd85fc56e72d4fdd3d079cf8590302f
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# Notas de la versión de Adobe Experience Platform Debugger

<!-- ## Version 1.4.0 - August 24, 2022

* Added support for Web SDK hybrid implementation.
* Added error message when enabling Target Trace fails.
* Updated dependencies. -->

## Versión 1.3.3: 20 de junio de 2022

* Se ha corregido un problema que impedía abrir ventanas emergentes de tablas de eventos de red.
* Se ha corregido un problema que impedía cargar la información de Asignación en la página.

## Versión 1.3.2: 9 de junio de 2022

* Se ha agregado un avatar predeterminado cuando el usuario ha iniciado sesión.
* Se ha añadido resaltado de sintaxis a los objetos JSON en los registros.

## Versión 1.3.1: 24 de mayo de 2022

* Se han actualizado las dependencias.
* Se ha corregido un problema de Analytics en el cual las visitas posteriores al proceso no podían habilitarse.
* Se ha corregido un problema que hacía que Debugger se adjuntara a la ventana de inicio de sesión del Adobe.
* Se ha corregido un problema de AT.js por el cual los mensajes de registro no aparecían en Debugger.

## Versión 1.3.0: 28 de enero de 2022

* Se ha agregado el vínculo Acerca para mostrar la versión y las notas de la versión actuales.
* Se ha añadido la opción de alternancia para ver las visitas procesadas posteriores a solicitudes de Analytics. El botón de alternancia está disponible en la sección Analytics .
* Se ha corregido un problema con la sesión de depuración remota cuando la sesión se cerraba fuera del depurador.
* Se ha corregido una notificación de error visible en la ficha Transacciones perimetrales del SDK web.
* Se ha corregido la advertencia Etiquetas de Adobe en la página de desaprobación cuando el depurador accedió al objeto _satellite .
* Se han corregido algunos casos en los que no se encontraba una instancia de AppMeasurement en la página.
* Se ha corregido un problema de conexión de página que se producía al abrir la ventana del depurador por primera vez.

## Versión 1.2.0: 26 de octubre de 2021

* Mostrar eventos de todas las pestañas del explorador en la vista de red. Para ver solo los eventos de la pestaña actual, seleccione el icono de bloqueo en la esquina inferior derecha del depurador.
* Se ha actualizado la marca.

## Versión 1.1.0: 5 de octubre de 2021

* Visualización de depuración remota : Organice los eventos de depuración remota en un gráfico de flujo visual en la sección Adobe Experience Platform Web SDK > Transacciones perimetrales .
* Requiere que la organización IMS del SDK web de Adobe Experience Platform que se utiliza en la página coincida con la organización registrada al iniciar una nueva sesión de depuración remota.
* Mostrar solo las transacciones de borde para la pestaña conectada. Los registros de seguimiento de Target siguen estando disponibles en la sección Registros > Edge .
* Permite la anulación de la configuración del ID de flujo de datos independiente para cada instancia del SDK web de Adobe Experience Platform en la página. Agregar la opción de depuración habilitada .
* Se ha corregido un problema en el cual el token de seguimiento de Adobe Target no siempre se enviaba con sesiones de depuración remota para el SDK web de Adobe Experience Platform.

## Versión 1.0.0, 5 de mayo de 2021

* Primera versión principal de Experience Platform Debugger. Se pretende reemplazar al Experience Cloud Debugger.
