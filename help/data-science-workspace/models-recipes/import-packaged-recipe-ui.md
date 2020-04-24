---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importación de una fórmula empaquetada (IU)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Importación de una fórmula empaquetada (IU)

En este tutorial se explica cómo configurar e importar una fórmula empaquetada mediante el ejemplo de venta minorista proporcionado. Al final de este tutorial, estará listo para crear, capacitar y evaluar un modelo en Adobe Experience Platform Data Science Workspace.

## Requisitos previos

Este tutorial requiere una fórmula empaquetada en forma de URL de imagen de Docker. Consulte el tutorial sobre cómo [empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) para obtener más información.

## Flujo de trabajo de la interfaz de usuario

La importación de una fórmula empaquetada en Data Science Workspace requiere configuraciones de fórmula específicas, compiladas en un solo archivo de Notación de objetos JavaScript (JSON), esta compilación de configuraciones de fórmula se denomina archivo **de** configuración. Una fórmula empaquetada con un conjunto concreto de configuraciones se denomina instancia **de** fórmula. Se puede usar una fórmula para crear muchas instancias de fórmula en el área de trabajo de ciencia de datos.

El flujo de trabajo para importar una fórmula de paquete consta de los siguientes pasos:
- [Configurar una fórmula](#configure)
- [Fórmula basada en el acoplador de importación: Python](#python)
- [Fórmula basada en el Docker de importación - R](#r)
- [Importar fórmula basada en el acoplador: PySpark](#pyspark)
- [Fórmula basada en el acoplador de importación: Scala](#scala)

flujos de trabajo obsoletos:
- [Importar fórmula binaria basada en PySpark](#pyspark-deprecated)
- [Importar fórmula basada en binarios: Scala Spark](#scala-deprecated)

### Configurar una fórmula {#configure}

Cada instancia de fórmula en Data Science Workspace está acompañada de un conjunto de configuraciones que adaptan la instancia de fórmula a un caso de uso concreto. Los archivos de configuración definen los comportamientos de puntuación y formación predeterminados de un modelo creado con esta instancia de fórmula.

>[!NOTE] Los archivos de configuración son fórmulas y casos específicos.

A continuación se muestra un archivo de configuración de muestra que muestra los comportamientos de puntuación y formación predeterminados para la fórmula de ventas minoristas.

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
| `n_estimators` | Número | Número de árboles del bosque para el clasificador de bosque aleatorio. |
| `max_depth` | Número | Profundidad máxima de un árbol en el clasificador de bosque aleatorio. |
| `ACP_DSW_INPUT_FEATURES` | Cadena | Lista de atributos de esquema de entrada separados por comas. |
| `ACP_DSW_TARGET_FEATURES` | Cadena | Lista de atributos de esquema de salida separados por comas. |
| `ACP_DSW_FEATURE_UPDATE_SUPPORT` | Booleano | Determina si las características de entrada y salida se pueden modificar |
| `tenantId` | Cadena | Este ID garantiza que los recursos que cree tengan un espacio de nombres adecuado y estén contenidos en la organización de IMS. [Siga los pasos aquí](../../xdm/api/getting-started.md#know-your-tenant_id) para encontrar su ID de inquilino. |
| `ACP_DSW_TRAINING_XDM_SCHEMA` | Cadena | esquema de entrada utilizado para la formación de un modelo. Deje esto vacío al importar en la interfaz de usuario, reemplácelo por SchemaID de formación al importar mediante API. |
| `evaluation.labelColumn` | Cadena | Etiqueta de columna para visualizaciones de evaluación. |
| `evaluation.metrics` | Cadena | lista separada por comas de las métricas de evaluación que se utilizarán para evaluar un modelo. |
| `ACP_DSW_SCORING_RESULTS_XDM_SCHEMA` | Cadena | esquema de salida utilizado para marcar un modelo. Deje esto vacío al importar en la interfaz de usuario, reemplácelo por SchemaID de puntuación al importar mediante API. |

A los efectos de este tutorial, puede dejar los archivos de configuración predeterminados para la fórmula de ventas minoristas en la Referencia de área de trabajo de ciencia de datos como están.

### Fórmula basada en el acoplador de importación: Python {#python}

Inicio navegando y seleccionando **[!UICONTROL Workflows]** ubicado en la parte superior izquierda de la interfaz de usuario de la plataforma. A continuación, seleccione *Importar fórmula* y haga clic en **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Se abre la página *Configurar* para el flujo de trabajo de la fórmula *Importar* . Escriba un nombre y una descripción para la fórmula y, a continuación, selecciónela **[!UICONTROL Next]** en la esquina superior derecha.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> En el tutorial [Empaquetar archivos de origen en un tutorial de fórmula](./package-source-files-recipe.md) , se proporcionó una URL de Docker al final de la generación de la fórmula de venta minorista mediante archivos de origen Python.

Una vez que se encuentre en la página *Seleccionar origen* , pegue la URL del Docker correspondiente a la fórmula empaquetada creada mediante archivos de origen Python en el **[!UICONTROL Source URL]** campo. A continuación, importe el archivo de configuración proporcionado arrastrándolo y soltándolo o utilice el **explorador** del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/python/retail/retail.config.json`. Seleccione **[!UICONTROL Python]** en la lista desplegable *Tiempo de ejecución* y **[!UICONTROL Classification]** en la lista desplegable *Tipo* . Una vez que todo se haya completado, haga clic en **[!UICONTROL Next]** en la esquina superior derecha para proceder a la *administración de esquemas*.

>[!NOTE]
> *El tipo *admite **[!UICONTROL Classification]**y **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_python.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales en la sección *Administrar Esquemas*, se crearon utilizando la secuencia de comandos de arranque proporcionada en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En la sección Administración *de* funciones, haga clic en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la **[!UICONTROL Field Properties]** ventana derecha. A los efectos de este tutorial, establezca **[!UICONTROL weeklySales]** como el **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Haga clic en **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Haga clic en **[!UICONTROL Finish]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para averiguar cómo crear un modelo en el área de trabajo de ciencias de datos mediante la fórmula de ventas minoristas recién creada.

### Fórmula basada en el Docker de importación - R {#r}

Inicio navegando y seleccionando **[!UICONTROL Workflows]** ubicado en la parte superior izquierda de la interfaz de usuario de la plataforma. A continuación, seleccione *Importar fórmula* y haga clic en **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Se abre la página *Configurar* para el flujo de trabajo de la fórmula *Importar* . Escriba un nombre y una descripción para la fórmula y, a continuación, selecciónela **[!UICONTROL Next]** en la esquina superior derecha.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> En el tutorial [Empaquetar archivos de origen en un tutorial de fórmula](./package-source-files-recipe.md) , se proporcionó una URL de Docker al final de la creación de la fórmula de venta minorista mediante archivos de origen R.

Una vez que se encuentre en la página *Seleccionar origen* , pegue la URL del Docker correspondiente a la fórmula empaquetada creada con archivos de origen R en el **[!UICONTROL Source URL]** campo. A continuación, importe el archivo de configuración proporcionado arrastrándolo y soltándolo o utilice el **explorador** del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/R/Retail\ -\ GradientBoosting/retail.config.json`. Seleccione **[!UICONTROL R]** en la lista desplegable *Tiempo de ejecución* y **[!UICONTROL Classification]** en la lista desplegable *Tipo* . Una vez que todo se haya completado, haga clic en **[!UICONTROL Next]** en la esquina superior derecha para proceder a la *administración de esquemas*.

>[!NOTE]
> *El tipo *admite **[!UICONTROL Classification]**y **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/recipe_source_R.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales en la sección *Administrar Esquemas*, se crearon utilizando la secuencia de comandos de arranque proporcionada en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En la sección Administración *de* funciones, haga clic en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la **[!UICONTROL Field Properties]** ventana derecha. A los efectos de este tutorial, establezca **[!UICONTROL weeklySales]** como el **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Haga clic en **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Haga clic en **Finalizar** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para averiguar cómo crear un modelo en el área de trabajo de ciencias de datos mediante la fórmula de ventas minoristas recién creada.

### Importar fórmula basada en el acoplador: PySpark {#pyspark}

Inicio navegando y seleccionando **[!UICONTROL Workflows]** ubicado en la parte superior izquierda de la interfaz de usuario de la plataforma. A continuación, seleccione *Importar fórmula* y haga clic en **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Se abre la página *Configurar* para el flujo de trabajo de la fórmula *Importar* . Introduzca un nombre y una descripción para la fórmula y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> En el tutorial [Empaquetar archivos de origen en un tutorial de fórmula](./package-source-files-recipe.md) , se proporcionó una URL de Docker al final de la creación de la fórmula de venta minorista mediante archivos de origen PySpark.

Una vez que se encuentre en la página *Seleccionar origen* , pegue la URL del Docker correspondiente a la fórmula empaquetada creada mediante los archivos de origen PySpark en el **[!UICONTROL Source URL]** campo. A continuación, importe el archivo de configuración proporcionado arrastrándolo y soltándolo o utilice el **explorador** del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/pyspark/retail/pipeline.json`. Seleccione **[!UICONTROL PySpark]** en la lista desplegable *Tiempo de ejecución* . Una vez seleccionado el tiempo de ejecución de PySpark, el artefacto predeterminado se rellena automáticamente en **[!UICONTROL Docker]**. A continuación, seleccione **[!UICONTROL Classification]** en la lista desplegable *Tipo* . Una vez que todo se haya completado, haga clic en **[!UICONTROL Next]** en la esquina superior derecha para proceder a la *administración de esquemas*.

>[!NOTE]
> *El tipo *admite **[!UICONTROL Classification]**y **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/pyspark-databricks.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales en la sección *Administrar Esquemas*, se crearon utilizando la secuencia de comandos de arranque proporcionada en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En la sección Administración *de* funciones, haga clic en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la **[!UICONTROL Field Properties]** ventana derecha. A los efectos de este tutorial, establezca **[!UICONTROL weeklySales]** como el **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Haga clic en **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Haga clic en **[!UICONTROL Finish]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para averiguar cómo crear un modelo en el área de trabajo de ciencias de datos mediante la fórmula de ventas minoristas recién creada.

### Fórmula basada en el acoplador de importación: Scala {#scala}

Inicio navegando y seleccionando **[!UICONTROL Workflows]** ubicado en la parte superior izquierda de la interfaz de usuario de la plataforma. A continuación, seleccione *Importar fórmula* y haga clic en **[!UICONTROL Launch]**.

![](../images/models-recipes/import-package-ui/launch-import.png)

Se abre la página *Configurar* para el flujo de trabajo de la fórmula *Importar* . Introduzca un nombre y una descripción para la fórmula y, a continuación, seleccione **[!UICONTROL Next]** en la esquina superior derecha para continuar.

![configurar flujo de trabajo](../images/models-recipes/import-package-ui/configure-workflow.png)

>[!NOTE]
> En el tutorial [Empaquetar archivos de origen en un tutorial de fórmula](./package-source-files-recipe.md) , se proporcionó una URL de Docker al final de la creación de la fórmula de venta minorista mediante archivos de origen de Scala (Spark).

Una vez que esté en la página *Seleccionar origen* , pegue la URL del Docker correspondiente a la fórmula empaquetada creada con archivos de origen Scala en el campo URL *de* origen. A continuación, importe el archivo de configuración proporcionado arrastrándolo y soltándolo o utilice el **explorador** del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/scala/retail/pipelineservice.json`. Seleccione **[!UICONTROL Spark]** en la lista desplegable *Tiempo de ejecución* . Una vez seleccionado el motor de ejecución de Spark, el artefacto predeterminado se rellena automáticamente en **[!UICONTROL Docker]**. A continuación, seleccione **[!UICONTROL Regression]** en la lista desplegable *Tipo* . Una vez que todo se haya completado, haga clic en **[!UICONTROL Next]** en la esquina superior derecha para proceder a la *administración de esquemas*.

>[!NOTE]
> *El tipo *admite **[!UICONTROL Classification]**y **[!UICONTROL Regression]**. Si el modelo no se encuentra dentro de uno de estos tipos, seleccione **[!UICONTROL Custom]**.

![](../images/models-recipes/import-package-ui/scala-databricks.png)

A continuación, seleccione los esquemas de entrada y salida de Retail Sales en la sección *Administrar Esquemas*, se crearon utilizando la secuencia de comandos de arranque proporcionada en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) .

![](../images/models-recipes/import-package-ui/recipe_schema.png)

En la sección Administración *de* funciones, haga clic en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando **[!UICONTROL Input Feature]** o **[!UICONTROL Target Feature]** en la **[!UICONTROL Field Properties]** ventana derecha. A los efectos de este tutorial, establezca **[!UICONTROL weeklySales]** como el **[!UICONTROL Target Feature]** y todo lo demás como **[!UICONTROL Input Feature]**. Haga clic en **[!UICONTROL Next]** para revisar la nueva fórmula configurada.

Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Haga clic en **[!UICONTROL Finish]** para crear la fórmula.

![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para averiguar cómo crear un modelo en el área de trabajo de ciencias de datos mediante la fórmula de ventas minoristas recién creada.

## Pasos siguientes {#next-steps}

Este tutorial proporciona una visión detallada sobre cómo configurar e importar una fórmula en el área de trabajo de ciencias de datos. Ahora puede crear, entrenar y evaluar un modelo con la fórmula recién creada.

- [Formación y evaluación de un modelo en la interfaz de usuario](./train-evaluate-model-ui.md)
- [Formación y evaluación de un modelo mediante la API](./train-evaluate-model-api.md)

## flujos de trabajo obsoletos

>[!CAUTION]
>Ya no se admite la importación de fórmulas basadas en binarios en PySpark 3 (Spark 2.4) y Scala (Spark 2.4).

### Importar fórmula binaria basada en PySpark {#pyspark-deprecated}

En el tutorial [Empaquetar archivos de origen en un tutorial de Fórmula](./package-source-files-recipe.md) , se creó un archivo binario **EGG** con los archivos de origen PySpark de Retail Sales.

1. En [Adobe Experience Platform](https://platform.adobe.com/), busque el panel de navegación izquierdo y haga clic en **Flujos de trabajo**. En la interfaz de Flujos de trabajo, **inicie** un nuevo proceso **Importar fórmula desde archivo** de origen.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Escriba un nombre apropiado para la fórmula de ventas minoristas. Por ejemplo, &quot;PySpark de fórmula de ventas minoristas&quot;. Si lo desea, puede incluir una descripción de fórmula y una URL de documentación. Haga clic en **Siguiente** cuando haya terminado.
   ![](../images/models-recipes/import-package-ui/recipe_info.png)
3. Importe la fórmula PySpark Retail Sales creada en los archivos de origen del [paquete en un tutorial de fórmula](./package-source-files-recipe.md) arrastrando y soltando, o utilice el **explorador** del sistema de archivos. La fórmula empaquetada debe estar ubicada en `experience-platform-dsw-reference/recipes/pyspark/dist`.
Del mismo modo, importe el archivo de configuración proporcionado arrastrándolo y soltándolo o utilice el **explorador** del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/pyspark/pipeline.json`. Haga clic en **Siguiente** cuando se hayan proporcionado ambos archivos.
   ![](../images/models-recipes/import-package-ui/recipe_source.png)
4. Puede encontrar errores en este punto. Esto es un comportamiento normal y es de esperar. Seleccione los esquemas de entrada y salida de Retail Sales en la sección **Administrar Esquemas**, que se crearon con la secuencia de comandos de arranque proporcionada en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
En la sección Administración **de** funciones, haga clic en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando Función **de** entrada o Función de **Destinatario** en la ventana Propiedades **del** campo derecha. Para este tutorial, establezca **semanalmente Ventas** como la función **de** Destinatario y todo lo demás como Función **de** entrada. Haga clic en **Siguiente** para revisar la nueva fórmula configurada.
5. Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Haga clic en **Finalizar** para crear la fórmula.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para averiguar cómo crear un modelo en el área de trabajo de ciencias de datos mediante la fórmula de ventas minoristas recién creada.


### Importar fórmula basada en binarios: Scala Spark {#scala-deprecated}

En el tutorial [Empaquetar archivos de origen en un tutorial de fórmula](./package-source-files-recipe.md) , se creó un archivo binario **JAR** con los archivos de origen de Retail Sales Scala Spark.

1. En [Adobe Experience Platform](https://platform.adobe.com/), busque el panel de navegación izquierdo y haga clic en **Flujos de trabajo**. En la interfaz de Flujos de trabajo, **inicie** un nuevo proceso **Importar fórmula desde archivo** de origen.
   ![](../images/models-recipes/import-package-ui/workflow_ss.png)
2. Escriba un nombre apropiado para la fórmula de ventas minoristas. Por ejemplo, &quot;La fórmula de venta minorista Scala Spark&quot;. Si lo desea, puede incluir una descripción de fórmula y una URL de documentación. Haga clic en **Siguiente** cuando haya terminado.
   ![](../images/models-recipes/import-package-ui/recipe_info_scala.png)
3. Importe la fórmula de ventas minoristas de Scala Spark que se creó en los archivos de origen del [paquete en un tutorial de fórmula](./package-source-files-recipe.md) arrastrando y soltando, o utilice el **explorador** del sistema de archivos. La fórmula empaquetada **con dependencias** se encuentra en `experience-platform-dsw-reference/recipes/scala/target`. Del mismo modo, importe el archivo de configuración proporcionado arrastrándolo y soltándolo o utilice el **explorador** del sistema de archivos. El archivo de configuración proporcionado se encuentra en `experience-platform-dsw-reference/recipes/scala/src/main/resources/pipelineservice.json`. Haga clic en **Siguiente** cuando se hayan proporcionado ambos archivos.
   ![](../images/models-recipes/import-package-ui/recipe_source_scala.png)
4. Puede encontrar errores en este punto. Esto es un comportamiento normal y es de esperar. Seleccione los esquemas de entrada y salida de Retail Sales en la sección **Administrar Esquemas**, que se crearon con la secuencia de comandos de arranque proporcionada en el tutorial [crear el esquema de ventas minoristas y el conjunto de datos](../models-recipes/create-retails-sales-dataset.md) .
   ![](../images/models-recipes/import-package-ui/recipe_schema.png)
En la sección Administración **de** funciones, haga clic en la identificación del inquilino en el visor de esquemas para expandir el esquema de entrada de ventas minoristas. Seleccione las funciones de entrada y salida resaltando la función deseada y seleccionando Función **de** entrada o Función de **Destinatario** en la ventana Propiedades **del** campo derecha. Para este tutorial, establezca **semanalmente Ventas** como la función **de** Destinatario y todo lo demás como Función **de** entrada. Haga clic en **Siguiente** para revisar la nueva fórmula configurada.
5. Revise la fórmula, agregue, modifique o elimine configuraciones según sea necesario. Haga clic en **Finalizar** para crear la fórmula.
   ![](../images/models-recipes/import-package-ui/recipe_review.png)

Continúe con los [siguientes pasos](#next-steps) para averiguar cómo crear un modelo en el área de trabajo de ciencias de datos mediante la fórmula de ventas minoristas recién creada.