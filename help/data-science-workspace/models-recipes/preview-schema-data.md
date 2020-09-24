---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: Esquemas y conjuntos de datos de previsualización
topic: tutorial
type: Tutorial
description: El siguiente documento describe la vista previa de esquemas y conjuntos de datos en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Esquemas y conjuntos de datos de previsualización

Una vez completada correctamente la secuencia de comandos de arranque desde el tutorial [Crear el esquema de ventas minoristas y el conjunto de datos](./create-retails-sales-dataset.md) . Los esquemas de salida y los conjuntos de datos se pueden ver en [!DNL Experience Platform]. Para realizar la vista de los esquemas y conjuntos de datos, siga los pasos a continuación:

1. Haga clic en el vínculo **[!UICONTROL Esquemas]** ubicado en la columna de navegación izquierda y busque el esquema de entrada creado por la secuencia de comandos de arranque. El nombre del esquema corresponderá a lo que se definió en `config.yaml` el paso anterior. Vista los detalles del esquema y su composición haciendo clic en él.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Haga clic en el vínculo **[!UICONTROL Conjuntos]** de datos ubicado en la columna de navegación izquierda y abra el conjunto de datos de entrada que se creó haciendo clic en el nombre del listado. El nombre del conjunto de datos corresponderá a lo que se definió en `config.yaml` el paso anterior.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Haga clic en **[!UICONTROL Previsualización Conjunto de datos]** ubicado en la previsualización superior derecha de un subconjunto del conjunto de datos.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Pasos siguientes

Ahora ha ingerido correctamente los datos de muestra de ventas minoristas en [!DNL Experience Platform] el uso de la secuencia de comandos de arranque proporcionada.

Para continuar trabajando con los datos ingestados:
- [Analizar los datos con los blocs de notas de Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilice los blocs de notas de Jupyter en [!DNL Data Science Workspace] para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo [!DNL Data Science Workspace] mediante el empaquetado de archivos de origen en un archivo de fórmula importable.