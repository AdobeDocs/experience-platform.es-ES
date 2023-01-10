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

En la siguiente guía se describen los pasos necesarios para crear y publicar un modelo de aprendizaje automático. Cada sección contiene una descripción de lo que hará y un vínculo a la interfaz de usuario y a la documentación de la API para llevar a cabo el paso descrito.

## Primeros pasos

Antes de iniciar este tutorial, debe tener los siguientes requisitos previos:

- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

- Todos los tutoriales de Data Science Workspace utilizan el modelo de propensión de Luma. Para poder seguir, debe haber creado la variable [Esquemas y conjuntos de datos del modelo de propensión de Luma](./create-luma-data.md).

### Explorar los datos y comprender los esquemas

Iniciar sesión en [Adobe Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Conjuntos de datos]** para enumerar todos los conjuntos de datos existentes y seleccionar el conjunto de datos que desea explorar. En este caso, debe seleccionar la variable **Datos web de Luma** conjunto de datos.

![seleccionar el conjunto de datos web de Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

Se abre la página de actividad del conjunto de datos, que enumera información relacionada con su conjunto de datos. Puede seleccionar **[!UICONTROL Vista previa del conjunto de datos]** cerca de la esquina superior derecha para examinar los registros de muestra. También puede ver el esquema del conjunto de datos seleccionado.

![vista previa de datos web de Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Seleccione el vínculo de esquema en el carril derecho. Aparece una ventana emergente, seleccionando el vínculo debajo de **[!UICONTROL nombre de esquema]** abre el esquema en una nueva pestaña.

![vista previa del esquema de datos web de luma](../images/models-recipes/model-walkthrough/preview-schema.png)

Puede explorar aún más los datos mediante el bloc de notas de Análisis de datos exploratorios (EDA) proporcionado. Este bloc de notas se puede utilizar para ayudar a comprender los patrones de los datos de Luma, comprobar la solidez de los datos y resumir los datos relevantes para el modelo de propensión predictiva. Para obtener más información sobre el análisis de datos exploratorios, visite [Documentación de EDA](../jupyterlab/eda-notebook.md).

## Creación de la fórmula de propensión de Luma {#author-your-model}

Un componente principal de la variable [!DNL Data Science Workspace] el ciclo vital implica la creación de fórmulas y modelos. El modelo de propensión a Luma está diseñado para generar una predicción sobre si los clientes tienen una alta propensión a comprar un producto de Luma.

Para crear el modelo de propensión de Luma, se utiliza la plantilla del generador de fórmulas. Las fórmulas son la base de un modelo, ya que contienen algoritmos de aprendizaje automático y lógica diseñados para resolver problemas específicos. Lo que es más importante, las fórmulas le permiten democratizar el aprendizaje automático en su organización, lo que permite a otros usuarios acceder a un modelo para casos de uso diferentes sin necesidad de escribir ningún código.

Siga las [crear un modelo utilizando equipos portátiles de JupyterLab](../jupyterlab/create-a-model.md) tutorial para crear la fórmula del modelo de propensión de Luma que se utiliza en tutoriales posteriores.

## Importar y empaquetar una fórmula a partir de fuentes externas (*opcional*)

Si desea importar y empaquetar una fórmula para utilizarla en Data Science Workspace, debe empaquetar los archivos de origen en un archivo. Siga las [empaquetar archivos de origen en una fórmula](./package-source-files-recipe.md) tutorial. Este tutorial le muestra cómo empaquetar archivos de origen en una fórmula, que es el paso previo para importar una fórmula en Data Science Workspace. Una vez completado el tutorial, se le proporcionará una imagen Docker en un Registro de contenedores de Azure, junto con la URL de la imagen correspondiente, es decir, un archivo.

Este archivo de archivo se puede utilizar para crear una fórmula en Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas utilizando la variable [Flujo de trabajo de la interfaz de usuario](./import-packaged-recipe-ui.md) o [Flujo de trabajo de API](./import-packaged-recipe-api.md).

## Capacitar y evaluar un modelo {#train-and-evaluate-your-model}

Ahora que los datos están preparados y una fórmula está lista, tiene la capacidad de crear, entrenar y evaluar aún más su modelo de aprendizaje automático. Al usar el Generador de fórmulas, ya debería haber entrenado, marcado y evaluado su modelo antes de empaquetarlo en una fórmula.

La interfaz de usuario y la API de Data Science Workspace permiten publicar la fórmula como modelo. Además, puede ajustar aspectos específicos del modelo, como agregar, quitar y cambiar hiperparámetros.

### Crear un modelo

Para obtener más información sobre la creación de un modelo mediante la interfaz de usuario, visite el tren y evalúe un modelo en Data Science Workspace [Tutorial de la interfaz de usuario](./train-evaluate-model-ui.md) o [Tutorial de API](./train-evaluate-model-api.md). Este tutorial proporciona un ejemplo sobre cómo crear, entrenar y actualizar hiperparámetros para ajustar el modelo.

>[!NOTE]
>
> Los hiperparámetros no se pueden aprender, por lo que deben asignarse antes de que se ejecuten las formaciones. Ajustar los hiperparámetros puede cambiar la precisión del modelo entrenado. Dado que la optimización de un modelo es un proceso iterativo, puede ser necesario realizar múltiples ejercicios de capacitación antes de que se logre una evaluación satisfactoria.

## Puntuación de un modelo {#score-a-model}

El siguiente paso para crear y publicar un modelo es poner en marcha su modelo para puntuar y consumir perspectivas del lago de datos y del perfil del cliente en tiempo real.

La puntuación en Data Science Workspace se puede lograr añadiendo datos de entrada a un modelo entrenado existente. Los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.

Para aprender a puntuar el modelo, visite la puntuación de un modelo [Tutorial de la interfaz de usuario](./score-model-ui.md) o [Tutorial de API](./score-model-api.md).

## Publicación de un modelo marcado como servicio

Data Science Workspace le permite publicar su modelo entrenado como servicio. Esto permite a los usuarios de la organización IMS puntuar los datos sin necesidad de crear sus propios modelos.

Para aprender a publicar un modelo como servicio, visite la [Tutorial de la interfaz de usuario](./publish-model-service-ui.md) o [Tutorial de API](./publish-model-service-api.md).

### Programar capacitación automatizada para un servicio

Una vez que haya publicado un modelo como servicio, puede configurar ejecuciones de puntuación y formación programadas para su servicio de aprendizaje automático. La automatización del proceso de capacitación y puntuación puede ayudar a mantener y mejorar la eficacia de un servicio a lo largo del tiempo al mantenerse al día con los patrones dentro de los datos. Visite la [programar un modelo en la interfaz de usuario de Data Science Workspace](./schedule-models-ui.md) tutorial.

>[!NOTE]
>
> Solo puede programar un modelo para la formación y puntuación automatizada desde la interfaz de usuario.

## Pasos siguientes {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones de datos y perspectivas. Cuando las perspectivas de aprendizaje automático se incorporan en un [!DNL Profile]conjunto de datos habilitado para , que los mismos datos también se introducen como [!DNL Profile] registros que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service].

A medida que se incorporan los datos de perfil y series temporales, el perfil del cliente en tiempo real decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo denominado segmentación de flujo continuo, antes de combinarlos con los datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos instantáneamente y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca.

Visite el tutorial para [enriquecimiento del perfil del cliente en tiempo real con perspectivas de aprendizaje automático](./enrich-profile.md) para obtener más información sobre cómo puede utilizar perspectivas de aprendizaje automático.
