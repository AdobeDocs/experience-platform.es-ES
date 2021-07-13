---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;Segmentación;crear un conjunto de datos;exportar segmento de audiencia;exportar segmento;
solution: Experience Platform
title: Crear un conjunto de datos para exportar un segmento de audiencia
topic-legacy: tutorial
type: Tutorial
description: Este tutorial explica los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante la interfaz de usuario del Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 44d7e11e79ed0e6041ff2e4438ddb7141ae3532d
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---

# Creación de un conjunto de datos para exportar un segmento de audiencia

[!DNL Adobe Experience Platform] le permite segmentar perfiles de clientes en audiencias en función de atributos específicos. Una vez creado un segmento, puede exportar esa audiencia a un conjunto de datos en el que se pueda acceder a él y actuar en consecuencia. Para que la exportación se realice correctamente, el conjunto de datos debe configurarse correctamente.

Este tutorial explica los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante la interfaz de usuario [!DNL Experience Platform].

Este tutorial está directamente relacionado con los pasos descritos en el tutorial sobre [evaluación y acceso a los resultados del segmento](./evaluate-a-segment.md). El tutorial de evaluación de segmentos proporciona pasos para crear un conjunto de datos mediante la API [!DNL Catalog Service] , mientras que este tutorial describe los pasos para crear un conjunto de datos mediante la interfaz de usuario [!DNL Experience Platform] .

## Primeros pasos

Para exportar un segmento, el conjunto de datos debe basarse en [!DNL XDM Individual Profile Union Schema]. Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de todos los esquemas que comparten la misma clase. Para obtener más información sobre los esquemas de unión, consulte la guía sobre [los conceptos básicos de la composición de esquema](../../xdm/schema/composition.md#union).

Para ver los esquemas de unión en la interfaz de usuario, seleccione **[!UICONTROL Profiles]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Union Schema]** como se muestra a continuación.

![Ficha Esquema de unión en la interfaz de usuario del Experience Platform](../images/tutorials/segment-export-dataset/union.png)


## Espacio de trabajo de conjuntos de datos

El espacio de trabajo [!UICONTROL Datasets] permite ver y administrar todos los conjuntos de datos de su organización.

Seleccione **[!UICONTROL Datasets]** en el panel de navegación izquierdo para acceder al espacio de trabajo y, a continuación, seleccione **[!UICONTROL Browse]**. Esta pestaña muestra una lista de conjuntos de datos y sus detalles. Según el ancho de cada columna, puede que sea necesario desplazarse a la izquierda o a la derecha para ver todas las columnas.

>[!NOTE]
>
>Seleccione el icono de filtro junto a la barra de búsqueda para utilizar las funcionalidades de filtrado para ver solo aquellos conjuntos de datos habilitados para [!DNL Real-time Customer Profile].

![Ver conjuntos de datos](../images/tutorials/segment-export-dataset/browse.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, seleccione **[!UICONTROL Crear conjunto de datos]**.

![Seleccionar Crear conjunto de datos](../images/tutorials/segment-export-dataset/create-dataset.png)

En la siguiente pantalla, seleccione **[!UICONTROL Crear conjunto de datos desde esquema]**.

![Seleccionar fuente de datos](../images/tutorials/segment-export-dataset/create-from-schema.png)

## Seleccionar esquema de unión de perfil individual XDM

Para seleccionar el [!DNL XDM Individual Profile Union Schema] para utilizarlo en el conjunto de datos, busque el esquema &quot;[!UICONTROL XDM Individual Profile]&quot; en la pantalla **[!UICONTROL Seleccionar esquema]**. Una vez seleccionado el esquema, puede confirmar si es el esquema de unión en **[!UICONTROL Uso de API]** en el carril derecho. Si la ruta [!UICONTROL Schema] termina con `_union`, es un esquema de unión.

>[!NOTE]
>
>A pesar del hecho de que los esquemas de unión participan en el Perfil del cliente en tiempo real por definición, se enumeran como &quot;No habilitado&quot; debido al hecho de que no están habilitados para Perfil de la misma manera que los esquemas tradicionales.

Seleccione el botón de opción situado junto a **[!UICONTROL XDM Individual Profile]** y, a continuación, seleccione **[!UICONTROL Next]**.

![Seleccionar esquema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar el conjunto de datos

En la siguiente pantalla, debe asignar un nombre al conjunto de datos. También puede añadir una descripción opcional.

**Notas sobre los nombres de conjuntos de datos:**
* Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que el conjunto de datos se pueda encontrar fácilmente en la biblioteca más adelante.
* Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro.
* Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que podría ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tiene un nombre y una descripción, seleccione **[!UICONTROL Finish]**.

![Configurar el conjunto de datos](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Actividad del conjunto de datos

Una vez creado el conjunto de datos, se le proporcionará la página de actividad para ese conjunto de datos. Debería ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación de que &quot;No se han agregado lotes&quot;. Esto es de esperar, ya que aún no ha agregado ningún lote a este conjunto de datos.

El carril correcto contiene información relacionada con su nuevo conjunto de datos, como ID del conjunto de datos, nombre, descripción, esquema, etc. Tenga en cuenta el **[!UICONTROL ID del conjunto de datos]**, ya que este valor es necesario para completar el flujo de trabajo de exportación del segmento de audiencia.

![Actividad del conjunto de datos](../images/tutorials/segment-export-dataset/activity.png)

## Pasos siguientes

Ahora que ha creado un conjunto de datos basado en [!DNL XDM Individual Profile Union Schema], puede utilizar el ID del conjunto de datos para continuar con el tutorial [evaluación y acceso a los resultados del segmento](./evaluate-a-segment.md).

En este momento, vuelva al tutorial de evaluación de resultados de segmentos y tome nota del paso [generación de perfiles para miembros de audiencia](./evaluate-a-segment.md#generate-profiles) de exportación de un flujo de trabajo de segmentos.
