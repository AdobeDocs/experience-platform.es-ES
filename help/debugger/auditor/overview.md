---
title: Pestaña Auditor
description: Aprenda a utilizar la pestaña Auditor en Adobe Experience Platform Debugger para probar las implementaciones de Adobe Experience Cloud.
keywords: debugger;extensión de experience platform debugger;chrome;extensión;auditor;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 39%

---

# Pestaña Auditor

En Adobe Experience Platform Debugger, puede usar la variable **[!UICONTROL Auditor]** para ejecutar una serie de pruebas de auditoría en su página.

Para usar esta función:

1. Select **[!UICONTROL Auditor]** en el panel de navegación izquierdo.
1. Select **[!UICONTROL Ejecutar pruebas de Auditor]**. Una vez completadas las pruebas, sus resultados aparecen a continuación.

![Captura de pantalla de los resultados de la prueba en la ficha Auditor](../images/auditor-results.png)

La lista de resultados muestra la prueba y su resultado y proporciona sugerencias para resolver cualquier problema.

## Interpretación de los resultados de la prueba

Cada prueba tiene una ponderación y la puntuación de la prueba es igual a la ponderación asignada. Si supera una prueba con una ponderación de 5 puntos, recibirá cinco puntos.

| Puntuación | Descripción |
| --- | --- |
| 0 | Le alerta de problemas que debe tener en cuenta, pero que no afectan a su puntuación. |
| 1 | Recomienda una optimización. No afecta a la precisión de los datos. |
| 2 | Si no realiza esta prueba, no tendrá acceso a las últimas funciones y correcciones de Adobe Experience Cloud. |
| 3 | Prueba de la eficacia y si la implementación cumple las prácticas recomendadas. |
| 4 | En caso de error, es posible que esté recopilando datos poco fiables. |
| 5 | Error en el que se podrían perder datos. |

Todas las pruebas superan o fallan. Comprueban el cumplimiento o el incumplimiento de las condiciones de prueba, por lo que no hay puntuaciones parciales para el cumplimiento parcial. Por ejemplo, si la prueba comprueba la última versión de una solución de Adobe y solo está una versión por detrás, obtendrá la misma puntuación que si estuviera cinco versiones por detrás. Las versiones más recientes incluyen mejoras de rendimiento y correcciones de errores, por lo que se recomienda utilizar la versión más reciente.

Se **recomienda especialmente** corregir cualquier resultado de los niveles 4 o 5.

Se **recomienda** corregir cualquier resultado de los niveles 1 a 3.

## Tecnologías de Adobe compatibles

La función de auditor puede clasificar las siguientes tecnologías de Adobe:

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Servicio de Adobe Experience Cloud Identity
* Adobe Target
* Etiquetas (anteriormente Adobe Experience Platform Launch)

## Prueba de implementación

Para obtener más información sobre las pruebas de implementación proporcionadas por esta función, consulte los siguientes documentos:

* [Coherencia de etiquetas](./tag-consistency.md)
* [Presencia de etiquetas](./tag-presence.md)
* [Configuración](./configuration.md)
* [Alertas](./alerts.md)
