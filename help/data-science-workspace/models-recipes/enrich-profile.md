---
keywords: Experience Platform;modelo de aprendizaje automático;Área de trabajo de ciencia de datos;Perfil del cliente en tiempo real;temas populares;perspectivas de aprendizaje automático
solution: Experience Platform
title: Enriquecer el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático
topic: tutorial
type: Tutorial
description: Este documento proporciona una guía sobre cómo enriquecer el Perfil del cliente en tiempo real con perspectivas aprendidas por el equipo.
translation-type: tm+mt
source-git-commit: 62e6bb7e72637b06808ff87dc21f40af2c4e2d45
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Enriquecer [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones y perspectivas de datos. Cuando las perspectivas de aprendizaje automático se ingieren en un conjunto de datos habilitado para [!DNL Profile], esos mismos datos también se ingieren como [!DNL Profile] registros que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service]. A medida que se ingieren datos de series temporales y de perfiles, el Perfil del cliente en tiempo real decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo denominado segmentación por flujo, antes de combinarlos con datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos instantáneamente y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca.

Este documento proporciona vínculos a tutoriales que le permiten enriquecer [!DNL Real-time Customer Profile] con sus perspectivas aprendidas por el equipo.

## Primeros pasos

Para completar los tutoriales a continuación, es necesario que tenga conocimientos prácticos sobre la ingesta de [!DNL Profile] datos y la creación de segmentos. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md):: Proporciona una representación completa y unificada de cada cliente individual basada en datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md):: Permite  [!DNL Real-time Customer Profile] el enlace de identidades de orígenes de datos dispares que se están ingeriendo en la plataforma.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):: El marco estandarizado por el cual Platform organiza los datos de experiencia del cliente.

Además de los documentos mencionados, se recomienda revisar también las siguientes guías sobre esquemas y el Editor de Esquemas:

- [Conceptos básicos de la composición](../../xdm/schema/composition.md) de esquemas: Describe los esquemas XDM, los componentes básicos, los principios y las prácticas recomendadas para la composición de esquemas que se van a utilizar en  [!DNL Experience Platform].
- [Tutorial](../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Proporciona instrucciones detalladas para crear esquemas con el Editor de Esquemas en  [!DNL Experience Platform].

## Crear y configurar un esquema de salida y un conjunto de datos {#create-an-output-schema-and-dataset}

El primer paso para enriquecer [!DNL Real-time Customer Profile] con perspectivas de puntuación es saber qué objeto real (como una persona) define sus datos. Conocer los datos le permite describir y diseñar una estructura para agregar significado, al igual que diseñar una base de datos relacional.

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Para crear sus propios esquemas con inicio, siga los pasos del tutorial sobre [creación de un esquema con el Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md). Tenga en cuenta que antes de habilitar un conjunto de datos para [!DNL Profile], debe configurar el esquema del conjunto de datos para que tenga un campo de identidad principal y luego habilitar el esquema para [!DNL Profile]. Cuando los datos se ingieren en un conjunto de datos habilitado para [!DNL Profile], esos mismos datos también se ingieren como [!DNL Profile] registros.

Si prefiere componer un esquema con la API [!DNL Schema Registry] en su lugar, lea la [[!DNL Schema Registry] guía para desarrolladores](../../xdm/api/getting-started.md) antes de intentar el tutorial sobre [la creación de un esquema con la API](../../xdm/tutorials/create-schema-api.md).

Una vez que el esquema y el conjunto de datos estén preparados, puede generar e ingestar datos de puntuación al conjunto de datos realizando ejecuciones de puntuación utilizando un modelo adecuado.

## Crear segmentos usando el [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Después de haber generado e ingerido las perspectivas de datos de puntuación en el conjunto de datos habilitado para [!DNL Profile], puede crear segmentos dinámicos mediante [!DNL Segment Builder].

El [!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar propiedades de datos. Siga la [[!DNL Segment Builder] guía del usuario](../../segmentation/ui/segment-builder.md) para obtener información sobre:

- Creación de definiciones de segmentos mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Uso del lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Ver estimaciones de su audiencia potencial, permitiéndole ajustar las definiciones de segmentos según sea necesario.
- Habilitar todas las definiciones de segmentos para la segmentación programada.
- Activación de definiciones de segmentos especificadas para la segmentación de flujo continuo.

## Pasos siguientes {#next-steps}

Para obtener más información sobre los segmentos y el [!DNL Segment Builder], lea la [información general del servicio de segmentación](../../segmentation/home.md).

Para obtener más información sobre [!DNL Real-time Customer Profile], lea la [información general del Perfil del cliente en tiempo real](../../profile/home.md)