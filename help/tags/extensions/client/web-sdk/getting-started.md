---
title: Introducción a la extensión de etiquetas Web SDK
description: Envíe datos de evento a Adobe Experience Platform Edge Network mediante la extensión de etiquetas de Web SDK.
exl-id: 01ddbb19-40bb-4cb5-bfca-b272b88008b3
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 3%

---

# Introducción a la extensión de etiquetas Web SDK

Use **tags** (anteriormente Launch) de Adobe Experience Platform para enviar datos de evento desde su sitio web a Edge Network y a las soluciones de Adobe posteriores.

Antes de seguir estos pasos, asegúrese de tener acceso a los siguientes [derechos de propiedad](/help/tags/ui/administration/user-permissions.md):

* [!UICONTROL Develop]
* [!UICONTROL Manage extensions]

Además, asegúrese de que tiene todos los [permisos](/help/access-control/home.md#permissions) en las siguientes categorías:

* Modelado de datos
* Identidades

## Creación de un esquema XDM {#schema}

El [Modelo de datos de experiencia (XDM)](/help/xdm/home.md) es una especificación de código abierto que proporciona estructuras y definiciones comunes para datos en forma de esquemas. Se recomienda encarecidamente configurar un esquema al enviar datos a Edge Network.

1. Inicie sesión en [experience.adobe.com](https://experience.adobe.com) con sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Schemas]**.
1. Seleccione **[!UICONTROL Create schema]**.
1. Seleccione **[!UICONTROL Experience Event]** y luego seleccione **[!UICONTROL Next]**.
1. Asigne un nombre al esquema y seleccione **[!UICONTROL Finish]**.
1. (Opcional) Puede agregar más campos o [grupos de campos](/help/xdm/ui/resources/field-groups.md) para cualquier dato adicional que desee recopilar.

![Lienzo de esquema](assets/getting-started/schema-structure.png)

>[!NOTE]
>\
>Una vez guardados, los esquemas solo permiten *cambios aditivos*. Consulte [evolución de esquema](/help/xdm/schema/composition.md#evolution) para obtener más información.

## Crear un flujo de datos {#datastream}

Un [conjunto de datos](/help/datastreams/overview.md) es una configuración que indica a Edge Network cómo gestionar los datos que lo envía. Al configurar un conjunto de datos para enviar datos a un producto determinado, el conjunto de datos pasa automáticamente los datos relevantes a cada producto respectivo de una manera que el producto específico entiende.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]**.
1. Seleccione **[!UICONTROL New datastream]**.
1. Asigne un nombre al conjunto de datos y seleccione el esquema creado recientemente en **[!UICONTROL Mapping schema]**.
1. Seleccione **[!UICONTROL Save]**.

![Lista de flujos de datos](assets/getting-started/datastreams.png)

## Creación de una propiedad de etiqueta

Una vez creados un esquema y una secuencia de datos, puede crear y configurar una propiedad de etiqueta.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione **[!UICONTROL New property]**.
1. Asigne un nombre y un dominio a la propiedad de etiqueta y seleccione **[!UICONTROL Save]**.

## Instalación de la extensión de etiqueta

La extensión de etiquetas Web SDK está instalada en una propiedad de etiquetas determinada.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]** > **[!UICONTROL Extensions]**.
1. Seleccione la pestaña **[!UICONTROL Catalog]** .
1. Use la búsqueda para encontrar la extensión **[!UICONTROL Adobe Experience Platform Web SDK]**.
1. Seleccione la tarjeta de extensión y, a continuación, seleccione **[!UICONTROL Install]** a la derecha.

![Instalar SDK](assets/getting-started/install-sdk.png)

## Configuración de la extensión de etiqueta

Al instalar la extensión de etiquetas Web SDK, se le redirige automáticamente a la página [Configuración](configure/config-overview.md).

1. En la sección [Secuencias de datos](configure/datastreams.md), seleccione la secuencia de datos que desee para cada entorno.

Todas las demás opciones de configuración se rellenan automáticamente o son opcionales. Defina las opciones de configuración que desee y seleccione **[!UICONTROL Save]**.

## Crear un elemento de datos variable

Adobe recomienda usar los elementos de datos [Variable](data-element-types.md#variable) para almacenar la carga útil que desea enviar a Adobe. Los objetos XDM también son elementos de datos disponibles, pero son más antiguos y limitados en los casos de uso aplicables.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Seleccione **[!UICONTROL Data elements]** > **[!UICONTROL Create new data element]**.
1. Asigne al elemento de datos las siguientes propiedades a la izquierda:
   * **[!UICONTROL Name]**: cualquier nombre deseado
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Data element type]**: [!UICONTROL Variable]
1. Establezca las siguientes propiedades a la derecha:
   **Tipo de variable**: XDM
   **[!UICONTROL Sandbox]**: la zona protegida en la que creó el esquema
   **[!UICONTROL Schema]**: el esquema deseado
1. Seleccione **[!UICONTROL Save]**.

## Crear una regla

Las reglas determinan cuándo desea almacenar en déclencheur algo o establecer variables. La creación de una regla que se ejecute cada vez que se carga la biblioteca de permite rellenar fácilmente las variables que desea que contengan un valor en cada página.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleccione la propiedad de etiquetas que desee.
1. Seleccione **[!UICONTROL Rules]** > **[!UICONTROL Add rule]**.
1. Asigne un nombre a la regla.
1. Seleccione el icono &#39;`+`&#39; junto a **[!UICONTROL Events]**.
1. Asigne al evento la siguiente configuración:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL Event type]**: [!UICONTROL Library loaded (page top)]
1. Seleccione **[!UICONTROL Keep changes]**.

Los pasos anteriores establecen la parte de criterios de la regla, que se almacena en déclencheur una vez que se carga la biblioteca. Los siguientes pasos establecen las medidas que deben tomarse cuando se cumplan esos criterios.

1. Seleccione el icono &#39;`+`&#39; junto a **[!UICONTROL Actions]**.
1. Asigne a la acción la siguiente configuración a la izquierda:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Send event]
1. Establezca los siguientes campos a la derecha:
   * **[!UICONTROL XDM]**: elemento de datos de la variable XDM
1. Seleccione **[!UICONTROL Keep changes]**.

![Configuración de acción](assets/getting-started/action-config.png)

## Publicación

La propiedad tag contiene todos los componentes necesarios para enviar datos a Edge Network.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Publishing flow]**.
1. Seleccione **[!UICONTROL Add library]**.
1. Asigne un nombre a la biblioteca. Considere este nombre similar a un nombre de confirmación cuando trabaje en el software de control de versiones.
1. Establezca el menú desplegable de entorno en **[!UICONTROL Development]**.
1. Seleccione **[!UICONTROL Add all changed resources]**.
1. Seleccione **[!UICONTROL Save & build to Development]**.

Los cambios se implementarán en el entorno de desarrollo.

1. Vaya a **[!UICONTROL Data Collection]** > **[!UICONTROL Environments]**.
1. Seleccione el icono de instalación situado junto al entorno de desarrollo de
1. Instale el código incrustado en una página web de prueba del sitio.

Una vez que valide que la etiqueta funciona en su entorno de desarrollo, puede utilizar la interfaz [!UICONTROL Publishing flow] para publicar la biblioteca en ensayo y, finalmente, en producción.

1. Agregue la extensión y la regla a una **biblioteca**, créela en un **entorno** e instale el código incrustado en el sitio.
2. Validar con **Adobe Experience Platform Debugger**.

Ahora tiene una configuración ligera que captura eventos y los envía a Edge Network. Ahora puede seguir creando la implementación añadiendo campos al esquema, añadiendo productos a un conjunto de datos o añadiendo elementos de datos a la propiedad de etiqueta.
