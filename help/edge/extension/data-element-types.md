---
title: Tipos de elementos de datos en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de los distintos tipos de elementos de datos que proporciona la extensión de etiqueta del SDK web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# Tipos de elementos de datos

Después de configurar su [tipos de acción](action-types.md) en el [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), configure los tipos de elementos de datos.

Esta página describe los tipos de elementos de datos disponibles.


## ID de combinación de eventos

Este elemento de datos proporciona un ID de combinación de eventos cuando se utiliza. No se necesita ninguna configuración para este elemento de datos. El elemento de datos que se proporciona permanece igual hasta que el visitante abandona la página o hasta que se utiliza el tipo de acción Restablecer ID de combinación de eventos.

## Mapa de identidad

Un mapa de identidad permite establecer identidades del visitante de la página web. Un mapa de identidad consta de áreas de nombres, como _phone_ o _email_, con cada área de nombres que contiene uno o más identificadores. Por ejemplo, si la persona del sitio web ha proporcionado dos números de teléfono, el área de nombres del teléfono debe contener dos identificadores.

En el [!UICONTROL Mapa de identidad] Para cada elemento de datos, debe proporcionar los siguientes datos para cada identificador:

* **[!UICONTROL ID]**: El valor que identifica al visitante. Por ejemplo, si el identificador pertenece a _phone_ namespace, la variable [!UICONTROL ID] puede ser _555-555-5555_. Este valor generalmente se deriva de una variable JavaScript o de algún otro dato de la página, por lo que es mejor crear un elemento de datos que haga referencia a los datos de página y, a continuación, hacer referencia al elemento de datos en la [!UICONTROL ID] dentro del campo [!UICONTROL Mapa de identidad] elemento de datos. Si, al ejecutarse en la página, el valor de ID no es una cadena rellenada, el identificador se eliminará automáticamente del mapa de identidad.
* **[!UICONTROL Estado autenticado]**: una selección que indica si el visitante está autenticado.
* **[!UICONTROL Principal]**: una selección que indica si el identificador debe utilizarse como identificador principal del individuo. Si no se marca ningún identificador como principal, el ECID se utilizará como identificador principal.

No debe proporcionar un ECID al crear un mapa de identidad. Al utilizar el SDK, se genera automáticamente un ECID en el servidor y se incluye en el mapa de identidad.

El elemento de datos del mapa de identidad se utiliza a menudo junto con el [[!UICONTROL Objeto XDM] tipo de elemento de datos](#xdm-object) y el [[!UICONTROL Definir consentimiento] tipo de acción](action-types.md#set-consent).

Más información sobre [Servicio de identidad de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=es).

![](./assets/identity-map-data-element.png)

## Objeto XDM {#xdm-object}

Utilice el formato XDM para enviar cualquier dato al SDK web de Adobe Experience Platform. El formato de los datos es más sencillo con el elemento de datos de objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y la zona protegida de Adobe Experience Platform correctos. Después de seleccionar el esquema, verá la estructura del esquema, que puede rellenar fácilmente.

![](./assets/XDM-object.png)

Tenga en cuenta que cuando abre ciertos campos del esquema, como `web.webPageDetails.URL`Sin embargo, algunos elementos se recopilan automáticamente. Aunque varios elementos se recopilan automáticamente, puede sobrescribir cualquiera, si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Rellene únicamente los datos que le interesen recopilar. Todo lo que no se rellene se omitirá cuando se envíen los datos a las soluciones.
