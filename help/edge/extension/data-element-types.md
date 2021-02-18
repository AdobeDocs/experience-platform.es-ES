---
title: Tipos de elementos de datos en Adobe Experience Platform Web SDK Extension
description: Obtenga información sobre los distintos tipos de elementos de datos proporcionados por la extensión Adobe Experience Platform Web SDK en Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 78%

---


# Tipos de elementos de datos

Después de configurar los [tipos de acción](action-types.md) en la [extensión del SDK web de Adobe Experience Platform](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure los tipos de elementos de datos.

Esta página describe los tipos de elementos de datos disponibles.

## ID de combinación de eventos

Este elemento de datos proporciona un ID de combinación de eventos cuando se utiliza. No se necesita ninguna configuración para este elemento de datos. El elemento de datos que se proporciona permanece igual hasta que el visitante abandona la página o hasta que se utiliza el tipo de acción Restablecer ID de combinación de eventos.

## Mapa de identidad

El elemento de datos de mapa de identidad permite crear identidades a partir de otros elementos de datos u otros valores que se especifiquen. Todas las identidades que cree deben estar vinculadas a una área de nombres correspondiente. Este elemento de datos proporciona un menú desplegable que muestra todas las áreas de nombres predeterminadas, así como todas las que haya creado.

![](./assets/identity-map-data-element.png)

## Objeto XDM

Los datos que envíe al SDK para web de Adobe Experience Platform deben estar en formato XDM. El formato de los datos es más sencillo con el elemento de datos de objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y el entorno limitado de Adobe Experience Platform correctos. Después de haber seleccionado su esquema verá la estructura de su esquema, que puede completar fácilmente.

![](./assets/XDM-object.png)

Tenga en cuenta que, cuando abre ciertos campos del esquema, como `web.webPageDetails.URL`, algunos elementos se recopilan automáticamente. Aunque varios elementos se recopilan automáticamente, tiene la opción de sobrescribir cualquiera, si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Solo necesita completar los datos que le interese recopilar. Todo lo que no se rellene se omitirá cuando se envíen los datos a las soluciones.
