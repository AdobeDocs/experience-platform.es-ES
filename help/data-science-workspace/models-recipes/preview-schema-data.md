---
keywords: Experience Platform;vista previa de datos de esquema;Data Science Workspace;temas populares
solution: Experience Platform
title: Vista previa del esquema de ventas minoristas y el conjunto de datos
topic-legacy: tutorial
type: Tutorial
description: El siguiente documento describe la vista previa de esquemas y conjuntos de datos en Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# Vista previa del esquema de ventas minoristas y el conjunto de datos

Una vez completada correctamente la secuencia de comandos de arranque desde el tutorial [retail sales schema and dataset](./create-retails-sales-dataset.md). Los esquemas de salida y los conjuntos de datos se pueden ver en [!DNL Experience Platform]. Para ver los esquemas y conjuntos de datos, siga los pasos a continuación:

Seleccione la pestaña **[!UICONTROL Schemas]** ubicada en la navegación izquierda y busque el esquema de entrada creado por el script de arranque. El nombre del esquema corresponderá a lo que se definió en `config.yaml` desde el paso anterior. Para ver los detalles del esquema y su composición, haga clic en él.

![](../images/models-recipes/access-data/schema.PNG)

Seleccione la pestaña **[!UICONTROL Datasets]** ubicada en la navegación izquierda y abra el conjunto de datos de entrada creado seleccionando el nombre del conjunto de datos. El nombre del conjunto de datos corresponde a lo que se definió en `config.yaml` desde el paso anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Seleccione **[!UICONTROL Preview Dataset]** , en la parte superior derecha, para obtener una vista previa de un subconjunto del conjunto de datos.

![](../images/models-recipes/access-data/preview.PNG)

## Pasos siguientes

Ahora ha introducido correctamente los datos de muestra de ventas minoristas en [!DNL Experience Platform] utilizando el script de arranque proporcionado.

Para continuar trabajando con los datos introducidos:
- [Analizar los datos con Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Utilice portátiles Jupyter en [!DNL Data Science Workspace] para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a introducir su propio modelo en [!DNL Data Science Workspace] empaquetando archivos de origen en un archivo de fórmula importable.
