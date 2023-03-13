---
keywords: Experience Platform;previsualizar datos de esquema;Data Science Workspace;temas populares
solution: Experience Platform
title: Vista previa del esquema y el conjunto de datos de ventas minoristas
type: Tutorial
description: El siguiente documento describe la vista previa de esquemas y conjuntos de datos en Adobe Experience Platform.
exl-id: dca9835b-4f76-42cc-b262-b20323bf4356
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Previsualizar el esquema de ventas minoristas y el conjunto de datos

Una vez completado correctamente el script de bootstrap desde el [esquema y conjunto de datos de ventas minoristas](./create-retails-sales-dataset.md) tutorial. Los esquemas y conjuntos de datos de salida se pueden ver en [!DNL Experience Platform]. Para ver los esquemas y conjuntos de datos, siga los pasos a continuación:

Seleccione el **[!UICONTROL Esquemas]** situado en el panel de navegación izquierdo y busque el esquema de entrada creado por el script de bootstrap. El nombre del esquema se corresponderá con lo definido en `config.yaml` del paso anterior. Vea los detalles del esquema y su composición haciendo clic en él.

![](../images/models-recipes/access-data/schema.PNG)

Seleccione el **[!UICONTROL Conjuntos de datos]** pestaña situada en el panel de navegación izquierdo y abra el conjunto de datos de entrada que se creó seleccionando el nombre del conjunto de datos. El nombre del conjunto de datos corresponde a lo que se definió en `config.yaml` del paso anterior.

![](../images/models-recipes/access-data/dataset.PNG)

Seleccionar **[!UICONTROL Previsualizar conjunto de datos]** situado en la parte superior derecha para previsualizar un subconjunto del conjunto de datos.

![](../images/models-recipes/access-data/preview.PNG)

## Pasos siguientes

Ahora ha ingerido correctamente datos de muestra de ventas minoristas en [!DNL Experience Platform] utilizando el script de bootstrap proporcionado.

Para seguir trabajando con los datos introducidos:
- [Analice sus datos con Jupyter Notebooks](../jupyterlab/analyze-your-data.md)
   - Uso de Jupyter Notebooks en [!DNL Data Science Workspace] para acceder, explorar, visualizar y comprender sus datos.
- [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md)
   - Siga este tutorial para aprender a incorporar su propio modelo a [!DNL Data Science Workspace] empaquetando archivos de origen en un archivo de fórmula importable.
