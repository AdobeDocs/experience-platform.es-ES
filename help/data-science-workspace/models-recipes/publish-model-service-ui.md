---
keywords: Experience Platform;publish a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Publicación de un modelo como servicio (UI)
topic: Tutorial
translation-type: tm+mt
source-git-commit: af491361c5c3518e9bcc0af41a5aa79022229a2d

---


# Publicación de un modelo como servicio (UI)

El espacio de trabajo de ciencias de datos de la plataforma de Adobe Experience Workspace le permite publicar el modelo evaluado y capacitado como un servicio, lo que permite a los usuarios de la organización de IMS puntuar datos sin necesidad de crear sus propios modelos.

En este tutorial se explican los pasos para publicar un modelo como servicio y se puntúan los datos mediante un servicio a través de la Galería *de servicios*. Se divide en las siguientes secciones principales:

- [Publicación de un modelo](#publish-a-model)
- [Puntuación mediante un servicio](#access-a-service)

## Primeros pasos

Para completar este tutorial, debe tener acceso a la plataforma de experiencias. Si no tiene acceso a una organización de IMS en la plataforma de experiencia, póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un modelo existente con una ejecución de formación correcta. Si no dispone de un modelo que se pueda publicar, siga el [programa de formación y evalúe un modelo en el tutorial de la interfaz de usuario](./train-evaluate-model-ui.md) antes de continuar.

Si prefiere publicar un modelo con las API de aprendizaje automático de Sensei, consulte el tutorial [de](./publish-model-service-api.md)API.

## Publicación de un modelo

1. En Adobe Experience Platform, haga clic en el vínculo **Modelos** ubicado en la columna de navegación izquierda para lista de todos los modelos existentes. Busque y haga clic en el nombre del modelo que se va a publicar como servicio.
   ![](../images/models-recipes/publish-model/1_browse_model.png)
1. Haga clic en **Publicar** cerca de la parte superior derecha de la página de información general del modelo para inicio de un proceso de creación de servicios.
   ![](../images/models-recipes/publish-model/2_view_training_runs.png)
1. Introduzca un nombre que desee para el servicio y, si lo desea, proporcione una descripción del servicio, haga clic en **Siguiente** cuando finalice.
   ![](../images/models-recipes/publish-model/3_configure_service.png)
1. Se muestran todas las ejecuciones de formación correctas para el modelo. El nuevo servicio heredará las configuraciones de capacitación y puntuación de la ejecución de formación seleccionada.
   ![](../images/models-recipes/publish-model/4_select_training_run.png)
1. Haga clic en **Finalizar** para crear el servicio y redirigir a la Galería **de** servicios para mostrar todos los servicios disponibles, incluido el servicio recién creado.
   ![](../images/models-recipes/publish-model/service_gallery.png)

## Puntuación mediante un servicio

1. En Adobe Experience Platform, haga clic en la ficha **Servicios** situada en la columna de navegación izquierda para acceder a la Galería *de servicios*. Busque el servicio que desee utilizar y haga clic en **Puntuación**.
   ![](../images/models-recipes/publish-model/click_to_score.png)
1. Seleccione un conjunto de datos de entrada adecuado para la ejecución de puntuación y haga clic en **Siguiente**.
   ![](../images/models-recipes/publish-model/6_scoring_input.png)
1. Seleccione un conjunto de datos de salida adecuado para los resultados de puntuación y haga clic en **Siguiente**.
   ![](../images/models-recipes/publish-model/7_scoring_output.png)
1. Cuando se crea un servicio, hereda las configuraciones de puntuación predeterminadas. Puede revisar estas configuraciones y ajustarlas según sea necesario haciendo clic con el doble en los valores. Una vez que esté satisfecho con las configuraciones, haga clic en **Finalizar** para comenzar la ejecución de la puntuación.
   ![](../images/models-recipes/publish-model/8_scoring_configure.png)
1. En la página *Información general* del servicio, se muestran los detalles del nuevo trabajo de puntuación y su progreso. Una vez finalizado el trabajo, se actualizará el trabajo de puntuación **Más reciente** .
   ![](../images/models-recipes/publish-model/score_pending.png)

## Pasos siguientes

Siguiendo este tutorial, ha publicado correctamente un modelo como un servicio accesible y ha puntuado datos mediante el nuevo servicio a través de la Galería *de* servicios. Continúe con el siguiente tutorial para obtener información sobre cómo puede [programar las ejecuciones de puntuación y formación automatizada en un servicio](./schedule-models-ui.md).
