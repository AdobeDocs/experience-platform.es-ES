---
title: Flujo de trabajo de extremo a extremo del enriquecimiento de la canalización de datos AI/ML
description: Utilice los portátiles del entorno de aprendizaje automático basados en la nube para crear un modelo de formación y puntuación que prediga las conversiones de suscripción a partir de los datos de Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 2853e7c7-cab8-4e1b-b73f-622c937fbbaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

<!-- 
title: Cloud Machine Learning Environment Notebooks
Cloud machine learning environment notebooks
Old title: 
# AI/ML data pipeline enrichment end-to-end workflow
-->

# Flujo de trabajo completo de enriquecimiento de la canalización de datos AI/ML

Utilice Data Distiller para enriquecer sus canalizaciones de aprendizaje automático con datos de experiencia del cliente de alto valor que se han recopilado y depurado en Adobe Experience Platform.

Este documento proporciona una serie de blocs de notas de entornos de aprendizaje automático basados en la nube que muestran un flujo de trabajo completo. El flujo de trabajo utiliza las herramientas de aprendizaje automático que prefiera para crear modelos de datos personalizados que admitan los casos de uso de marketing con datos de Experience Platform.

Este flujo de trabajo requiere el uso de [!DNL Python] blocs de notas en los entornos de aprendizaje automático. Las instrucciones para comenzar a usar estos [!DNL Python] blocs de notas se incluyen en sus respectivos archivos léame.

Antes de continuar con esta guía, siga los pasos descritos en la [descripción general de las canalizaciones de características AI/ML](./overview.md) para habilitar el uso de los blocs de notas de Python de muestra utilizados en este caso de uso de canalización de características AI/ML.

## Notebooks de entorno de aprendizaje de máquinas en la nube {#cmle-notebooks}

El flujo de trabajo de extremo a extremo se puede dividir en tres fases amplias en función de los servicios utilizados para implementar el flujo de trabajo.

- La exploración y preparación iniciales de los datos de Experience Platform se basan en los servicios de Experience Platform.
- La formación y puntuación de modelos aprovecha las herramientas de en su entorno XML basado en la nube. Las opciones comunes para las plataformas ML incluyen: Databricks ML, AWS Sagemaker, DataRobot, etc.
- Volver a ingerir puntuaciones en Experience Platform y cualquier creación y activación de audiencia basada en código en función de esas puntuaciones dependería de nuevo de los servicios de Experience Platform.

Sin embargo, todas estas fases se pueden ejecutar en uno o más blocs de notas desde el entorno de ML sin que el usuario tenga que cambiar de contexto entre Experience Platform y sus herramientas de ML basadas en la nube.

Los pasos típicos de este flujo de extremo a extremo se han dividido en un conjunto de portátiles modulares que, juntos, muestran los pasos involucrados en el proyecto típico de aprendizaje automático que implica datos de Experience Platform. Esto facilita el uso de los portátiles como referencia para implementar actividades específicas y seleccionar y adaptar el código de los portátiles relevantes para implementar un caso de uso en el mundo real. En la práctica, un científico de datos puede preparar un solo bloc de notas que implemente la canalización de extremo a extremo para su proyecto XML. Alternativamente, un científico de datos puede simplemente adaptar el código de muestra para consultar los datos de Experience Platform y ponerlos a disposición en su entorno XML antes de continuar el proyecto y utilizar las funciones basadas en la IU en su plataforma XML.

A continuación se describen brevemente los blocs de notas de muestra incluidos en el repositorio vinculado. La documentación detallada de cada bloc de notas se intercala con el código de los propios blocs.

<!-- Below is the meat - the how to (but without links or details) -->

### Generar datos sintéticos {#generate-synthetic-data}

Este bloc de notas proporciona código para generar conjuntos de datos de perfiles sintéticos y eventos de experiencia en su Experience Platform que se utilizarán para ilustrar el flujo de trabajo de CMLE.

### EDA y funcionalidad con el servicio de consultas {#eda-and-featurization-with-query-service}

Este bloc de notas incluye ejemplos de análisis exploratorio en conjuntos de datos de Experience Platform mediante consultas interactivas a través del servicio de consultas de Experience Platform. A continuación se muestran ejemplos de consultas de características para crear un conjunto de datos de formación para el modelo de tendencia de ejemplo.

### Exportar datos de formación {#export-training-data}

Este bloc de notas ilustra la exportación del conjunto de datos de formación al almacenamiento en la nube que pueden leer las herramientas XML.

### Formación de un modelo de tendencia {#train-a-propensity-model}

Este bloc de notas ilustra la formación de un modelo de tendencia. Supone que Databricks ML es su entorno XML, pero está escrito genéricamente (es decir, sin el uso intensivo de funciones/API específicas de Databricks) para que se pueda adaptar a otras plataformas.

### Puntuación del modelo de tendencia

Este bloc de notas ilustra la puntuación del modelo de tendencia entrenado para producir un conjunto de datos de puntuaciones de tendencia para cada perfil de cliente de Experience Platform.

### Ingesta de puntuaciones en AEP

Este breve bloc de notas ilustra la ingesta del conjunto de datos de puntuaciones de tendencia para enriquecer los perfiles de los clientes en AEP.

### Crear y activar audiencias a partir de código

Este bloc de notas ilustra cómo el usuario puede crear audiencias a partir de las puntuaciones y activarlas a través de aplicaciones de Experience Platform desde su código de bloc de notas.
