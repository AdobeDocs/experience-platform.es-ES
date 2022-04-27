---
title: Notas de la versión de Adobe Experience Platform Debugger
description: Últimas notas de la versión de Adobe Experience Platform Debugger.
keywords: debugger;extensión de experience Platform Debugger;chrome;extensión;notas de la versión
uuid: 47a5d6f3-c074-4ad5-ad4b-e6030496689b
exl-id: 3eed44da-5f85-413e-a783-3a0df03a2baf
source-git-commit: a15b5525d3a2fa034715803c83dc22a94915347e
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# Notas de la versión de Adobe Experience Platform Debugger

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
