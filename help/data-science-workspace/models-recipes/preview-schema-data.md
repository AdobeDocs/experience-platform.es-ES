---
keywords: Experience Platform;preview schema data;Data Science Workspace;popular topics
solution: Experience Platform
title: esquemas y conjuntos de datos de Previsualización
topic: Tutorial
translation-type: tm+mt
source-git-commit: 11eb1859f3e4b059765709e750f18b61509a2f93

---


# esquemas y conjuntos de datos de Previsualización

Una vez completada correctamente la secuencia de comandos de arranque desde el tutorial [Crear el esquema de ventas minoristas y el conjunto de datos](./create-retails-sales-dataset.md) . Los esquemas de salida y los conjuntos de datos se pueden ver en la plataforma de experiencias. Para realizar la vista de los esquemas y conjuntos de datos, siga los pasos a continuación:

1. Haga clic en el vínculo **Esquemas** ubicado en la columna de navegación izquierda y busque el esquema de entrada creado por la secuencia de comandos de arranque. El nombre del esquema corresponderá a lo que se definió en `config.yaml` el paso anterior. Vista los detalles del esquema y su composición haciendo clic en él.

   ![](../images/models-recipes/access-data/schema_overview.png)

2. Haga clic en el vínculo **Conjuntos** de datos ubicado en la columna de navegación izquierda y abra el conjunto de datos de entrada que se creó haciendo clic en el nombre del listado. El nombre del conjunto de datos corresponderá a lo que se definió en `config.yaml` el paso anterior.

   ![](../images/models-recipes/access-data/dataset_overview.png)

3. Haga clic en **Previsualización Conjunto de datos** ubicado en la previsualización superior derecha de un subconjunto del conjunto de datos.

   ![](../images/models-recipes/access-data/preview_dataset.png)

## Pasos siguientes

Ahora ha ingerido correctamente los datos de muestra de ventas minoristas en la plataforma de experiencias mediante el script de arranque proporcionado.

Para continuar trabajando con los datos ingestados:
- [Analizar los datos con los blocs de notas de Jupyter](../jupyterlab/analyze-your-data.md)
   - Utilice los blocs de notas Jupyter en el área de trabajo de ciencia de datos para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a Área de trabajo de ciencias de datos empaquetando archivos de origen en un archivo de fórmula importable.