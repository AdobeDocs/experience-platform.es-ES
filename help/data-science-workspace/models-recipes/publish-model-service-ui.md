---
keywords: Experience Platform;publicar un modelo;Workspace de ciencia de datos;temas populares;puntuar un servicio
solution: Experience Platform
title: Publicación de un modelo como servicio en la IU de Workspace de ciencia de datos
type: Tutorial
description: Adobe Experience Platform Data Science Workspace le permite publicar su modelo entrenado y evaluado como servicio, lo que permite a los usuarios de su organización puntuar datos sin necesidad de crear sus propios modelos.
exl-id: ebbec1b1-20d3-43b5-82d3-89c79757625a
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 4%

---

# Publicación de un modelo como servicio en la IU de Espacio de trabajo de ciencia de datos {#publish-a-model-as-a-service}

>[!NOTE]
>
>Data Science Workspace ya no se puede adquirir.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

>[!CONTEXTUALHELP]
>id="platform_intelligentservices_publishmodel"
>title="Publicación de un modelo como servicio"
>abstract=""

Adobe Experience Platform Data Science Workspace le permite publicar su modelo entrenado y evaluado como servicio, lo que permite a los usuarios de su organización puntuar datos sin necesidad de crear sus propios modelos.

## Introducción

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo existente con una ejecución de formación correcta. Si no dispone de un modelo editable, siga el tutorial [Entrenar y evaluar un modelo en la interfaz de usuario](./train-evaluate-model-ui.md) antes de continuar.

Si prefiere publicar un modelo mediante las API de aprendizaje automático de Sensei, consulte el [tutorial de la API](./publish-model-service-api.md).

## Publicación de un modelo {#publish-a-model}

En Adobe Experience Platform, seleccione **[!UICONTROL Modelos]** ubicados en la columna de navegación izquierda y, a continuación, seleccione la pestaña **[!UICONTROL Examinar]** para ver una lista de todos los modelos existentes. Seleccione el nombre del modelo que desea publicar como servicio.

![](../images/models-recipes/publish-model/browse_model.png)

Seleccione **[!UICONTROL Publicar]** cerca de la parte superior derecha de la página Información general del modelo para iniciar un proceso de creación de servicio.

![](../images/models-recipes/publish-model/view_training.png)

Escriba un nombre para el servicio y, opcionalmente, proporcione una descripción del servicio. Seleccione **[!UICONTROL Siguiente]** cuando haya terminado.

![](../images/models-recipes/publish-model/configure_training.png)

Se muestran todas las ejecuciones de formación correctas para en el modelo. El nuevo servicio heredará las configuraciones de formación y puntuación de la ejecución de formación seleccionada.

![](../images/models-recipes/publish-model/select_training_run.png)

Seleccione **[!UICONTROL Finalizar]** para crear el servicio y redirigir a la **[!UICONTROL Galería de servicios]** para mostrar todos los servicios disponibles, incluido el servicio recién creado.

![](../images/models-recipes/publish-model/service_gallery.png)

## Puntuación mediante un servicio {#access-a-service}

En Adobe Experience Platform, seleccione la ficha **[!UICONTROL Servicios]** que se encuentra en la columna de navegación izquierda para acceder a **[!UICONTROL Galería de servicios]**. Busque el servicio que desea usar y seleccione **[!UICONTROL Abrir]**.

![](../images/models-recipes/publish-model/open_service.png)

En la página de información general del servicio, seleccione **[!UICONTROL Puntuación]**.

![](../images/models-recipes/publish-model/score_service.png)

Seleccione un conjunto de datos de entrada apropiado para la ejecución de puntuación y, a continuación, seleccione **[!UICONTROL Siguiente]**. Se le pide que haga lo mismo para el conjunto de datos de puntuación. Una vez seleccionado el conjunto de datos de entrada y salida, puede actualizar las configuraciones.

![](../images/models-recipes/publish-model/select_datasets.png)

Cuando se crea un servicio, hereda las configuraciones de puntuación predeterminadas. Puede revisar estas configuraciones y ajustarlas según sea necesario haciendo doble clic en los valores. Una vez que esté satisfecho con las configuraciones, seleccione **[!UICONTROL Finalizar]** para comenzar la ejecución de puntuación.

![](../images/models-recipes/publish-model/scoring_configs.png)

En la página **Información general** del servicio se muestran los detalles del nuevo trabajo de puntuación y su progreso. Una vez finalizado el trabajo, se actualiza el encabezado **[!UICONTROL Más reciente]** dentro del contenedor **[!UICONTROL Puntuación]**.

![](../images/models-recipes/publish-model/pending_scoring.png)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ha publicado correctamente un modelo como servicio accesible y ha puntuado los datos mediante el nuevo servicio a través de [!UICONTROL Service Gallery]. Continúe con el siguiente tutorial para aprender cómo puede [programar ejecuciones automatizadas de entrenamiento y puntuación en un servicio](./schedule-models-ui.md).
