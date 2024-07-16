---
title: Notas de la versión de la extensión Common Analytics Plugins
description: Últimas notas de la versión de la extensión de etiquetas Common Analytics Plugins en Adobe Experience Platform.
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 94%

---

# Notas de la versión de Common Analytics Plugins

## 3 de junio de 2022

### Extensión de complementos de Analytics comunes 3.0.7

#### Funcionalidades

* Los complementos que establecen cookies ahora utilizan el indicador seguro

## 23 de junio de 2021

### Extensión de complementos de Analytics comunes 3.0.6

#### Correcciones de errores

* Se ha corregido un problema en el cual getPercentPageViewed se dañaba al utilizar caracteres especiales

## 20 de mayo de 2021

### Extensión de complementos de Analytics comunes 3.0.5

#### Correcciones de errores

* Se ha corregido un problema por el cual getTimeParting no se inicializaba correctamente al utilizar la acción de inicialización genérica

## 26 de marzo de 2021

### Extensión de complementos de Analytics comunes 3.0.4

#### Correcciones de errores

* Se ha corregido un problema por el cual getPageLoadTime establecía variables incorrectamente en el objeto window
* Se ha corregido un problema por el cual getQueryParam devolvía indefinido en lugar de &quot;&quot; si queryParam no estaba presente en la cadena de consulta
* Se ha corregido un problema por el cual se mostraban números de versión incorrectos en la acción de inicialización

## 19 de marzo de 2021

### Extensión de complementos de Analytics comunes 3.0.2

#### Funcionalidades

* Todos los plug-ins se han actualizado para incluir automáticamente la información de versión como datos de contexto
* Se ha añadido el plug-in getPercentPageViewed
* Se han añadido elementos de datos para los siguientes plug-ins
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Estilos actualizados

## 9 de abril de 2020

### Extensión de complementos de Analytics comunes 2.2.0

#### Correcciones de errores

* Se ha corregido la redacción de las vistas de extensión

#### Funcionalidades

* Documentación actualizada en la acción initialize

## 5 de diciembre de 2019

### Extensión de complementos de Analytics comunes 2.1.1

#### Correcciones de errores

* Se ha corregido un problema que impedía la retrocompatibilidad con las versiones 2.0.X
* Se ha corregido un problema que hacía que los vínculos de documentación indicaran la documentación incorrecta
* Se ha corregido un problema en el que `getTimeSinceLastVisit` aparecía dos veces en la acción initialize

## 15 de noviembre de 2019

### Extensión de complementos de Analytics comunes 2.1.0

#### Correcciones de errores

* Se han vuelto a introducir acciones de plug-in individuales para admitir la compatibilidad con versiones anteriores
* Se ha corregido un problema con el complemento `cleanStr`
* Se ha corregido un problema con el complemento `getResponsiveLayout`
* Se ha corregido un problema con el complemento `getPageName`

#### Funcionalidades

* Actualización de versión para `getTimeParting`
* Actualización de versión para `numberSuite`
* Actualización de versión para `getNewRepeat`
* Documentación actualizada para todos los complementos

## 30 de octubre de 2019

### Extensión de complementos de Analytics comunes 2.0.3

#### Correcciones de errores

* Se ha solucionado el problema de los vínculos de documentación dañados

## 11 de octubre de 2019

### Extensión de complementos de Analytics comunes 2.0.2

#### Funcionalidades

* Se añadieron 15 complementos a la extensión
* Se ha creado una nueva acción initialize para facilitar la implementación

## 11 de julio de 2019

### Extensión de complementos de Analytics comunes 1.0.4

#### Funcionalidades

* Extensión publicada con siete plug-ins
* Acciones individuales para inicializar cada complemento
