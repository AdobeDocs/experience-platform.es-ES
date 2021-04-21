---
keywords: Experience Platform;modelo de aprendizaje automático;Data Science Workspace;Perfil del cliente en tiempo real;temas populares;perspectivas de aprendizaje automático
solution: Experience Platform
title: Enriquecimiento del perfil del cliente en tiempo real con perspectivas de aprendizaje automático
topic-legacy: tutorial
type: Tutorial
description: Este documento proporciona una guía sobre cómo enriquecer el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Enriquezca [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático para generar predicciones de datos e información. Cuando se incorporan perspectivas de aprendizaje automático en un conjunto de datos habilitado para [!DNL Profile] , esos mismos datos también se incorporan como registros [!DNL Profile] que luego se pueden segmentar mediante [!DNL Adobe Experience Platform Segmentation Service]. A medida que se incorporan los datos de perfil y series temporales, el perfil del cliente en tiempo real decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo denominado segmentación de flujo continuo, antes de combinarlos con los datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos instantáneamente y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca.

Este documento proporciona vínculos a tutoriales que permiten enriquecer [!DNL Real-time Customer Profile] con las perspectivas de aprendizaje automático.

## Primeros pasos

Para completar los tutoriales siguientes, debe tener una comprensión práctica de la ingesta de datos [!DNL Profile] y la creación de segmentos. Antes de comenzar este tutorial, consulte la documentación de los siguientes servicios:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Proporciona una representación unificada completa de cada cliente individual basada en datos agregados de varias fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita  [!DNL Real-time Customer Profile] mediante el puente de identidades de fuentes de datos dispares que se están incorporando en Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente.

Además de los documentos mencionados anteriormente, se recomienda revisar también las siguientes guías sobre esquemas y el Editor de esquemas:

- [Aspectos básicos de la composición](../../xdm/schema/composition.md) del esquema: Describe esquemas XDM, componentes básicos, principios y prácticas recomendadas para componer esquemas que se van a utilizar en  [!DNL Experience Platform].
- [Tutorial del Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Proporciona instrucciones detalladas para crear esquemas con el Editor de esquemas en  [!DNL Experience Platform].

## Crear y configurar un esquema de salida y un conjunto de datos {#create-an-output-schema-and-dataset}

El primer paso para enriquecer [!DNL Real-time Customer Profile] con perspectivas de puntuación es saber qué objeto del mundo real (como una persona) definen los datos. Conocer los datos le permite describir y diseñar una estructura que añada significado, como diseñar una base de datos relacional.

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrá el esquema (registro o serie temporal). Para empezar a crear sus propios esquemas, siga los pasos del tutorial sobre la [creación de un esquema con el Editor de esquemas](../../xdm/tutorials/create-schema-ui.md). Tenga en cuenta que antes de habilitar un conjunto de datos para [!DNL Profile], debe configurar el esquema del conjunto de datos para que tenga un campo de identidad principal y luego habilitar el esquema para [!DNL Profile]. Cuando los datos se incorporan en un conjunto de datos habilitado para [!DNL Profile], esos mismos datos también se incorporan como registros [!DNL Profile].

Si prefiere componer un esquema utilizando la API [!DNL Schema Registry] en su lugar, comience leyendo la [[!DNL Schema Registry] guía para desarrolladores](../../xdm/api/getting-started.md) antes de intentar el tutorial sobre la [creación de un esquema con la API](../../xdm/tutorials/create-schema-api.md).

Una vez preparados el esquema y el conjunto de datos, puede generar e incorporar datos de puntuación al conjunto de datos realizando ejecuciones de puntuación utilizando un modelo apropiado.

## Crear segmentos utilizando [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Una vez que haya generado e introducido las perspectivas de datos de puntuación en el conjunto de datos habilitado para [!DNL Profile], puede crear segmentos dinámicos utilizando [!DNL Segment Builder].

El [!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos. Siga la [[!DNL Segment Builder] guía del usuario](../../segmentation/ui/segment-builder.md) para obtener más información:

- Creación de definiciones de segmentos mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Uso del lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Ver las estimaciones de la audiencia potencial, lo que le permite ajustar las definiciones de segmentos según sea necesario.
- Habilitación de todas las definiciones de segmentos para la segmentación programada.
- Habilitación de definiciones de segmento especificadas para la segmentación de flujo continuo.

## Pasos siguientes {#next-steps}

Para obtener más información sobre los segmentos y el [!DNL Segment Builder], lea la [información general del Servicio de segmentación](../../segmentation/home.md).

Para obtener más información sobre [!DNL Real-time Customer Profile], lea la [Descripción general del perfil del cliente en tiempo real](../../profile/home.md)
