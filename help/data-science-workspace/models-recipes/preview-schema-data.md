---
keywords: Experience Platform;previsualizar datos de esquema;Data Science Workspace;temas populares
solution: Experience Platform
title: Vista previa del esquema y el conjunto de datos de ventas minoristas
type: Tutorial
description: El siguiente documento describe la vista previa de esquemas y conjuntos de datos en Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 3%

---

# Previsualizar el esquema de ventas minoristas y el conjunto de datos

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Una vez completado correctamente el script de bootstrap del tutorial [retail sales schema and dataset](./create-retails-sales-dataset.md). Los esquemas y conjuntos de datos de salida se pueden ver en [!DNL Experience Platform]. Para ver los esquemas y conjuntos de datos, siga los pasos a continuación:

Seleccione la ficha **[!UICONTROL Esquemas]** ubicada en el panel de navegación izquierdo y busque el esquema de entrada creado por el script de bootstrap. El nombre del esquema corresponderá al definido en `config.yaml` desde el paso anterior. Vea los detalles del esquema y su composición haciendo clic en él.

![](../images/models-recipes/access-data/schema.PNG)

Seleccione la pestaña **[!UICONTROL Conjuntos de datos]** ubicada en el panel de navegación izquierdo y abra el conjunto de datos de entrada que se creó al seleccionar el nombre del conjunto de datos. El nombre del conjunto de datos corresponde a lo que se definió en `config.yaml` desde el paso anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Seleccione **[!UICONTROL Previsualizar conjunto de datos]** ubicado en la parte superior derecha para obtener una vista previa de un subconjunto del conjunto de datos.

![](../images/models-recipes/access-data/preview.PNG)

## Pasos siguientes

Ahora ha ingerido correctamente datos de muestra de ventas minoristas en [!DNL Experience Platform] mediante el script de arranque proporcionado.

Para seguir trabajando con los datos introducidos:
- [Analice sus datos con Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Use Jupyter Notebooks en [!DNL Data Science Workspace] para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] empaquetando los archivos de origen en un archivo de fórmula importable.
