---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;Segmentación;crear un conjunto de datos;exportar segmento de audiencia;exportar segmento;
solution: Experience Platform
title: Crear un conjunto de datos para exportar un segmento de audiencia
topic-legacy: tutorial
type: Tutorial
description: Este tutorial explica los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante la interfaz de usuario del Experience Platform.
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 1%

---

# Creación de un conjunto de datos para exportar un segmento de audiencia

[!DNL Adobe Experience Platform] le permite segmentar fácilmente perfiles de clientes en audiencias basadas en atributos específicos. Una vez creados los segmentos, puede exportar esa audiencia a un conjunto de datos en el que se pueda acceder a ella y actuar en consecuencia. Para que la exportación se realice correctamente, el conjunto de datos debe configurarse correctamente.

Este tutorial explica los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante la interfaz de usuario [!DNL Experience Platform].

Este tutorial está directamente relacionado con los pasos descritos en el tutorial para [evaluar y acceder a los resultados del segmento](./evaluate-a-segment.md). El tutorial de evaluación de un segmento proporciona pasos para crear un conjunto de datos mediante la API [!DNL Catalog Service] , mientras que este tutorial describe los pasos para crear un conjunto de datos mediante la interfaz de usuario [!DNL Experience Platform] .

## Primeros pasos

Para exportar un segmento, el conjunto de datos debe basarse en [!DNL XDM Individual Profile Union Schema]. Un esquema de unión es un esquema de solo lectura generado por el sistema que agrega los campos de todos los esquemas que comparten la misma clase, en este caso que es la clase [!DNL XDM Individual Profile]. Para obtener más información sobre los esquemas de vista de unión, consulte la sección [Perfil del cliente en tiempo real de la guía para desarrolladores del Registro de esquemas](../../xdm/schema/composition.md#union).

Para ver los esquemas de unión en la interfaz de usuario, haga clic en **[!UICONTROL Profiles]** en el panel de navegación izquierdo y, a continuación, haga clic en la pestaña **[!UICONTROL Union schema]** como se muestra a continuación.

![Ficha Esquema de unión en la interfaz de usuario del Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espacio de trabajo de conjuntos de datos

El espacio de trabajo de los conjuntos de datos dentro de la interfaz de usuario [!DNL Experience Platform] le permite ver y administrar todos los conjuntos de datos que ha realizado su organización de IMS, así como crear otros nuevos.

Para ver el espacio de trabajo de los conjuntos de datos, haga clic en **[!UICONTROL Datasets]** en la navegación izquierda y, a continuación, haga clic en la pestaña **[!UICONTROL Browse]**. El espacio de trabajo de conjuntos de datos contiene una lista de conjuntos de datos, que incluye columnas que muestran el nombre, la fecha y la hora creadas, el origen, el esquema y el estado del último lote, así como la fecha y la hora de la última actualización del conjunto de datos. Según el ancho de cada columna, puede que sea necesario desplazarse a la izquierda o a la derecha para ver todas las columnas.

>[!NOTE]
>
>Haga clic en el icono de filtro junto a la barra de búsqueda para utilizar las funcionalidades de filtrado para ver solo los conjuntos de datos habilitados para [!DNL Real-time Customer Profile].

![Ver todos los conjuntos de datos](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, haga clic en **[!UICONTROL Create Dataset]** en la esquina superior derecha del espacio de trabajo **[!UICONTROL Datasets]**.

![Haga clic en Crear conjunto de datos](../images/tutorials/segment-export-dataset/dataset-click-create.png)

En la pantalla **[!UICONTROL Create Dataset]**, haga clic en **[!UICONTROL Create Dataset from Schema]** para continuar.

![Seleccionar fuente de datos](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleccionar esquema de unión de perfil individual XDM

Para seleccionar [!DNL XDM Individual Profile Union Schema] para usar en el conjunto de datos, busque el esquema &quot;[!UICONTROL XDM Individual Profile]&quot; con un tipo &quot;[!UICONTROL Union]&quot; en la pantalla **[!UICONTROL Select Schema]**.

Seleccione el botón de opción situado junto a **[!UICONTROL XDM Individual Profile]** y haga clic en **[!UICONTROL Next]** en la esquina superior derecha.

![Seleccionar esquema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar el conjunto de datos

En la pantalla **[!UICONTROL Configure Dataset]**, se le pedirá que asigne un nombre al conjunto de datos y que proporcione también una descripción del conjunto de datos.

**Notas sobre los nombres de conjuntos de datos:**
- Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que el conjunto de datos se pueda encontrar fácilmente en la biblioteca más adelante.
- Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro.
- Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que podría ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tiene un nombre y una descripción, haga clic en **[!UICONTROL Finish]**.

![Configurar el conjunto de datos](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Actividad del conjunto de datos

Ahora se ha creado un conjunto de datos vacío y se le ha devuelto a la pestaña **[!UICONTROL Dataset Activity]** en el espacio de trabajo **[!UICONTROL Datasets]**. Debería ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación de que &quot;No se han agregado lotes&quot;. Esto es de esperar, ya que aún no ha agregado ningún lote a este conjunto de datos.

A la derecha del espacio de trabajo de conjuntos de datos , verá la pestaña **[!UICONTROL Info]** que contiene información relacionada con el nuevo conjunto de datos, como ID del conjunto de datos, nombre, descripción, nombre de tabla, esquema, flujo continuo y origen. La pestaña **[!UICONTROL Info]** también incluye información sobre cuándo se creó el conjunto de datos y su última fecha de modificación.

Tenga en cuenta el **[!UICONTROL Dataset ID]**, ya que este valor es necesario para completar el flujo de trabajo de exportación de segmentos de audiencia.

![Actividad del conjunto de datos](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Pasos siguientes

Ahora que ha creado un conjunto de datos basado en [!DNL XDM Individual Profile Union Schema], puede utilizar el ID del conjunto de datos para continuar con el tutorial [evaluación y acceso a los resultados del segmento](./evaluate-a-segment.md).

En este momento, vuelva al tutorial de evaluación de resultados de segmentos y tome nota del paso [generación de perfiles para miembros de audiencia](./evaluate-a-segment.md#generate-profiles) de exportación de un flujo de trabajo de segmentos.
