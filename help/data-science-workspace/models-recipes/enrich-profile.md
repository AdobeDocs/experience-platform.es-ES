---
keywords: Experience Platform; modelo de aprendizaje automático; Data Science Espacio de trabajo; Perfil del cliente en tiempo real; temas populares; Perspectivas de aprendizaje automático
solution: Experience Platform
title: Enriquezca el perfil del cliente en tiempo real con Insights de aprendizaje automático
type: Tutorial
description: Este documento proporciona una guía sobre cómo enriquecer el perfil del cliente en tiempo real con información de aprendizaje automático.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Enriquezca [!DNL Real-Time Customer Profile] con información sobre el aprendizaje automático

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] proporciona las herramientas y los recursos para crear, evaluar y utilizar modelos de aprendizaje automático con el fin de generar predicciones y perspectivas de datos. Cuando se incorporan datos de aprendizaje automático en un conjunto de datos habilitado para [!DNL Profile], esos mismos datos también se incorporan como [!DNL Profile] registros que luego se pueden segmentar con [!DNL Adobe Experience Platform Segmentation Service].

El proceso de segmentación depende del método de evaluación de la audiencia. Si una audiencia está configurada como **streaming**, procesará todas las actualizaciones nuevas escritas por el modelo en el perfil en tiempo real. Sin embargo, si se configura una audiencia para la evaluación de **batch**, los nuevos valores se evaluarán en el siguiente lote.

Este documento proporciona vínculos a tutoriales que le permiten enriquecer [!DNL Real-Time Customer Profile] con sus perspectivas de aprendizaje automático.

## Introducción

Para completar los tutoriales siguientes, necesita tener conocimientos prácticos sobre la ingesta de datos de [!DNL Profile] y la creación de audiencias. Antes de comenzar este tutorial, revise la documentación de los siguientes servicios:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): proporciona una representación completa y unificada de cada cliente individual basada en datos agregados de múltiples fuentes.
- [[!DNL Identity Service]](../../identity-service/home.md): Permite [!DNL Real-Time Customer Profile] unir identidades de orígenes de datos dispares que se ingieren en Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): El marco de trabajo estandarizado según el cual Platform organiza experiencia del cliente datos.

Además de los documentos mencionados anteriormente, es muy recomendable que también revise las siguientes guías sobre esquemas y el Editor de esquemas:

- [Conceptos básicos de composición de esquemas](../../xdm/schema/composition.md): Describe esquemas XDM, componentes básicos, principios y prácticas recomendadas para componer esquemas que se utilizarán en [!DNL Experience Platform].
- [Tutorial del editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Proporciona instrucciones detalladas para crear esquemas utilizando el editor de esquemas en [!DNL Experience Platform].

## Creación y configuración de un esquema y un conjunto de datos de salida {#create-an-output-schema-and-dataset}

El primer paso para enriquecer a [!DNL Real-Time Customer Profile] con perspectivas de puntuación es saber qué objeto del mundo real (como una persona) definen sus datos. Comprender los datos le permite describir y diseñar una estructura para agregar significado, como diseñar una base de datos relacional.

La composición de un esquema comienza asignando una clase. Las clases definen los aspectos de comportamiento de los datos que contendrán los esquema (registro o series temporales). Para empezar a crear sus propios esquemas, siga los pasos del tutorial sobre [creación de un esquema con el Editor de esquemas](../../xdm/tutorials/create-schema-ui.md). Tenga en cuenta que antes de poder activar un conjunto de datos para [!DNL Profile], debe configurar el esquema del conjunto de datos para que tenga un campo de identidad principal y, a continuación, habilitar el esquema para [!DNL Profile]. Cuando los datos se ingieren en un [!DNL Profile]conjunto de datos habilitado, esos mismos datos también se ingieren como [!DNL Profile] registros.

Si prefiere redactar una esquema usando la [!DNL Schema Registry] API en su lugar, inicio leyendo el [[!DNL Schema Registry] guía](../../xdm/api/getting-started.md) para desarrolladores antes de intentar la tutorial para [crear una esquema con la API](../../xdm/tutorials/create-schema-api.md).

Una vez que su esquema y conjunto de datos estén preparados, puede generar e ingerir datos de puntuación al conjunto de datos realizando carreras de puntuación utilizando un modelo apropiado.

## Crear audiencias con [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Después de generar e ingerir sus datos de puntuación en el conjunto de datos habilitado para [!DNL Profile], puede crear audiencias dinámicas con [!DNL Segment Builder].

[!DNL Segment Builder] proporciona un área de trabajo enriquecida que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos. Siga la [[!DNL Segment Builder] guía del usuario](../../segmentation/ui/segment-builder.md) para obtener más información:

- Creación de definiciones de segmentos utilizando una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Uso del lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de audiencia.
- Visualizar estimaciones de su audiencia potencial, lo que le permite ajustar sus definiciones de segmentos según sea necesario.
- Habilitación de todas las definiciones de segmento para segmentación programados.
- Habilitación de definiciones de segmento especificadas para el flujo continuo de segmentación.

## Pasos siguientes {#next-steps}

Para obtener más información sobre las audiencias y el [!DNL Segment Builder], lea la información general](../../segmentation/home.md) del [servicio de segmentación.

Para obtener más información acerca de [!DNL Real-Time Customer Profile], lea la [Descripción general del perfil del cliente en tiempo real](../../profile/home.md)
