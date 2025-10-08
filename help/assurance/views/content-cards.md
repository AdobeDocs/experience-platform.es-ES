---
title: Vista de tarjetas de contenido
description: Esta guía detalla información sobre la vista Tarjetas de contenido en Adobe Experience Platform Assurance.
source-git-commit: fa5dbbfcc0c178c8886000479f44afd5d63c8c34
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---

# Vista de tarjetas de contenido en Assurance

La vista Mensajería en la aplicación de Adobe Experience Platform Assurance permite validar la aplicación, monitorizar las tarjetas de contenido que se envían al dispositivo y previsualizar las tarjetas.

## Tarjetas de contenido

En la parte superior de la pestaña **[!UICONTROL Tarjetas de contenido]** hay una lista desplegable de **[!UICONTROL Tarjeta de contenido]**. Esta lista enumera todas las tarjetas de contenido que se han recibido en la sesión de Assurance. Si una tarjeta no está en la lista, significa que la aplicación nunca la recibió.

![Menú desplegable de la tarjeta de contenido que contiene una lista de tarjetas](./images/content-cards/dropdown.png)

Si selecciona una tarjeta de contenido, se mostrará mucha información sobre esa tarjeta, tal como se describe en las secciones siguientes.

### Vista previa de tarjeta

En el panel derecho hay un panel **[!UICONTROL Vista previa de tarjeta]** que muestra cómo se procesa una tarjeta en plantillas comunes: Imagen pequeña, Imagen grande y Solo imagen.

![Vista previa de la tarjeta de contenido seleccionada](./images/content-cards/preview.png)

Utilice la opción **[!UICONTROL Tema]** para ver la tarjeta en modo claro u oscuro.

![Vista previa de la tarjeta de contenido seleccionada en el tema oscuro](./images/content-cards/preview-dark.png)

### Fichas disponibles

En la sección izquierda, las pestañas disponibles dependen de la tarjeta seleccionada. Si la tarjeta incluye reglas, verá tres fichas: **[!UICONTROL Información]**, **[!UICONTROL Interacciones]** y **[!UICONTROL Analizar reglas]**.

![Pestañas disponibles cuando hay reglas: Información, Interacciones, Analizar reglas](./images/content-cards/tabs-with-rules.png)

Si la tarjeta no incluye reglas, verá dos fichas: **[!UICONTROL Información]** e **[!UICONTROL Interacciones]**.

![Fichas disponibles cuando no hay reglas: Información e interacciones](./images/content-cards/tabs-no-rules.png)

### Pestaña Información

La pestaña **[!UICONTROL Información]** muestra la sección **[!UICONTROL Propiedades de la tarjeta]** en la parte superior, que incluye insignias para el **[!UICONTROL Estado actual]** (déclencheur, mostrar, descartar, descalificar) además de metadatos como **[!UICONTROL Plantilla]** (Imagen pequeña, Imagen grande o Solo imagen), **[!UICONTROL Superficie]** y cualquier par de clave-valor personalizado.

![Propiedades de tarjeta que muestran distintivos de estado actual, plantilla, superficie y pares clave-valor](./images/content-cards/card-properties.png)

Debajo de eso, la sección **[!UICONTROL Propiedades de la campaña]** muestra información cargada desde Adobe Journey Optimizer (AJO).

También puede seleccionar **[!UICONTROL Ver campaña]** para abrir la tarjeta en AJO e inspeccionarla o editarla.

![Sección Propiedades de la campaña con botón para ver la campaña](./images/content-cards/campaign-properties.png)

### Pestaña Interacciones

La ficha **[!UICONTROL Interacciones]** resume el ciclo de vida de cada tarjeta como una secuencia de distintivos: siempre comienza con **[!UICONTROL déclencheur]**, seguido del resultado que hayan producido las reglas: **[!UICONTROL mostrar]**, **[!UICONTROL descartar]** o **[!UICONTROL descalificar]**.

![Tabla de interacciones que muestra distintivos del ciclo vital desde el déclencheur para mostrar, descartar o descalificar](./images/content-cards/interactions-tab.png)

### Pestaña Analizar reglas

La pestaña **[!UICONTROL Analizar]** muestra una tabla de eventos con hasta tres columnas de reglas (**[!UICONTROL Mostrar]**, **[!UICONTROL Descartar]** y **[!UICONTROL Descalificar]**) según las reglas de la tarjeta. Si la tarjeta define solo una regla, solo aparecerá esa columna.

Cada fila representa un evento de sesión y cada columna indica si la regla de la tarjeta coincide con las condiciones de ese evento. Una puntuación del 0% significa que no se cumplen las condiciones; el 100% es una coincidencia completa (la regla se activaría).

Si el evento coincide con una condición, mostrará una marca de verificación verde. Si el evento no coincide, mostrará un icono rojo.

![Analizar tabla de eventos de ficha con columnas de reglas Mostrar, Descartar y Descalificar](./images/content-cards/rules-tab.png)

Utilice el control deslizante **[!UICONTROL Umbral de coincidencia]** para filtrar los eventos por porcentaje de coincidencia mínimo.

![Umbral de coincidencia para filtrar eventos por porcentaje de coincidencia mínimo](./images/content-cards/match-threshold.png)

Cuando selecciona un evento, se abre un panel de detalles a la derecha con un acordeón que enumera las tres reglas: **[!UICONTROL Mostrar]**, **[!UICONTROL Descartar]** y **[!UICONTROL Descalificar]**.

![El panel Detalles del evento enumera las reglas Mostrar, Descartar y Descalificar](./images/content-cards/rules-panel.png)

Expanda cualquier sección para ver las condiciones de la regla, qué condiciones coinciden y el porcentaje de coincidencia calculada para ese resultado.

![Acordeón de regla expandido que muestra condiciones coincidentes y porcentaje de coincidencia](./images/content-cards/expanded-accordion.png)

## Pestaña Solicitudes

La pestaña **[!UICONTROL Solicitudes]** muestra qué tarjetas de contenido se solicitaron y en qué superficie.

![Pestaña Solicitudes que muestra solicitudes de tarjeta de contenido](./images/content-cards/requests-tab.png)

Utilice el botón **[!UICONTROL Ver tarjeta]** para volver a la ficha de información de una tarjeta de contenido específica.

## Pestaña Lista de eventos

La pestaña **[!UICONTROL Lista de eventos]** muestra los eventos de sesión relevantes para las tarjetas de contenido, incluidas las solicitudes/respuestas de propuestas de AJO, los eventos del ciclo vital de las tarjetas y el seguimiento de interacciones. Puede buscar, filtrar, ordenar y personalizar columnas, así como exportar resultados.

Al seleccionar un evento, se abre un panel de detalles del lado derecho con la carga útil sin procesar y los atributos clave; también puede marcar eventos para su seguimiento. Esta vista es útil para correlacionar solicitudes, resultados de reglas e interacciones en toda la sesión.

![Ficha Lista de eventos con eventos de sesión que permiten filtro y búsqueda para las tarjetas de contenido](./images/content-cards/event-list.png)

## Pestaña Validación

La ficha **[!UICONTROL Validation]** ejecuta validaciones en la sesión actual para comprobar si la aplicación se ha configurado correctamente para mensajería:

![La pestaña Validación comprobó la configuración de mensajería para la sesión actual](./images/content-cards/validation.png)
