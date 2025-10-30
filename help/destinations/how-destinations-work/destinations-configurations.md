---
title: Configuración de exportación configurable y común en destinos
description: Descubra qué configuración de exportación de destinos se puede configurar en un nivel de destino y cuáles son fijos y no se pueden editar.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Configuración de exportación configurable y común en destinos

Cuando piense en el comportamiento de exportación a destinos de Experience Platform, debe tener en cuenta tres niveles independientes en los que actúan las configuraciones.

* En un primer nivel, algunas de las opciones relacionadas con el comportamiento de exportación de perfiles y los ajustes de configuración son comunes en todos los destinos que pertenecen a un tipo de destino. Esta configuración se refiere a los déclencheur que exporta un destino y a los que se incluye en una exportación, y los desarrolladores de destinos o los usuarios de Real-Time CDP no pueden editarlos.
* En un segundo nivel, el desarrollador de destinos puede personalizar algunos ajustes en un nivel de destino al crear destinos mediante Destination SDK.
* En un tercer nivel, hay opciones de configuración que los usuarios de Real-Time CDP pueden establecer en los flujos de trabajo de activación.

![Diagrama que muestra la interacción entre las opciones de exportación comunes y configurables para los destinos](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Esta página describe o vincula todos los ajustes de exportación comunes y configurables para destinos en los tres niveles descritos anteriormente.

## Configuración común de exportación entre tipos de destino {#common-settings-across-destination-types}

El comportamiento de exportación de destino es consistente entre destinos que pertenecen a un tipo de destino con respecto a *qué déclencheur se exportan* y *qué se incluye en las exportaciones de destino*. Las exportaciones de destino se activan mediante notificaciones que el servicio de destinos recibe del [servicio de perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=es#adobe-experience-platform-%26-applications-detailed-architecture-diagram) del flujo ascendente.

Lo que se incluye en las exportaciones de destino varía ligeramente entre los tipos de destino. Obtenga más información sobre [patrones de comportamiento de exportación comunes por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md). Los desarrolladores de destino o los usuarios de Real-Time CDP no pueden editar esta configuración.

## Configuración de exportación personalizable por los desarrolladores de destino {#customizable-settings-by-destination-developers}

Los desarrolladores de destinos pueden usar [Destination SDK](/help/destinations/destination-sdk/overview.md) para crear destinos personalizados o producidos (privados o públicos). Destination SDK proporciona a los desarrolladores gran flexibilidad para configurar destinos en función de las capacidades de flujo descendente de sus puntos finales de API y sistemas de recepción de archivos. En función de las funciones descendentes, los desarrolladores de destinos tienen disponibles las siguientes opciones de configuración al configurar un destino con Destination SDK:

* Determine qué atributos e identidades se pueden exportar desde Experience Platform al destino. Determine también qué identidades son necesarias en sus destinos para que la exportación de datos se realice correctamente.
* Establezca una directiva de agregación, que determina cuánto tiempo debe esperar Experience Platform al agregar mensajes HTTP para enviarlos a integraciones de API. Los desarrolladores de destinos pueden configurar diferentes tipos de agregación para determinar cuántos perfiles deben incluirse en los mensajes HTTP salientes y cuánto tiempo debe esperar Experience Platform hasta que se envíe el mensaje HTTP. Encuentre información detallada acerca de las [opciones de configuración de directivas de agregación](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) disponibles para los desarrolladores de destino en la documentación de Destination SDK.
* Determine si las exportaciones de mensajes HTTP deben incluir perfiles que cumplan los requisitos para los segmentos, que se eliminen de los segmentos o ambos.
* Determine qué configuraciones de nombre de archivo y formato de archivo deben estar disponibles para los usuarios al exportar archivos.

## Configuración en un nivel de flujo de datos personalizable por los usuarios {#settings-on-dataflow-level}

Además de la configuración no editable que depende del tipo de destino y la configuración configurada por el desarrollador de destino, hay ciertas opciones de exportación que los usuarios pueden configurar en el flujo de trabajo de activación. Esta configuración está relacionada con la programación de exportación de un flujo de datos determinado a un destino, los atributos y campos de identidad que deben exportarse en un flujo de datos o las opciones de formato de archivo para los archivos exportados.

La configuración disponible para los usuarios al conectarse a un destino depende de cómo haya configurado el destino el desarrollador de destinos y de qué configuración hayan puesto a disposición de los usuarios.

Por ejemplo, para [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations), un desarrollador de destino puede configurar qué identidades acepta su destino y solo esas identidades se mostrarán al usuario en el paso [asignación del flujo de trabajo de activación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), como se muestra a continuación:

![Grabación de pantalla de la selección de identidad para el campo de destino en el paso de asignación del flujo de trabajo de activación.](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Del mismo modo, para [destinos basados en archivos](/help/destinations/destination-types.md#file-based), el desarrollador de destinos puede determinar qué [opciones de adición de nombres de archivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) desea que estén disponibles para su destino, o qué [opciones de formato de archivo](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) desea que estén disponibles, y el usuario solo podrá seleccionar entre estas opciones, como se muestra a continuación:

![Grabación de pantalla de la opción de formato de archivo al conectarse a un destino basado en archivos.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Grabación de pantalla de la opción de adición de nombre de archivo en el paso de programación del flujo de trabajo de activación.](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Obtenga más información acerca de las diferentes opciones y pasos disponibles en el flujo de trabajo de activación:

* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Activar datos de audiencia en destinos empresariales](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de audiencia de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportar archivos bajo demanda a destinos por lotes](/help/destinations/ui/export-file-now.md)
* [Exportar conjuntos de datos a destinos de almacenamiento en la nube](/help/destinations/ui/export-datasets.md)

## Próximos pasos {#next-steps}

Después de leer este documento, ahora sabe qué configuración de exportación para destinos es común en todos los tipos de destino, qué configuración de destino individual pueden configurar los desarrolladores y qué configuración pueden editar los usuarios en el flujo de trabajo de activación.

A continuación, puede leer información más detallada sobre los [patrones de comportamiento de exportación comunes por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md).

Para los desarrolladores de destino, [puedes empezar](/help/destinations/destination-sdk/getting-started.md) con Destination SDK. Para los usuarios que buscan activar los datos, puede desproteger todos los destinos disponibles en el [catálogo](/help/destinations/catalog/overview.md).
