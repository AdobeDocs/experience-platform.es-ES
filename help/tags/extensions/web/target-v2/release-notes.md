---
title: Notas de la versión de la extensión Adobe Target v2
description: Últimas notas de la versión de la extensión de etiqueta Adobe Target v2 en Adobe Experience Platform.
source-git-commit: 573c13f5136a4efc3accf2838783a91ea914e949
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 78%

---

# Notas de la versión de la extensión de Adobe Target v2

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 19 de mayo de 2021

### Extensión 0.14.1 de la versión 2.0 de Adobe Target

- Se ha solucionado una regresión introducida con la versión 0.14 en la que la acción Cargar destinatario activaba llamadas de mbox globales

## 14 de mayo de 2021

### Extensión 0.14 de la versión 2.0 de Adobe Target

- Se ha añadido una nueva acción Cargar destinatario con [Toma de decisiones en el dispositivo](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/targetv2-extension/adobe-target-extension-v2.html?lang=es#load-target-with-on-device-decisioning), que carga at.js 2.5 con capacidades de toma de decisiones en el dispositivo
- Se ha actualizado at.js a la versión 2.5


## 25 de marzo de 2021

### Extensión 0.13.7 de la versión 2.0 de Adobe Target

- Se ha corregido un problema por el que `targetPageParams` se incluía en las solicitudes de mbox. `targetPageParams` solo debe incluirse en las solicitudes de `pageLoad`.
- Se ha corregido un problema con los objetos globales de documento y ventana en la extensión de etiqueta al reemplazar las dependencias de objeto globales por referencias directas a ellos.
- Se ha actualizado at.js a la versión 2.4.1.

## 25 de enero de 2021

### Extensión 0.13.6 de la versión 2.0 de Adobe Target

- Añade la compatibilidad con el ID de plataforma/perfil unificado en los ID de cliente de API de entrega
- Corrige los problemas de introducción de etiquetas con estilo no válido
- Se ha actualizado at.s a la versión 2.4.0
- Se ha solucionado un problema en el que los parámetros no definidos podían dar como resultado solicitudes de envío incorrectas

## 25 de noviembre de 2020

### Extensión 0.13.4 de la versión 2.0 de Adobe Target

- Se ha corregido un error que hacía que los parámetros de mbox no se mostraran en la IU
- Actualizaciones de promoción de la marca
- Actualización de at.js a la versión 2.3.3.

## 24 de julio de 2020

### Extensión 0.13.3 de la versión 2.0 de Adobe Target

- Se ha corregido un error por el que los vínculos de modo de control de calidad no funcionaban en actividades inactivas.
- Se ha corregido un error por el que la extensión fallaba si un script o código agrega la propiedad `default` a `window` o `document`.

## 15 de junio de 2020

### Extensión 0.13.2 de la versión 2.0 de Adobe Target

- Se ha corregido un problema que se producía al usar CNAME y el reemplazo perimetral, por el cual at.js 1.x podía crear, de manera incorrecta, el dominio del servidor, lo que provocaba un error en la solicitud de Target.
- Se ha corregido un problema en el cual, al usar la extensión de etiqueta v2 para las extensiones de etiqueta Target y Adobe Analytics, Target demoraba la llamada de sendBeacon de Analytics.
- Se ha mejorado la configuración de `deviceIdLifetime` al permitir que sea reemplazable mediante `targetGlobalSettings`.

## 25 de marzo de 2020

### Extensión 0.13.0 de la versión 2.0 de Adobe Target

- Se ha actualizado at.js a la versión 2.3.
- Se añadió compatibilidad de Mbox global de Target en la API de adobe.target.getOffer.
- Se corrigió un problema en el que los parámetros y los parámetros de carga de página no se procesaban correctamente.

## 10 de octubre de 2019

### Extensión 0.12.0 de la versión 2.0 de Adobe Target

- Se ha actualizado at.js a la versión 2.2.
- Se ha mejorado el rendimiento de las integraciones entre la biblioteca de Experience Cloud ID (ECID) 4.4 y at.js 2.2.
- Anteriormente, la biblioteca de ECID realizaba dos llamadas de bloqueo antes de que at.js pudiera recuperar experiencias. Esto se ha reducido a una sola llamada, lo que mejora significativamente el rendimiento.

>[!NOTE]
>Actualice la extensión de la etiqueta ECID a la versión 4.4.1 para aprovechar esta mejora de rendimiento.

## 31 de julio de 2019

### Extensión 0.11.1 de la versión 2.0 de Adobe Target

- Versión actualizada para utilizar at.js 2.1.1.
- Se añadió una corrección para la gestión de parámetros.

## 3 de junio de 2019

### Extensión 0.11.0 de la versión 2.0 de Adobe Target

- Nueva extensión de etiqueta compatible con at.js 2.1
