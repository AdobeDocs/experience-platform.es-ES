---
title: Introducción Al Reenvío De Eventos
description: Siga este tutorial paso a paso para empezar a utilizar el reenvío de eventos en Adobe Experience Platform.
source-git-commit: 1d3415146335d3011963c969d5b6aeea1f1a51d0
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 48%

---

# Introducción al reenvío de eventos

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Para utilizar el reenvío de eventos en Adobe Experience Platform, los datos deben enviarse a Adobe Experience Platform Edge Network mediante una o varias de las tres opciones siguientes:

* [SDK web de Adobe Experience Platform](../../extensions/web/sdk/overview.md)
* [SDK de Adobe Experience Platform Mobile](https://sdkdocs.com)
* [API de servidor a servidor](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html?lang=en)

>[!NOTE]
>El SDK web de Platform y el SDK de Platform Mobile no requieren la implementación mediante etiquetas en Adobe Experience Platform. Sin embargo, el método recomendado es utilizar etiquetas para implementar estos SDK.

Después de enviar datos a Edge Network, puede activar las soluciones de Adobe para enviar datos allí. Para enviar datos a una solución que no sea de Adobe, configúrela en el reenvío de eventos.

## Requisitos previos

* Adobe Experience Platform Collection Enterprise (póngase en contacto con su administrador de cuentas para conocer los precios)
* Reenvío de eventos en Adobe Experience Platform
* SDK web o móvil de Adobe Experience Platform, configurados para enviar datos a Edge Network
* Asignación de datos al modelo de datos de Experience (XDM) (esta asignación se puede realizar con etiquetas)

## Creación de un esquema XDM

En Adobe Experience Platform, puede crear su propio esquema.

1. Para crear un esquema, seleccione **[!UICONTROL Esquemas]** > **[!UICONTROL Crear esquema]** y elija la opción **[!UICONTROL XDM ExperienceEvent]**.

1. Asigne al esquema un nombre y una descripción breve.

1. Puede agregar el grupo de campos &quot;Detalles web de ExperienceEvent&quot; seleccionando **[!UICONTROL Agregar]** junto a **[!UICONTROL Grupos de campos]**.

   >[!NOTE]
   >
   >Si lo desea, se pueden agregar varios grupos de campos.

1. Guarde el esquema y anote el nombre que le ha asignado.

Para obtener más información sobre esquemas, consulte la [Ayuda del sistema del modelo de datos de Experience (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es).

## Crear una propiedad de reenvío de eventos

En la interfaz de usuario de la recopilación de datos, cree una propiedad de tipo &quot;Edge&quot;.

1. Seleccione **[!UICONTROL Nueva propiedad]**.

1. Asigne un nombre a la propiedad.

1. Elija el tipo de plataforma &quot;Edge&quot;.

1. Seleccione **[!UICONTROL Guardar]**.

Después de crear la propiedad, vaya a la pestaña **[!UICONTROL Entornos]** de la nueva propiedad y tome
nota de los ID de entorno. Si la organización de Adobe utilizada en el conjunto de datos difiere de la organización de Adobe utilizada en el reenvío de eventos, puede copiar el ID de entorno de la pestaña **[!UICONTROL Environments]** y pegarlo al crear un conjunto de datos. De lo contrario, puede seleccionar el entorno de un menú desplegable.

## Crear un conjunto de datos

Para crear el conjunto de datos en Adobe Experience Platform, utilice el ID de entorno generado al crear la propiedad de reenvío de eventos.

1. Utilice el vínculo del carril izquierdo de la interfaz de usuario de la recopilación de datos para abrir la interfaz de conjuntos de datos.

1. Seleccione **[!UICONTROL Datastreams]**.

1. Asigne un nombre a la configuración y proporcione una descripción opcional.
La descripción ayuda a identificar las configuraciones en una lista de varias configuraciones.

1. Seleccione **[!UICONTROL Guardar]**.



## Habilitar el reenvío de eventos

A continuación, configure la red perimetral para enviar datos al reenvío de eventos y a otros productos de Adobe.

1. En la interfaz de usuario de los conjuntos de datos, seleccione la propiedad que ha creado.

1. Seleccione el entorno Desarrollo, Producción o Ensayo.

   O bien, para enviar datos a un entorno de reenvío de eventos fuera de la organización de Adobe, seleccione **[!UICONTROL Switch to Advanced Mode]** y pegue un ID. El ID se proporciona al crear una propiedad de reenvío de eventos.

1. Active las herramientas necesarias y configúrelas según sea necesario.

   * Adobe Analytics requiere un ID del grupo de informes.

   * El reenvío de eventos en Adobe Experience Platform requiere un ID de propiedad y un ID de entorno. Es la ruta de publicación de la propiedad de reenvío de eventos.

Después de realizar la configuración, anote los ID de entorno para la nueva propiedad.

## Configurar la extensión del SDK web de etiquetas para enviar datos al conjunto de datos creado anteriormente

Cree su propiedad en la interfaz de usuario de recopilación de datos y, a continuación, utilice la extensión web SDK de Adobe Experience Platform para configurarla.

1. Asigne un nombre a la propiedad.

   Puede tener varias instancias de Alloy. Por ejemplo, puede tener diferentes propiedades de seguimiento previo y posterior a Paywall.

1. Seleccione el ID de la organización.

1. Seleccione el dominio de Edge.

Consulte la [documentación de la extensión del SDK web](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html?lang=es) para obtener más opciones de configuración.

## Creación de una regla de etiqueta para enviar datos al SDK web de Platform

Una vez que se haya implementado lo anterior, genere definiciones de datos, reglas, etc. que usen el reenvío de eventos y las etiquetas, pero que solo necesiten una solicitud de la página.

Cree una regla de carga de página con la extensión del SDK web de Platform y el tipo de acción Enviar evento:

1. Abra la pestaña **[!UICONTROL Reglas]** y seleccione **[!UICONTROL Crear nueva regla]**.

1. Asigne un nombre a la regla.

1. Seleccione **[!UICONTROL Añadir eventos]**.

1. Seleccione una extensión y uno de los tipos de evento disponibles para dicha extensión para añadir un evento y, a continuación, especifique la configuración del evento. Por ejemplo, seleccione **[!UICONTROL Core - Ventana cargada]**.

1. Añada una acción con la extensión del SDK web de Platform. Seleccione **[!UICONTROL Enviar evento]** de la lista **[!UICONTROL Tipo de acción]**, escoja la instancia deseada (instancia de Alloy configurada anteriormente) y, a continuación, elija un elemento de datos para añadirlo al bloque de datos XDM en la visita de Alloy.

1. Deje el resto de la configuración como predeterminada para este ejemplo y seleccione **[!UICONTROL Guardar]**.

Para otro ejemplo, puede crear una regla que envíe la capa de datos a Edge si el usuario coloca el ratón sobre un botón determinado.

## Resumen

Con lo siguiente en su lugar, ahora puede crear reglas de reenvío de eventos para reenviar datos a destinos que no sean de Adobe.

* Esquema del modelo de datos de Experience (tenga en cuenta el nombre que le ha asignado).
* Una propiedad de reenvío de eventos (realice un seguimiento del ID de propiedad y los ID de entorno).
* Un conjunto de datos (observe el ID de entorno, que no debe confundirse con el ID de entorno del reenvío de eventos).
* Una propiedad de etiqueta
