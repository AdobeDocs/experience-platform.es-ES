---
keywords: Experience Platform;vista previa de datos de esquema;Data Science Workspace;temas populares
solution: Experience Platform
title: Vista previa del esquema de ventas minoristas y el conjunto de datos
type: Tutorial
description: El siguiente documento describe la vista previa de esquemas y conjuntos de datos en Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Vista previa del esquema de ventas minoristas y el conjunto de datos

Una vez completado correctamente el script bootstrap desde la [esquema de ventas minoristas y conjunto de datos](./create-retails-sales-dataset.md) tutorial. Los esquemas de salida y los conjuntos de datos se pueden ver en [!DNL Experience Platform]. Para ver los esquemas y conjuntos de datos, siga los pasos a continuación:

Seleccione el **[!UICONTROL Esquemas]** situado en la parte izquierda de navegación y busque el esquema de entrada creado por el script bootstrap. El nombre del esquema corresponderá a lo definido en `config.yaml` del paso anterior. Para ver los detalles del esquema y su composición, haga clic en él.

![](../images/models-recipes/access-data/schema.PNG)

Seleccione el **[!UICONTROL Conjuntos de datos]** ubicada en la navegación izquierda y abra el conjunto de datos de entrada creado seleccionando el nombre del conjunto de datos. El nombre del conjunto de datos corresponde a lo que se definió en `config.yaml` del paso anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Select **[!UICONTROL Vista previa del conjunto de datos]** situado en la parte superior derecha para obtener una vista previa de un subconjunto del conjunto de datos.

![](../images/models-recipes/access-data/preview.PNG)

## Pasos siguientes

Ahora ha introducido correctamente los datos de muestra de ventas minoristas en [!DNL Experience Platform] usando el script de arranque proporcionado.

Para continuar trabajando con los datos introducidos:
- [Analizar los datos con Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Usar equipos portátiles de Jupyter en [!DNL Data Science Workspace] para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] empaquetando archivos de origen en un archivo de fórmula importable.
