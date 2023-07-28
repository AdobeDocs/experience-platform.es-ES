---
title: Tipos de elementos de datos en la extensión SDK para web de Adobe Experience Platform
description: Obtenga información acerca de los distintos tipos de elementos de datos que proporciona la extensión de etiqueta del SDK web de Adobe Experience Platform.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 44fac57a30295b476910c0b37314eaebba175157
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 5%

---


# Tipos de elementos de datos

Después de configurar su [tipos de acción](action-types.md) en el [Extensión de etiqueta de SDK web de Adobe Experience Platform](web-sdk-extension-configuration.md), debe configurar los tipos de elementos de datos. Esta página describe los tipos de elementos de datos disponibles.

## Mapa de identidad {#identity-map}

Un mapa de identidad permite establecer identidades del visitante de la página web. Un mapa de identidad consta de áreas de nombres, como `CRMID`, `Phone` o `Email`, con cada área de nombres que contiene uno o más identificadores. Por ejemplo, si la persona del sitio web ha proporcionado dos números de teléfono, el área de nombres del teléfono debe contener dos identificadores.

En el [!UICONTROL Mapa de identidad] Para cada elemento de datos, debe proporcionar los siguientes datos para cada identificador:

* **[!UICONTROL ID]**: El valor que identifica al visitante. Por ejemplo, si el identificador pertenece a _phone_ namespace, la variable [!UICONTROL ID] puede ser _555-555-5555_. Este valor generalmente se deriva de una variable JavaScript o de algún otro dato de la página, por lo que es mejor crear un elemento de datos que haga referencia a los datos de página y, a continuación, hacer referencia al elemento de datos en la [!UICONTROL ID] dentro del campo [!UICONTROL Mapa de identidad] elemento de datos. Si, al ejecutarse en la página, el valor de ID no es una cadena rellenada, el identificador se eliminará automáticamente del mapa de identidad.
* **[!UICONTROL Estado autenticado]**: una selección que indica si el visitante está autenticado.
* **[!UICONTROL Principal]**: una selección que indica si el identificador debe utilizarse como identificador principal del individuo. Si no se marca ningún identificador como principal, el ECID se utilizará como identificador principal.

![Imagen de la IU que muestra la pantalla Editar elemento de datos.](assets/identity-map-data-element.png)

>[!TIP]
>
>El Adobe recomienda enviar identidades que representen a una persona, como `Luma CRM Id` como identidad principal.
>
>Si el mapa de identidad contiene el identificador de persona (por ejemplo, `Luma CRM Id`), el identificador de persona se convertirá en el identificador principal. De lo contrario, `ECID` se convierte en la identidad principal.

No debe proporcionar un [!DNL ECID] al crear un mapa de identidad. Al utilizar el SDK, una variable [!DNL ECID] se genera automáticamente en el servidor y se incluye en el mapa de identidad.

El elemento de datos del mapa de identidad se utiliza a menudo junto con el [[!UICONTROL Objeto XDM] tipo de elemento de datos](#xdm-object) y el [[!UICONTROL Definir consentimiento] tipo de acción](action-types.md#set-consent).

Más información sobre [Servicio de identidad de Adobe Experience Platform](../../../../identity-service/home.md).

## Objeto XDM {#xdm-object}

El formato de los datos a XDM es más sencillo con el elemento de datos de objeto XDM. Cuando abra este elemento de datos por primera vez, seleccione el esquema y la zona protegida de Adobe Experience Platform correctos. Después de seleccionar el esquema, verá la estructura del esquema, que puede rellenar fácilmente.

![Imagen de la IU que muestra la estructura de objetos XDM.](assets/XDM-object.png)

Tenga en cuenta que cuando abre ciertos campos del esquema, como `web.webPageDetails.URL`Sin embargo, algunos elementos se recopilan automáticamente. Aunque varios elementos se recopilan automáticamente, puede sobrescribir cualquiera, si es necesario. Todos los valores se pueden rellenar manualmente o con otros elementos de datos.

>[!NOTE]
>
>Rellene únicamente los datos que le interesen recopilar. Todo lo que no se rellene se omitirá cuando se envíen los datos a las soluciones.

## Variable {#variable}

Otra forma de crear objetos XDM es utilizar **[!UICONTROL Variable]** elemento de datos. Mientras que el elemento de datos del objeto XDM se crea cuando se hace referencia a él, como dentro de un `sendEvent` , el comando **[!UICONTROL Variable]** El elemento de datos de se puede actualizar mediante [!UICONTROL Actualizar variable] acciones. Para utilizar el elemento de datos, seleccione el esquema y la zona protegida de Adobe Experience Platform correctos.

![Imagen de la IU que muestra la pantalla Crear elemento de datos.](assets/variable-data-element.png)

Una vez creado este elemento de datos, puede utilizar [Actualizar variable](./action-types.md#update-variable) acciones para modificar el elemento de datos. A continuación, dentro de las acciones de enviar evento, utilice el elemento de datos variable para la opción XDM.

## Pasos siguientes {#next-steps}

Obtenga información acerca de casos de uso específicos como [acceso al ECID](accessing-the-ecid.md).
