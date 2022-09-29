---
keywords: Experience Platform;modelo de aprendizaje automático;Data Science Workspace;Perfil del cliente en tiempo real;temas populares;perspectivas de aprendizaje automático
solution: Experience Platform
title: Enriquecimiento del perfil del cliente en tiempo real con perspectivas de aprendizaje automático
topic-legacy: tutorial
type: Tutorial
description: Este documento proporciona una guía sobre cómo enriquecer el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 89a9b64f2fb238c08a281f29a035ce0b24b34804
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Enriquecimiento [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones de datos y perspectivas. Cuando las perspectivas de aprendizaje automático se incorporan en un [!DNL Profile]conjunto de datos habilitado para , que los mismos datos también se introducen como [!DNL Profile] registros que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service].

Este documento proporciona vínculos a tutoriales que le permiten enriquecer [!DNL Real-time Customer Profile] con sus perspectivas de aprendizaje automático.

## Primeros pasos

Para completar los tutoriales siguientes, debe tener una comprensión práctica de la ingesta [!DNL Profile] datos y creación de segmentos. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona una representación unificada completa de cada cliente individual basada en datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilitación [!DNL Real-time Customer Profile] al unir identidades de fuentes de datos dispares que se están incorporando a Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

Además de los documentos mencionados anteriormente, se recomienda revisar también las siguientes guías sobre esquemas y el Editor de esquemas:

- [Aspectos básicos de la composición del esquema](../../xdm/schema/composition.md): Describe los esquemas XDM, componentes básicos, principios y prácticas recomendadas para componer esquemas que se van a utilizar en [!DNL Experience Platform].
- [Tutorial del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Proporciona instrucciones detalladas para crear esquemas con el Editor de esquemas en [!DNL Experience Platform].

## Crear y configurar un esquema de salida y un conjunto de datos {#create-an-output-schema-and-dataset}

El primer paso hacia el enriquecimiento [!DNL Real-time Customer Profile] con perspectivas de puntuación es saber qué objeto real (como una persona) definen los datos. Conocer los datos le permite describir y diseñar una estructura que añada significado, como diseñar una base de datos relacional.

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Para empezar a crear sus propios esquemas, siga los pasos del tutorial en [creación de un esquema con el Editor de esquemas](../../xdm/tutorials/create-schema-ui.md). Tenga en cuenta que, antes de habilitar un conjunto de datos para [!DNL Profile], debe configurar el esquema del conjunto de datos para que tenga un campo de identidad principal y, a continuación, habilitar el esquema para [!DNL Profile]. Cuando los datos se introducen en un [!DNL Profile]conjunto de datos habilitado para , que los mismos datos también se introducen como [!DNL Profile] registros.

Si prefiere componer un esquema utilizando la variable [!DNL Schema Registry] En su lugar, comience leyendo la [[!DNL Schema Registry] guía para desarrolladores](../../xdm/api/getting-started.md) antes de intentar el tutorial en [creación de un esquema con la API](../../xdm/tutorials/create-schema-api.md).

Una vez preparados el esquema y el conjunto de datos, puede generar e incorporar datos de puntuación al conjunto de datos realizando ejecuciones de puntuación utilizando un modelo apropiado.

## Cree segmentos usando la variable [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Una vez que haya generado e introducido las perspectivas de datos de puntuación en su [!DNL Profile]conjunto de datos habilitado para , puede crear segmentos dinámicos mediante el [!DNL Segment Builder].

La variable [!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos. Siga las [[!DNL Segment Builder] guía del usuario](../../segmentation/ui/segment-builder.md) para obtener más información sobre:

- Creación de definiciones de segmentos mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Uso del lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Ver las estimaciones de la audiencia potencial, lo que le permite ajustar las definiciones de segmentos según sea necesario.
- Habilitación de todas las definiciones de segmentos para la segmentación programada.
- Habilitación de definiciones de segmento especificadas para la segmentación de flujo continuo.

## Pasos siguientes {#next-steps}

Para obtener más información sobre los segmentos y el [!DNL Segment Builder], lea la [Información general del servicio de segmentación](../../segmentation/home.md).

Para obtener más información sobre [!DNL Real-time Customer Profile], lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md)
