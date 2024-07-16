---
title: Notas de la versión de la extensión de Adobe Target
description: Últimas notas de la versión de la extensión de etiqueta de Adobe Target en Adobe Experience Platform.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 95%

---

# Notas de la versión de Adobe Target

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## 16 de septiembre de 2021

### Extensión de Adobe Target 0.11.4

* Actualización a at.js v1.8.3
* Se agregaron los atributos `SameSite=None` y `Secure` al configurar las cookies

## 24 de julio de 2020

### Extensión de Adobe Target 0.11.3

* Se ha corregido un error por el que la extensión fallaba si un script o código agrega la propiedad `default` a `window` o `document`.

## 15 de junio de 2020

### Extensión de Adobe Target 0.11.2

* Se ha corregido un problema que se producía al usar CNAME y el reemplazo perimetral, por el cual at.js 1.x podía crear, de manera incorrecta, el dominio del servidor, lo que provocaba un error en la solicitud de Target.

## 25 de marzo de 2020

### Extensión de Adobe Target 0.11.1

* Se ha actualizado at.js a la versión 1.8.1.
* Se corrigió un problema en el que los parámetros y los parámetros de carga de página no se procesaban correctamente.

## 10 de octubre de 2019

### Extensión de Adobe Target 0.11.0

* Se ha actualizado at.js a la versión 1.8.
* Se ha mejorado el rendimiento de las integraciones entre la biblioteca de Experience Cloud ID (ECID) 4.4 y at.js 1.8.
* Anteriormente, la biblioteca de ECID realizaba dos llamadas de bloqueo antes de que at.js pudiera recuperar experiencias. Esto se ha reducido a una sola llamada, lo que mejora significativamente el rendimiento.

>[!NOTE]
>Actualice la extensión de etiqueta ECID para Adobe Experience Platform a la versión 4.4.1 para aprovechar esta mejora de rendimiento.

## 31 de julio de 2019

### Extensión de Adobe Target 0.10.1

* Revisión para parámetros que gestionan la extensión de etiqueta para Adobe Target

## 4 de mayo de 2019

### Extensión de Adobe Target 0.10.0

* Se ha corregido un problema de elementos de datos ocasionado por los cambios más recientes de Google Chrome.

## 14 de marzo de 2019

### Extensión de Adobe Target 0.9.3

* Versión actualizada de extensión para utilizar at.js 1.7.1.

## 20 de febrero de 2019

### Extensión de Adobe Target 0.9.2

* Se han corregido las condiciones de carrera entre las extensiones de Target y Analytics.

## 12 de febrero de 2019

### Extensión de Adobe Target 0.9.1

#### **Funcionalidades**

* Extensión actualizada para utilizar at.js 1.7.0 con la funcionalidad de privacidad de inclusión admitida mediante etiquetas para controlar cómo y cuándo se activa la etiqueta de Target. Consulte la documentación de etiquetas sobre cómo configurar la implementación de inclusión. Se ha agregado la posibilidad de personalizar si un parámetro de mbox que tenga un valor vacío debe enviarse a Target o no.

## 23 de enero de 2019

### Extensión de Adobe Target 0.8.4

* Actualización de at.js a la versión 1.6.4.
* Interfaz de usuario de extensión migrada a Adobe Spectrum.

## 15 de noviembre de 2018

### Extensión de Adobe Target 0.8.2

* Actualización de at.js a la versión 1.6.3.

## 24 de octubre de 2018

### Extensión de Adobe Target 0.8.1

* Actualización de at.js a la versión 1.6.2.

## 23 de agosto de 2018

### Extensión de Adobe Target 0.8.0

* Actualización de at.js a la versión 1.6.0.

## 10 de agosto de 2018

### Extensión de Adobe Target 0.7.2

* Cambios menores
* Se ha actualizado la propiedad de `exchangeUrl` en el archivo `extension.json`.

## 1 de agosto de 2018

### Extensión de Adobe Target 0.7.1

* Correcciones poco importantes.

## 18 de junio de 2018

### Extensión de Adobe Target 0.7.0

* Actualización de at.js a la versión 1.5.0.
* Se ha corregido un problema por el que Media Optimizer arrojaba un error de referencia nulo en IE 11.

## 15 de junio de 2018

### Extensión de Adobe Target 0.6.0

#### **Funcionalidades**

* Target Extension se ha actualizado para utilizar at.js v1.3.1. Al implementar Target con Analytics, ahora esperamos hasta que todas las llamadas de Target se hayan resuelto (incluidas las ofertas de redireccionamiento) antes de que Analytics se active, resolviendo la condición de carrera que existía anteriormente.

## 22 de febrero de 2018

### Extensión de Adobe Target 0.4.1

#### **Funcionalidades**

* Se ha agregado la lista de Adobe Exchange a extension.json.
* Se han añadido comprobaciones para verificar si Target está deshabilitado y Authoring está habilitado.

#### **Correcciones de errores**

* Se ha corregido un error en la extensión de Adobe Target que impedía que el Compositor de experiencias visuales mostrara la página al implementarla mediante etiquetas.

## 8 de febrero de 2018

### Extensión de Adobe Target 0.4.0

#### **Funcionalidades**

* Vistas actualizadas en pantallas de configuración de extensiones.
* Se ha actualizado at.js a la versión 1.2.3 (agrega compatibilidad con ofertas JSON).
