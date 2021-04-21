---
keywords: Experience Platform;inicio;temas populares;dsw;DSW
solution: Experience Platform
title: Tutoriales de Data Science Workspace
topic-legacy: tutorial
type: Tutorial
description: Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe.
exl-id: 7cfd71b1-584f-4588-bbcd-bc42a08a0bc0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# [!DNL Data Science Workspace] tutoriales

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe. Los científicos de datos de todos los niveles tienen herramientas sofisticadas y fáciles de usar que respaldan el rápido desarrollo, capacitación y ajuste de recetas de aprendizaje automático -todos los beneficios de la tecnología de IA, sin la complejidad.

Para obtener más información, comience por leer la [información general de Data Science Workspace](../data-science-workspace/home.md).

## [!DNL Sensei Machine Learning] API

La API [!DNL Sensei Machine Learning] proporciona un mecanismo para que los científicos de datos organicen y gestionen los servicios de aprendizaje automático, desde la incorporación de algoritmos hasta la experimentación y la implementación de servicios.

**Estas son las guías para desarrolladores de API disponibles:**
- [Motores](../data-science-workspace/api/engines.md) : Obtenga información sobre cómo buscar en el  [!DNL Docker] registro, crear un motor, crear un motor de canalización de funciones, recuperar la información de un motor, actualizar un motor y eliminar un motor.
- [Instancias MLI (fórmulas)](../data-science-workspace/api/mlinstances.md) : Aprenda a crear una instancia MLI, recuperar la información para una instancia MLI, actualizar una instancia MLI y eliminar una instancia MLI.
- [Experimentos](../data-science-workspace/api/experiments.md) : Aprenda a crear un experimento, recuperar un experimento o experimento ejecuta información, actualizar un experimento y eliminar un experimento.
- [Modelos](../data-science-workspace/api/models.md) : Aprenda a registrar su propio modelo, recuperar la información de un modelo, actualizar un modelo, eliminar un modelo, crear una nueva transcodificación para un modelo y recuperar los detalles de un modelo transcodificado.
- [MLServices](../data-science-workspace/api/mlservices.md) : Aprenda a crear un MLService, recuperar la información de un MLService, actualizar un MLService y eliminar un MLService.
- [Perspectivas](../data-science-workspace/api/insights.md) : Aprenda a recuperar la información de una perspectiva, añada una nueva perspectiva de modelo y recupere una lista de métricas predeterminadas para los algoritmos.

Para obtener más información y obtener los valores necesarios para realizar operaciones de CRUD con la API de aprendizaje automático de Sensei, visite la [guía de introducción](../data-science-workspace/api/getting-started.md).

## Cómo usar [!DNL JupyterLab] equipos portátiles

[!DNL JupyterLab] es una interfaz de usuario basada en web para  [!DNL Project Jupyter] y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con [!DNL Jupyter Notebooks], código y datos. Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

**Esta guía le ayudará a:**
- Acceda y comprenda la interfaz [!DNL JupyterLab].
- Comprender las celdas de código y los núcleos disponibles en [!DNL JupyterLab].
- Comprender la configuración de GPU y del servidor de memoria en [!DNL Python]/R.

Para obtener más información, visite la [guía del usuario de JupyterLab](../data-science-workspace/jupyterlab/overview.md).

## Acceso a datos en portátiles de JupyterLab

Actualmente, JupyterLab en Data Science Workspace admite portátiles para [!DNL Python], R, PySpark y Scala. Cada núcleo soportado proporciona funcionalidades incorporadas que permiten leer datos de Platform desde un conjunto de datos dentro de un bloc de notas. Sin embargo, la compatibilidad con la paginación de datos se limita a los [!DNL Python] y los portátiles R. Esta guía se centra en cómo utilizar los portátiles JupyterLab para acceder a sus datos.

**Esta guía le ayudará a:**
- Lea, escriba y realice consultas en los datos de Platform mediante los portátiles Python, R, PySpark o Scala.
- Comprenda las limitaciones de lectura de cada tipo de bloc de notas.

Para obtener más información, visite la [guía para desarrolladores de acceso a datos de JupyterLab](../data-science-workspace/jupyterlab/access-notebook-data.md)

## Archivos de origen de paquetes para la creación de fórmulas [!DNL Docker]

Una imagen [!DNL Docker] le permite empaquetar una aplicación con todas las partes que necesite. Esto incluye bibliotecas y otras dependencias en un paquete. La imagen [!DNL Docker] creada se inserta en el [!DNL Azure Container Registry] mediante las credenciales proporcionadas durante el flujo de trabajo de creación de la fórmula.

**Este tutorial le ayudará a:**
- Descargue los requisitos previos necesarios para la creación de fórmulas.
- Comprender la creación de modelos basados en [!DNL Docker].
- Cree una imagen [!DNL Docker] para [!DNL Python], R, PySpark o Scala ([!DNL Spark]).
- Obtenga una dirección URL de archivo de origen [!DNL Docker].

Para obtener más información, siga el [paquete de archivos de origen en un tutorial de fórmula](../data-science-workspace/models-recipes/package-source-files-recipe.md).

## Importar una fórmula

>[!NOTE]
>
>Este tutorial requiere que tenga una URL de archivo de origen [!DNL Docker]. Visite los [archivos de origen de paquetes en un tutorial de fórmula](../data-science-workspace/models-recipes/package-source-files-recipe.md) si no tiene una dirección URL de [!DNL Docker] archivo de origen.

Los tutoriales de fórmula de importación proporcionan información sobre cómo configurar e importar una fórmula empaquetada. Al final de este tutorial, puede crear, entrenar y evaluar un modelo en Adobe Experience Platform [!DNL Data Science Workspace].

**Este tutorial le ayudará a:**
- Cree un conjunto de configuraciones para una fórmula.
- Importe una fórmula basada en [!DNL Docker] para [!DNL Python], R, PySpark o Scala ([!DNL Spark]).

Para obtener más información, siga el tutorial de importación de una fórmula empaquetada [UI](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) o el [tutorial de API](../data-science-workspace/models-recipes/import-packaged-recipe-api.md).

## Capacitar y evaluar un modelo

En Adobe Experience Platform [!DNL Data Science Workspace], se crea un modelo de aprendizaje automático mediante la incorporación de una fórmula existente que es adecuada para la intención del modelo. A continuación, el Modelo es entrenado y evaluado para optimizar su eficacia y eficiencia operativa mediante el ajuste de sus hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear varios modelos y adaptarlos a propósitos específicos con una sola fórmula.

**Este tutorial le ayudará a:**
- Crear un nuevo modelo.
- Cree una ejecución de formación para el modelo.
- Evalúe las ejecuciones de formación del modelo.

Para empezar, siga la formación y evaluación de un modelo [tutorial de API](../data-science-workspace/models-recipes/train-evaluate-model-api.md) o el [tutorial de interfaz de usuario](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

## Optimización de un modelo mediante el marco de información del modelo

Model Insights Framework proporciona a los científicos de datos herramientas en Adobe Experience Platform [!DNL Data Science Workspace] para tomar decisiones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo de aprendizaje automático, así como la facilidad de uso de los científicos de datos. Esto se hace proporcionando una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático para ayudar con el ajuste del modelo. El resultado final permite a los científicos de datos y a los científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

**Este tutorial le ayudará a:**
- Configure el código de fórmula.
- Definir métricas personalizadas.
- Utilice métricas de evaluación y gráficos de visualización creados previamente.

Para empezar, siga el tutorial sobre [optimización de un modelo](../data-science-workspace/models-recipes/optimize-model.md).

## Puntuación de un modelo

La puntuación en Adobe Experience Platform [!DNL Data Science Workspace] se puede lograr añadiendo datos de entrada a un modelo entrenado existente. Los resultados de puntuación se almacenan y pueden verse en un conjunto de datos de salida especificado como un nuevo lote.

**Este tutorial le ayudará a:**
- Cree una nueva ejecución de puntuación.
- Vea los resultados de puntuación.

Para empezar, siga la puntuación de un modelo [tutorial de API](../data-science-workspace/models-recipes/score-model-api.md) o el [tutorial de interfaz de usuario](../data-science-workspace/models-recipes/score-model-ui.md).

## Publicación de un modelo como servicio

Adobe Experience Platform [!DNL Data Science Workspace] permite publicar el modelo como servicio, lo que permite a los usuarios de la organización IMS puntuar los datos sin necesidad de crear sus propios modelos. Esto se puede hacer mediante la interfaz de usuario [!DNL Platform] o la API [!DNL Sensei Machine Learning].

**Este tutorial le ayudará a:**
- Publique un modelo como servicio.
- Puntuación de datos mediante un servicio mediante [!DNL Platform] [!UICONTROL Service Gallery].

Para empezar, siga el tutorial [API](../data-science-workspace/models-recipes/publish-model-service-api.md) del servicio Publish a model as a service o el tutorial [UI](../data-science-workspace/models-recipes/publish-model-service-ui.md).

## Programar la formación y la puntuación para un modelo

Adobe Experience Platform [!DNL Data Science Workspace] le permite configurar ejecuciones de puntuación y formación programadas en un servicio de aprendizaje automático. La automatización del proceso de capacitación y puntuación puede ayudar a mantener y mejorar la eficacia de un servicio a lo largo del tiempo al mantenerse al día con los patrones dentro de los datos.

**Este tutorial le ayudará a:**
- Configurar la puntuación programada
- Configuración de la formación programada

Para empezar, siga el [tutorial de programación de una IU modelo](../data-science-workspace/models-recipes/schedule-models-ui.md).

## Creación de una canalización de funciones

>[!NOTE]
>
>Actualmente, las canalizaciones de funciones solo están disponibles mediante API.

Adobe Experience Platform le permite crear y crear canalizaciones de funciones personalizadas para realizar ingeniería de funciones a escala a través de [!DNL Sensei Machine Learning Framework Runtime].

**Esta guía le ayudará a:**
- Implemente clases de canalización de funciones.
- Cree un motor de canalización de funciones mediante la API .

Para obtener más información, visite el tutorial para [crear una canalización de funciones](../data-science-workspace/authoring/feature-pipeline.md).

## Generar una aplicación [!DNL Real-Time Machine Learning] (alfa)

Una combinación de computación optimizada tanto en el Hub como en el [!DNL Edge] reduce drásticamente la latencia que tradicionalmente está involucrada en la generación de experiencias hiperpersonalizadas que son relevantes y responden. Por lo tanto, [!DNL Real-time Machine Learning] proporciona inferencias con una latencia increíblemente baja para la toma de decisiones sincrónica. Algunos ejemplos son el procesamiento de contenido personalizado de una página web, el envío de una oferta y los descuentos para reducir la pérdida y aumentar las conversiones en una tienda web.

**Esta guía le ayudará a:**
- Comprenda la arquitectura [!DNL Real-time Machine Learning].
- Comprender el flujo de trabajo [!DNL Real-time Machine Learning].
- Comprender la funcionalidad actual de [!DNL Real-time Machine Learning].
- Proporcione los siguientes pasos para crear su propio [!DNL Real-time Machine Learning model].

Para obtener más información, visite [Información general de aprendizaje automático en tiempo real](../data-science-workspace/real-time-machine-learning/home.md).
