---
keywords: Experience Platform;inicio;temas populares;visor de gráficos de identidad;visor de gráficos de identidad;visor de gráficos;visor de gráficos;espacio de nombres de identidad;área de nombres de identidad;identidad;identidad;servicio de identidad;servicio de identidad
solution: Experience Platform
title: Información general del visualizador de gráficos de identidad
description: Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 25f1b2197e5b10b04668d16bff3a6ce48cfad5fc
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 1%

---

# Resumen del visor de gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales. El servicio de identidad de Adobe Experience Platform administra y actualiza todos los gráficos de identidad de los clientes de forma colectiva casi en tiempo real como respuesta a la actividad de los clientes.

El visor de gráficos de identidad en la interfaz de usuario de Platform le permite visualizar y comprender mejor qué identidades de cliente se vinculan entre sí y de qué manera. El visor le permite arrastrar e interactuar con diferentes partes del gráfico, lo que le permite examinar relaciones de identidad complejas, depurar de forma más eficaz y beneficiarse de una mayor transparencia con la forma en que se utiliza la información.

## Tutorial en vídeo

El siguiente vídeo pretende comprender mejor el visor de gráficos de identidad.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Primeros pasos

Para trabajar con el visor de gráficos de identidad es necesario conocer los distintos servicios de Adobe Experience Platform implicados. Antes de comenzar a trabajar con el visor de gráficos de identidad, revise la documentación de los siguientes servicios:

- [[!DNL Identity Service]](../home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.

### Terminología

- **Identidad (nodo):** Una identidad o un nodo son datos exclusivos de una entidad, normalmente una persona. Una identidad consta de un área de nombres y un valor de identidad.
- **Vínculo (borde):** Un vínculo o un borde representa la conexión entre identidades.
- **Gráfico (clúster):** Un gráfico o un clúster es un grupo de identidades y vínculos que representan a una persona.

## Acceso al visor del gráfico de identidad {#access-identity-graph-viewer}

Para utilizar el visor de gráficos de identidad en la interfaz de usuario, seleccione **[!UICONTROL Identidades]** en el panel de navegación izquierdo y, a continuación, seleccione la **[!UICONTROL Gráfico de identidad]** pestaña . En el **[!UICONTROL Área de nombres de identidad]** , haga clic en **[!UICONTROL Seleccionar área de nombres de identidad]** para buscar el espacio de nombres que desea utilizar.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

La variable **[!UICONTROL Seleccionar área de nombres de identidad]** aparece. Esta pantalla contiene una lista de áreas de nombres disponibles para su organización, incluida información sobre el **[!UICONTROL Nombre para mostrar]**, **[!UICONTROL Símbolo de identidad]**, **[!UICONTROL Propietario]**, **[!UICONTROL Última actualización]** fecha y **[!UICONTROL Descripción]**. Puede utilizar cualquiera de las áreas de nombres siempre que tenga un valor de identidad válido conectado a ellas.

Seleccione el espacio de nombres que desea utilizar y haga clic en **[!UICONTROL Select]** para continuar.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Una vez que haya seleccionado un área de nombres, introduzca su valor correspondiente para un cliente en particular en la **[!UICONTROL Valor de identidad]** cuadro de texto y seleccione **[!UICONTROL Ver]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

### Acceso al visor de gráficos de identidad desde conjuntos de datos

También puede acceder al visor de gráficos de identidad mediante la interfaz de conjuntos de datos. Desde los conjuntos de datos [!UICONTROL Examinar] , seleccione un conjunto de datos con el que desee interactuar y, a continuación, seleccione **[!UICONTROL Vista previa del conjunto de datos]**

![vista previa del conjunto de datos](../images/identity-graph-viewer/preview-dataset.png)

En la ventana de vista previa, seleccione un icono de huella digital para ver las identidades representadas a través del visor de gráficos de identidad.

>[!TIP]
>
>El icono de huella digital solo aparece si el conjunto de datos tiene dos o más identidades.

![huella digital](../images/identity-graph-viewer/fingerprint.png)

Aparece el visor del gráfico de identidad. En la parte izquierda de la pantalla, aparece el gráfico de identidad que muestra todas las identidades vinculadas al área de nombres seleccionada y el valor de identidad introducido. Cada nodo de identidad consta de un área de nombres y su valor de ID correspondiente. Puede seleccionar y mantener cualquier identidad para arrastrar e interactuar con el gráfico. Como alternativa, puede pasar el ratón sobre una identidad para ver información sobre su valor de ID. El resultado del gráfico también se muestra como una lista tabulada en el centro de la pantalla.

>[!IMPORTANT]
>
>Un gráfico de identidad requiere un mínimo de dos identidades vinculadas para generarse, así como un espacio de nombres y un par de ID válidos. El número máximo de identidades que puede mostrar el visor de gráficos es de 150. Consulte la [apéndice](#appendix) para obtener más información.

![id-graph](../images/identity-graph-viewer/graph-viewer.png)

Seleccione una identidad para actualizar la fila resaltada en la **[!UICONTROL Identidades]** y para actualizar la información proporcionada en el carril derecho, que incluye el **[!UICONTROL Valor]**, **[!UICONTROL ID de lote]** y su **[!UICONTROL Última actualización]** fecha.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Puede filtrar por un gráfico y aislar un área de nombres específica mediante la opción de ordenación situada encima del **[!UICONTROL Identidades]** tabla. En el menú desplegable, seleccione el espacio de nombres que desee resaltar.

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

El visor de gráficos devuelve, resaltando el espacio de nombres seleccionado. La opción de filtro también actualiza el **[!UICONTROL Identidades]** para devolver información únicamente para el área de nombres seleccionada.

![filtrado](../images/identity-graph-viewer/filtered.png)

La parte superior derecha del cuadro del visor de gráficos contiene opciones para la ampliación. Seleccione el **(+)** para acercar el gráfico o el **(-)** para alejar.

![zoom](../images/identity-graph-viewer/zoom.png)

Para ver más información sobre los lotes, seleccione la opción **[!UICONTROL Fuente de datos]** del encabezado. La variable **[!UICONTROL Fuente de datos]** muestra una lista de **[!UICONTROL ID de lote]** asociados al gráfico, así como a su **[!UICONTROL ID vinculados]**, esquema de origen y fecha de ingesta.

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
- El visor de gráficos de identidad requiere un mínimo de dos identidades vinculadas para generarse. Es posible que solo haya un valor de identidad y ninguna identidad vinculada, y en este caso, el valor solo existiría en [!DNL Profile] espectador.
- El visor de gráficos de identidad no puede superar el máximo de 150 identidades.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Pasos siguientes

Al leer este documento, ha aprendido a explorar los gráficos de identidad de los clientes en la interfaz de usuario de Platform. Para obtener más información sobre las identidades en Platform, consulte la [Información general del servicio de identidad](../home.md)

## Cambio

| Fecha | Acción |
| ---- | ------ |
| 2021-01 | <ul><li>Se ha agregado compatibilidad con la transmisión de datos incorporados y entornos limitados que no sean de producción.</li><li>Se han corregido errores menores.</li></ul> |
| 2021-02 | <ul><li>Se puede acceder al visor de gráficos de identidad mediante la vista previa de conjuntos de datos.</li><li>Se han corregido errores menores.</li><li>El visor de gráficos de identidad está disponible de forma general.</li></ul> |
