---
title: Notas de la versión de la extensión Adobe Target v2
description: Notas de la versión de la extensión de etiquetas de Adobe Target v2 en Adobe Experience Platform.
exl-id: c1a04e62-026d-4b16-aa70-bc6d5dbe6b2d
source-git-commit: a51bc1fb536347840eef113a8649b64fbf573287
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 49%

---

# Notas de la versión de la extensión Adobe Target v2

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## v0.20.1 (3 de noviembre de 2023)

- Actualizado para admitir `at.js` 2.11.2.
- Se ha corregido un error que provocaba incoherencias en los tokens de respuesta enviados en eventos personalizados.

## v0.20.0 (9 de octubre de 2023)

- Actualizado para admitir `at.js` 2.11.0.
- Se ha agregado compatibilidad con la configuración de sandboxId y sandboxName personalizados de Adobe Experience Platform en targetGlobalSettings, que se pasarán a la API de entrega en las llamadas getOffer/getOffers.
- Corrección DOM de sombreado para encadenar :eq() en el selector.

## v0.19.3 (18 de septiembre de 2023)

- Actualizado para admitir `at.js` Versión 2.10.3.
- Se ha corregido un problema que activaba incorrectamente el evento personalizado at-content-rendering-succeeded cuando no se procesaban ofertas. Ahora se activa el evento correcto, at-content-rendering-no-offers.
- Se han agregado eventToken y responseTokens al objeto de error para el evento personalizado at-content-rendering-failed.

## v0.19.2 (14 de febrero de 2023)

- Se ha corregido un problema que permitía que el tiempo de espera se estableciera en un elemento de datos.

## v0.19.1 (3 de febrero de 2023)

- Actualizado para admitir `at.js` Versión 2.10.1
- Los parámetros de mbox personalizados de cliente ahora admiten correctamente la notación de puntos
- Las llamadas de envío ya no se realizan en VEC

## v0.19.0 (19 de septiembre de 2022)

- Actualizado para admitir `at.js` Versión 2.10.0
- Se ha agregado compatibilidad con el seguimiento entre dominios.

## v0.18.0 (1 de junio de 2022)

- Actualizado para admitir `at.js` Versión 2.9.0
- Se ha añadido la compatibilidad con User Agent Client Hints.

## v0.17.1 (28 de enero de 2022)

- Actualizado para admitir `at.js` Versión 2.8.1
- Fijo `pageLoad` no asignado a `target-global-mbox` en modo de ejecución híbrida ODD
- Se ha corregido un problema con los detalles de análisis para `mbox` solicitud
- Se han actualizado las dependencias de desarrollo para corregir las vulnerabilidades de seguridad

## v0.17.0 (7 de enero de 2022)

- Actualizado para admitir `at.js` v2.8.0, que ahora recopila datos de uso de funciones y telemetría de rendimiento.  Los datos personales no se recopilan. Para excluirse de esta función, establezca `telemetryEnabled` hasta `false` in `targetGlobalSettings`.

## v0.16.0 (28 de octubre de 2021)

- Actualizado para admitir `at.js` La versión 2.7.0 ya está disponible para su descarga en Adobe Target.

## v0.15.2 (16 de agosto de 2021)

- Actualizado para admitir `at.js` 2.6.1.
- Inicialice la toma de decisiones en el dispositivo al iniciar, independientemente del evento de carga de página.
- Ahora, la toma de decisiones en el dispositivo se puede utilizar en la primera visita después de descargar el artefacto.

## v0.15.1 (20 de julio de 2021)

- Se ha corregido un problema con un conflicto de nombre de función `stringify`, que provocaba que se generaran valores de UUID incorrectos para `sessionId`, `requestId`, etc.

## v0.15.0 (16 de julio de 2021)

- Añadir atributo seguro a las cookies cada vez que `at.js` La configuración secureOnly se establece en true
- Los tokens de respuesta ya están disponibles al utilizar `triggerView()`
- Se ha corregido un error relacionado con el evento `CONTENT_RENDERING_NO_OFFERS`. Ahora se activa correctamente cuando no hay contenido devuelto desde Target
- Los detalles de las métricas de clic de A4T se devuelven correctamente al usar solicitudes de captura previa.
- La generación UUID ya no utiliza `Math.random()`, sino que depende de `window.crypto`
- La caducidad de la cookie `sessionId` se amplía correctamente en cada llamada de red
- La inicialización de la caché de la vista SPA ahora se gestiona correctamente y respeta la configuración `viewsEnable`

## v0.14.2 (2 de junio de 2021)

- Se ha corregido un error por el que el paquete final contenía dos `at.js` versiones, una con Toma de decisiones en el dispositivo y otra sin.

## v0.14.1 (19 de mayo de 2021)

- Se ha solucionado una regresión introducida con la versión 0.14 en la que la acción Cargar destinatario activaba llamadas de mbox globales

## v0.14 (14 de mayo de 2021)

- Se ha añadido una nueva acción Cargar destinatario con [Toma de decisiones en el dispositivo](./overview.md#load-target-with-on-device-decisioning), que carga 2.5 con capacidades de toma de decisiones en el dispositivo`at.js`
- Actualizado `at.js` a 2.5


## v0.13.7 (25 de marzo de 2021)

- Se ha corregido un problema por el que `targetPageParams` se incluía en las solicitudes de mbox. `targetPageParams` solo debe incluirse en las solicitudes de `pageLoad`.
- Se ha corregido un problema con los objetos globales de documento y ventana en la extensión de etiqueta al reemplazar las dependencias de objeto global por referencias directas a ellos.
- Actualizado `at.js` a 2.4.1.

## v0.13.6 (25 de enero de 2021)

- Añade la compatibilidad con el ID de plataforma/perfil unificado en los ID de cliente de API de entrega
- Corrige los problemas de introducción de etiquetas con estilo no válido
- Se ha actualizado at.s a la versión 2.4.0
- Se ha solucionado un problema en el que los parámetros no definidos podían dar como resultado solicitudes de envío incorrectas

## v0.13.4 (25 de noviembre de 2020)

- Se ha corregido un error que hacía que los parámetros de mbox no se mostraran en la IU
- Actualizaciones de promoción de la marca
- Se ha actualizado el `at.js` versión 2.3.3

## v0.13.3 (24 de julio de 2020)

- Se ha corregido un error por el que los vínculos de modo de control de calidad no funcionaban en actividades inactivas.
- Se ha corregido un error por el que la extensión fallaba si un script o código agrega la propiedad `default` a `window` o `document`.

## v0.13.2 (15 de junio de 2020)

- Se ha corregido un problema que se producía al usar CNAME y la anulación de perímetros, donde `at.js` 1.x podría crear incorrectamente el dominio del servidor, lo que provocaría un error en la solicitud de Target
- Se ha corregido un problema en el cual, al usar la extensión de etiquetas v2 para las extensiones de etiquetas Target y Adobe Analytics, Target demoraba la llamada de sendBeacon de Analytics.
- Se ha mejorado la configuración de `deviceIdLifetime` al permitir que sea reemplazable mediante `targetGlobalSettings`.

## v0.13.0 (25 de marzo de 2020)

- Actualizado `at.js` a la versión 2.3.
- Se añadió compatibilidad de Mbox global de Target en la API de adobe.target.getOffer.
- Se corrigió un problema en el que los parámetros y los parámetros de carga de página no se procesaban correctamente.

## v0.12.0 (10 de octubre de 2019)

- Actualizado `at.js` a la versión 2.2.
- Se ha mejorado el rendimiento de las integraciones entre la biblioteca de ID de Experience Cloud (ECID) 4.4 y `at.js` 2.2.
- Anteriormente, la biblioteca ECID realizaba dos llamadas de bloqueo antes de `at.js` podría recuperar experiencias. Esto se ha reducido a una sola llamada, lo que mejora significativamente el rendimiento.

>[!NOTE]
>Actualice la extensión de etiqueta de ECID a la versión 4.4.1 para disfrutar de esta mejora de rendimiento.

## v0.11.1 (31 de julio de 2019)

- Versión actualizada para utilizar `at.js` 2.1.1
- Se añadió una corrección para la gestión de parámetros.

## v0.11.0 (3 de junio de 2019)

- Nueva extensión de etiquetas compatible con `at.js` 2,1
