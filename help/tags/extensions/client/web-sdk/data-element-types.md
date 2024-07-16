---
title: Tipos de elementos de datos en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de los distintos tipos de elementos de datos que proporciona la extensión de etiqueta del SDK web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: fbca8a47c500e89d82cf636e8cb639f2bb59c2e6
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 5%

---


# Tipos de elementos de datos

Después de establecer los [tipos de acción](action-types.md) en la [extensión de etiqueta del SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de elementos de datos. Esta página describe los tipos de elementos de datos disponibles.

## Mapa de identidad {#identity-map}

Un mapa de identidad permite establecer identidades del visitante de la página web. Un mapa de identidad consta de áreas de nombres, como `CRMID`, `Phone` o `Email`, con cada área de nombres que contiene uno o más identificadores. Por ejemplo, si la persona del sitio web ha proporcionado dos números de teléfono, el área de nombres del teléfono debe contener dos identificadores.

En el elemento de datos [!UICONTROL mapa de identidad], debe proporcionar la siguiente información para cada identificador:

* **[!UICONTROL ID]**: El valor que identifica al visitante. Por ejemplo, si el identificador pertenece al área de nombres _phone_, el [!UICONTROL ID] puede ser _555-555-5555_. Este valor generalmente se deriva de una variable de JavaScript o de algún otro dato de la página, por lo que es mejor crear un elemento de datos que haga referencia a los datos de la página y, a continuación, hacer referencia al elemento de datos en el campo [!UICONTROL ID] dentro del elemento de datos [!UICONTROL mapa de identidad]. Si, al ejecutarse en la página, el valor de ID no es una cadena rellenada, el identificador se eliminará automáticamente del mapa de identidad.
* **[!UICONTROL Estado autenticado]**: Una selección que indica si el visitante está autenticado.
* **[!UICONTROL Principal]**: una selección que indica si el identificador debe usarse como identificador principal del individuo. Si no se marca ningún identificador como principal, el ECID se utilizará como identificador principal.

![Imagen de la interfaz de usuario que muestra la pantalla Editar elemento de datos.](assets/identity-map-data-element.png)

>[!TIP]
>
>El Adobe recomienda enviar identidades que representen a una persona, como `Luma CRM Id`, como la identidad principal.
>
>Si el mapa de identidad contiene el identificador de persona (p. ej. `Luma CRM Id`), entonces el identificador de persona se convertirá en el identificador principal. De lo contrario, `ECID` se convierte en la identidad principal.

No debe proporcionar un [!DNL ECID] al crear un mapa de identidad. Al utilizar el SDK, se genera automáticamente un [!DNL ECID] en el servidor y se incluye en el mapa de identidad.

El elemento de datos del mapa de identidad se usa a menudo en combinación con el tipo de elemento de datos [[!UICONTROL XDM object]](#xdm-object) y el tipo de acción [[!UICONTROL Establecer consentimiento]](action-types.md#set-consent).

Más información sobre [Servicio de identidad de Adobe Experience Platform](../../../../identity-service/home.md).

## Objeto XDM {#xdm-object}

El formato de los datos a XDM es más sencillo con el elemento de datos de objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y la zona protegida de Adobe Experience Platform correctos. Después de seleccionar el esquema, verá la estructura del esquema, que puede rellenar fácilmente.

![Imagen de interfaz de usuario que muestra la estructura de objetos XDM.](assets/XDM-object.png)

Tenga en cuenta que cuando abre ciertos campos del esquema, como `web.webPageDetails.URL`, algunos elementos se recopilan automáticamente. Aunque varios elementos se recopilan automáticamente, puede sobrescribir cualquiera, si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Rellene únicamente los datos que le interesen recopilar. Todo lo que no se rellene se omitirá cuando se envíen los datos a las soluciones.

## Variable {#variable}

Puede crear objetos de carga útil usando el elemento de datos **[!UICONTROL Variable]**. Se admiten los objetos [!UICONTROL XDM] y [!UICONTROL Data].

* Al seleccionar [!UICONTROL XDM], seleccione la [!UICONTROL zona protegida] y el [!UICONTROL esquema] deseados.
* Cuando seleccione [!UICONTROL Datos], seleccione las soluciones que desee. Las soluciones disponibles incluyen [!UICONTROL Adobe Analytics] y [!UICONTROL Adobe Target].

![Imagen de la interfaz de usuario de etiquetas que muestra las opciones del elemento de datos.](assets/variable-data-element.png)

Después de crear este elemento de datos, puede usar la acción [Actualizar variable](./action-types.md#update-variable) para modificarlo. Cuando esté listo, puede incluir este elemento de datos en la acción [Enviar evento](./action-types.md#send-event) para enviar datos a un conjunto de datos.

## Medios: calidad de la experiencia {#quality-experience}

Un elemento de datos de **[!UICONTROL Calidad de la experiencia]** es útil cuando se envían eventos de medios de streaming a Adobe Experience Platform. Puede añadir este elemento al crear una sesión de contenido y los siguientes eventos de contenido contendrán datos actualizados de calidad de la experiencia.

![Imagen de la interfaz de usuario que muestra la pantalla Crear elemento de datos de calidad de la experiencia.](assets/qoe-data-element.png)

## Pasos siguientes {#next-steps}

Obtenga información acerca de casos de uso específicos como [acceso al ECID](accessing-the-ecid.md).
