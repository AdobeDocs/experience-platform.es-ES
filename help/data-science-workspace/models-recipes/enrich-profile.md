---
keywords: Experience Platform;modelo de aprendizaje automático;Data Science Workspace;Perfil del cliente en tiempo real;temas populares;perspectivas de aprendizaje automático
solution: Experience Platform
title: Enriquezca el perfil del cliente en tiempo real con perspectivas de aprendizaje automático
type: Tutorial
description: Este documento proporciona una guía sobre cómo enriquecer el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Enriquecer [!DNL Real-Time Customer Profile] con perspectivas de aprendizaje automático

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones y perspectivas de datos. Cuando se ingieren perspectivas de aprendizaje automático en una [!DNL Profile]Conjunto de datos habilitado para, esos mismos datos también se incorporan como [!DNL Profile] registros que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service].

Este documento proporciona vínculos a tutoriales que le permiten enriquecer [!DNL Real-Time Customer Profile] con sus perspectivas de aprendizaje automático.

## Primeros pasos

Para completar los tutoriales siguientes, necesita tener una comprensión práctica de la ingesta [!DNL Profile] datos y creación de segmentos. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Proporciona una representación completa y unificada de cada cliente individual en función de los datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] uniendo identidades de diferentes fuentes de datos que se están introduciendo en Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

Además de los documentos mencionados anteriormente, es muy recomendable que también revise las siguientes guías sobre esquemas y el Editor de esquemas:

- [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Describe los esquemas XDM, los bloques de creación, los principios y las prácticas recomendadas para componer esquemas que se utilizarán en [!DNL Experience Platform].
- [Tutorial del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Proporciona instrucciones detalladas para crear esquemas utilizando el Editor de esquemas en [!DNL Experience Platform].

## Creación y configuración de un esquema y un conjunto de datos de salida {#create-an-output-schema-and-dataset}

El primer paso hacia el enriquecimiento [!DNL Real-Time Customer Profile] con perspectivas de puntuación es saber qué objeto del mundo real (como una persona) definen sus datos. Comprender los datos le permite describir y diseñar una estructura para agregar significado, como diseñar una base de datos relacional.

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Para empezar a crear sus propios esquemas, siga los pasos del tutorial sobre [creación de un esquema con el Editor de esquemas](../../xdm/tutorials/create-schema-ui.md). Tenga en cuenta que antes de poder habilitar un conjunto de datos para [!DNL Profile], debe configurar el esquema del conjunto de datos para que tenga un campo de identidad principal y, a continuación, habilitar el esquema para [!DNL Profile]. Cuando los datos se incorporan a un [!DNL Profile]Conjunto de datos habilitado para, esos mismos datos también se incorporan como [!DNL Profile] registros.

Si prefiere componer un esquema con la variable [!DNL Schema Registry] En su lugar, comience por leer la [[!DNL Schema Registry] guía para desarrolladores](../../xdm/api/getting-started.md) antes de intentar realizar el tutorial en [creación de un esquema con la API](../../xdm/tutorials/create-schema-api.md).

Una vez que el esquema y el conjunto de datos estén preparados, puede generar e introducir datos de puntuación en el conjunto de datos realizando ejecuciones de puntuación utilizando un modelo adecuado.

## Creación de segmentos con [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Después de generar e ingerir las perspectivas de datos de puntuación en su [!DNL Profile]Conjunto de datos habilitado para, puede crear segmentos dinámicos utilizando [!DNL Segment Builder].

El [!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos. Siga las [[!DNL Segment Builder] guía del usuario](../../segmentation/ui/segment-builder.md) para obtener más información sobre:

- Creación de definiciones de segmentos utilizando una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Uso del lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Visualizar estimaciones de su audiencia potencial, lo que le permite ajustar sus definiciones de segmentos según sea necesario.
- Habilitando todas las definiciones de segmentos para la segmentación programada.
- Habilitando definiciones de segmento especificadas para la segmentación de streaming.

## Pasos siguientes {#next-steps}

Para obtener más información sobre los segmentos y la [!DNL Segment Builder], lea la [Resumen del servicio de segmentación](../../segmentation/home.md).

Para obtener más información acerca de [!DNL Real-Time Customer Profile], lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md)
