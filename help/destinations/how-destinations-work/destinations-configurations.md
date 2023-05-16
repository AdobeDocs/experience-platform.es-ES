---
title: Configuración de exportación configurable y común en destinos
description: Aprenda qué configuración de exportación en los destinos se puede configurar en un nivel de destino y cuáles son fijas y no se pueden editar.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: a0400ab255b3b6a7edb4dcfd5c33a0f9e18b5157
workflow-type: tm+mt
source-wordcount: '845'
ht-degree: 0%

---

# Configuración de exportación configurable y común en destinos

Cuando tenga en cuenta el comportamiento de exportación a los destinos de Experience Platform, debe tener en cuenta tres niveles independientes en los que actúan las configuraciones.

* En el primer nivel, algunos de los ajustes relacionados con el comportamiento de exportación de perfiles y los ajustes de configuración son comunes en todos los destinos pertenecientes a un tipo de destino. Estos ajustes hacen referencia a los déclencheur de una exportación de destino y a lo que se incluye en una exportación, y no pueden editarlos los desarrolladores de destino ni los usuarios de CDP en tiempo real.
* En un segundo nivel, el desarrollador de destino puede personalizar algunos ajustes en un nivel de destino al crear destinos con Destination SDK.
* En un tercer nivel, hay opciones de configuración que los usuarios de CDP en tiempo real pueden establecer en los flujos de trabajo de activación.

![Diagrama que muestra la interacción entre la configuración de exportación común y configurable para los destinos](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Esta página describe o vincula a todos los ajustes de exportación comunes y configurables para destinos, en los tres niveles descritos anteriormente.

## Configuración común de exportación en tipos de destino {#common-settings-across-destination-types}

El comportamiento de exportación del destino es coherente entre los destinos que pertenecen a un tipo de destino con respecto a *déclencheur de una exportación de destino* y *qué se incluye en las exportaciones de destino*. Las exportaciones de destino se activan mediante notificaciones que el servicio de destinos recibe del [Servicio de perfil del cliente en tiempo real ascendente](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

Lo que se incluye en las exportaciones de destino varía ligeramente entre los tipos de destino. Obtenga más información sobre [patrones de comportamiento de exportación comunes por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md). Los desarrolladores de destino o los usuarios de CDP en tiempo real no pueden editar estas configuraciones.

## Ajustes de exportación personalizables por desarrolladores de destino {#customizable-settings-by-destination-developers}

Los desarrolladores de destino pueden utilizar [Destination SDK](/help/destinations/destination-sdk/overview.md) para crear destinos personalizados o productizados (privados o públicos). Destination SDK proporciona a los desarrolladores una buena flexibilidad para configurar los destinos en función de las funciones descendentes de sus extremos de API y sistemas de recepción de archivos. En función de las funciones descendentes, los desarrolladores de destino tienen disponibles las siguientes opciones de configuración al configurar un destino mediante el Destination SDK :

* Determine qué atributos e identidades se pueden exportar de Experience Platform al destino. Determine también qué identidades necesitan sus destinos para que la exportación de datos se realice correctamente.
* Establezca una directiva de agregación, que determina cuánto tiempo debe esperar el Experience Platform al agregar mensajes HTTP para enviarlos a integraciones de API. Los desarrolladores de destino pueden configurar diferentes tipos de agregación para determinar cuántos perfiles se deben incluir en los mensajes HTTP salientes y cuánto tiempo debe esperar el Experience Platform hasta que envíe el mensaje HTTP. Encuentre información detallada sobre el [opciones de configuración de directiva de agregación](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) disponible para los desarrolladores de destino en la documentación de Destination SDK.
* Determine si las exportaciones de mensajes HTTP deben incluir perfiles que cumplan los requisitos para los segmentos, que se eliminen de los segmentos o ambos.
* Determine qué configuraciones de formato de archivo y nombre de archivo deben estar disponibles para los usuarios al exportar archivos.

## Configuración de un nivel de flujo de datos personalizable por los usuarios {#settings-on-dataflow-level}

Además de los ajustes no editables que dependen del tipo de destino y de la configuración del desarrollador de destino, hay ciertos ajustes de exportación que los usuarios pueden configurar en el flujo de trabajo de activación. Estos ajustes están relacionados con la programación de exportación de un determinado flujo de datos a un destino, los atributos y los campos de identidad que deben exportarse en un flujo de datos o las opciones de formato de archivo para los archivos exportados.

La configuración disponible para los usuarios al conectarse a un destino depende de cómo el desarrollador de destino configuró el destino y de qué configuración pusieron a disposición de los usuarios.

Por ejemplo, para [destinos de flujo continuo](/help/destinations/destination-types.md#streaming-destinations), un desarrollador de destino puede configurar qué identidades acepta su destino y solo esas identidades se mostrarán al usuario en [paso de asignación del flujo de trabajo de activación](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), como se muestra a continuación:

![Registro de la pantalla de la selección de identidad para el campo de destino en el paso de asignación del flujo de trabajo de activación. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Del mismo modo, para [destinos basados en archivos](/help/destinations/destination-types.md#file-based), el desarrollador de destino puede determinar cuál [opciones de adición de nombre de archivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) desean que estén disponibles para su destino, o que [opciones de formato de archivo](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) desean que estén disponibles y el usuario solo podrá seleccionar entre estas opciones, como se muestra a continuación:

![Grabación en pantalla de la opción de formato de archivo al conectarse a un destino basado en archivos.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Registro de pantalla de la opción de adición de nombre de archivo en el paso de programación del flujo de trabajo de activación. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Obtenga más información sobre las distintas opciones y pasos disponibles en el flujo de trabajo de activación:

* [Activar datos de audiencia en destinos de exportación de perfiles en lote](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Activar datos de audiencia en destinos empresariales](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportar archivos bajo demanda a destinos por lotes](/help/destinations/ui/export-file-now.md)
* [(Beta) Exportar conjuntos de datos a destinos de almacenamiento en la nube](/help/destinations/ui/export-datasets.md)

## Pasos siguientes {#next-steps}

Después de leer este documento, ahora sabe qué configuración de exportación para destinos es común en los tipos de destino, qué pueden configurar los desarrolladores en un nivel de destino individual y qué configuración pueden editar los usuarios en el flujo de trabajo de activación.

A continuación, puede leer información más detallada sobre el [patrones de comportamiento de exportación comunes por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md).

Para los desarrolladores de destino, puede [introducción](/help/destinations/destination-sdk/getting-started.md) con Destination SDK. Para los usuarios que buscan activar datos, puede consultar todos los destinos disponibles en la [catálogo](/help/destinations/catalog/overview.md).
