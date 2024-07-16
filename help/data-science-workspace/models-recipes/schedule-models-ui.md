---
keywords: Experience Platform;programar un modelo;Workspace de ciencia de datos;temas populares;programar puntuación;programar formación
solution: Experience Platform
title: Programar un modelo en la IU de Workspace de ciencia de datos
type: Tutorial
description: Adobe Experience Platform Data Science Workspace le permite configurar ejecuciones programadas de puntuación y formación en un servicio de aprendizaje automático. La automatización del proceso de formación y puntuación puede ayudar a mantener y mejorar la eficacia de un servicio a lo largo del tiempo, al estar al día con los patrones de los datos.
exl-id: 51f6f328-7c63-4de1-9184-2ba526bb82e2
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---

# Programar un modelo en la interfaz de usuario de Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] le permite configurar ejecuciones de formación y puntuación programadas en un servicio de aprendizaje automático. La automatización del proceso de formación y puntuación puede ayudar a mantener y mejorar la eficacia de un servicio a lo largo del tiempo, al estar al día con los patrones de los datos.

Este tutorial muestra los pasos para configurar las programaciones de entrenamiento y puntuación en un servicio existente a través de [!UICONTROL Service Gallery]. Se divide en las siguientes secciones principales:

- [Configurar puntuación programada](#configure-scheduled-scoring)
- [Configuración de la formación programada](#configure-scheduled-training)

## Introducción

Para completar este tutorial, debe tener acceso a [!DNL Experience Platform]. Si no tiene acceso a una organización en [!DNL Experience Platform], comuníquese con el administrador del sistema antes de continuar.

Este tutorial requiere un servicio existente. Si no tiene un servicio accesible con el que trabajar, puede crear uno siguiendo el tutorial de [publicación de un modelo como servicio](./publish-model-service-ui.md).

## Configurar puntuación programada {#configure-scheduled-scoring}

La puntuación del modelo se puede configurar para que sea un proceso automatizado de forma programada. Una vez creado un servicio, puede seguir los pasos a continuación para configurar y aplicar una programación de puntuación:

En Adobe Experience Platform, seleccione la ficha **[!UICONTROL Servicios]** ubicada en la columna de navegación izquierda para acceder a **[!DNL Service Gallery]**. Busque el servicio en el que desea programar ejecuciones de puntuación y seleccione **[!UICONTROL Abrir]** para ver su página **[!UICONTROL Información general]**.

![](../images/models-recipes/schedule/select_service.png)

La página Información general muestra la información de puntuación del servicio. Seleccione el vínculo **[!UICONTROL Programación de actualizaciones]** para configurar una programación de puntuación.

![](../images/models-recipes/schedule/update_scoring.png)

Configure la frecuencia, la fecha de inicio, la fecha de finalización, el conjunto de datos de entrada y el conjunto de datos de salida para la programación de puntuación. Una vez que esté satisfecho con las configuraciones, seleccione **[!UICONTROL Crear]** para actualizar la programación de puntuación del servicio.

![](../images/models-recipes/schedule/set_scoring_schedule.png)

Su programación de puntuación actualizada se muestra en la página **[!UICONTROL Información general]** del servicio.

![](../images/models-recipes/schedule/scoring_set.png)

## Configuración de la formación programada {#configure-scheduled-training}

La configuración de ejecuciones de formación programadas en un servicio garantiza que el modelo de aprendizaje automático se actualice a los patrones de datos más recientes. Cada vez que se completa una ejecución de formación programada, se utiliza el modelo formado resultante para activar el servicio hasta la siguiente ejecución de formación programada.

Una vez creado un servicio, puede seguir los pasos a continuación para configurar y aplicar una programación de formación:

En Adobe Experience Platform, seleccione la ficha **[!UICONTROL Servicios]** que se encuentra en la columna de navegación izquierda para acceder a **[!UICONTROL Galería de servicios]**. Busque el servicio en el que desea programar ejecuciones de formación y seleccione **[!UICONTROL Abrir]** para ver su página **[!UICONTROL Información general]**.

![](../images/models-recipes/schedule/select_service.png)

La página Información general muestra la información de formación del servicio. Seleccione el vínculo **[!UICONTROL Calendario de actualizaciones]** para configurar un programa de aprendizaje.

![](../images/models-recipes/schedule/update_training.png)

Configure la frecuencia, la fecha de inicio, la fecha de finalización y el conjunto de datos de entrada utilizado para la programación de formación. Una vez que esté satisfecho con las configuraciones, seleccione **[!UICONTROL Crear]** para actualizar el horario de entrenamiento del servicio.

![](../images/models-recipes/schedule/set_training_schedule.png)

Su horario de entrenamiento actualizado se muestra en la página **[!UICONTROL Información general]** del servicio.

![](../images/models-recipes/schedule/training_set.png)

## Pasos siguientes

Al seguir este tutorial, ha programado correctamente ejecuciones de puntuación y formación automatizada en un servicio y ha completado el flujo de trabajo de la interfaz de usuario del tutorial [!DNL Data Science Workspace]. Si aún no lo ha hecho, considere [reiniciar el tutorial](./create-retails-sales-dataset.md) y siga el flujo de trabajo de la API para crear, entrenar, puntuar y publicar un modelo.
