---
keywords: Experience Platform;publicar un modelo;Data Science Workspace;temas populares;puntuación de un servicio
solution: Experience Platform
title: Publicación de un modelo como servicio en la interfaz de usuario de Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace permite publicar el modelo entrenado y evaluado como servicio, lo que permite a los usuarios de la organización IMS puntuar datos sin necesidad de crear sus propios modelos.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# Publicación de un modelo como servicio en la interfaz de usuario de Data Science Workspace

Adobe Experience Platform Data Science Workspace permite publicar el modelo entrenado y evaluado como servicio, lo que permite a los usuarios de la organización IMS puntuar datos sin necesidad de crear sus propios modelos.

## Primeros pasos

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización de IMS en [!DNL Experience Platform], póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo existente con una ejecución de formación correcta. Si no tiene un modelo editable, siga el tutorial [Train and evaluate a Model in the UI](./train-evaluate-model-ui.md) antes de continuar.

Si prefiere publicar un modelo utilizando las API de aprendizaje automático de Sensei, consulte el [tutorial de API](./publish-model-service-api.md).

## Publicar un modelo {#publish-a-model}

En Adobe Experience Platform, seleccione **[!UICONTROL Models]** , que se encuentra en la columna de navegación de la izquierda, y luego seleccione la pestaña **[!UICONTROL Browse]** para enumerar todos los modelos existentes. Seleccione el nombre del Modelo que desea publicar como Servicio.

![](../images/models-recipes/publish-model/browse_model.png)

Seleccione **[!UICONTROL Publish]** cerca de la parte superior derecha de la página Información general del modelo para iniciar un proceso de creación del servicio.

![](../images/models-recipes/publish-model/view_training.png)

Introduzca un nombre para el Servicio y, opcionalmente, proporcione una descripción del Servicio. Seleccione **[!UICONTROL Next]** cuando termine.

![](../images/models-recipes/publish-model/configure_training.png)

Se muestran todas las ejecuciones de formación correctas para hasta el modelo. El nuevo Servicio heredará las configuraciones de capacitación y puntuación de la ejecución de capacitación seleccionada.

![](../images/models-recipes/publish-model/select_training_run.png)

Seleccione **[!UICONTROL Finish]** para crear el Servicio y redirigir al **[!UICONTROL Service Gallery]** para mostrar todos los Servicios disponibles, incluido el Servicio recién creado.

![](../images/models-recipes/publish-model/service_gallery.png)

## Puntuación mediante un servicio {#access-a-service}

En Adobe Experience Platform, seleccione la pestaña **[!UICONTROL Services]** situada en la columna de navegación izquierda para acceder a **[!UICONTROL Service Gallery]**. Busque el Servicio que desea utilizar y seleccione **[!UICONTROL Open]**.

![](../images/models-recipes/publish-model/open_service.png)

En la página de información general del servicio, seleccione **[!UICONTROL Score]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleccione un conjunto de datos de entrada adecuado para la ejecución de puntuación y, a continuación, seleccione **[!UICONTROL Next]**. Se le pedirá que realice el mismo paso para el conjunto de datos de puntuación. Una vez que haya seleccionado el conjunto de datos de entrada y salida, puede actualizar las configuraciones.

![](../images/models-recipes/publish-model/select_datasets.png)

Cuando se crea un servicio, hereda las configuraciones de puntuación predeterminadas. Puede revisar estas configuraciones y ajustarlas según sea necesario haciendo doble clic en los valores. Una vez que esté satisfecho con las configuraciones, seleccione **[!UICONTROL Finish]** para comenzar la ejecución de la puntuación.

![](../images/models-recipes/publish-model/scoring_configs.png)

En la página **Overview** del servicio, se muestran detalles del nuevo trabajo de puntuación y su progreso. Una vez finalizado el trabajo, se actualiza el encabezado **[!UICONTROL Most Recent]** dentro del contenedor **[!UICONTROL Scoring]**.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha publicado correctamente un Modelo como Servicio accesible y ha marcado los datos utilizando el nuevo Servicio a través de [!UICONTROL Service Gallery]. Continúe con el siguiente tutorial para aprender cómo puede [programar la formación automatizada y las ejecuciones de puntuación en un Servicio](./schedule-models-ui.md).
