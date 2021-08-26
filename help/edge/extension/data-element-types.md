---
title: Tipos de elementos de datos en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de elementos de datos proporcionados por la extensión de etiqueta del SDK web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# Tipos de elementos de datos

Después de establecer los [tipos de acción](action-types.md) en la [extensión de etiqueta del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), configure los tipos de elementos de datos.

Esta página describe los tipos de elementos de datos disponibles.


## ID de combinación de eventos

Este elemento de datos proporciona un ID de combinación de eventos cuando se utiliza. No se necesita ninguna configuración para este elemento de datos. El elemento de datos que se proporciona permanece igual hasta que el visitante abandona la página o hasta que se utiliza el tipo de acción Restablecer ID de combinación de eventos.

## Mapa de identidad

Un mapa de identidad permite establecer identidades para el visitante de la página web. Un mapa de identidad consta de áreas de nombres, como _phone_ o _email_, con cada área de nombres que contiene uno o más identificadores. Por ejemplo, si la persona del sitio web ha proporcionado dos números de teléfono, el espacio de nombres del teléfono debe contener dos identificadores.

En el elemento de datos [!UICONTROL Identity map] , debe proporcionar los siguientes datos para cada identificador:

* **[!UICONTROL ID]**: El valor que identifica al visitante. Por ejemplo, si el identificador pertenece al espacio de nombres _phone_, [!UICONTROL ID] puede ser _555-555-5555_. Este valor generalmente se deriva de una variable JavaScript o de algún otro dato de la página, por lo que es mejor crear un elemento de datos que haga referencia a los datos de la página y luego hacer referencia al elemento de datos en el campo [!UICONTROL ID] dentro del elemento de datos [!UICONTROL Identity map] . Si, al ejecutarse en la página, el valor de ID es cualquier cosa excepto una cadena rellenada, el identificador se eliminará automáticamente del mapa de identidad.
* **[!UICONTROL Estado]** autenticado: Selección que indica si el visitante está autenticado.
* **[!UICONTROL Principal]**: Selección que indica si el identificador debe utilizarse como identificador principal del individuo. Si ningún identificador está marcado como principal, el ECID se utilizará como identificador principal.

No debe proporcionar un ECID al crear un mapa de identidad. Al utilizar el SDK, se genera automáticamente un ECID en el servidor y se incluye en el mapa de identidad.

El elemento de datos del mapa de identidad se utiliza a menudo junto con el tipo de elemento de datos [[!UICONTROL XDM object] y el tipo de acción [[!UICONTROL Set permission]](action-types.md#set-consent).](#xdm-object)

Obtenga más información sobre [Servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=es).

![](./assets/identity-map-data-element.png)

## Objeto XDM {#xdm-object}

Utilice el formato XDM para enviar cualquier dato al SDK web de Adobe Experience Platform. El formato de los datos es más sencillo con el elemento de datos de objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y el entorno limitado de Adobe Experience Platform correctos. Después de seleccionar el esquema, verá la estructura del esquema, que puede rellenar fácilmente.

![](./assets/XDM-object.png)

Tenga en cuenta que al abrir ciertos campos del esquema, como `web.webPageDetails.URL`, algunos elementos se recopilan automáticamente. Aunque se recopilen automáticamente varios elementos, puede sobrescribirlos si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Rellene solamente los fragmentos de información que le interese recopilar. Todo lo que no se rellena se omite al enviar los datos a las soluciones.
