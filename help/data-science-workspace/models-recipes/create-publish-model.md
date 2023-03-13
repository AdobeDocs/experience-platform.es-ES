---
keywords: Experience Platform;modelo de aprendizaje automático;Data Science Workspace;temas populares;crear y publicar un modelo
solution: Experience Platform
title: Creación y publicación de un modelo de aprendizaje automático
type: Tutorial
description: En la siguiente guía se describen los pasos necesarios para crear y publicar un modelo de aprendizaje automático.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# Creación y publicación de un modelo de aprendizaje automático

En la siguiente guía se describen los pasos necesarios para crear y publicar un modelo de aprendizaje automático. Cada sección contiene una descripción de lo que va a hacer y un vínculo a la interfaz de usuario y a la documentación de la API para realizar el paso descrito.

## Primeros pasos

Antes de iniciar este tutorial, debe cumplir los siguientes requisitos previos:

- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

- Todos los tutoriales de Data Science Workspace utilizan el modelo de tendencia de Luma. Para poder seguir adelante, debe haber creado el [Esquemas y conjuntos de datos del modelo de tendencia de Luma](./create-luma-data.md).

### Explorar los datos y comprender los esquemas

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Conjuntos de datos]** para enumerar todos los conjuntos de datos existentes y seleccionar el conjunto de datos que desea explorar. En este caso, debe seleccionar la variable **Datos web de Luma** conjunto de datos.

![seleccionar conjunto de datos web de Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

Se abre la página de actividad del conjunto de datos, que enumera información relacionada con el conjunto de datos. Puede seleccionar **[!UICONTROL Previsualizar conjunto de datos]** situado cerca de la parte superior derecha para examinar los registros de muestra. También puede ver el esquema del conjunto de datos seleccionado.

![Previsualizar datos web de Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Seleccione el vínculo de esquema en el carril derecho. Aparece una ventana emergente que selecciona el vínculo en **[!UICONTROL nombre de esquema]** abre el esquema en una nueva pestaña.

![previsualización del esquema de datos web de luma](../images/models-recipes/model-walkthrough/preview-schema.png)

Puede explorar aún más los datos con el bloc de notas de análisis exploratorio de datos (EDA) proporcionado. Este bloc de notas se puede utilizar para comprender mejor los patrones de los datos de Luma, comprobar la sanidad de los datos y resumir los datos relevantes para el modelo de tendencia predictiva. Para obtener más información sobre Análisis de datos exploratorios, visite la [Documentación de EDA](../jupyterlab/eda-notebook.md).

## Creación de la fórmula de tendencia de Luma {#author-your-model}

Un componente principal del [!DNL Data Science Workspace] El ciclo de vida implica crear fórmulas y modelos. El modelo de tendencia de Luma está diseñado para generar una predicción sobre si los clientes tienen una alta tendencia a comprar un producto de Luma.

Para crear el modelo de tendencia de Luma, se utiliza la plantilla del generador de fórmulas. Las fórmulas son la base de un modelo, ya que contienen algoritmos de aprendizaje automático y lógica diseñados para resolver problemas específicos. Más importante aún, las fórmulas le permiten democratizar el aprendizaje automático en toda la organización, lo que permite a otros usuarios acceder a un modelo para casos de uso dispares sin escribir ningún código.

Siga las [creación de un modelo con JupyterLab Notebooks](../jupyterlab/create-a-model.md) tutorial para crear la fórmula del modelo de tendencia de Luma que se utiliza en tutoriales posteriores.

## Importar y empaquetar una fórmula desde fuentes externas (*opcional*)

Si desea importar y empaquetar una fórmula para utilizarla en Data Science Workspace, debe empaquetar los archivos de origen en un archivo de almacenamiento. Siga las [empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) tutorial. Este tutorial muestra cómo empaquetar archivos de origen en una fórmula, que es el paso previo para importar una fórmula en Data Science Workspace. Una vez completado el tutorial, se le proporciona una imagen Docker en un Registro de contenedores de Azure, junto con la URL de imagen correspondiente, en otras palabras, un archivo.

Este archivo puede utilizarse para crear una fórmula en Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas con [Flujo de trabajo IU](./import-packaged-recipe-ui.md) o el [Flujo de trabajo API](./import-packaged-recipe-api.md).

## Formación y evaluación de un modelo {#train-and-evaluate-your-model}

Ahora que los datos están preparados y la fórmula está lista, puede crear, entrenar y evaluar el modelo de aprendizaje automático en mayor medida. Al utilizar el Generador de fórmulas, ya debería haber entrenado, puntuado y evaluado el modelo antes de empaquetarlo en una fórmula.

La IU y la API de Data Science Workspace le permiten publicar la fórmula como modelo. Además, puede ajustar aún más aspectos específicos del modelo, como agregar, quitar y cambiar hiperparámetros.

### Creación de un modelo

Para obtener más información sobre la creación de un modelo mediante la interfaz de usuario, visite el tren y evalúe un modelo en el espacio de trabajo de ciencia de datos [Tutorial de IU](./train-evaluate-model-ui.md) o [Tutorial de API](./train-evaluate-model-api.md). Este tutorial proporciona un ejemplo sobre cómo crear, entrenar y actualizar hiperparámetros para ajustar el modelo.

>[!NOTE]
>
> Los hiperparámetros no se pueden aprender, por lo que se deben asignar antes de que se produzcan ejecuciones de formación. El ajuste de los hiperparámetros puede cambiar la precisión del modelo entrenado. Dado que la optimización de un modelo es un proceso iterativo, pueden ser necesarias varias ejecuciones de formación antes de lograr una evaluación satisfactoria.

## Puntuación de un modelo {#score-a-model}

El siguiente paso para crear y publicar un modelo es ponerlo en funcionamiento para puntuar y consumir perspectivas del lago de datos y del perfil del cliente en tiempo real.

La puntuación en Data Science Workspace se puede lograr alimentando los datos de entrada en un modelo formado existente. A continuación, los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.

Para aprender a puntuar el modelo, visite la puntuación de un modelo [Tutorial de IU](./score-model-ui.md) o [Tutorial de API](./score-model-api.md).

## Publicación de un modelo clasificado como servicio

El espacio de trabajo de ciencia de datos le permite publicar su modelo entrenado como servicio. Esto permite a los usuarios de su organización IMS puntuar los datos sin necesidad de crear sus propios modelos.

Para obtener información sobre cómo publicar un modelo como servicio, visite la [Tutorial de IU](./publish-model-service-ui.md) o [Tutorial de API](./publish-model-service-api.md).

### Programar formación automatizada para un servicio

Una vez que haya publicado un modelo como servicio, puede configurar ejecuciones programadas de puntuación y formación para el servicio de aprendizaje automático. La automatización del proceso de formación y puntuación puede ayudar a mantener y mejorar la eficacia de un servicio a lo largo del tiempo, al estar al día con los patrones de los datos. Visite la [Programar un modelo en la IU de Data Science Workspace](./schedule-models-ui.md) tutorial.

>[!NOTE]
>
> Solo puede programar un modelo para formación automatizada y puntuación desde la interfaz de usuario.

## Pasos siguientes {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones y perspectivas de datos. Cuando se ingieren perspectivas de aprendizaje automático en una [!DNL Profile]Conjunto de datos habilitado para, esos mismos datos también se incorporan como [!DNL Profile] registros que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service].

A medida que se incorporan los datos de perfil y serie temporal, el Perfil del cliente en tiempo real decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo denominado segmentación de flujo continuo, antes de combinarlos con los datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos y tomar decisiones de forma instantánea para ofrecer experiencias mejoradas e individualizadas a los clientes mientras interactúan con su marca.

Visite el tutorial de [enriquecimiento del perfil del cliente en tiempo real con perspectivas de aprendizaje automático](./enrich-profile.md) para obtener más información sobre cómo utilizar las perspectivas de aprendizaje automático.
