---
title: Notas de la versión de la extensión de Adobe Content Analytics
description: Últimas notas de la versión de la extensión de etiquetas Content Analytics en Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 9fad0b092263c08a2744023b08f5f353f2c85422
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---

# Notas de la versión de Adobe Content Analytics

A continuación se muestra una lista de notas de la versión de la extensión de etiquetas de Content Analytics.

| Versión | Fecha | Correcciones |
|---|---|---|
| 1.0.47 | 23 de julio de 2025 | <ul><li>Se ha corregido un error que se producía cuando las experiencias no estaban habilitadas, lo que provocaba que fallara la comprobación de expresiones regulares para experiencias. Este problema impedía que se recopilaran datos de Content Analytics.</li><li>Se ha resuelto un problema con la configuración de idioma predeterminada que impedía que se mostrara la interfaz de usuario de etiquetas para algunos usuarios que no tenían su idioma predeterminado principal establecido en Experience Cloud.</li></ul> |
| 1.0.46 | 18 de junio de 2025 | <ul><li>Se ha añadido una notificación de mensaje cuando se intentaba guardar la configuración de la extensión, si no había un conjunto de datos de producción.</li><li>Se ha corregido temporalmente el problema de visibilidad de la carga útil de Content Analytics colocando el contenido de carga útil estructurado en la consola en su lugar.</li><li>Se ha agregado compatibilidad con la localización a la IU de Extensión.</li><li>Se ha corregido parcialmente un problema con CSS que provocaba un relleno adicional en el contenido de la IU de extensión.</li></ul> |
| 1.0.45 | 14 de abril de 2025 | <ul><li>Se han corregido varios errores en las opciones de configuración relacionadas con la celebración de eventos de Content Analytics mientras se esperaba un evento de vista de página. De forma predeterminada, Content Analytics esperará a que se activen eventos hasta que se produzca el evento PRIMERA vista de página.</li></ul> |
| 1.0.44 | 31 de marzo de 2025 | <ul><li>Primera iteración de la integración de AppMeasurement.</li><li>Esta versión aún no admite el filtrado de solicitudes específicas (por ejemplo, vistas de página), pero esta funcionalidad puede agregarse en una actualización futura. Actualmente utiliza la primera instancia de AppMeasurement que se encuentra en la página.</li></ul> |
| 1.0.43 | 10 de marzo de 2025 | <ul><li>Versión inicial de la extensión.</li></ul> |
