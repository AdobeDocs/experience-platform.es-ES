---
title: Tipos de elementos de datos en la extensión del SDK web de Adobe Experience Platform
description: Obtenga información sobre los distintos tipos de elementos de datos proporcionados por la extensión de etiqueta del SDK web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# Tipos de elementos de datos

Una vez configurado el [tipos de acción](action-types.md) en el [Extensión de la etiqueta del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de elementos de datos. Esta página describe los tipos de elementos de datos disponibles.

## ID de combinación de eventos {#event-merge-id}

Este elemento de datos proporciona un ID de combinación de eventos cuando se utiliza. No se necesita ninguna configuración para este elemento de datos. El elemento de datos que se proporciona permanece igual hasta que el visitante abandona la página o hasta que el **[!UICONTROL Restablecer ID de combinación de eventos]** se utiliza el tipo de acción .

## Mapa de identidad {#identity-map}

Un mapa de identidad permite establecer identidades para el visitante de la página web. Un mapa de identidad consta de áreas de nombres, como _phone_ o _email_, con cada área de nombres que contiene uno o más identificadores. Por ejemplo, si la persona del sitio web ha proporcionado dos números de teléfono, el espacio de nombres del teléfono debe contener dos identificadores.

En el [!UICONTROL Mapa de identidad] elemento de datos , debe proporcionar los siguientes fragmentos de información para cada identificador:

* **[!UICONTROL ID]**: El valor que identifica al visitante. Por ejemplo, si el identificador pertenece al grupo _phone_ espacio de nombres, la variable [!UICONTROL ID] puede ser _555-555-5555_. Normalmente, este valor se deriva de una variable JavaScript o de algún otro fragmento de datos de la página, por lo que es mejor crear un elemento de datos que haga referencia a los datos de la página y luego hacer referencia al elemento de datos en la variable [!UICONTROL ID] dentro del [!UICONTROL Mapa de identidad] elemento de datos. Si, al ejecutarse en la página, el valor de ID es cualquier cosa excepto una cadena rellenada, el identificador se eliminará automáticamente del mapa de identidad.
* **[!UICONTROL Estado autenticado]**: Selección que indica si el visitante está autenticado.
* **[!UICONTROL Principal]**: Selección que indica si el identificador debe utilizarse como identificador principal del individuo. Si ningún identificador está marcado como principal, el ECID se utilizará como identificador principal.

![La imagen de la interfaz de usuario muestra la pantalla Editar elemento de datos .](./assets/identity-map-data-element.png)

No debe proporcionar una [!DNL ECID] al crear un mapa de identidad. Al utilizar el SDK, una [!DNL ECID] se genera automáticamente en el servidor y se incluye en el mapa de identidad.

El elemento de datos del mapa de identidad se utiliza a menudo junto con la variable [[!UICONTROL Objeto XDM] tipo de elemento de datos](#xdm-object) y [[!UICONTROL Establecer consentimiento] tipo de acción](action-types.md#set-consent).

Más información sobre [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md).

## Objeto XDM {#xdm-object}

El formato de los datos a XDM es más fácil con el elemento de datos del objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y la zona protegida de Adobe Experience Platform correctos. Después de seleccionar el esquema, verá la estructura del esquema, que puede rellenar fácilmente.

![La imagen de la interfaz de usuario muestra la estructura del objeto XDM.](assets/XDM-object.png)

Tenga en cuenta que, al abrir ciertos campos del esquema, como `web.webPageDetails.URL`, algunos elementos se recopilan automáticamente. Aunque se recopilen automáticamente varios elementos, puede sobrescribirlos si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Rellene solamente los fragmentos de información que le interese recopilar. Todo lo que no se rellena se omite al enviar los datos a las soluciones.

## Variable (Beta) {#variable}

>[!IMPORTANT]
>
>Actualmente se trata de una funcionalidad beta y está sujeta a cambios. Las versiones futuras pueden contener cambios de ruptura.

Otra forma de crear objetos XDM es usar la variable **[!UICONTROL Variable]** elemento de datos. Mientras que el elemento de datos del objeto XDM se crea cuando se hace referencia a él, como dentro de un `sendEvent` el comando **[!UICONTROL Variable]** el elemento de datos se puede actualizar mediante [!UICONTROL Actualizar variable] acciones. Para utilizar el elemento de datos, seleccione el entorno limitado y el esquema de Adobe Experience Platform correctos.

![La imagen de la interfaz de usuario muestra la pantalla Crear elemento de datos .](assets/variable-data-element.png)

Una vez creado este elemento de datos, puede utilizar [Actualizar variable](./action-types.md#update-variable) acciones para modificar el elemento de datos. A continuación, dentro de las acciones de eventos de envío, utilice el elemento de datos variable para la opción XDM.

## Pasos siguientes {#next-steps}

Obtenga información sobre casos de uso específicos como [acceso al ECID](accessing-the-ecid.md).
