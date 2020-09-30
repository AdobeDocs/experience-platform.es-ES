---
keywords: Experience Platform;home;popular topics;Real-time Customer Profile;Identity Service;
solution: Experience Platform
title: Tutoriales de Perfil para clientes en tiempo real
topic: tutorial
type: Tutorial
description: Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.
translation-type: tm+mt
source-git-commit: 844ef4a0131e41d3a7a3da319ccf7f8d5cf1f40d
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---


# Configurar [!DNL Real-time Customer Profile] y [!DNL Identity Service]

Para configurar [!DNL Real-time Customer Profile] la organización, debe completar varios flujos de trabajo independientes. Este documento describe los pasos necesarios y proporciona vínculos a tutoriales para completar cada flujo de trabajo individual.

Para obtener más información sobre [!DNL Real-time Customer Profile], lea la descripción general [del](../profile/home.md)Perfil.

## Información general sobre la interfaz de usuario de Perfil del cliente en tiempo real

El Perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros.

**Esta guía le ayudará a:**
- Conozca la interfaz de usuario de [!UICONTROL Perfiles] y las funciones disponibles.
- Vista y administración de los datos de Perfil.

Para obtener más información, visite la guía del usuario de Perfil del cliente en tiempo [real](../profile/ui/user-guide.md)

## API de Perfil del cliente en tiempo real

La API de Perfil del cliente en tiempo real incluye varios extremos. Perfil le permite consolidar datos de clientes dispares de varios canales, como datos en línea, sin conexión, CRM y de terceros, en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con el cliente. Lea la descripción general [de la API de Perfil del cliente en tiempo](../profile/api/overview.md) real para obtener más información sobre cada uno de los extremos disponibles y sus casos de uso.

**Están disponibles las siguientes guías para desarrolladores de API:**
- [Atributos calculados (alfa) ](../profile/api/computed-attributes.md) : Obtenga información sobre los casos de uso de atributos calculados, así como sobre cómo configurar, acceder, actualizar y eliminar un atributo calculado.
- [Proyecciones](../profile/api/edge-projections.md) avanzadas: Descubra cómo crear, vista, actualizar, eliminar y lista de destinos de proyección. Además, este documento contiene información sobre cómo enumerar y crear configuraciones de proyección y proporciona ejemplos para usar selectores.
- [Entidades (acceso a Perfiles)](../profile/api/entities.md) : Aprenda a acceder a los datos de perfil por identidad o lista de identidades. Además, aprenda a acceder a eventos de series temporales para varios perfiles mediante identidades, un único perfil por identidad y acceso a varias entidades de esquema.
- [Trabajos de exportación (exportación de Perfil)](../profile/api/export-jobs.md) : aprenda a crear, vista, supervisar y cancelar trabajos de exportación.
- [Políticas](../profile/api/merge-policies.md) de combinación: obtenga información sobre los componentes de las políticas de combinación, así como sobre cómo acceder, crear, actualizar y eliminar una política de combinación.
- [Estado de muestra de previsualización (previsualización de Perfil)](../profile/api/preview-sample-status.md) : aprenda a vista el estado de la última muestra, la distribución del perfil de lista por conjunto de datos y la distribución del perfil de lista por Área de nombres.
- [Trabajos del sistema de perfil (Eliminar solicitudes)](../profile/api/profile-system-jobs.md) : aprenda a vista, crear y eliminar una solicitud de eliminación de un conjunto de datos o lote en el almacén de Perfiles.

Para obtener más información y obtener los valores necesarios para realizar operaciones de CRUD con la API de Perfil del cliente en tiempo real, visite la guía de [introducción](../profile/api/getting-started.md).

## Habilitar un esquema para [!DNL Profile] y un [!DNL Identity] servicio

Antes de poder ingerir datos en Adobe Experience Platform y utilizarlos en la creación de datos [!DNL Real-time Customer Profiles], se debe crear un esquema que proporcione la estructura de los datos que se van a ingerir y que el esquema se debe habilitar para su uso en [!DNL Profile] y Adobe Experience Platform [!DNL Identity Service].

**Esta guía le ayudará a:**
- Examinar esquemas existentes.
- Cree y asigne un nombre a un esquema.
- Añada y defina mezclas XDM.
- Defina los campos de esquema como campos de identidad.
- Habilite el Perfil para su esquema.

Para obtener instrucciones paso a paso sobre la creación de un esquema habilitado tanto para [!DNL Profile] como para [!DNL Identity Service], consulte los tutoriales para [crear un esquema con la API](../xdm/tutorials/create-schema-api.md) del Registro de Esquema o [crear un esquema con la interfaz de usuario](../xdm/tutorials/create-schema-ui.md)de Esquema Builder.

## Configure un conjunto de datos para [!DNL Profile] y [!DNL Identity]

Para empezar a ingerir datos en [!DNL Profile], debe tener un conjunto de datos configurado correctamente para su uso con [!DNL Real-time Customer Profile] y [!DNL Identity Service].

**Esta guía le ayudará a:**
- Cree un conjunto de datos habilitado para Perfil.
- Configure los conjuntos de datos existentes.
- Ingresar datos en el conjunto de datos.
- Confirme que el conjunto de datos está habilitado para Perfil y que utiliza el servicio de identidad.

Para empezar, siga el tutorial de la API para [configurar un conjunto de datos para Perfil e identidad](../profile/tutorials/dataset-configuration.md).

## Configurar directivas de combinación

Adobe Experience Platform le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada.

**Esta guía le ayudará a:**
- Crear nuevas directivas de combinación.
- Administrar directivas de combinación existentes.
- Defina una directiva de combinación predeterminada para su organización.
- Comprenda las infracciones de directivas de combinación.

Para trabajar con políticas de combinación en la [!DNL Platform] interfaz de usuario, visite la guía [del usuario de directivas de](../profile/ui/merge-policies.md)combinación. Para trabajar con políticas de combinación mediante la API de Perfil del cliente en tiempo real, consulte la guía [para desarrolladores de políticas de](../profile/api/merge-policies.md)combinación.

## Configurar proyecciones de borde

Para ofrecer a sus clientes experiencias coordinadas, coherentes y personalizadas en varios canales en tiempo real, es necesario disponer de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. El Adobe [!DNL Experience Platform] permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como bordes. Un edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde.

**Esta guía le ayudará a:**
- Lista, creación, vista, actualización y eliminación de un destino de proyección de arista.
- Lista y creación de una configuración de proyección de arista.
- Comprenda los selectores.

Para obtener más información y empezar a trabajar con los bordes, consulte la [!DNL Real-time Customer Profile] guía [auxiliar de API sobre proyecciones](../profile/api/edge-projections.md)de bordes.

## Personalice cómo se muestran los datos de Perfil en la interfaz de usuario

En la interfaz de usuario de Experience Platform, puede realizar vistas e interactuar con los datos de Perfil de clientes en tiempo real en forma de perfiles de clientes. La información de perfil mostrada en la interfaz de usuario se ha combinado desde varios fragmentos de perfil para formar una sola vista de cada cliente individual. Esto incluye detalles como atributos básicos, identidades vinculadas y preferencias de canal. Los campos predeterminados que se muestran en los perfiles también se pueden cambiar en el nivel de organización para mostrar los atributos de Perfil preferidos.

**Esta guía le ayudará a:**
- Reordene, cambie el tamaño, edite y elimine tarjetas.
- Añadir atributos.
- Añada una tarjeta nueva.
- Restaurar valores predeterminados.

Para obtener más información sobre la personalización de datos de perfil, visite la documentación de personalización de [Perfil](../profile/ui/profile-customization.md)

## Pasos siguientes

Una vez configurada [!DNL Real-time Customer Profile] para su organización, puede empezar a agregar datos a perfiles de cliente individuales y a crear segmentos de audiencia basados en atributos de cliente específicos. Para empezar, consulte los siguientes tutoriales:

- [Añadir datos al Perfil del cliente en tiempo real](../profile/tutorials/add-profile-data.md)
- [Crear un segmento](../segmentation/tutorials/create-a-segment.md)