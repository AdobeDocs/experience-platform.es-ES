---
title: Notas de la versión de Adobe Experience Platform, septiembre de 2020
description: Notas de la versión de septiembre de 2020 de Adobe Experience Platform.
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
exl-id: bf401f3a-b088-4cbd-9a64-224294b797b9
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 6%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 9 de septiembre de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Control de datos](#governance)
- [[!DNL Destinations]](#destinations)
- [[!DNL Observability Insights]](#observability)
- [[!DNL Privacy Service]](#privacy)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## Control de datos {#governance}

Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de datos. Desempeña un papel clave dentro de [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para acciones de marketing.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de IU de etiquetado de conjuntos de datos | Se han agregado varios nuevos controles de ordenación y filtrado a la interfaz de usuario de etiquetado de conjuntos de datos para facilitar el trabajo con esquemas grandes: <ul><li>Ordene los campos por orden alfabético en función de la ruta de esquema completa.</li><li>Realizar búsquedas parciales en los nombres de rutas de campo.</li><li>Filtre los campos sin etiquetas, con una etiqueta seleccionada o con una categoría de etiqueta.</li></ul> |

Consulte la [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información sobre el servicio.

## Destinos {#destinations}

Entrada [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma fluida.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de UX | Los usuarios pueden acceder a las acciones de tablas en línea para acceder más fácilmente a las acciones principales, como añadir datos, editar programación y añadir segmentos. Consulte la [destination workspace](../../destinations/ui/destinations-workspace.md) para obtener más información. |

Para obtener más información, visite la [información general sobre destinos](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] permite supervisar las actividades en Adobe Experience Platform mediante el uso de métricas estadísticas y notificaciones de eventos.

**Nuevas características**

| Función | Descripción |
| --- | --- |
| Adobe I/O Notificaciones de eventos | [!DNL Observability Insights] utiliza Eventos de Adobe I/O para crear notificaciones de eventos para varios servicios de Experience Platform. Las cargas de notificación se envían a un webhook configurado que puede utilizar para automatizar procesos descendentes adicionales. |

Consulte la [[!DNL Observability Insights] descripción general](../../observability/home.md) para obtener más información sobre el servicio.

## [!DNL Privacy Service] {#privacy}

Varias regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder o eliminar sus datos personales de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder a datos de clientes privados o personales y eliminarlos de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las regulaciones de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad con LGPD (Brasil) | Ahora se pueden crear trabajos de privacidad bajo la ley de Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD). Estos trabajos se rastrean bajo el código de regulación `lgpd_bra`. |

Consulte la [Introducción al Privacy Service](../../privacy-service/home.md) para obtener más información sobre el servicio.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los distintos datos de clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

| Función | Descripción |
| ------- | ----------- |
| Visualizador de perfiles | El visor de perfiles, en la interfaz de usuario de Platform, se ha actualizado para que sea un panel con personalización completa. El usuario tiene ahora la opción de realizar las siguientes tareas: <ul><li>Actualice el estándar seleccionado y los atributos personalizados en el widget de información básica.</li><li>Crear, editar y eliminar widgets personalizados</li><li>Cambiar el tamaño y reorganizar widgets</li></ul> |

Para obtener más información sobre [!DNL Real-Time Customer Profile], incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] data, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite generar segmentos y audiencias a partir de [!DNL Real-Time Customer Profile] datos. Estos segmentos se configuran de forma centralizada y se mantienen en [!DNL Platform], haciéndolos fácilmente accesibles desde cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Exportar trabajos | Se ha añadido un indicador para permitir que los segmentos se evalúen como parte de un trabajo de exportación. Como resultado, los usuarios pueden ejecutar tanto la segmentación como las exportaciones en un solo trabajo. |
| Políticas de combinación | Se pueden incluir varias políticas de combinación en un solo trabajo de segmentación por lotes. |

Para obtener más información sobre [!DNL Segmentation Service], consulte la [Resumen de segmentación](../../segmentation/home.md)

## Fuentes {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Asignación automática | [!DNL Platform] proporciona recomendaciones inteligentes para la asignación automática durante el flujo de trabajo de ingesta de datos, en función de un esquema de destino o conjunto de datos seleccionado por el usuario. Puede ajustar manualmente reglas de asignación automática flexibles para adaptarlas a sus casos de uso. |
| Mejoras de UX | Los usuarios pueden acceder a las acciones de tabla en línea para acceder más fácilmente a las acciones principales, como añadir datos, editar programación y añadir segmentos. Consulte la [monitorización de flujos de datos](../../sources/tutorials/ui/monitor.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
