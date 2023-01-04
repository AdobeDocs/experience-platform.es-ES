---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;Segmentación;crear un conjunto de datos;exportar segmento de audiencia;exportar segmento;
solution: Experience Platform
title: Crear un conjunto de datos para exportar un segmento de audiencia
topic-legacy: tutorial
type: Tutorial
description: Este tutorial explica los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante la interfaz de usuario del Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# Creación de un conjunto de datos para exportar un segmento de audiencia

[!DNL Adobe Experience Platform] le permite segmentar perfiles de clientes en audiencias en función de atributos específicos. Una vez creado un segmento, puede exportar esa audiencia a un conjunto de datos en el que se pueda acceder a él y actuar en consecuencia. Para que la exportación se realice correctamente, el conjunto de datos debe configurarse correctamente.

Este tutorial recorre los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante el [!DNL Experience Platform] IU.

Este tutorial está directamente relacionado con los pasos descritos en el tutorial de [evaluación y acceso a resultados de segmentos](./evaluate-a-segment.md). El tutorial de evaluación de segmentos proporciona pasos para crear un conjunto de datos mediante el uso de [!DNL Catalog Service] API, mientras que este tutorial describe los pasos para crear un conjunto de datos mediante el [!DNL Experience Platform] IU.

## Primeros pasos

Para exportar un segmento, el conjunto de datos debe basarse en la variable [!DNL XDM Individual Profile Union Schema]. Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de todos los esquemas que comparten la misma clase. Para obtener más información sobre los esquemas de unión, consulte la guía de [los conceptos básicos de la composición del esquema](../../xdm/schema/composition.md#union).

Para ver los esquemas de unión en la interfaz de usuario, seleccione **[!UICONTROL Perfiles]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Esquema de unión]** como se muestra a continuación.

![Se resalta la pestaña del esquema de unión.](../images/tutorials/segment-export-dataset/union.png)

## Espacio de trabajo de conjuntos de datos

La variable [!UICONTROL Conjuntos de datos] workspace le permite ver y administrar todos los conjuntos de datos de su organización.

Select **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo para acceder al espacio de trabajo, seleccione **[!UICONTROL Examinar]**. Esta pestaña muestra una lista de conjuntos de datos y sus detalles. Según el ancho de cada columna, puede que sea necesario desplazarse a la izquierda o a la derecha para ver todas las columnas.

>[!NOTE]
>
>Seleccione el icono de filtro situado junto a la barra de búsqueda para utilizar las funcionalidades de filtrado y ver solo aquellos conjuntos de datos habilitados para [!DNL Real-Time Customer Profile].

![Se muestra el espacio de trabajo de los conjuntos de datos.](../images/tutorials/segment-export-dataset/browse.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, seleccione **[!UICONTROL Crear conjunto de datos]**.

![Se resalta el botón Crear conjunto de datos .](../images/tutorials/segment-export-dataset/create-dataset.png)

En la siguiente pantalla, seleccione **[!UICONTROL Crear conjunto de datos a partir del esquema]**.

![Se resalta la opción Crear conjunto de datos a partir del esquema.](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Seleccionar esquema de unión de perfil individual XDM

Para seleccionar la variable [!DNL XDM Individual Profile Union Schema] para usar en el conjunto de datos, busque &quot;[!UICONTROL Perfil individual XDM]&quot; en el **[!UICONTROL Seleccionar esquema]** en el Navegador. Una vez seleccionado el esquema, puede confirmar si es el esquema de unión en **[!UICONTROL Uso de API]** en el carril derecho. Si la variable [!UICONTROL Esquema] la ruta termina con `_union`, es un esquema de unión.

>[!NOTE]
>
>A pesar de que los esquemas de unión participan en el perfil del cliente en tiempo real por definición, se enumeran como &quot;No habilitado&quot; debido al hecho de que no están habilitados para Perfil de la misma manera que los esquemas tradicionales.

Seleccione el botón de opción situado junto a **[!UICONTROL Perfil individual XDM]** y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Se resalta el esquema de perfil individual XDM.](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar el conjunto de datos

En la siguiente pantalla, debe asignar un nombre al conjunto de datos. También puede añadir una descripción opcional.

**Notas sobre los nombres de conjuntos de datos:**

* Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que el conjunto de datos se pueda encontrar fácilmente en la biblioteca más adelante.
* Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro.
* Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que podría ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tiene un nombre y una descripción, seleccione **[!UICONTROL Finalizar]**.

![Se muestra la página Configurar conjunto de datos . Se resaltan las opciones de configuración.](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Actividad del conjunto de datos

Una vez creado el conjunto de datos, se le proporcionará la página de actividad para ese conjunto de datos. Debería ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación de que &quot;No se han agregado lotes&quot;. Esto es de esperar, ya que aún no ha agregado ningún lote a este conjunto de datos.

El carril correcto contiene información relacionada con su nuevo conjunto de datos, como ID del conjunto de datos, nombre, descripción, esquema, etc. Tenga en cuenta que **[!UICONTROL ID de conjunto de datos]**, ya que este valor es necesario para completar el flujo de trabajo de exportación de segmentos de audiencia.

![Se muestra la página de actividad del conjunto de datos. Se resalta el ID del conjunto de datos, ya que este valor debe tenerse en cuenta para los pasos futuros.](../images/tutorials/segment-export-dataset/activity.png)

## Pasos siguientes

Ahora que ha creado un conjunto de datos basado en la variable [!DNL XDM Individual Profile Union Schema], puede utilizar el ID del conjunto de datos para continuar con el [evaluación y acceso a resultados de segmentos](./evaluate-a-segment.md) tutorial.

En este momento, vuelva al tutorial de resultados del segmento de evaluación y elija la opción de [generación de perfiles para miembros de audiencia](./evaluate-a-segment.md#generate-profiles) del flujo de trabajo de exportación de un segmento.
