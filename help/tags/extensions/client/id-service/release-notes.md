---
title: Notas de la versión de la extensión del servicio de identidad de Adobe Experience Cloud
description: Últimas notas de la versión de la extensión de etiqueta del servicio de identidad de Adobe Experience Cloud en Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 75%

---

# Notas de la versión de la extensión del servicio de identidad de Adobe Experience Cloud

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Este documento describe las notas de la versión de la extensión de Adobe Experience Cloud Identity Service. Para obtener las notas de la versión del propio servicio de identidad del Experience Cloud, consulte la [documentación del servicio de identidad](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=es).

## 17 de octubre de 2022

### Extensión de Experience Cloud ID 5.5.0

* La extensión ahora admite la versión 5.5.0 de [Visitor JS Client](https://github.com/Adobe-Marketing-Cloud/id-service). Consulte [Notas de la versión de Visitante](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0) para obtener actualizaciones específicas.

## 9 de marzo de 2022

### Extensión de Experience Cloud ID 5.4.0

* Esta versión contiene la última versión, Visitor 5.4.0, que tiene las siguientes actualizaciones:

   * Capacidad para configurar la duración de la cookie `s_ecid` mediante la configuración cookieLifetime
   * Actualización de un problema con el navegador Firefox que se produce cuando una página se carga en un iFrame secundario

## 10 de octubre de 2021

### Extensión de Experience Cloud ID 5.3.1

* Esta versión contiene la última versión, Visitor 5.3.0, que tiene las siguientes actualizaciones nuevas:

   * Algoritmo actualizado para generar ECID local
   * Última inclusión con `Secure` y `SameSite` indicadores para la cookie de privacidad
   * Se ha corregido un problema con el navegador Firefox cuando una página se carga en un iFrame secundario

## 12 de enero de 2021

### Extensión de Experience Cloud ID 5.2.0

* La actualización al parche de VisitorJS 5.2.0 con una corrección para DataElement de ECID no se pudo realizar cuando se recibió el consentimiento.

## 3 de noviembre de 2020

### Extensión de Experience Cloud ID 5.2.1

* Este parche contiene una corrección que permite la escritura de cookies desde un iFrame con el atributo `SameSite=None` en el explorador Google Chrome.

## 27 de octubre de 2020

### Extensión de Experience Cloud ID 5.1.0

* Añadir la configuración de `sameSiteCookie` para especificar el atributo `SameSite` de la cookie `AMCV`. Esta configuración admite los siguientes valores para el atributo `SameSite`:

   * `Strict`
   * `Lax`
   * `None`

Los detalles de estos valores de atributos se encuentran en [web.dev](https://web.dev/samesite-cookies-explained/) y [chromium](https://www.chromium.org/updates/same-site)


## 13 de agosto de 2020

### Extensión de Experience Cloud ID 5.0.1

* Actualización al parche de VisitorJS 5.0.1 con una corrección para agregar el indicador d_cf cuando la cadena de consentimiento de IAB haya cambiado.

## 15 de junio de 2020

### Extensión de Experience Cloud ID 5.0.0

* Añadiendo compatibilidad con `IAB TCF`: Transparencia y plataforma de consentimiento `Version 2.0`.

## 13 de abril de 2020

### Extensión de Experience Cloud ID 4.6.0

* Marcar `loadSSL` como activo de forma predeterminada. Todas las llamadas al servicio de identidad estarán en `https` de forma predeterminada. Los clientes pueden configurarlo como False si desean llamar a los servicios de identidad en un protocolo http desde las páginas que no sean ssl.
* Se ha actualizado la función utilizada para detectar la versión de Internet Explorer (IE) con el fin de corregir un problema del que informó ESLint.
* Se ha corregido un error que provocaba un problema de rendimiento en Internet-Explorer (IE) 11 cuando ECID recibía la aprobación previa de optIn y se actualizaba más tarde.

## 22 de enero de 2020

### Extensión de Experience Cloud ID 4.5.2

* Se ha actualizado visitor.js a la versión 4.5.2
* Visitor 4.5.1 incluye una corrección de errores para el complemento IAB de inclusión
* Se ha actualizado el método `setCustomerIDs` para rechazar cualquier ID vacío que se haya enviado.

## 7 de enero de 2020

### Extensión de Experience Cloud ID 4.4.2

* Se ha actualizado visitor.js a la versión 4.4.2
* Mejoras del método `getVisitorValues` para recuperar valores más rápido.


## 19 de septiembre de 2019

### Extensión de Experience Cloud ID 4.4.1

* Se ha actualizado visitor.js a la versión 4.4.1
* Se ha corregido un error para obtener la entrada de aprobaciones previas de inclusión
* Se cambió el nombre de VIDEO_ANALYTICS a MEDIA_ANALYTICS en preOptInApprovals

  ![](../../../images/ecid-media-analytics.png)

## 17 de julio de 2019

### Extensión de Experience Cloud ID 4.4.0

* Se ha actualizado visitor.js a la versión 4.4.0
* Ahora se admite el proceso de hash SHA256 para setCustomerIDs

  ![](../../../images/ecid-setCustomerIDs-hash.png)

## 13 de mayo de 2019

### Extensión Experience Cloud ID 4.3.1

* Se ha actualizado visitor.js en 4.3
* Se ha añadido el tipo de elemento de datos para ECID como parte de la extensión de etiqueta

  ![](../../../images/ecid-data-element.png)

## 9 de abril de 2019

### Extensión Experience Cloud ID 4.2.0

* Se ha actualizado visitor.js en 4.2, que incluye compatibilidad con el complemento IAB TCF de Audience Manager.

## 25 de febrero de 2019

### Extensión de Experience Cloud ID 4.1.0

* Se ha actualizado visitor.js a la versión 4.1, que actualizaba publishDestinations por cada nuevo cambio de API. Con esta actualización, la información del referente de la página se puede exponer durante la sincronización de ID si lo desea.

## 15 de febrero de 2019

### Extensión Experience Cloud ID 4.0.0

* Se ha actualizado visitor.js en 4.0
* Se han agregado opciones de configuración para el nuevo complemento de objeto integrado. La configuración del complemento se puede utilizar para eliminar llamadas de señalización y señalización de soluciones de Adobe con el fin de admitir mejor algunas normativas como el RGPD

  ![](../../../images/ext-mcid-opt-in.png)

## 20 de marzo de 2018

### Extensión Experience Cloud ID 3.1.0

* Se ha actualizado visitor.js en 3.1
* Se han agregado dos propiedades de configuración: `resetBeforeVersion` y `serverState`.
