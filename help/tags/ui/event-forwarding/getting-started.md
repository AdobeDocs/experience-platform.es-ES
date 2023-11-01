---
title: Introducción al reenvío de eventos
description: Siga este tutorial paso a paso para empezar a utilizar el reenvío de eventos en Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 78%

---

# Introducción al reenvío de eventos

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Para utilizar el reenvío de eventos en Adobe Experience Platform, los datos deben enviarse a Adobe Experience Platform Edge Network mediante una o varias de las tres opciones siguientes:

* [SDK web de Adobe Experience Platform](../../extensions/client/web-sdk/overview.md)
* [SDK móvil de Adobe Experience Platform](https://sdkdocs.com)
* [API de servidor a servidor](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-apis/dcs-s2s.html)

>[!NOTE]
>El SDK web de Platform y el SDK móvil de Platform no requieren implementación a través de etiquetas en Adobe Experience Platform. Sin embargo, el método recomendado es utilizar etiquetas para implementar estos SDK.

Después de enviar datos a Edge Network, puede activar las soluciones de Adobe para enviar datos allí. Para enviar datos a una solución que no sea de Adobe, configúrela en el reenvío de eventos.

## Requisitos previos

* Adobe Real-Time CDP Connections, Prime o Ultimate (póngase en contacto con el equipo de su cuenta de Adobe para conocer los precios)
* Reenvío de eventos en Adobe Experience Platform
* SDK web o móvil de Adobe Experience Platform, configurados para enviar datos a Edge Network
* Los datos deben asignarse al modelo de datos de experiencia (XDM) (esta asignación puede realizarse utilizando etiquetas)

## Creación de un esquema XDM

En Adobe Experience Platform, puede crear su propio esquema.

1. Para crear un esquema, seleccione **[!UICONTROL Esquemas]** > **[!UICONTROL Crear esquema]** y elija la opción **[!UICONTROL XDM ExperienceEvent]**.

1. Asigne al esquema un nombre y una descripción breve.

1. Puede añadir el grupo de campo Detalles web de ExperienceEvent seleccionando **[!UICONTROL Añadir]** junto a **[!UICONTROL Grupos de campos]**.

   >[!NOTE]
   >
   >Puede añadir varios grupos de campo si lo desea.

1. Guarde el esquema y anote el nombre que le ha asignado.

Para obtener más información sobre esquemas, consulte la [Ayuda del sistema del modelo de datos de Experience (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es).

## Crear una propiedad de reenvío de eventos

En el **[!UICONTROL Etiquetas]** espacio de trabajo, crear una propiedad de tipo **[!UICONTROL Edge]**.

1. Seleccione **[!UICONTROL Nueva propiedad]**.

1. Asigne un nombre a la propiedad.

1. Elija el tipo de plataforma &quot;Edge&quot;.

1. Seleccione **[!UICONTROL Guardar]**.

Después de crear la propiedad, vaya a la pestaña **[!UICONTROL Entornos]** de la nueva propiedad y tome
nota de los ID de entorno. Si la organización de Adobe utilizada en el conjunto de datos difiere de la organización de Adobe utilizada en el reenvío de eventos, puede copiar el ID de entorno del **[!UICONTROL Entornos]** y péguelo al crear una secuencia de datos. De lo contrario, puede seleccionar el entorno de un menú desplegable.

## Crear un flujo de datos

Para crear un flujo de datos en Adobe Experience Platform, utilice el ID de entorno generado al crear la propiedad de reenvío de eventos.

1. Seleccionar **[!UICONTROL Datastreams]** en el panel de navegación izquierdo.

1. Asigne un nombre a la configuración y proporcione una descripción opcional.
La descripción ayuda a identificar las configuraciones en una lista de varias configuraciones.

1. Seleccione **[!UICONTROL Guardar]**.

## Habilitar el reenvío de eventos

A continuación, configure Edge Network para enviar datos a reenvío de eventos y a otros productos de Adobe.

1. En el **[!UICONTROL Datastreams]** workspace, seleccione la propiedad que ha creado.

1. Seleccione el entorno Desarrollo, Producción o Ensayo.

   O bien, para enviar datos a un entorno fuera de Adobe, seleccione **[!UICONTROL Cambiar a Modo avanzado]** y pegue su valor en un ID. El ID se proporciona al crear un evento reenviado a una propiedad.

1. Active las herramientas necesarias y configúrelas según sea necesario.

   * Adobe Analytics requiere un ID del grupo de informes.

   * El reenvío de eventos en Adobe Experience Platform requiere un ID de propiedad y un ID de entorno. Es la ruta de publicación de la propiedad de reenvío de eventos.

Después de realizar la configuración, anote los ID de entorno para la nueva propiedad.

## Configure la extensión del SDK web de Platform para enviar datos al conjunto de datos creado anteriormente

Cree su propiedad en **[!UICONTROL Etiquetas]** espacio de trabajo y, a continuación, vaya a **[!UICONTROL Extensiones]** y seleccione la extensión del SDK web de Experience Platform en el catálogo para configurarla e instalarla.

Consulte la [Documentación de extensión del SDK web](../../extensions/client/web-sdk/overview.md) para obtener más información sobre las opciones de configuración.

## Creación de una regla de etiqueta para enviar datos al SDK web de Platform

Cuando todo lo anterior esté listo, podrá generar las definiciones de datos, las reglas, etc. que utilicen el reenvío de eventos y etiquetas, pero que solo necesiten una única solicitud de la página.

Cree una regla de carga de página con la extensión del SDK web de Platform y el tipo de acción Enviar evento:

1. Abra la pestaña **[!UICONTROL Reglas]** y seleccione **[!UICONTROL Crear nueva regla]**.

1. Asigne un nombre a la regla.

1. Seleccione **[!UICONTROL Añadir eventos]**.

1. Seleccione una extensión y uno de los tipos de evento disponibles para dicha extensión para añadir un evento y, a continuación, especifique la configuración del evento. Por ejemplo, seleccione **[!UICONTROL Core - Ventana cargada]**.

1. Añada una acción con la extensión del SDK web de Platform. Seleccione **[!UICONTROL Enviar evento]** de la lista **[!UICONTROL Tipo de acción]**, escoja la instancia deseada (instancia de Alloy configurada anteriormente) y, a continuación, elija un elemento de datos para añadirlo al bloque de datos XDM en la visita de Alloy.

1. Deje el resto de la configuración como predeterminada para este ejemplo y seleccione **[!UICONTROL Guardar]**.

Para otro ejemplo, puede crear una regla que envíe la capa de datos a Edge si el usuario coloca el ratón sobre un botón determinado.

## Resumen

Con lo siguiente, ahora podrá crear reglas de reenvío de eventos para reenviar datos a destinos que no son de Adobe.

* Esquema del modelo de datos de Experience (tenga en cuenta el nombre que le ha asignado).
* Una propiedad de reenvío de eventos (realice un seguimiento del ID de propiedad y los ID de entorno).
* Un conjunto de datos (observe el ID de entorno, que no debe confundirse con el ID de entorno del reenvío de eventos).
* Una propiedad de etiqueta
