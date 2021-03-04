---
keywords: Experience Platform;inicio;temas populares;Perfil del cliente en tiempo real;Servicio de identidad;
solution: Experience Platform
title: Tutoriales del perfil del cliente en tiempo real
topic: tutorial
type: Tutorial
description: Este documento describe los pasos involucrados y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---


# Configurar [!DNL Real-time Customer Profile]

Para configurar [!DNL Real-time Customer Profile] para su organización, debe completar varios flujos de trabajo independientes. Este documento describe los pasos involucrados y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.

Para obtener más información sobre [!DNL Real-time Customer Profile], comience por leer [Información general del perfil](../profile/home.md).

## Información general sobre la interfaz de usuario del perfil del cliente en tiempo real

El perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros.

**Esta guía le ayudará a:**
- Comprenda la interfaz de usuario de [!UICONTROL Profiles] y las funciones disponibles.
- Vea y administre sus datos de perfil.

Para obtener más información, visite la [Guía del usuario del perfil del cliente en tiempo real](../profile/ui/user-guide.md)

## API de perfil de cliente en tiempo real

La API de perfil de cliente en tiempo real incluye varios extremos. Lea [Información general de la API del perfil del cliente en tiempo real](../profile/api/overview.md) para obtener más información sobre cada uno de los extremos disponibles y sus casos de uso.

Para obtener más información y obtener los valores necesarios para realizar operaciones de CRUD con la API del perfil del cliente en tiempo real, visite la [guía de introducción](../profile/api/getting-started.md).

## Habilitar un esquema para el servicio [!DNL Profile] y [!DNL Identity]

Antes de poder ingerir datos en Adobe Experience Platform y utilizarlos en la creación de [!DNL Real-time Customer Profiles], se debe crear un esquema para proporcionar la estructura de los datos que se incorporarán y ese esquema debe habilitarse para utilizarse en [!DNL Profile] y Adobe Experience Platform [!DNL Identity Service].

**Esta guía le ayudará a:**
- Examine los esquemas existentes.
- Cree y asigne un nombre a un esquema.
- Añada y defina mezclas XDM.
- Defina los campos de esquema como campos de identidad.
- Habilite Perfil para el esquema.

Para obtener instrucciones paso a paso sobre la creación de un esquema habilitado para [!DNL Profile] y [!DNL Identity Service], consulte los tutoriales para [crear un esquema con la API del Registro de esquemas](../xdm/tutorials/create-schema-api.md) o [crear un esquema con la IU del Generador de esquemas](../xdm/tutorials/create-schema-ui.md).

## Configurar un conjunto de datos para [!DNL Profile] y [!DNL Identity]

Para empezar a ingerir datos en [!DNL Profile], debe tener un conjunto de datos que se haya configurado correctamente para su uso con [!DNL Real-time Customer Profile] y [!DNL Identity Service].

**Esta guía le ayudará a:**
- Cree un conjunto de datos habilitado para Perfil.
- Configure conjuntos de datos existentes.
- Ingeste datos en el conjunto de datos.
- Confirme que el conjunto de datos tiene habilitado Perfil y utiliza el servicio de identidad.

Para empezar, siga el tutorial de API para [configurar un conjunto de datos para Perfil e identidad](../profile/tutorials/dataset-configuration.md).

## Configuración de directivas de combinación

Adobe Experience Platform le permite agrupar los datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

**Esta guía le ayudará a:**
- Cree nuevas directivas de combinación.
- Administre las directivas de combinación existentes.
- Establezca una directiva de combinación predeterminada para su organización.
- Comprender las violaciones de políticas de combinación.

Para trabajar con políticas de combinación en la interfaz de usuario [!DNL Platform], visite la [guía del usuario de directivas de combinación](../profile/ui/merge-policies.md). Para trabajar con políticas de combinación usando la API de perfil de cliente en tiempo real, consulte la [guía para desarrolladores de políticas de combinación](../profile/api/merge-policies.md).

## Configurar proyecciones de borde

Para ofrecer experiencias coordinadas, coherentes y personalizadas a sus clientes en varios canales en tiempo real, es necesario disponer fácilmente de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. Adobe [!DNL Experience Platform] permite este acceso en tiempo real a los datos mediante lo que se conoce como perímetros. Un Edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que se pondrá a disposición en el borde.

**Esta guía le ayudará a:**
- Enumerar, crear, ver, actualizar y eliminar un destino de proyección de borde.
- Enumere y cree una configuración de proyección de borde.
- Comprenda los selectores.

Para obtener más información y empezar a trabajar con los bordes, consulte la [!DNL Real-time Customer Profile] API [subguía sobre proyecciones de aristas](../profile/api/edge-projections.md).

## Personalice cómo se muestran los datos de perfil en la interfaz de usuario

En la interfaz de usuario de Experience Platform, puede ver e interactuar con los datos del perfil del cliente en tiempo real en forma de perfiles de cliente. La información de perfil mostrada en la interfaz de usuario se ha combinado desde varios fragmentos de perfil para formar una sola vista de cada cliente individual. Esto incluye detalles como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados que se muestran en los perfiles también se pueden cambiar en el nivel de organización para mostrar los atributos de perfil preferidos.

**Esta guía le ayudará a:**
- Reordenar, cambiar el tamaño, editar y eliminar tarjetas.
- Agregue atributos.
- Agregue una tarjeta nueva.
- Restaurar valores predeterminados.

Para obtener más información sobre la personalización de datos de perfil, visite [Profile customization documentation](../profile/ui/profile-customization.md)

## Pasos siguientes

Una vez que haya configurado [!DNL Real-time Customer Profile] para su organización, puede empezar a agregar datos a perfiles de cliente individuales y a crear segmentos de audiencia basados en atributos de cliente específicos. Para empezar, consulte los siguientes tutoriales:

- [Añadir datos al perfil del cliente en tiempo real](../profile/tutorials/add-profile-data.md)
- [Creación de segmentos](../segmentation/tutorials/create-a-segment.md)