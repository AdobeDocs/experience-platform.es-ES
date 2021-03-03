---
title: Tipos de elementos de datos en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de elementos de datos proporcionados por la extensión web SDK de Adobe Experience Platform en Adobe Experience Platform Launch.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 47%

---


# Tipos de elementos de datos

Después de establecer los [tipos de acción](action-types.md) en la [extensión del SDK web de Adobe Experience Platform](web-sdk-extension.md) para [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html), configure los tipos de elementos de datos.

Esta página describe los tipos de elementos de datos disponibles.

## ID de combinación de eventos

Este elemento de datos proporciona un ID de combinación de eventos cuando se utiliza. No se necesita ninguna configuración para este elemento de datos. El elemento de datos que se proporciona permanece igual hasta que el visitante abandona la página o hasta que se utiliza el tipo de acción Restablecer ID de combinación de eventos.

## Mapa de identidad

El elemento de datos de mapa de identidad permite crear identidades a partir de otros elementos de datos u otros valores que se especifiquen. Todas las identidades que cree deben estar vinculadas a una área de nombres correspondiente. Este elemento de datos proporciona un menú desplegable que muestra todos los espacios de nombres predeterminados y todos los que ha creado.

![](./assets/identity-map-data-element.png)

## Objeto XDM

Utilice el formato XDM para enviar cualquier dato al SDK web de Adobe Experience Platform. El formato de los datos es más sencillo con el elemento de datos de objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y el entorno limitado de Adobe Experience Platform correctos. Después de seleccionar el esquema, verá la estructura del esquema, que puede rellenar fácilmente.

![](./assets/XDM-object.png)

Tenga en cuenta que, cuando abre ciertos campos del esquema, como `web.webPageDetails.URL`, algunos elementos se recopilan automáticamente. Aunque se recopilen automáticamente varios elementos, puede sobrescribirlos si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Rellene solamente los fragmentos de información que le interese recopilar. Todo lo que no se rellena se omite al enviar los datos a las soluciones.
