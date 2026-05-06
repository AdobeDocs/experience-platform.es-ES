---
title: Notas de la versión de la extensión de Adobe Content Analytics
description: Últimas notas de la versión de la extensión de etiquetas Content Analytics en Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 057d1ad8d61ed386a777175026a3f01f21541389
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---

# Notas de la versión de Adobe Content Analytics

A continuación se muestra una lista de notas de la versión de la extensión de etiquetas de Content Analytics.

| Versión | Fecha | Correcciones |
|---|---|---|
| 1.0.52 | 27 de abril de 2026 | <ul><li>Se ha agregado seguimiento para los recursos en los que CSS carga imágenes en segundo plano de un elemento en el DOM.</li><li>Se ha agregado una matriz `permanentlyBlockedURLs` codificada de forma rígida que contiene [maps.googleapis.com](https://maps.googleapis.com) y [mapsresources-pa.googleapis.com](https://mapsresources-pa.googleapis.com). Estas direcciones URL siempre están bloqueadas de forma predeterminada en la biblioteca de Content Analytics.</li><li>Se agregaron `idSource` y `channel` campos a las solicitudes de recopilación de datos XDM.</li></ul> |
| 1.0.51 | 13 de marzo de 2026 | <ul><li>Se ha corregido un error menor que podría provocar que `experienceIDs` se almacene en caché al navegar entre páginas.</li><li>Se ha corregido un problema con la captura de parámetros de cadena de consulta de experiencia. Los parámetros de consulta funcionan de la siguiente manera:<ul><li>El campo Parámetros de consulta está vacío: no se capturan parámetros de cadena de consulta en el ID de experiencia.</li><li>Los parámetros de consulta se definen explícitamente (por ejemplo, uno, dos, tres): en el ID de experiencia solo se capturan esos parámetros y valores de cadena de consulta.</li><li>El parámetro de consulta se ha establecido en un comodín (`.*`): toda la cadena document.location.search se incluye en la dirección URL.</li></ul></li></ul> |
| 1.0.49 | 12 de septiembre de 2025 | <ul><li>Se ha corregido un error menor que hacía que la interfaz de usuario de la extensión de etiquetas no se cargara si el usuario no tenía permisos de secuencia de datos. La interfaz de usuario ahora mostrará una advertencia de permiso en la opción de secuencia de datos **[!UICONTROL Choose from list]** y seguirá permitiendo al usuario introducir valores manualmente.</li><li>Se ha actualizado un problema de ruta para l10n.</li><li>Se ha corregido un problema en el cual algunas imágenes que eran elementos secundarios de elementos principales que no eran imágenes no capturaban correctamente los clics de recursos para esos elementos de imagen secundarios.</li><li>Si un usuario tiene WebSDK configurado en etiquetas con un nombre de instancia diferente de `alloy`, la biblioteca Content Analytics detectará la primera instancia de la biblioteca WebSDK y la utilizará para enviar eventos de Content Analytics.</li></ul> |
| 1.0.48 | 25 de agosto de 2025 | <ul><li>Añade compatibilidad con el seguimiento de recursos dentro de los elementos DOM raíz en la sombra de un documento.</li></ul> |
| 1.0.47 | 23 de julio de 2025 | <ul><li>Se ha corregido un error que se producía cuando las experiencias no estaban habilitadas, lo que provocaba que fallara la comprobación de expresiones regulares para experiencias. Este problema impedía que se recopilaran datos de Content Analytics.</li><li>Se ha resuelto un problema con la configuración de idioma predeterminada que impedía que se mostrara la interfaz de usuario de etiquetas para algunos usuarios que no tenían su idioma predeterminado principal establecido en Experience Cloud.</li></ul> |
| 1.0.46 | 18 de junio de 2025 | <ul><li>Se ha añadido una notificación de mensaje cuando se intentaba guardar la configuración de la extensión, si no había un conjunto de datos de producción.</li><li>Se ha corregido temporalmente el problema de visibilidad de la carga útil de Content Analytics colocando el contenido de carga útil estructurado en la consola en su lugar.</li><li>Se ha agregado compatibilidad con la localización a la IU de Extensión.</li><li>Se ha corregido parcialmente un problema con CSS que provocaba un relleno adicional en el contenido de la IU de extensión.</li></ul> |
| 1.0.45 | 14 de abril de 2025 | <ul><li>Se han corregido varios errores en las opciones de configuración relacionadas con la celebración de eventos de Content Analytics mientras se esperaba un evento de vista de página. De forma predeterminada, Content Analytics esperará a que se activen eventos hasta que se produzca el evento PRIMERA vista de página.</li></ul> |
| 1.0.44 | 31 de marzo de 2025 | <ul><li>Primera iteración de la integración de AppMeasurement.</li><li>Esta versión aún no admite el filtrado de solicitudes específicas (por ejemplo, vistas de página), pero esta funcionalidad puede agregarse en una actualización futura. Actualmente utiliza la primera instancia de AppMeasurement que se encuentra en la página.</li></ul> |
| 1.0.43 | 10 de marzo de 2025 | <ul><li>Versión inicial de la extensión.</li></ul> |
