---
keywords: Experience Platform;importar fórmula empaquetada;espacio de trabajo de ciencia de datos;temas populares;recetas;iu;crear motor
solution: Experience Platform
title: Importar una fórmula empaquetada en la interfaz de usuario de Data Science Workspace
type: Tutorial
description: Este tutorial proporciona información sobre cómo configurar e importar una fórmula empaquetada mediante el ejemplo de ventas minoristas proporcionado. Al final de este tutorial, estará listo para crear, entrenar y evaluar un modelo en Adobe Experience Platform Data Science Workspace.
exl-id: 2556e1f0-3f9c-4884-a699-06c041d5c4d1
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 0%

---

# Importar una fórmula empaquetada en la interfaz de usuario de Data Science Workspace

Este tutorial proporciona información sobre cómo configurar e importar una fórmula empaquetada mediante el ejemplo de ventas minoristas proporcionado. Al final de este tutorial, estará listo para crear, entrenar y evaluar un modelo en Adobe Experience Platform [!DNL Data Science Workspace].

## Requisitos previos

Este tutorial requiere una fórmula empaquetada en forma de URL de imagen Docker. Consulte el tutorial sobre cómo [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) para obtener más información.

## Flujo de trabajo IU

Importación de una fórmula empaquetada en [!DNL Data Science Workspace] requiere configuraciones de fórmula específicas, compiladas en un solo archivo JavaScript Object Notation (JSON), esta compilación de configuraciones de fórmula se denomina archivo de configuración. Una fórmula empaquetada con un conjunto particular de configuraciones se denomina instancia de fórmula. Se puede utilizar una fórmula para crear muchas instancias de fórmula en [!DNL Data Science Workspace].

El flujo de trabajo para importar una fórmula de paquete consta de los siguientes pasos:
- [Configuración de una fórmula](#configure)
- [Importar fórmula basada en Docker: Python](#python)
- [Importar fórmula basada en Docker: R](#r)
- [Importar fórmula basada en Docker: PySpark](#pyspark)
- [Importar fórmula basada en Docker: Scala](#scala)

### Configuración de una fórmula {#configure}

Cada instancia de fórmula en [!DNL Data Science Workspace] va acompañado de un conjunto de configuraciones que personalizan la instancia de fórmula para adaptarla a un caso de uso determinado. Los archivos de configuración definen los comportamientos de formación y puntuación predeterminados de un modelo creado con esta instancia de fórmula.

>[!NOTE]
>
>Los archivos de configuración son específicos de fórmula y caso.

A continuación se muestra un archivo de configuración de muestra que muestra los comportamientos predeterminados de formación y puntuación para la fórmula de ventas minoristas.

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
| `learning_rate` | Número | Escalar para multiplicación de degradado. |
| `n_estimators` | Número | Número de árboles del bosque para el Clasificador de bosque aleatorio. |
| `max_depth` | Número | Profundidad máxima de un árbol en el Clasificador de bosque aleatorio. |
| `ACP_DSW_INPUT_FEATURES` | Cadena | Lista de atributos de esquema de entrada separados por comas. |
| `ACP_DSW_TARGET_FEATURES` | Cadena | Lista de atributos de esquema de salida separados por comas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina si se pueden modificar las características de entrada y salida |
| `tenantId` | Cadena | Este ID garantiza que los recursos que cree tengan un espacio de nombres correcto y estén contenidos en su organización IMS. [Siga los pasos aquí](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar su ID de inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Cadena | El esquema de entrada utilizado para entrenar un modelo. Deje esto vacío al importar en la interfaz de usuario, reemplace con SchemaID de formación al importar mediante API. |
| `evaluation.labelColumn` | Cadena | Etiqueta de columna para visualizaciones de evaluación. |
| `evaluation.metrics` | Cadena | Lista separada por comas de las métricas de evaluación que se utilizarán para evaluar un modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Cadena | Esquema de salida utilizado para puntuar un modelo. Deje esto vacío al importar en la interfaz de usuario, reemplace por SchemaID de puntuación al importar mediante API. |

Para los fines de este tutorial, puede dejar los archivos de configuración predeterminados para la fórmula de ventas minoristas en la [!DNL Data Science Workspace] Haga referencia a cómo son.

### Importar fórmula basada en Docker: [!DNL Python] {#python}

Comience por navegar y seleccionar **[!UICONTROL Flujos de trabajo]** situado en la parte superior izquierda de la [!DNL Platform] IU. A continuación, seleccione **Importar fórmula** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

El **Configurar** página para el **Importar fórmula** flujo de trabajo aparece. Introduzca un nombre y una descripción para la fórmula y seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) En este tutorial, se ha proporcionado una URL de Docker al final de la creación de la fórmula de ventas minoristas con archivos de origen de Python.

Una vez que esté en la **Seleccionar origen** , pegue la URL de Docker correspondiente a la fórmula empaquetada creada con [!DNL Python] archivos de origen en **[!UICONTROL URL de origen]** field. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el sistema de archivos **Explorador**. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Seleccionar **[!UICONTROL Python]** en el **Runtime** desplegable y **[!UICONTROL Clasificación]** en el **Tipo** desplegable. Una vez completado todo, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar a **Administrar esquemas**.

>[!NOTE]
>
> El tipo admite **[!UICONTROL Clasificación]** y **[!UICONTROL Regresión]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

A continuación, seleccione los esquemas de entrada y salida de Ventas minoristas en la sección **Administrar esquemas**, se crearon utilizando el script de bootstrap proporcionado en el [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En el **Administración de funciones** , seleccione la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de Ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Función de entrada]** o **[!UICONTROL Función de destino]** en la derecha **[!UICONTROL Propiedades del campo]** ventana. Para los fines de este tutorial, configure **[!UICONTROL weeklySales]** como el  **[!UICONTROL Función de destino]** y todo lo demás como **[!UICONTROL Función de entrada]**. Seleccionar **[!UICONTROL Siguiente]** para revisar la nueva fórmula configurada.

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Seleccionar **[!UICONTROL Finalizar]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con la [pasos siguientes](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] mediante la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en Docker: R {#r}

Comience por navegar y seleccionar **[!UICONTROL Flujos de trabajo]** situado en la parte superior izquierda de la [!DNL Platform] IU. A continuación, seleccione **Importar fórmula** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

El **Configurar** página para el **Importar fórmula** flujo de trabajo aparece. Introduzca un nombre y una descripción para la fórmula y seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) , se ha proporcionado una URL de Docker al final de la creación de la fórmula de ventas minoristas con archivos de origen R.

Una vez que esté en la **Seleccionar origen** , pegue la URL de Docker correspondiente a la fórmula empaquetada creada con archivos de origen R en la **[!UICONTROL URL de origen]** field. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el sistema de archivos **Explorador**. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Seleccionar **[!UICONTROL R]** en el **Runtime** desplegable y **[!UICONTROL Clasificación]** en el **Tipo** desplegable. Una vez completado todo, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar a **Administrar esquemas**.

>[!NOTE]
>
> *Tipo* admite **[!UICONTROL Clasificación]** y **[!UICONTROL Regresión]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

A continuación, seleccione los esquemas de entrada y salida de Ventas minoristas en la sección **Administrar esquemas**, se crearon utilizando el script de bootstrap proporcionado en el [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) tutorial.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En el *Administración de funciones* , seleccione la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de Ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Función de entrada]** o **[!UICONTROL Función de destino]** en la derecha **[!UICONTROL Propiedades del campo]** ventana. Para los fines de este tutorial, configure **[!UICONTROL weeklySales]** como el  **[!UICONTROL Función de destino]** y todo lo demás como **[!UICONTROL Función de entrada]**. Seleccionar **[!UICONTROL Siguiente]** para revisar la nueva fórmula configurada.

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Seleccionar **Finalizar** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con la [pasos siguientes](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] mediante la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en Docker: PySpark {#pyspark}

Comience por navegar y seleccionar **[!UICONTROL Flujos de trabajo]** situado en la parte superior izquierda de la [!DNL Platform] IU. A continuación, seleccione **Importar fórmula** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

El **Configurar** página para el **Importar fórmula** flujo de trabajo aparece. Introduzca un nombre y una descripción para la fórmula y seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) , se ha proporcionado una URL de Docker al final de la creación de la fórmula de ventas minoristas con archivos de origen PySpark.

Una vez que esté en la **Seleccionar origen** , pegue la URL de Docker correspondiente a la fórmula empaquetada creada con los archivos de origen de PySpark en **[!UICONTROL URL de origen]** field. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el sistema de archivos **Explorador**. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Seleccionar **[!UICONTROL PySpark]** en el **Runtime** desplegable. Una vez seleccionado el tiempo de ejecución de PySpark, el artefacto predeterminado se rellena automáticamente en **[!UICONTROL Docker]**. A continuación, seleccione **[!UICONTROL Clasificación]** en el **Tipo** desplegable. Una vez completado todo, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar a **Administrar esquemas**.

>[!NOTE]
>
> *Tipo* admite **[!UICONTROL Clasificación]** y **[!UICONTROL Regresión]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

A continuación, seleccione los esquemas de entrada y salida de Ventas minoristas utilizando **Administrar esquemas** , los esquemas se crearon utilizando el script de bootstrap proporcionado en el [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) tutorial.

![administrar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

En el **Administración de funciones** , seleccione la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de Ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Función de entrada]** o **[!UICONTROL Función de destino]** en la derecha **[!UICONTROL Propiedades del campo]** ventana. Para los fines de este tutorial, configure **[!UICONTROL weeklySales]** como el  **[!UICONTROL Función de destino]** y todo lo demás como **[!UICONTROL Función de entrada]**. Seleccionar **[!UICONTROL Siguiente]** para revisar la nueva fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Seleccionar **[!UICONTROL Finalizar]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con la [pasos siguientes](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] mediante la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en Docker: Scala {#scala}

Comience por navegar y seleccionar **[!UICONTROL Flujos de trabajo]** situado en la parte superior izquierda de la [!DNL Platform] IU. A continuación, seleccione **Importar fórmula** y seleccione **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

El **Configurar** página para el **Importar fórmula** flujo de trabajo aparece. Introduzca un nombre y una descripción para la fórmula y seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
>
> En el [Empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) , se ha proporcionado una URL de Docker al final de la creación de la fórmula de ventas minoristas con Scala ([!DNL Spark]) archivos de origen.

Una vez que esté en la **Seleccionar origen** , pegue la URL de Docker correspondiente a la fórmula empaquetada creada con archivos de origen de Scala en el campo URL de origen. A continuación, importe el archivo de configuración proporcionado arrastrando y soltando, o utilice el explorador del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Seleccionar **[!UICONTROL Spark]** en el **Runtime** desplegable. Una vez que [!DNL Spark] runtime está seleccionado; el artefacto predeterminado se rellena automáticamente en **[!UICONTROL Docker]**. A continuación, seleccione **[!UICONTROL Regresión]** desde el **Tipo** desplegable. Una vez completado todo, seleccione **[!UICONTROL Siguiente]** en la esquina superior derecha para continuar a **Administrar esquemas**.

>[!NOTE]
>
> El tipo admite **[!UICONTROL Clasificación]** y **[!UICONTROL Regresión]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Personalizado]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

A continuación, seleccione los esquemas de entrada y salida de Ventas minoristas utilizando **Administrar esquemas** , los esquemas se crearon utilizando el script de bootstrap proporcionado en el [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) tutorial.

![administrar esquemas](../images/models-recipes/import-package-ui/manage-schemas.png)

En el **Administración de funciones** , seleccione la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de Ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Función de entrada]** o **[!UICONTROL Función de destino]** en la derecha **[!UICONTROL Propiedades del campo]** ventana. A los efectos de este tutorial, se debe establecer &quot;[!UICONTROL weeklySales]&quot; como el  **[!UICONTROL Función de destino]** y todo lo demás como **[!UICONTROL Función de entrada]**. Seleccionar **[!UICONTROL Siguiente]** para revisar la nueva fórmula configurada.

![](../images/models-recipes/import-package-ui/recipe_schema.png)

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Seleccionar **[!UICONTROL Finalizar]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con la [pasos siguientes](#next-steps) para saber cómo crear un modelo en [!DNL Data Science Workspace] mediante la fórmula de ventas minoristas recién creada.

## Pasos siguientes {#next-steps}

Este tutorial proporciona información sobre la configuración e importación de una fórmula en [!DNL Data Science Workspace]. Ahora puede crear, entrenar y evaluar un modelo con la fórmula recién creada.

- [Formación y evaluación de un modelo en la IU de](./train-evaluate-model-ui.md)
- [Formación y evaluación de un modelo mediante la API](./train-evaluate-model-api.md)
