---
keywords: Experience Platform;schedule a model;Data Science Workspace;popular topics
solution: Experience Platform
title: Programar un modelo (IU)
topic: Tutorial
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Programar un modelo (IU)

El espacio de trabajo de ciencias de datos de la plataforma de Adobe Experience Workspace le permite configurar las ejecuciones de puntuación y formación programadas en un servicio de aprendizaje automático. La automatización del proceso de calificación y capacitación puede ayudar a mantener y mejorar la eficiencia de un servicio a través del tiempo, al mantenerse al día con los patrones dentro de sus datos.

En este tutorial se explican los pasos para configurar las programaciones de capacitación y puntuación en un servicio existente a través de la Galería *de servicios*. Se divide en las siguientes secciones principales:

- [Configurar puntuación programada](#configure-scheduled-scoring)
- [Configurar la formación programada](#configure-scheduled-training)

## Primeros pasos

Para completar este tutorial, debe tener acceso a la plataforma de experiencias. Si no tiene acceso a una organización de IMS en la plataforma de experiencia, póngase en contacto con el administrador del sistema antes de continuar.

Este tutorial requiere un servicio existente. Si no tiene un servicio accesible con el que trabajar, puede crear uno siguiendo el tutorial [Publicar el modelo como servicio de la interfaz de usuario](./publish-model-service-ui.md) .

## Configurar puntuación programada {#configure-scheduled-scoring}

La puntuación de modelo se puede configurar para que sea un proceso automatizado y programado. Una vez creado el servicio, puede seguir los pasos a continuación para configurar y aplicar un programa de puntuación:

1. En Adobe Experience Platform, haga clic en la **[!UICONTROL Services]** ficha situada en la columna de navegación izquierda para acceder a la Galería *de servicios*. Busque el servicio en el que desea programar las ejecuciones de puntuación y haga clic en **[!UICONTROL Open]** para vista de su página *Información general* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La página Información general muestra la información de puntuación del servicio. Haga clic en el **[!UICONTROL Update Schedule]** vínculo para configurar un programa de puntuación.
   ![](../images/models-recipes/schedule/service_overview_score.png)

3. Configure la frecuencia, la fecha de inicio, la fecha de finalización, el conjunto de datos de entrada y el conjunto de datos de salida para la programación de puntuación. Una vez que esté satisfecho con las configuraciones, haga clic en **[!UICONTROL Create]** para actualizar el programa de puntuación del Servicio.
   ![](../images/models-recipes/schedule/14_configure_scoring_schedule.png)

4. El programa de puntuación actualizado se muestra en la página *Información general* del servicio.
   ![](../images/models-recipes/schedule/service_with_scoring_schedule.png)


## Configurar la formación programada {#configure-scheduled-training}

La configuración de las ejecuciones de formación programadas en un servicio garantiza que el modelo de aprendizaje automático se actualice a los patrones de datos más recientes. Siempre que se completa una ejecución de formación programada, se utiliza el modelo capacitado resultante para activar el servicio hasta la siguiente ejecución de formación programada.

Una vez creado el servicio, puede seguir los pasos que se indican a continuación para configurar y aplicar una programación de formación:

1. En Adobe Experience Platform, haga clic en la **[!UICONTROL Services]** ficha situada en la columna de navegación izquierda para acceder a la Galería *de servicios*. Busque el servicio en el que desea programar las ejecuciones de formación y haga clic en **[!UICONTROL Open]** para vista de su página *Información general* .
   ![](../images/models-recipes/schedule/click_to_open.png)

2. La página Información general muestra la información de capacitación del servicio. Haga clic en el **[!UICONTROL Update Schedule]** vínculo para configurar una programación de formación.
   ![](../images/models-recipes/schedule/service_overview_train.png)

3. Configure la frecuencia, la fecha de inicio, la fecha de finalización y el conjunto de datos de entrada utilizados para la programación de formación. Una vez que esté satisfecho con las configuraciones, haga clic en **[!UICONTROL Create]** para actualizar la programación de capacitación del Servicio.
   ![](../images/models-recipes/schedule/12_configure_training_schedule.png)

4. La programación de formación actualizada se muestra en la página *Información general* del servicio.
   ![](../images/models-recipes/schedule/service_with_training_schedule.png)

## Pasos siguientes

Siguiendo este tutorial, ha programado correctamente las ejecuciones de puntuación y formación automatizada en un servicio y ha completado el flujo de trabajo de la interfaz de usuario del tutorial de espacio de trabajo de ciencia de datos. Si aún no lo ha hecho, considere [reiniciar el tutorial](./create-retails-sales-dataset.md) y siga el flujo de trabajo de API para crear, entrenar, marcar y publicar un modelo.
