---
keywords: Experience Platform;inicio;temas populares;visor de gráficos de identidad;visor de gráficos de identidad;visor de gráficos;visor de gráficos;espacio de nombres de identidad;área de nombres de identidad;identidad;identidad;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Información general del visualizador de gráficos de identidad
topic-legacy: tutorial
description: Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 1%

---

# Resumen del visor de gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales. El servicio de identidad de Adobe Experience Platform administra y actualiza todos los gráficos de identidad de los clientes de forma colectiva casi en tiempo real como respuesta a la actividad de los clientes.

El visor de gráficos de identidad en la interfaz de usuario de Platform le permite visualizar y comprender mejor qué identidades de cliente se vinculan entre sí y de qué manera. El visor le permite arrastrar e interactuar con diferentes partes del gráfico, lo que le permite examinar relaciones de identidad complejas, depurar de forma más eficaz y beneficiarse de una mayor transparencia con la forma en que se utiliza la información.

## Videotutorial

El siguiente vídeo pretende comprender mejor el visor de gráficos de identidad.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Primeros pasos

Para trabajar con el visor de gráficos de identidad es necesario conocer los distintos servicios de Adobe Experience Platform implicados. Antes de comenzar a trabajar con el visor de gráficos de identidad, revise la documentación de los siguientes servicios:

- [[!DNL Identity Service]](../home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.

### Terminología

- **Identidad (nodo):** Una identidad o un nodo son datos exclusivos de una entidad, normalmente una persona. Una identidad consta de un área de nombres y un valor de identidad.
- **Vínculo (borde):** un vínculo o un borde representa la conexión entre identidades.
- **Gráfico (clúster):** un gráfico o un clúster es un grupo de identidades y vínculos que representan a una persona.

## Acceso al visor del gráfico de identidad

Para utilizar el visor de gráficos de identidad en la interfaz de usuario, seleccione **[!UICONTROL Identities]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Identity graph]** . En la pantalla **[!UICONTROL Identity Namespace]**, haga clic en el icono **[!UICONTROL Select identity namespace]** para buscar el espacio de nombres que desea utilizar.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

Aparece el panel **[!UICONTROL Select identity namespace]** . Esta pantalla contiene una lista de áreas de nombres disponibles para su organización, incluida información sobre las fechas **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]**, **[!UICONTROL Owner]**, **[!UICONTROL Last updated]** y **[!UICONTROL Description]** de un área de nombres. Puede utilizar cualquiera de las áreas de nombres siempre que tenga un valor de identidad válido conectado a ellas.

Seleccione el espacio de nombres que desea utilizar y haga clic en **[!UICONTROL Select]** para continuar.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Una vez que haya seleccionado un área de nombres, introduzca su valor correspondiente para un cliente en particular en el cuadro de texto **[!UICONTROL Identity value]** y seleccione **[!UICONTROL View]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### Acceso al visor de gráficos de identidad desde conjuntos de datos

También puede acceder al visor de gráficos de identidad mediante la interfaz de conjuntos de datos. En la página datasets [!UICONTROL Browse] , seleccione un conjunto de datos con el que desee interactuar y, a continuación, seleccione **[!UICONTROL Preview dataset]**

![vista previa del conjunto de datos](../images/identity-graph-viewer/preview-dataset.png)

En la ventana de vista previa, seleccione un icono de huella digital para ver las identidades representadas a través del visor de gráficos de identidad.

>[!TIP]
>
>El icono de huella digital solo aparece si el conjunto de datos tiene dos o más identidades.

![huella digital](../images/identity-graph-viewer/fingerprint.png)

Aparece el visor del gráfico de identidad. En la parte izquierda de la pantalla, aparece el gráfico de identidad que muestra todas las identidades vinculadas al área de nombres seleccionada y el valor de identidad introducido. Cada nodo de identidad consta de un área de nombres y su valor de ID correspondiente. Puede seleccionar y mantener cualquier identidad para arrastrar e interactuar con el gráfico. Como alternativa, puede pasar el ratón sobre una identidad para ver información sobre su valor de ID. El resultado del gráfico también se muestra como una lista tabulada en el centro de la pantalla.

>[!IMPORTANT]
>
>Un gráfico de identidad requiere un mínimo de dos identidades vinculadas para generarse, así como un espacio de nombres y un par de ID válidos. El número máximo de identidades que puede mostrar el visor de gráficos es de 150. Consulte la sección [apéndice](#appendix) a continuación para obtener más información.

![id-graph](../images/identity-graph-viewer/graph-viewer.png)

Seleccione una identidad para actualizar la fila resaltada en la tabla **[!UICONTROL Identities]** y para actualizar la información proporcionada en el carril derecho, que incluye las fechas **[!UICONTROL Value]**, **[!UICONTROL Batch ID]** y **[!UICONTROL Last updated]** de una identidad.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Puede filtrar por un gráfico y aislar un área de nombres específica mediante la opción de ordenación situada en la parte superior de la tabla **[!UICONTROL Identities]**. En el menú desplegable, seleccione el espacio de nombres que desee resaltar.

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

El visor de gráficos devuelve, resaltando el espacio de nombres seleccionado. La opción de filtro también actualiza la tabla **[!UICONTROL Identities]** para devolver información solamente para el área de nombres seleccionada.

![filtrado](../images/identity-graph-viewer/filtered.png)

La parte superior derecha del cuadro del visor de gráficos contiene opciones para la ampliación. Seleccione el icono **(+)** para acercar el gráfico o el icono **(-)** para alejarlo.

![zoom](../images/identity-graph-viewer/zoom.png)

Para ver más información sobre los lotes, seleccione **[!UICONTROL Data source]** en el encabezado. La tabla **[!UICONTROL Data source]** muestra una lista de **[!UICONTROL Batch IDs]** asociados con el gráfico, así como su **[!UICONTROL Linked IDs]**, esquema de origen y fecha de ingesta.

![fuente de datos](../images/identity-graph-viewer/data-source-table.png)

Puede seleccionar cualquiera de los vínculos de un gráfico de identidad para ver todos los lotes de origen que contribuyeron al vínculo.

![vínculos de selección](../images/identity-graph-viewer/select-edge.png)

Como alternativa, puede seleccionar un lote para ver todos los vínculos a los que contribuyó este lote.

![vínculos de selección](../images/identity-graph-viewer/select-batch.png)

También se puede acceder a los gráficos de identidad con clústeres de identidades más grandes a través del visor de gráficos de identidad.

![clúster grande](../images/identity-graph-viewer/large-cluster.png)

## Apéndice

La siguiente sección proporciona información adicional para trabajar con el visor de gráficos de identidad.

### Comprensión de los mensajes de error

Pueden producirse errores al acceder al visor del gráfico de identidad. A continuación se muestra una lista de requisitos previos y limitaciones que deben tenerse en cuenta al trabajar con el visor de gráficos de identidad.

- Debe existir un valor de identidad en el espacio de nombres seleccionado.
- El visor de gráficos de identidad requiere un mínimo de dos identidades vinculadas para generarse. Es posible que solo haya un valor de identidad y ninguna identidad vinculada y, en este caso, el valor solo existiría en el visor [!DNL Profile].
- El visor de gráficos de identidad no puede superar el máximo de 150 identidades.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Pasos siguientes

Al leer este documento, ha aprendido a explorar los gráficos de identidad de los clientes en la interfaz de usuario de Platform. Para obtener más información sobre las identidades en Platform, consulte la [información general del servicio de identidad](../home.md)

## Cambio

| Fecha | Acción |
| ---- | ------ |
| 2021-01 | <ul><li>Se ha agregado compatibilidad con la transmisión de datos incorporados y entornos limitados que no sean de producción.</li><li>Se han corregido errores menores.</li></ul> |
| 2021-02 | <ul><li>Se puede acceder al visor de gráficos de identidad mediante la vista previa de conjuntos de datos.</li><li>Se han corregido errores menores.</li><li>El visor de gráficos de identidad está disponible de forma general.</li></ul> |
