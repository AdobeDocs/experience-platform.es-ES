---
title: Notas de la versión de la extensión de Adobe Content Analytics
description: Últimas notas de la versión de la extensión de etiquetas Content Analytics en Adobe Experience Platform.
source-git-commit: 24ff17af89bc882f08ec0f331ebae53b61f35d78
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Notas de la versión de Adobe Content Analytics

A continuación se muestra una lista de notas de la versión de la extensión de etiquetas de Content Analytics.

| Versión | Fecha | Correcciones |
|---|---|---|
| <p>1.0.47</p> | <p>23 de julio de 2025</p> | <ul><li>Corrige el error que encontraba un cliente cuando las experiencias no estaban habilitadas y la comprobación de expresión regular para experiencias fallaba. Esto hace que no se recopilen los datos de Content Analytics.</li><li>Corrige el error de idioma predeterminado que impedía que la interfaz de usuario de etiquetas se mostrara para algunos usuarios si no tenían su idioma predeterminado principal establecido en Experience Cloud.</li></ul> |
| <p>1.0.46</p> | <p>18 de junio de 2025</p> | <ul><li>Agrega una notificación de mensaje si un conjunto de datos de producción no está presente al intentar guardar la configuración de la extensión.</li><li>Corrige temporalmente que la carga útil de Content Analytics sea visible, pero colocando el contenido de carga útil de Content Analytics estringido en la consola.</li><li>Añade localización a la interfaz de usuario de la extensión.</li><li>Corrige parcialmente un problema de CSS con relleno adicional alrededor del contenido de la interfaz de usuario de la extensión.</li></ul> |
| <p>1.0.45</p> | <p>14 de abril de 2025</p> | <ul><li>Soluciona algunos errores en los ajustes de configuración de al celebrar eventos de Content Analytics mientras espera eventos de vista de página. Ahora Content Analytics esperará de forma predeterminada para activar eventos hasta que se produzca el evento PRIMERA vista de página.</li></ul> |
| <p>1.0.44</p> | <p>31 de marzo de 2025</p> | <ul><li>Primera iteración de la integración de AppMeasurement.</li><li>Esta versión no admite el filtrado en solicitudes específicas (por ejemplo, vistas de página), pero podría añadirse en una fecha posterior.  También se utiliza la primera instancia de AppMeasurement que se encuentra en la página.</li></ul> |
| <p>1.0.43</p> | <p>10 de marzo de 2025</p> | <ul><li>Versión inicial de la extensión.</li></ul> |

