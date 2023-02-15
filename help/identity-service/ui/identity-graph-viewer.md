---
title: Visor de gráficos de identidad
description: Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 4bf939011e6246a553f67805ff99a70610782ea6
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 2%

---

# Visor de gráficos de identidad

Un gráfico de identidad es un mapa de relaciones entre distintas identidades para un cliente en particular, que proporciona una representación visual de cómo el cliente interactúa con la marca a través de diferentes canales. El servicio de identidad de Adobe Experience Platform administra y actualiza todos los gráficos de identidad de los clientes de forma colectiva casi en tiempo real como respuesta a la actividad de los clientes.

El visor de gráficos de identidad en la interfaz de usuario de Platform le permite visualizar y comprender mejor qué identidades de cliente se vinculan entre sí y de qué manera. El visor le permite arrastrar e interactuar con diferentes partes del gráfico, lo que le permite examinar relaciones de identidad complejas, depurar de forma más eficaz y beneficiarse de una mayor transparencia con la forma en que se utiliza la información.

El siguiente documento proporciona pasos sobre cómo acceder y utilizar el visor de gráficos de identidad en la interfaz de usuario de Platform.

## Tutorial en vídeo

El siguiente vídeo pretende comprender mejor el visor de gráficos de identidad.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Primeros pasos

Para trabajar con el visor de gráficos de identidad es necesario conocer los distintos servicios de Adobe Experience Platform implicados. Antes de comenzar a trabajar con el visor de gráficos de identidad, revise la documentación de los siguientes servicios:

- [[!DNL Identity Service]](../home.md): Obtenga una mejor visión de los clientes individuales y su comportamiento al unir identidades entre dispositivos y sistemas.
- [Perfil del cliente en tiempo real](../../profile/home.md): El perfil del cliente en tiempo real aprovecha los gráficos de identidad para crear una vista completa y singular de los atributos y el comportamiento del cliente.

### Terminología

- **Identidad (nodo):** Una identidad o un nodo son datos exclusivos de una entidad, normalmente una persona. Una identidad consta de un área de nombres de identidad y un valor de identidad. Por ejemplo, una identidad completa podría consistir en un área de nombres de identidad para **Correo electrónico**, combinado con un valor de identidad de **robin<span>@email.com**.
- **Vínculo (borde):** Un vínculo o un borde representa la conexión entre identidades. Los vínculos de identidad incluyen propiedades como las primeras y últimas marcas de hora actualizadas. La primera marca de tiempo establecida define la fecha y la hora a la que una nueva identidad está vinculada a una identidad existente. La última marca de tiempo actualizada define la fecha y la hora en la que se actualizó por última vez un vínculo de identidad existente.
- **Gráfico (clúster):** Un gráfico o un clúster es un grupo de identidades y vínculos que representan a una persona.

## Acceso al visor del gráfico de identidad {#access-identity-graph-viewer}

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Identidades]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Gráfico de identidad]** de la lista de pestañas del encabezado.

![El espacio de trabajo Identidades en la interfaz de usuario del Experience Platform, con la pestaña Gráfico de identidad seleccionada.](../images/graph-viewer/identity-graph.png)

Para ver un gráfico de identidad, proporcione un área de nombres de identidad y su valor correspondiente y, a continuación, seleccione **[!UICONTROL Ver]**.

>[!TIP]
>
>Seleccione el icono de tabla ![icono de tabla](../images/identity-graph-viewer/table-icon.png) para ver un panel con una lista de todos los áreas de nombres de identidad disponibles en su organización. Puede utilizar cualquiera de los espacios de nombres de identidad siempre y cuando tenga un valor de identidad válido conectado a ellos. Para obtener más información, lea la [guía del área de nombres de identidad](../namespaces.md).

![Un área de nombres de identidad y su valor correspondiente, proporcionados en la pantalla de búsqueda del gráfico de identidad.](../images/graph-viewer/namespace-and-value.png)

## Explicación de la interfaz del visor de gráficos de identidad

La interfaz del visor de gráficos de identidad consta de varios elementos que puede utilizar para interactuar con los datos de identidad y comprenderlos mejor.

![Interfaz del visor del gráfico de identidad.](../images/graph-viewer/identity-graph-viewer-main.png)

El gráfico de identidad muestra todas las identidades vinculadas al área de nombres de identidad y la combinación de valores que ha introducido. Cada nodo consta de un área de nombres de identidad y su valor correspondiente. Puede seleccionar, mantener presionado y arrastrar cualquier nodo para interactuar con el gráfico. Como alternativa, puede pasar el ratón sobre un nodo para ver información sobre su valor de identidad correspondiente. Select **[!UICONTROL Ver gráfico]** para ocultar o mostrar el gráfico.

>[!IMPORTANT]
>
>Un gráfico de identidad requiere que se genere un mínimo de dos identidades vinculadas y una combinación válida de área de nombres de identidad y valor. El número máximo de identidades que puede mostrar el visor de gráficos es de 150. Consulte la [apéndice](#appendix) para obtener más información.

![El visor de gráficos de identidad con cinco identidades vinculadas.](../images/graph-viewer/graph.png)

Seleccione un vínculo dentro del gráfico para ver el conjunto de datos y el ID de lote que contribuyen a ese vínculo. Al seleccionar un vínculo, también se actualiza el carril derecho para proporcionar más información sobre los detalles de la fuente de datos, así como propiedades como las marcas de tiempo establecidas por primera vez y las actualizadas por última vez.

![El vínculo de identidad entre los nodos de correo electrónico y GAID seleccionados.](../images/graph-viewer/identity-link.png)

La variable [!UICONTROL Identidades] proporciona una vista diferente de los datos de identidad, que enumera el área de nombres de identidad y la combinación del valor de identidad en un formato tabular. Si se selecciona un nodo en el gráfico, se actualizará el elemento de línea resaltado en la variable [!UICONTROL Identidades] tabla.

![La tabla Identidades con la lista de identidades vinculadas dentro del gráfico.](../images/graph-viewer/identities-table.png)

Utilice el menú desplegable para ordenar los datos del gráfico y resaltar la información en un área de nombres de identidad específica. Por ejemplo, seleccione **[!UICONTROL Correo electrónico]** en el menú para ver los datos específicos del área de nombres de identidad del correo electrónico.

![La tabla Identidades ordenada para mostrar solo los datos de correo electrónico.](../images/graph-viewer/sort-email.png)

El carril derecho muestra información sobre una identidad seleccionada, incluida la última marca de tiempo actualizada. El carril derecho también muestra información sobre el origen de datos que corresponde a la identidad seleccionada, incluido su ID de lote, el nombre del conjunto de datos, el ID del conjunto de datos y el nombre del esquema.

La tabla siguiente proporciona información adicional sobre las propiedades de origen de datos que se muestran en el carril derecho:

| Fuente de datos | Descripción |
| --- | --- | 
| ID de lote | Identificador generado automáticamente que corresponde a los datos de lote. |
| ID de conjunto de datos | Identificador generado automáticamente que corresponde al conjunto de datos. |
| Nombre del conjunto de datos | El nombre del conjunto de datos que contiene los datos por lotes. |
| Nombre del esquema | Nombre del esquema. El esquema proporciona un conjunto de reglas que representan y validan la estructura y el formato de los datos. |

![El carril derecho, que muestra los datos de identidad, así como la fuente de datos de información.](../images/graph-viewer/right-rail.png)

También puede usar la variable *[!UICONTROL Fuente de datos]* para ver una lista de las fuentes de datos que contribuyen a sus identidades. Select [!UICONTROL Fuente de datos] para obtener una vista tabular de sus conjuntos de datos e ID de lote.

![La pestaña de fuente de datos seleccionada.](../images/graph-viewer/data-source-table.png)

Utilice el control deslizante para filtrar los datos del gráfico por el momento en que se establecieron las identidades por primera vez. De forma predeterminada, el visor de gráficos de identidad muestra todas las identidades vinculadas dentro del gráfico. Mantenga presionado y arrastre el control deslizante para ajustar el tiempo a la última marca de tiempo en la que se vinculó una nueva identidad al gráfico. En el siguiente ejemplo, el gráfico muestra que el vínculo de identidad (GAID) más reciente se estableció en **[!UICONTROL 19/8/2020, 4:29:29 PM]**.

![El control deslizante de la marca de tiempo del visor de gráficos seleccionado.](../images/graph-viewer/slider-one.png)

Ajuste el control deslizante para ver que se ha establecido otro vínculo de identidad (correo electrónico) en **[!UICONTROL 19/8/2020, 4:25:30 PM]**.

![El control deslizante de la marca de tiempo del visor de gráficos se ajustó al último vínculo nuevo establecido.](../images/graph-viewer/slider-two.png)

También puede ajustar el control deslizante para ver la primera iteración del gráfico. En el ejemplo siguiente, el visor de gráficos de identidad muestra que el gráfico se creó por primera vez en **[!UICONTROL 19/8/2020, 4:11:49 PM]**, con sus primeros vínculos como ECID, correo electrónico y teléfono.

![El control deslizante de la marca de tiempo del visor de gráficos se ajustó al primer vínculo nuevo establecido.](../images/graph-viewer/slider-three.png)

## Apéndice

La siguiente sección proporciona información adicional para trabajar con el visor de gráficos de identidad.

### Comprensión de los mensajes de error

Pueden producirse errores al acceder al visor del gráfico de identidad. A continuación se muestra una lista de requisitos previos y limitaciones que deben tenerse en cuenta al trabajar con el visor de gráficos de identidad.

- Debe existir un valor de identidad en el espacio de nombres seleccionado.
- El visor de gráficos de identidad requiere un mínimo de dos identidades vinculadas para generarse. Es posible que solo haya un valor de identidad y ninguna identidad vinculada, y en este caso, el valor solo existiría en [!DNL Profile] espectador.
- El visor de gráficos de identidad no puede superar el máximo de 150 identidades.

![error-screen](../images/graph-viewer/error-screen.png)

### Acceso al visor de gráficos de identidad desde conjuntos de datos

También puede acceder al visor de gráficos de identidad mediante la interfaz de conjuntos de datos. Desde los conjuntos de datos [!UICONTROL Examinar] , seleccione un conjunto de datos con el que desee interactuar y, a continuación, seleccione **[!UICONTROL Vista previa del conjunto de datos]**

![vista previa del conjunto de datos](../images/identity-graph-viewer/preview-dataset.png)

En la ventana de vista previa, seleccione un icono de huella digital para ver las identidades representadas a través del visor de gráficos de identidad.

>[!TIP]
>
>El icono de huella digital solo aparece si el conjunto de datos tiene dos o más identidades.

![huella digital](../images/identity-graph-viewer/fingerprint.png)

## Pasos siguientes

Al leer este documento, ha aprendido a explorar los gráficos de identidad de los clientes en la interfaz de usuario de Platform. Para obtener más información sobre las identidades en Platform, consulte la [Información general del servicio de identidad](../home.md)

## Cambio

| Fecha | Acción |
| ---- | ------ |
| 2021-01 | <ul><li>Se ha agregado compatibilidad con la transmisión de datos incorporados y entornos limitados que no sean de producción.</li><li>Se han corregido errores menores.</li></ul> |
| 2021-02 | <ul><li>Se puede acceder al visor de gráficos de identidad mediante la vista previa de conjuntos de datos.</li><li>Se han corregido errores menores.</li><li>El visor de gráficos de identidad está disponible de forma general.</li></ul> |
| 2023-01 | <ul><li>Actualizaciones de la interfaz de usuario.</li></ul> |
