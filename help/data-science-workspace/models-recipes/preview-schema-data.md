---
keywords: Experience Platform;datos de esquema de previsualización;Área de trabajo de ciencia de datos;temas populares
solution: Experience Platform
title: Previsualización del Esquema de ventas minoristas y del conjunto de datos
topic: tutorial
type: Tutorial
description: El siguiente documento describe la vista previa de esquemas y conjuntos de datos en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Previsualización del esquema y conjunto de datos de ventas minoristas

Tras completar correctamente la secuencia de comandos de bootstrap desde el tutorial [Crear el esquema de ventas minoristas y el conjunto de datos](./create-retails-sales-dataset.md). Los esquemas y conjuntos de datos de salida se pueden ver en [!DNL Experience Platform]. Para realizar la vista de los esquemas y conjuntos de datos, siga los pasos a continuación:

1. Haga clic en el vínculo **[!UICONTROL Esquemas]** ubicado en la columna de navegación izquierda y busque el esquema de entrada creado por la secuencia de comandos de arranque. El nombre del esquema corresponderá a lo que se definió en `config.yaml` del paso anterior. Vista los detalles del esquema y su composición haciendo clic en él.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Haga clic en el vínculo **[!UICONTROL Datasets]** ubicado en la columna de navegación izquierda y abra el conjunto de datos de entrada que se creó haciendo clic en el nombre del listado. El nombre del conjunto de datos corresponderá a lo que se definió en `config.yaml` del paso anterior.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Haga clic en **[!UICONTROL Conjunto de datos de Previsualización]** ubicado en la previsualización superior derecha de un subconjunto del conjunto de datos.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Pasos siguientes

Ahora ha ingerido correctamente datos de muestra de ventas minoristas en [!DNL Experience Platform] mediante la secuencia de comandos de arranque proporcionada.

Para continuar trabajando con los datos ingestados:
- [Analizar los datos con los equipos portátiles Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilice los portátiles Jupyter de [!DNL Data Science Workspace] para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] mediante el empaquetado de archivos de origen en un archivo de fórmula importable.