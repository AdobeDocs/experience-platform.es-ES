---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;Segmentation;create a dataset;export audience segment;export segment;
solution: Experience Platform
title: Crear un conjunto de datos para exportar un segmento de audiencia
topic: tutorial
type: Tutorial
description: En este tutorial se explican los pasos necesarios para crear un conjunto de datos que pueda utilizarse para exportar un segmento de audiencia mediante la interfaz de usuario del Experience Platform.
translation-type: tm+mt
source-git-commit: fce215edb99cccc8be0109f8743c9e56cace2be0
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---


# Crear un conjunto de datos para exportar un segmento de audiencia

[!DNL Adobe Experience Platform] le permite segmentar fácilmente perfiles de clientes en audiencias basadas en atributos específicos. Una vez creados los segmentos, puede exportar esa audiencia a un conjunto de datos donde se pueda acceder a ella y actuar en consecuencia. Para que la exportación se realice correctamente, el conjunto de datos debe configurarse correctamente.

En este tutorial se explican los pasos necesarios para crear un conjunto de datos que se pueda utilizar para exportar un segmento de audiencia mediante la [!DNL Experience Platform] interfaz de usuario.

Este tutorial está directamente relacionado con los pasos descritos en el tutorial para [evaluar y acceder a los resultados](./evaluate-a-segment.md)del segmento. En el tutorial de evaluación de un segmento se proporcionan pasos para crear un conjunto de datos mediante la [!DNL Catalog Service] API, mientras que en este tutorial se describen los pasos para crear un conjunto de datos mediante la [!DNL Experience Platform] interfaz de usuario.

## Primeros pasos

Para exportar un segmento, el conjunto de datos debe basarse en el [!DNL XDM Individual Profile Union Schema]. Un esquema de unión es un esquema de sólo lectura generado por el sistema que agrega los campos de todos los esquemas que comparten la misma clase, en este caso la [!DNL XDM Individual Profile] clase. Para obtener más información sobre los esquemas de vista de uniones, consulte la sección Perfil de clientes en tiempo [real de la guía](../../xdm/schema/composition.md#union)para desarrolladores de Esquema Registry.

Para vista de esquemas de unión en la interfaz de usuario, haga clic en **[!UICONTROL Perfiles]** en el panel de navegación izquierdo y, a continuación, haga clic en la ficha esquema **[!UICONTROL de]** Unión como se muestra a continuación.

![Ficha esquema de unión en la interfaz de usuario de Experience Platform](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## Espacio de trabajo de conjuntos de datos

El espacio de trabajo de conjuntos de datos dentro de la interfaz de usuario le permite realizar vistas y administrar todos los conjuntos de datos que ha realizado su organización de IMS, así como crear otros nuevos. [!DNL Experience Platform]

Para vista del espacio de trabajo de conjuntos de datos, haga clic en **[!UICONTROL Conjuntos]** de datos en el panel de navegación izquierdo y, a continuación, haga clic en la ficha **[!UICONTROL Examinar]** . El espacio de trabajo de conjuntos de datos contiene una lista de conjuntos de datos, que incluye columnas con el nombre, la fecha y la hora de creación, el origen, el esquema y el estado del último lote, así como la fecha y la hora de la última actualización del conjunto de datos. Según el ancho de cada columna, puede que sea necesario desplazarse hacia la izquierda o la derecha para ver todas las columnas.

>[!NOTE]
>
>Haga clic en el icono de filtro situado junto a la barra de búsqueda para utilizar las capacidades de filtrado con el fin de vista solo de los conjuntos de datos habilitados para [!DNL Real-time Customer Profile].

![Vista de todos los conjuntos de datos](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## Crear un conjunto de datos

Para crear un conjunto de datos, haga clic en **[!UICONTROL Crear conjunto]** de datos en la esquina superior derecha del espacio de trabajo **[!UICONTROL Conjuntos]** de datos.

![Haga clic en Crear conjunto de datos](../images/tutorials/segment-export-dataset/dataset-click-create.png)

En la pantalla **[!UICONTROL Crear conjunto de datos]** , haga clic en **[!UICONTROL Crear conjunto de datos desde Esquema]** para continuar.

![Seleccionar fuente de datos](../images/tutorials/segment-export-dataset/create-dataset.png)

## Seleccionar Esquema de Unión de Perfil individual XDM

Para seleccionar el [!DNL XDM Individual Profile Union Schema] que se usará en el conjunto de datos, busque el esquema &quot;Perfil[!UICONTROL individual]XDM&quot; con un tipo de &quot;[!UICONTROL Unión]&quot; en la pantalla **[!UICONTROL Seleccionar Esquema]** .

Seleccione el botón de radio junto a Perfil **[!UICONTROL individual]** XDM y, a continuación, haga clic en **[!UICONTROL Siguiente]** en la esquina superior derecha.

![Seleccionar esquema](../images/tutorials/segment-export-dataset/select-schema.png)

## Configurar el conjunto de datos

En la pantalla **[!UICONTROL Configurar conjunto de datos]** , se le pedirá que asigne un nombre al conjunto de datos y que también proporcione una descripción del conjunto de datos.

**Notas sobre los nombres de conjuntos de datos:**
- Los nombres de los conjuntos de datos deben ser cortos y descriptivos para que el conjunto de datos pueda encontrarse fácilmente en la biblioteca más adelante.
- Los nombres de los conjuntos de datos deben ser únicos, lo que significa que también deben ser lo suficientemente específicos como para que no se vuelvan a utilizar en el futuro.
- Se recomienda proporcionar información adicional sobre el conjunto de datos mediante el campo de descripción, ya que puede ayudar a otros usuarios a diferenciar entre conjuntos de datos en el futuro.

Una vez que el conjunto de datos tenga un nombre y una descripción, haga clic en **[!UICONTROL Finalizar]**.

![Configurar el conjunto de datos](../images/tutorials/segment-export-dataset/configure-dataset.png)

## Actividad de conjunto de datos

Ahora se ha creado un conjunto de datos vacío y se le ha devuelto a la ficha Actividad **[!UICONTROL del]** conjunto de datos en el espacio de trabajo **[!UICONTROL Conjuntos]** de datos. Debe ver el nombre del conjunto de datos en la esquina superior izquierda del espacio de trabajo, junto con una notificación de que &quot;No se han agregado lotes&quot;. Esto es de esperar, ya que todavía no ha agregado ningún lote a este conjunto de datos.

A la derecha del espacio de trabajo Conjunto de datos, verá la ficha **[!UICONTROL Información]** que contiene información relacionada con el nuevo conjunto de datos, como ID de conjunto de datos, nombre, descripción, nombre de tabla, esquema, flujo continuo y origen. La ficha **[!UICONTROL Información]** también incluye información sobre cuándo se creó el conjunto de datos y su fecha de última modificación.

Tenga en cuenta el ID **[!UICONTROL del]** conjunto de datos, ya que este valor es necesario para completar el flujo de trabajo de exportación del segmento de audiencia.

![Actividad de conjunto de datos](../images/tutorials/segment-export-dataset/dataset-activity.png)

## Pasos siguientes

Ahora que ha creado un conjunto de datos basado en el [!DNL XDM Individual Profile Union Schema], puede utilizar el ID del conjunto de datos para continuar con el tutorial de [evaluación y acceso a los resultados](./evaluate-a-segment.md) del segmento.

En este momento, regrese al tutorial de resultados del segmento de evaluación y tome el paso [de generación de perfiles para miembros](./evaluate-a-segment.md#generate-profiles) de audiencia de la exportación de un flujo de trabajo de segmentos.
