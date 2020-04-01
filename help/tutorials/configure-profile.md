---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriales de Perfil para clientes en tiempo real
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Configurar el servicio de Perfil e identidad del cliente en tiempo real

Para configurar el Perfil del cliente en tiempo real para su organización, debe completar varios flujos de trabajo independientes. Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual. Para obtener más información sobre el Perfil del cliente en tiempo real, lea la descripción general [del](../profile/home.md)Perfil.

## Habilitar esquema para Perfil e identidad

Antes de poder ingerir datos en Adobe Experience Platform y utilizarlos en la creación de Perfiles de cliente en tiempo real, se debe crear un esquema que proporcione la estructura de los datos que se van a ingerir y que el esquema se debe habilitar para su uso en Perfil y Adobe Experience Platform Identity Service. Para obtener instrucciones paso a paso sobre la creación de un esquema habilitado para Perfil y servicio de identidad, consulte los tutoriales para [crear un esquema con la API](../xdm/tutorials/create-schema-api.md) del Registro de Esquema o [crear un esquema con la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)de Esquema Builder.

## Configurar un conjunto de datos para Perfil e identidad

Para empezar a ingerir datos en Perfil, debe disponer de un conjunto de datos configurado correctamente para su uso con el servicio de Perfil e identidad del cliente en tiempo real. Para empezar, siga el tutorial [](../profile/tutorials/dataset-configuration.md)Configurar un conjunto de datos para Perfil e identidad.

## Configurar directivas de combinación

Adobe Experience Platform le permite reunir datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que utiliza la Plataforma para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para trabajar con políticas de combinación en la interfaz de usuario de la plataforma, visite la guía [del usuario de directivas de](../profile/ui/merge-policies.md)combinación. Para trabajar con políticas de combinación mediante la API de Perfil del cliente en tiempo real, consulte la guía [para desarrolladores de políticas de](../profile/api/merge-policies.md)combinación.

## Configurar proyecciones de borde

Para ofrecer a sus clientes experiencias coordinadas, coherentes y personalizadas en varios canales en tiempo real, es necesario disponer de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. Adobe Experience Platform permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como bordes. Un edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde. Para obtener más información y empezar a trabajar con los bordes, consulte la [subguía de la API de Perfil del cliente en tiempo real sobre proyecciones](../profile/api/edge-projections.md)de bordes.

## Pasos siguientes

Una vez que haya configurado el Perfil del cliente en tiempo real para su organización, puede empezar a agregar datos a perfiles de clientes individuales y a crear segmentos de audiencia basados en atributos de cliente específicos. Para empezar, consulte los siguientes tutoriales:

* [Añadir datos al Perfil del cliente en tiempo real](../profile/tutorials/add-profile-data.md)
* [Crear un segmento](../segmentation/tutorials/create-a-segment.md)