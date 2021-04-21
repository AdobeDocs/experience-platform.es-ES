---
keywords: Experience Platform;importar fórmula empaquetada;Data Science Workspace;temas populares;fórmulas;ui;crear motor
solution: Experience Platform
title: Importar una fórmula empaquetada en la interfaz de usuario de Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Este tutorial proporciona información sobre cómo configurar e importar una fórmula empaquetada mediante el ejemplo de ventas minoristas proporcionado. Al final de este tutorial, estará listo para crear, entrenar y evaluar un modelo en Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1738'
ht-degree: 0%

---

# Importar una fórmula empaquetada en la interfaz de usuario de Data Science Workspace

Este tutorial proporciona información sobre cómo configurar e importar una fórmula empaquetada mediante el ejemplo de ventas minoristas proporcionado. Al final de este tutorial, estará listo para crear, entrenar y evaluar un modelo en Adobe Experience Platform [!DNL Data Science Workspace].

## Requisitos previos

Este tutorial requiere una fórmula empaquetada en forma de URL de imagen Docker. Consulte el tutorial sobre cómo [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) para obtener más información.

## Flujo de trabajo de la interfaz de usuario

La importación de una fórmula empaquetada en [!DNL Data Science Workspace] requiere configuraciones de fórmula específicas, compiladas en un único archivo de Notación de objetos JavaScript (JSON), esta compilación de configuraciones de fórmula se denomina archivo de configuración. Una fórmula empaquetada con un conjunto particular de configuraciones se denomina instancia de fórmula. Se puede usar una fórmula para crear muchas instancias de fórmula en [!DNL Data Science Workspace].

El flujo de trabajo para importar una fórmula de paquete consta de los siguientes pasos:
- [Configurar una fórmula](#configure)
- [Importar fórmula basada en Docker: Python](#python)
- [Importar fórmula basada en Docker - R](#r)
- [Importar fórmula basada en Docker - PySpark](#pyspark)
- [Importar fórmula basada en Docker - Scala](#scala)

### Configurar una fórmula {#configure}

Cada instancia de fórmula de [!DNL Data Science Workspace] va acompañada de un conjunto de configuraciones que adaptan la instancia de fórmula a un caso de uso determinado. Los archivos de configuración definen los comportamientos de formación y puntuación predeterminados de un modelo creado con esta instancia de fórmula.

>[!NOTE]
>
>Los archivos de configuración son específicos de fórmula y de caso.

A continuación, se muestra un archivo de configuración de muestra con los comportamientos de puntuación y formación predeterminados para la fórmula de ventas minoristas.

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "learning_rate",
                "value": "0.1"  
            },
            {
                "key": "n_estimators",
                "value": "100"
            },
            {
                "key": "max_depth",
                "value": "3"
            },
            {
                "key": "ACP_DSW_INPUT_FEATURES",
                "value": "date,store,storeType,storeSize,temperature,regionalFuelPrice,markdown,cpi,unemployment,isHoliday"
            },
            {
                "key": "ACP_DSW_TARGET_FEATURES",
                "value": "weeklySales"
            },
            {
                "key": "ACP_DSW_FEATURE_UPDATE_SUPPORT",
                "value": false
            },
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key": "ACP_DSW_TRAINING_XDM_SCHEMA",
                "value": "{SEE BELOW FOR DETAILS}"
            },
            {
                "key": "evaluation.labelColumn",
                "value": "weeklySalesAhead"
            },
            {
                "key": "evaluation.metrics",
                "value": "MAPE,MAE,RMSE,MASE"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "tenantId",
                "value": "_{TENANT_ID}"
            },
            {
                "key":"ACP_DSW_SCORING_RESULTS_XDM_SCHEMA",
                "value":"{SEE BELOW FOR DETAILS}"
            }
        ]
    }
]
```

| Clave de parámetro | Tipo | Descripción |
| ----- | ----- | ----- |
| `learning_rate` | Número | Escalar para la multiplicación de degradado. |
| `n_estimators` | Número | Número de árboles del bosque para el clasificador de bosque aleatorio. |
| `max_depth` | Número | Profundidad máxima de un árbol en el clasificador de bosque aleatorio. |
| `ACP_DSW_INPUT_FEATURES` | Cadena | Lista de los atributos de esquema de entrada separados por comas. |
| `ACP_DSW_TARGET_FEATURES` | Cadena | Lista de los atributos de esquema de salida separados por comas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina si las funciones de entrada y salida se pueden modificar |
| `tenantId` | Cadena | Este ID garantiza que los recursos que cree tengan un espacio de nombres adecuado y estén contenidos dentro de su organización de IMS. [Siga los pasos ](../../xdm/api/getting-started.md#know-your-tenant_id) aquí para encontrar su ID de inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Cadena | El esquema de entrada utilizado para entrenar un modelo. Deje esto vacío al importar en la interfaz de usuario, reemplace por SchemaID de capacitación al importar mediante API. |
| `evaluation.labelColumn` | Cadena | Etiqueta de columna para visualizaciones de evaluación. |
| `evaluation.metrics` | Cadena | Lista separada por comas de las métricas de evaluación que se utilizarán para evaluar un modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Cadena | El esquema de salida utilizado para puntuación de un modelo. Deje esto vacío al importar en la interfaz de usuario, reemplace con Scoring SchemaID al importar con API. |

A los efectos de este tutorial, puede dejar los archivos de configuración predeterminados para la fórmula Venta minorista en la [!DNL Data Science Workspace] Referencia de la forma en que están.

### Importar fórmula basada en Docker: [!DNL Python] {#python}

Comience por navegar y seleccionar **[!UICONTROL Workflows]** , que se encuentra en la parte superior izquierda de la [!DNL Platform] interfaz de usuario. A continuación, seleccione **Import recipe** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Aparece la página **Configurar** para el flujo de trabajo **Importar fórmula**. Introduzca un nombre y una descripción para la fórmula y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el tutorial [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md), se proporcionó una URL de Docker al final de la generación de la fórmula de ventas minoristas utilizando archivos de origen Python.

Una vez que esté en la página **Select source**, pegue la URL del Docker correspondiente a la fórmula empaquetada creada utilizando [!DNL Python] archivos de origen en el campo **[!UICONTROL Source URL]**. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el sistema de archivos **Explorador**. El archivo de configuración proporcionado se puede encontrar en `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Seleccione **[!UICONTROL Python]** en la lista desplegable **Runtime** y **[!UICONTROL Classification]** en la lista desplegable **Type**. Una vez rellenado todo, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar con **Administrar esquemas**.

>[!NOTE]
>
> El tipo admite **[!UICONTROL Classification]** y **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales en la sección **Administrar esquemas**, que se crearon utilizando el script de arranque proporcionado en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En la sección **Administración de funciones**, seleccione en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada Venta minorista. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la ventana derecha **[!UICONTROL Field Properties]**. Para los fines de este tutorial, establezca **[!UICONTROL weeklySales]** como **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Seleccione **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

Revise la fórmula, añada, modifique o elimine configuraciones según sea necesario. Seleccione **[!UICONTROL Finish]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] utilizando la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en Docker - R {#r}

Comience por navegar y seleccionar **[!UICONTROL Workflows]** , que se encuentra en la parte superior izquierda de la [!DNL Platform] interfaz de usuario. A continuación, seleccione **Import recipe** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Aparece la página **Configurar** para el flujo de trabajo **Importar fórmula**. Introduzca un nombre y una descripción para la fórmula y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el tutorial [Empaquete los archivos de origen en una fórmula](./package-source-files-recipe.md), se proporcionó una URL de Docker al final de la generación de la fórmula de ventas minoristas utilizando los archivos de origen R.

Una vez que esté en la página **Select source**, pegue la URL del Docker correspondiente a la fórmula empaquetada creada utilizando archivos de origen R en el campo **[!UICONTROL Source URL]**. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el sistema de archivos **Explorador**. El archivo de configuración proporcionado se puede encontrar en `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Seleccione **[!UICONTROL R]** en la lista desplegable **Runtime** y **[!UICONTROL Classification]** en la lista desplegable **Type**. Una vez rellenado todo, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar con **Administrar esquemas**.

>[!NOTE]
>
> ** Los tipos admiten  **[!UICONTROL Classification]** y  **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales en la sección **Administrar esquemas**, que se crearon utilizando el script de arranque proporcionado en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md).

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En la sección *Administración de funciones*, seleccione en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada Venta minorista. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la ventana derecha **[!UICONTROL Field Properties]**. Para los fines de este tutorial, establezca **[!UICONTROL weeklySales]** como **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Seleccione **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

Revise la fórmula, añada, modifique o elimine configuraciones según sea necesario. Seleccione **Finish** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] utilizando la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en Docker - PySpark {#pyspark}

Comience por navegar y seleccionar **[!UICONTROL Workflows]** , que se encuentra en la parte superior izquierda de la [!DNL Platform] interfaz de usuario. A continuación, seleccione **Import recipe** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Aparece la página **Configurar** para el flujo de trabajo **Importar fórmula**. Introduzca un nombre y una descripción para la fórmula y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el tutorial [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md), se proporcionó una URL de Docker al final de la generación de la fórmula de ventas minoristas utilizando archivos de origen PySpark.

Una vez que esté en la página **Select source**, pegue la URL del Docker correspondiente a la fórmula empaquetada creada utilizando archivos de origen PySpark en el campo **[!UICONTROL Source URL]**. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el sistema de archivos **Explorador**. El archivo de configuración proporcionado se puede encontrar en `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Seleccione **[!UICONTROL PySpark]** en la lista desplegable **Runtime**. Una vez seleccionado el tiempo de ejecución de PySpark, el artefacto predeterminado se rellena automáticamente en **[!UICONTROL Docker]**. A continuación, seleccione **[!UICONTROL Classification]** en la lista desplegable **Type**. Una vez rellenado todo, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar con **Administrar esquemas**.

>[!NOTE]
>
> ** Los tipos admiten  **[!UICONTROL Classification]** y  **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales utilizando el selector **Administrar esquemas**, los esquemas se crearon utilizando el script de arranque proporcionado en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md).

![administrar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

En la sección **Administración de funciones**, seleccione en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada Venta minorista. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la ventana derecha **[!UICONTROL Field Properties]**. Para los fines de este tutorial, establezca **[!UICONTROL weeklySales]** como **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Seleccione **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise la fórmula, añada, modifique o elimine configuraciones según sea necesario. Seleccione **[!UICONTROL Finish]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] utilizando la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en Docker: Scala {#scala}

Comience por navegar y seleccionar **[!UICONTROL Workflows]** , que se encuentra en la parte superior izquierda de la [!DNL Platform] interfaz de usuario. A continuación, seleccione **Import recipe** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Aparece la página **Configurar** para el flujo de trabajo **Importar fórmula**. Introduzca un nombre y una descripción para la fórmula y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el tutorial [Empaquete los archivos de origen en una fórmula](./package-source-files-recipe.md), se proporcionó una URL de Docker al final de la generación de la fórmula de ventas minoristas utilizando archivos de origen Scala ([!DNL Spark]).

Una vez que esté en la página **Seleccionar origen**, pegue la URL del Docker correspondiente a la fórmula empaquetada creada utilizando archivos de origen Scala en el campo URL de origen. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el Explorador del sistema de archivos. El archivo de configuración proporcionado se puede encontrar en `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Seleccione **[!UICONTROL Spark]** en la lista desplegable **Runtime**. Una vez seleccionado el tiempo de ejecución [!DNL Spark], el artefacto predeterminado se rellena automáticamente en **[!UICONTROL Docker]**. A continuación, seleccione **[!UICONTROL Regression]** en la lista desplegable **Type**. Una vez rellenado todo, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar con **Administrar esquemas**.

>[!NOTE]
>
> El tipo admite **[!UICONTROL Classification]** y **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales utilizando el selector **Administrar esquemas**, los esquemas se crearon utilizando el script de arranque proporcionado en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md).

![administrar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

En la sección **Administración de funciones**, seleccione en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada Venta minorista. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la ventana derecha **[!UICONTROL Field Properties]**. Para los fines de este tutorial, establezca &quot;[!UICONTROL weeklySales]&quot; como **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Seleccione **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise la fórmula, añada, modifique o elimine configuraciones según sea necesario. Seleccione **[!UICONTROL Finish]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] utilizando la fórmula de ventas minoristas recién creada.

## Pasos siguientes {#next-steps}

Este tutorial proporciona información sobre la configuración e importación de una fórmula en [!DNL Data Science Workspace]. Ahora puede crear, entrenar y evaluar un modelo con la fórmula recién creada.

- [Capacitar y evaluar un modelo en la interfaz de usuario](./train-evaluate-model-ui.md)
- [Capacitar y evaluar un modelo mediante la API](./train-evaluate-model-api.md)
