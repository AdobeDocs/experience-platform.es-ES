---
keywords: Experience Platform;inicio;temas populares;Perfil del cliente en tiempo real;servicio de identidad;
solution: Experience Platform
title: Tutoriales de Perfil para clientes en tiempo real
topic: tutorial
type: Tutorial
description: Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.
translation-type: tm+mt
source-git-commit: 0aa59a5375757f81d63ac43d778ff2c7179d449b
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# Configurar [!DNL Real-time Customer Profile]

Para configurar [!DNL Real-time Customer Profile] para su organización, debe completar varios flujos de trabajo independientes. Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.

Para obtener más información sobre [!DNL Real-time Customer Profile], empiece por leer la [información general del Perfil](../profile/home.md).

## Información general sobre la interfaz de usuario de Perfil del cliente en tiempo real

El Perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros.

**Esta guía le ayudará a:**
- Conozca la interfaz de usuario de [!UICONTROL Perfiles] y las funciones disponibles.
- Vista y administración de los datos de Perfil.

Para obtener más información, visite la [guía del usuario de Perfil del cliente en tiempo real](../profile/ui/user-guide.md)

## API de Perfil del cliente en tiempo real

La API de Perfil del cliente en tiempo real incluye varios extremos. Lea la [información general de la API de Perfil del cliente en tiempo real](../profile/api/overview.md) para obtener más información sobre cada uno de los extremos disponibles y sus casos de uso.

Para obtener más información y obtener los valores necesarios para realizar operaciones de CRUD con la API de Perfil del cliente en tiempo real, visite la [guía de introducción](../profile/api/getting-started.md).

## Habilitar un esquema para el servicio [!DNL Profile] y [!DNL Identity]

Antes de poder ingerir datos en Adobe Experience Platform y utilizarlos para crear [!DNL Real-time Customer Profiles], se debe crear un esquema que proporcione la estructura de los datos que se van a ingerir y ese esquema debe habilitarse para utilizarse en [!DNL Profile] y Adobe Experience Platform [!DNL Identity Service].

**Esta guía le ayudará a:**
- Examinar esquemas existentes.
- Cree y asigne un nombre a un esquema.
- Añada y defina mezclas XDM.
- Defina los campos de esquema como campos de identidad.
- Habilite el Perfil para su esquema.

Para obtener instrucciones paso a paso sobre la creación de un esquema habilitado para [!DNL Profile] y [!DNL Identity Service], consulte los tutoriales para [crear un esquema mediante la API del Registro de Esquema](../xdm/tutorials/create-schema-api.md) o [crear un esquema mediante la interfaz de usuario de Esquema Builder](../xdm/tutorials/create-schema-ui.md).

## Configurar un conjunto de datos para [!DNL Profile] y [!DNL Identity]

Para empezar a ingerir datos en [!DNL Profile], debe tener un conjunto de datos configurado correctamente para su uso con [!DNL Real-time Customer Profile] y [!DNL Identity Service].

**Esta guía le ayudará a:**
- Cree un conjunto de datos habilitado para Perfil.
- Configure los conjuntos de datos existentes.
- Ingresar datos en el conjunto de datos.
- Confirme que el conjunto de datos está habilitado para Perfil y que utiliza el servicio de identidad.

Para empezar, siga el tutorial de API para [configurar un conjunto de datos para Perfil e identidad](../profile/tutorials/dataset-configuration.md).

## Configurar directivas de combinación

Adobe Experience Platform le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

**Esta guía le ayudará a:**
- Crear nuevas directivas de combinación.
- Administrar directivas de combinación existentes.
- Defina una directiva de combinación predeterminada para su organización.
- Comprenda las infracciones de directivas de combinación.

Para trabajar con directivas de combinación en la [!DNL Platform] interfaz de usuario, visite la [guía del usuario de directivas de combinación](../profile/ui/merge-policies.md). Para trabajar con políticas de combinación mediante la API de Perfil del cliente en tiempo real, consulte la [guía para desarrolladores de políticas de combinación](../profile/api/merge-policies.md).

## Configurar proyecciones de borde

Para ofrecer a sus clientes experiencias coordinadas, coherentes y personalizadas en varios canales en tiempo real, es necesario disponer de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. El Adobe [!DNL Experience Platform] permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como bordes. Un edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde.

**Esta guía le ayudará a:**
- Lista, creación, vista, actualización y eliminación de un destino de proyección de arista.
- Lista y creación de una configuración de proyección de arista.
- Comprenda los selectores.

Para obtener más información y empezar a trabajar con los bordes, consulte la [!DNL Real-time Customer Profile] API [subguía de proyecciones de aristas](../profile/api/edge-projections.md).

## Personalice cómo se muestran los datos de Perfil en la interfaz de usuario

En la interfaz de usuario de Experience Platform, puede realizar vistas e interactuar con los datos de Perfil de clientes en tiempo real en forma de perfiles de clientes. La información de perfil mostrada en la interfaz de usuario se ha combinado desde varios fragmentos de perfil para formar una sola vista de cada cliente individual. Esto incluye detalles como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados que se muestran en los perfiles también se pueden cambiar en el nivel de organización para mostrar los atributos de Perfil preferidos.

**Esta guía le ayudará a:**
- Reordene, cambie el tamaño, edite y elimine tarjetas.
- Añadir atributos.
- Añada una tarjeta nueva.
- Restaurar valores predeterminados.

Para obtener más información sobre la personalización de datos de perfil, visite la [documentación de personalización de Perfil](../profile/ui/profile-customization.md)

## Pasos siguientes

Una vez configurada [!DNL Real-time Customer Profile] para su organización, puede empezar a agregar datos a perfiles de clientes individuales y a crear segmentos de audiencia basados en atributos de cliente específicos. Para empezar, consulte los siguientes tutoriales:

- [Añadir datos al Perfil del cliente en tiempo real](../profile/tutorials/add-profile-data.md)
- [Crear un segmento](../segmentation/tutorials/create-a-segment.md)