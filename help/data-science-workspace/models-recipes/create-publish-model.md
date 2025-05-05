---
keywords: Experience Platform; modelo de aprendizaje automático; Data Science Espacio de trabajo; temas populares; Crear y publicar un modelo
solution: Experience Platform
title: Crear y Publish un modelo de aprendizaje automático
type: Tutorial
description: En la siguiente guía se describen los pasos necesarios para crear y publicar un modelo de aprendizaje automático.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# Crear y publicar un modelo de aprendizaje automático

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

En la siguiente guía se describen los pasos necesarios para crear y publicar un modelo de aprendizaje automático. Cada sección contiene una descripción de lo que va a hacer y un vincular a la documentación de IU y API para realizar previamente el paso descrito.

## Introducción

Antes de comenzar este tutorial, debe cumplir los siguientes requisitos previos:

- Acceso a [!DNL Adobe Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

- Todos los tutoriales de Data Science Workspace utilizan el modelo de tendencia de Luma. Para continuar, debe haber creado los [esquemas y conjuntos de datos del modelo de tendencia de Luma](./create-luma-data.md).

### Explorar los datos y comprender los esquemas

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com/) y seleccione **[!UICONTROL Conjuntos de datos]** para ver una lista de todos los conjuntos de datos existentes y seleccione el conjunto de datos que desee explorar. En este caso, debe seleccionar el conjunto de datos **Luma web data**.

![seleccione el conjunto de datos web de Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

Se abre la conjunto de datos actividad Página con información relacionada con su conjunto de datos. Puede seleccionar **[!UICONTROL Vista previa conjunto]** de datos cerca de la parte superior derecha para examinar los registros de muestra. También puede vista la esquema del conjunto de datos seleccionado.

![perview Datos web de Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Seleccione el esquema vincular en el carril derecho. Aparece una ventana emergente donde al seleccionar la vincular bajo **[!UICONTROL esquema nombre]** se abre la esquema en una nueva pestaña.

![previsualización el esquema de datos web de Luma](../images/models-recipes/model-walkthrough/preview-schema.png)

Puede explorar más a fondo los datos utilizando el bloc de notas de análisis de datos exploratorio (EDA) proporcionado. Este cuaderno se puede utilizar para ayudar a comprender los patrones de los datos de Luma, comprobar la validez de los datos y resumir los datos relevantes para el modelo de propensión predictiva. Para obtener más información sobre el análisis exploratorio de datos, visita la [documentación EDA](../jupyterlab/eda-notebook.md).

## Crear la propensión a Luma fórmula {#author-your-model}

Un componente principal del [!DNL Data Science Workspace] ciclo vital implica la creación de fórmulas y modelos. El modelo de propensión de Luma está diseñado para generar una predicción sobre si los clientes tienen una alta propensión a comprar un producto de Luma.

Para crear el modelo de propensión de Luma, se utiliza el generador de fórmula plantilla. Las recetas son la base de un modelo, ya que contienen algoritmos de aprendizaje automático y lógica diseñada para resolver problemas específicos. Más importante aún, Recipes le permite democratizar el aprendizaje automático en toda su organización, permitiendo a otros usuarios acceder a un modelo para casos de uso dispares sin escribir ningún código.

Siga el [tutorial Crear un modelo con JupyterLab Notebooks para crear el modelo de](../jupyterlab/create-a-model.md) propensión de Luma fórmula que se utiliza en tutoriales posteriores.

## Importar y empaquetar un fórmula desde fuentes externas (*opcional*)

Si desea importar y empaquetar un fórmula para su uso en Data Science Espacio de trabajo, debe empaquetar los archivos de origen en un archivo de almacenamiento. Siga los archivos de origen del [paquete en una fórmula](./package-source-files-recipe.md) tutorial. Este tutorial muestra cómo empaquetar archivos de origen en una fórmula, que es el paso previo para importar una fórmula en Data Science Workspace. Una vez completado el tutorial, se le proporciona una imagen Docker en un Registro de contenedores de Azure, junto con la URL de imagen correspondiente, en otras palabras, un archivo.

Este archivo puede utilizarse para crear una fórmula en Data Science Workspace siguiendo el flujo de trabajo de importación de fórmulas con [flujo de trabajo de interfaz de usuario](./import-packaged-recipe-ui.md) o [flujo de trabajo de API](./import-packaged-recipe-api.md).

## Entrena y evalúa un modelo {#train-and-evaluate-your-model}

Ahora que los datos están preparados y la fórmula está lista, puede crear, entrenar y evaluar el modelo de aprendizaje automático en mayor medida. Al utilizar el Generador de fórmulas, ya debería haber entrenado, puntuado y evaluado el modelo antes de empaquetarlo en una fórmula.

La IU y la API de Data Science Workspace le permiten publicar la fórmula como modelo. Además, puede ajustar aún más aspectos específicos de su modelo, como agregar, quitar y cambiar hiperparámetros.

### Crear un modelo

Para obtener más información sobre cómo crear un modelo con el IU, visita la formación y evaluación de un modelo en el IU tutorial de ciencia de datos o en el tutorial de API Espacio de trabajo[&#128279;](./train-evaluate-model-ui.md) [&#128279;](./train-evaluate-model-api.md). Este tutorial proporciona un ejemplo sobre cómo crear, entrenar y actualizar hiperparámetros para ajustar el modelo.

>[!NOTE]
>
> Los hiperparámetros no se pueden aprender, por lo que deben asignarse antes de que se produzcan aprendizaje ejecuciones. El ajuste de los hiperparámetros puede cambiar la precisión del modelo entrenado. Dado que la optimización de un modelo es un proceso iterativo, es posible que se requieran varias ejecuciones aprendizaje antes de lograr una evaluación satisfactoria.

## Puntuación de un modelo {#score-a-model}

El siguiente paso en la creación y publicación de un modelo es poner en práctica su modelo para obtener y consumir información del lago de datos y el perfil del cliente en tiempo real.

La puntuación en Data Science Espacio de trabajo se puede lograr mediante la introducción de datos de entrada en un modelo entrenado existente. Los resultados de la puntuación se almacenan y se pueden visualizar en un conjunto de datos de salida especificado como un nuevo lote.

Para obtener información sobre cómo calificar su modelo, visita la puntuación de un modelo [IU tutorial](./score-model-ui.md) o [un tutorial](./score-model-api.md) API.

## Publish un modelo puntuado como servicio

Data Science Espacio de trabajo le permite publicar su modelo entrenado como un servicio. Esto permite a los usuarios de su organización puntuar los datos sin necesidad de crear sus propios modelos.

Para aprender a publicar un modelo como servicio, visita el [tutorial de la interfaz de usuario](./publish-model-service-ui.md) o el [tutorial de la API](./publish-model-service-api.md).

### Programar formación automatizada para un servicio

Una vez que haya publicado un modelo como servicio, puede configurar ejecuciones programadas de puntuación y formación para el servicio de aprendizaje automático. La automatización del proceso de formación y puntuación puede ayudar a mantener y mejorar la eficacia de un servicio a lo largo del tiempo, al estar al día con los patrones de los datos. Visite el tutorial [Programar un modelo en la interfaz de usuario de Data Science Workspace](./schedule-models-ui.md).

>[!NOTE]
>
> Únicamente se puede programar un modelo para aprendizaje automatizado y para la puntuación a partir de la IU.

## Pasos siguientes {#next-steps}

[!DNL Data Science Workspace] Adobe Experience Platform proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones y conocimientos de datos. Cuando la información de aprendizaje automático se ingiere en un [!DNL Profile]conjunto de datos habilitado, esos mismos datos también se ingieren como [!DNL Profile] registros que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service].

A medida que se ingieren datos de perfil y series temporales, Real-Time Customer Profile decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo llamado transmisión segmentación, antes de fusionarlos con los datos existentes y actualizar el unión vista. Como resultado, puede realizar cálculos instantáneos y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca.

Visite la tutorial para [enriquecer el perfil del cliente en tiempo real con información](./enrich-profile.md) sobre el aprendizaje automático para obtener más información sobre cómo puede utilizar las estadísticas del aprendizaje automático.
