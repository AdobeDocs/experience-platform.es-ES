---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Tutoriales de Perfil para clientes en tiempo real
topic: tutorial
type: Tutorial
description: Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Configurar [!DNL Real-time Customer Profile] y [!DNL Identity Service]

Para configurar [!DNL Real-time Customer Profile] la organización, debe completar varios flujos de trabajo independientes. Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual. Para obtener más información sobre [!DNL Real-time Customer Profile], lea la descripción general [del](../profile/home.md)Perfil.

## Habilitar esquema para [!DNL Profile] y [!DNL Identity]

Antes de poder ingerir datos en Adobe Experience Platform y utilizarlos en la creación de datos [!DNL Real-time Customer Profiles], se debe crear un esquema que proporcione la estructura de los datos que se van a ingerir y que el esquema se debe habilitar para su uso en [!DNL Profile] y Adobe Experience Platform [!DNL Identity Service]. Para obtener instrucciones paso a paso sobre la creación de un esquema habilitado tanto para [!DNL Profile] como para [!DNL Identity Service], consulte los tutoriales para [crear un esquema con la API](../xdm/tutorials/create-schema-api.md) del Registro de Esquema o [crear un esquema con la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)de Esquema Builder.

## Configure un conjunto de datos para [!DNL Profile] y [!DNL Identity]

Para empezar a ingerir datos en [!DNL Profile], debe tener un conjunto de datos configurado correctamente para su uso con [!DNL Real-time Customer Profile] y [!DNL Identity Service]. Para empezar, siga el tutorial [](../profile/tutorials/dataset-configuration.md)Configurar un conjunto de datos para Perfil e identidad.

## Configurar directivas de combinación

Adobe Experience Platform le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para trabajar con políticas de combinación en la [!DNL Platform] interfaz de usuario, visite la guía [del usuario de directivas de](../profile/ui/merge-policies.md)combinación. Para trabajar con políticas de combinación mediante la API de Perfil del cliente en tiempo real, consulte la guía [para desarrolladores de políticas de](../profile/api/merge-policies.md)combinación.

## Configurar proyecciones de borde

Para ofrecer a sus clientes experiencias coordinadas, coherentes y personalizadas en varios canales en tiempo real, es necesario disponer de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. El Adobe [!DNL Experience Platform] permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como bordes. Un edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde. Para obtener más información y empezar a trabajar con los bordes, consulte la [!DNL Real-time Customer Profile] guía [auxiliar de API sobre proyecciones](../profile/api/edge-projections.md)de bordes.

## Pasos siguientes

Una vez configurada [!DNL Real-time Customer Profile] para su organización, puede empezar a agregar datos a perfiles de cliente individuales y a crear segmentos de audiencia basados en atributos de cliente específicos. Para empezar, consulte los siguientes tutoriales:

* [Añadir datos al Perfil del cliente en tiempo real](../profile/tutorials/add-profile-data.md)
* [Crear un segmento](../segmentation/tutorials/create-a-segment.md)