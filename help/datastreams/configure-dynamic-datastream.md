---
title: Crear configuraciones de flujo de datos dinámico
description: Aprenda a crear configuraciones de flujo de datos dinámico para enrutar los datos a varios servicios de Experience Cloud, según las reglas.
hide: true
hidefromtoc: true
badge: label="Beta" type="Informative"
source-git-commit: 615318744c233930fb9bc20e55ff42c3a396e651
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---


# Crear configuraciones de flujo de datos dinámico

>[!AVAILABILITY]
>
>* La opción para definir configuraciones de flujo de datos dinámico se encuentra actualmente en Beta y está disponible para un número limitado de clientes. Para obtener acceso a esta funcionalidad, póngase en contacto con el representante del Adobe. La documentación y las funcionalidades están sujetas a cambios.

De manera predeterminada, el Edge Network Experience Platform envía todos los eventos que llegan a una secuencia de datos a todos los [servicios](configure.md#add-services) del Experience Cloud que haya habilitado para sus secuencias de datos. Este podría no ser siempre el flujo de trabajo ideal, según sus casos de uso.

Las configuraciones de flujo de datos dinámico solucionan este problema mediante conjuntos de reglas configurables por el usuario que se definen para cada servicio habilitado para el flujo de datos, que dictan qué solución de Experience Cloud debe recibir cada tipo de datos.

## Requisitos previos {#prerequisites}

Para crear una configuración dinámica para el conjunto de datos, deben cumplirse dos condiciones:

* Debe haber creado *al menos* un conjunto de datos para trabajar con él. Consulte la documentación sobre cómo [crear un conjunto de datos](configure.md) para obtener información detallada.
* Debe tener *al menos* un servicio de Experience Cloud agregado a su secuencia de datos. Consulte la documentación sobre cómo [agregar un servicio](configure.md#add-services) a un conjunto de datos para obtener información detallada.

Después de crear una secuencia de datos y agregarle un servicio de Experience Cloud, puede [crear una configuración dinámica](#create-dynamic-configuration).

## Crear una configuración de flujo de datos dinámico {#create-dynamic-configuration}

Después de [crear un conjunto de datos](configure.md) y [agregarle un servicio](configure.md#add-services), siga los pasos a continuación para agregar una configuración dinámica al servicio.

1. Vaya a la página **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Flujos de datos]** y seleccione el flujo de datos que ha creado.

   ![Imagen de la interfaz de usuario de flujos de datos que muestra la lista de flujos de datos.](assets/configure-dynamic-datastream/select-datastream.png)

1. Seleccione la opción **[!UICONTROL Edit]** en el servicio para el que desea definir una configuración dinámica.

   ![Imagen de la interfaz de usuario de flujos de datos que muestra los servicios agregados a un flujo de datos.](assets/configure-dynamic-datastream/select-service.png)

1. En la página **[!UICONTROL Configurar]**, seleccione **[!UICONTROL Guardar y editar configuración dinámica]**.

   ![Imagen de la interfaz de usuario de flujos de datos que muestra la página de configuración del flujo de datos.](assets/configure-dynamic-datastream/save-and-edit.png)

1. Seleccione **[!UICONTROL Agregar configuración dinámica]**.

   ![Imagen de la interfaz de usuario de flujos de datos que muestra el mensaje de configuración dinámica sin regla agregada.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. En el panel **[!UICONTROL Recursos]**, arrastre y suelte los elementos con los que desee generar la regla en el lado derecho de la ventana. Puede combinar varios recursos para crear reglas complejas.

   Use las opciones de cada recurso, como **[!UICONTROL igual a]**, **[!UICONTROL no es igual a]**, **[!UICONTROL existe]** y más, para ajustar las reglas.

   ![Imagen de la interfaz de usuario de flujos de datos que muestra la regla de configuración dinámica.](assets/configure-dynamic-datastream/drag-resources.png)

1. En la sección **[!UICONTROL Configuración]**, active o desactive los servicios que desee habilitar o deshabilitar para cada regla, dependiendo de si desea que los datos se envíen a cada servicio. Si desactiva la opción, el enrutamiento del servicio se deshabilita y *no se enviarán datos* al servicio ascendente.

   ![Imagen de la interfaz de usuario de flujos de datos que muestra la regla de configuración dinámica.](assets/configure-dynamic-datastream/enable-service.png)

1. Cuando termine de configurar las reglas, seleccione **[!UICONTROL Guardar]**.

## Consideraciones de prioridad de reglas {#considerations}

Puede definir varias reglas para cada configuración de flujo de datos dinámico. Sin embargo, si los datos coinciden con las condiciones de varias reglas, solo se tendrá en cuenta la primera regla que coincida en la lista y el resto de reglas que coincidan se ignorarán.

Para lograr el comportamiento de enrutamiento de datos deseado, preste atención al orden en que organiza las reglas.

Para configurar el orden de las reglas, puede arrastrar y soltar las ventanas de reglas en el orden que desee.

![GIF que muestra cómo cambiar el orden de las reglas mediante arrastrar y soltar.](assets/configure-dynamic-datastream/move-rules.gif)