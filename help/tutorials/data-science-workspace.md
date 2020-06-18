---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriales de Área de trabajo de Data Science
topic: tutorial
translation-type: tm+mt
source-git-commit: 4d7d61660e6691d77701db1c089b84eee7f60974
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---


# Tutoriales de Área de trabajo de Data Science

Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de los datos. Integrado en Adobe Experience Platform, el espacio de trabajo de ciencia de datos le ayuda a realizar predicciones con sus recursos de contenido y datos en todas las soluciones de Adobe. Los científicos de datos de todos los niveles tienen herramientas sofisticadas y fáciles de usar que respaldan el rápido desarrollo, capacitación y ajuste de recetas de aprendizaje automático -todos los beneficios de la tecnología de IA, sin la complejidad.

Para obtener más información, lea la información general [de](../data-science-workspace/home.md)Data Science Workspace.

## API de aprendizaje automático de Sensei

La API de aprendizaje automático de Sensei proporciona un mecanismo para que los científicos de datos organicen y gestionen los servicios de aprendizaje automático, desde la incorporación de algoritmos hasta la experimentación y la implementación del servicio.

**Están disponibles las siguientes guías para desarrolladores de API:**
- [Motores](../data-science-workspace/api/engines.md) : Aprenda a buscar el registro del Docker, crear un motor, crear una canalización de funciones Motor, recuperar la información de un motor, actualizar un motor y eliminar un motor.
- [Instancias MLI (fórmulas)](../data-science-workspace/api/mlinstances.md) : Aprenda a crear una instancia MLI, recuperar la información de una instancia MLI, actualizar una instancia MLI y eliminar una instancia MLI.
- [Experimentos](../data-science-workspace/api/experiments.md) : Aprenda a crear un experimento, recuperar un experimento o experimento ejecuta información, actualizar un experimento y eliminar un experimento.
- [Modelos](../data-science-workspace/api/models.md) : Aprenda a registrar su propio modelo, recuperar la información de un modelo, actualizar un modelo, eliminar un modelo, crear una nueva transcodificación para un modelo y recuperar los detalles de un modelo transcodificado.
- [MLServices](../data-science-workspace/api/mlservices.md) : Aprenda a crear un MLService, recuperar la información de un MLService, actualizar un MLService y eliminar un MLService.
- [Perspectivas](../data-science-workspace/api/insights.md) : Descubra cómo recuperar la información de una perspectiva, agregue una nueva perspectiva de modelo y recupere una lista de las métricas predeterminadas para los algoritmos.

Para obtener más información y obtener los valores necesarios para realizar operaciones de CRUD con la API de aprendizaje automático de Sensei, visite la guía de [introducción](../data-science-workspace/api/getting-started.md).

## Cómo usar equipos portátiles JupyterLab

[!DNL JupyterLab] es una interfaz de usuario basada en web para [!DNL Project Jupyter] y está estrechamente integrada en Adobe Experience Platform. Proporciona un entorno de desarrollo interactivo para que los científicos de datos trabajen con portátiles Jupyter, código y datos. Este documento proporciona información general sobre [!DNL JupyterLab] y sus características, así como instrucciones para realizar acciones comunes.

**Esta guía le ayudará a:**
- Obtenga acceso y comprenda la [!DNL JupyterLab] interfaz.
- Comprender las celdas de código y los núcleos disponibles dentro de [!DNL JupyterLab].
- Comprender la configuración de la GPU y del servidor de memoria en Python/R.
- Leer y consulta [!DNL Platform] de datos con portátiles.
- Comprender los límites de datos del bloc de notas.

Para obtener más información, visite la guía [del usuario de](../data-science-workspace/jupyterlab/overview.md)JupyterLab.

## Empaquetar archivos de origen para la creación de fórmulas de Docker

Una imagen de Docker le permite empaquetar una aplicación con todas las partes que necesita. Esto incluye bibliotecas y otras dependencias en un solo paquete. La imagen de Docker creada se inserta en el Registro de Contenedor de Azure mediante las credenciales proporcionadas durante el flujo de trabajo de creación de fórmulas.

**Este tutorial le ayudará a:**
- Descargue los requisitos previos necesarios para la creación de fórmulas.
- Comprender la creación de modelos basados en Docker.
- Cree una imagen de acoplamiento para Python, R, PySpark o Scala (Chispa).
- Obtenga una URL de archivo de origen de Docker.

Para obtener más información, siga los archivos de origen del [paquete en un tutorial](../data-science-workspace/models-recipes/package-source-files-recipe.md)de fórmula.

## Importar una fórmula

>[!NOTE]
>Este tutorial requiere que tenga una URL de archivo de origen de Docker. Visite los archivos de origen del [paquete en un tutorial](../data-science-workspace/models-recipes/package-source-files-recipe.md) de fórmula si no tiene una URL de archivo de origen del Docker.

Los tutoriales de las fórmulas de importación proporcionan información sobre cómo configurar e importar una fórmula empaquetada. Al final de este tutorial, puede crear, capacitar y evaluar un modelo en Adobe Experience Platform Data Science Workspace.

**Este tutorial le ayudará a:**
- Cree un conjunto de configuraciones para una fórmula.
- Importe una fórmula basada en el Docker para Python, R, PySpark o Scala (Spark).

Para obtener más información, siga el tutorial [de importación de una](../data-science-workspace/models-recipes/import-packaged-recipe-ui.md) interfaz de usuario de fórmula empaquetada o el tutorial [de](../data-science-workspace/models-recipes/import-packaged-recipe-api.md)API.

## Formación y evaluación de un modelo

En Adobe Experience Platform Data Science Workspace, se crea un modelo de aprendizaje automático mediante la incorporación de una fórmula existente que es apropiada para la intención del modelo. A continuación, se capacita y evalúa al Modelo para optimizar su eficacia y eficiencia operativa mediante el ajuste de sus hiperparámetros asociados. Las fórmulas son reutilizables, lo que significa que se pueden crear y adaptar varios modelos a fines específicos con una sola fórmula.

**Este tutorial le ayudará a:**
- Crear un nuevo modelo.
- Cree una ejecución de formación para el modelo.
- Evalúe las ejecuciones de formación del modelo.

Para empezar, siga la formación y evaluación de un tutorial [de](../data-science-workspace/models-recipes/train-evaluate-model-api.md) API de modelo o el tutorial [de](../data-science-workspace/models-recipes/train-evaluate-model-ui.md)IU.

## Optimizar un modelo mediante el marco de perspectivas de modelo

Model Insights Framework proporciona al científico de datos herramientas en Adobe Experience Platform Data Science Workspace para tomar decisiones rápidas e informadas para modelos óptimos de aprendizaje automático basados en experimentos. El marco mejorará la velocidad y la eficacia del flujo de trabajo del aprendizaje automático, así como la facilidad de uso de los científicos de datos. Esto se lleva a cabo proporcionando una plantilla predeterminada para cada tipo de algoritmo de aprendizaje automático para facilitar el ajuste del modelo. El resultado final permite a los científicos de datos y a los científicos de datos ciudadanos tomar mejores decisiones de optimización de modelos para sus clientes finales.

**Este tutorial le ayudará a:**
- Configure el código de fórmula.
- Definir métricas personalizadas.
- Utilice métricas de evaluación y gráficos de visualización creados previamente.

Para empezar, siga el tutorial sobre la [optimización de un modelo](../data-science-workspace/models-recipes/optimize-model.md).

## Puntuación de un modelo

La puntuación en Adobe Experience Platform Data Science Workspace se puede lograr mediante la incorporación de datos de entrada a un modelo existente capacitado. Los resultados de puntuación se almacenan y se pueden ver en un conjunto de datos de salida especificado como un nuevo lote.

**Este tutorial le ayudará a:**
- Crear una nueva carrera de puntuación.
- Vista los resultados de puntuación.

Para empezar, siga el tutorial [de puntaje de una](../data-science-workspace/models-recipes/score-model-api.md) API de modelo o el tutorial [de la](../data-science-workspace/models-recipes/score-model-ui.md)interfaz de usuario.

## Publicación de un modelo como servicio

Adobe Experience Platform Data Science Workspace le permite publicar el modelo como un servicio, lo que permite a los usuarios de la organización de IMS puntuar datos sin necesidad de crear sus propios modelos. Esto se puede hacer mediante la interfaz de usuario o la API de aprendizaje automático Sensei. [!DNL Platform]

**Este tutorial le ayudará a:**
- Publicar un modelo como servicio.
- Puntuación de datos mediante un servicio a través de la Galería de [!DNL Platform] servicios.

Para empezar, siga el tutorial [de publicación de un modelo como](../data-science-workspace/models-recipes/publish-model-service-api.md) API de servicio o el tutorial [de](../data-science-workspace/models-recipes/publish-model-service-ui.md)interfaz de usuario.

## Programar la formación y la puntuación de un modelo

Adobe Experience Platform Data Science Workspace le permite configurar las ejecuciones de puntuación y formación programadas en un servicio de aprendizaje automático. La automatización del proceso de calificación y capacitación puede ayudar a mantener y mejorar la eficacia de un servicio a través del tiempo, al mantenerse al día con los patrones dentro de los datos.

**Este tutorial le ayudará a:**
- Configurar puntuación programada
- Configurar la formación programada

Para empezar, siga la [programación de un tutorial](../data-science-workspace/models-recipes/schedule-models-ui.md)de la IU de modelo.

## Creación de una canalización de funciones

>[!NOTE]
>Actualmente, las tuberías de funciones solo están disponibles mediante API.

Adobe Experience Platform le permite crear y crear tuberías de funciones personalizadas para realizar ingeniería de funciones a escala a través de Sensei Machine Learning Framework Runtime.

**Esta guía le ayudará a:**
- Implemente clases de canalización de funciones.
- Cree un motor de canalización de funciones mediante la API.

Para obtener más información, visite el tutorial para [crear una canalización](../data-science-workspace/authoring/feature-pipeline.md)de funciones.

## Creación de una aplicación de aprendizaje automático en tiempo real (alfa)

Una combinación de computación sin fisuras tanto en el concentrador como en el borde reduce considerablemente la latencia que tradicionalmente está involucrada en la generación de experiencias hiperpersonalizadas que son relevantes y responden. Por lo tanto, el aprendizaje automático en tiempo real proporciona inferencias con una latencia increíblemente baja para la toma de decisiones sincrónica. Algunos ejemplos son el procesamiento de contenido personalizado de una página web, la aparición de una oferta y los descuentos para reducir la producción y aumentar las conversiones en una tienda web.

**Esta guía le ayudará a:**
- Conozca la arquitectura de aprendizaje automático en tiempo real.
- Conozca el flujo de trabajo de aprendizaje automático en tiempo real.
- Conozca la funcionalidad actual de aprendizaje automático en tiempo real.
- Proporcione los siguientes pasos para crear su propio modelo de aprendizaje automático en tiempo real.

Para obtener más información, visite la información general [de aprendizaje automático en tiempo](../data-science-workspace/real-time-machine-learning/home.md)real.