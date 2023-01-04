---
title: Notas de la versión de Adobe Experience Platform, septiembre de 2020
description: Notas de la versión de septiembre de 2020 para Adobe Experience Platform.
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

Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] en varios niveles, incluida la catalogación, el linaje de datos, el etiquetado del uso de datos, las políticas de acceso a datos y el control de acceso a los datos para las acciones de marketing.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en la interfaz de usuario del etiquetado de conjuntos de datos | Se han agregado varios controles de clasificación y filtrado nuevos a la interfaz de usuario de etiquetado de conjuntos de datos para facilitar el trabajo con esquemas grandes: <ul><li>Ordene los campos por orden alfabético en función de la ruta completa del esquema.</li><li>Realice búsquedas parciales en los nombres de rutas de campos.</li><li>Filtre campos sin etiquetas, una etiqueta seleccionada o una categoría de etiqueta.</li></ul> |

Consulte la [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información sobre el servicio.

## Destinos {#destinations}

En [Real-time Customer Data Platform](../../rtcdp/overview.md), los destinos son integraciones prediseñadas con plataformas de destino que activan los datos para esos socios de una manera sencilla.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en la experiencia de usuario | Los usuarios pueden acceder a las acciones de tablas en línea para acceder más fácilmente a las acciones principales, como agregar datos, editar programación y agregar segmentos. Consulte la [espacio de trabajo de destinos](../../destinations/ui/destinations-workspace.md) documento para obtener más información. |

Para obtener más información, visite [información general sobre destinos](../../destinations/home.md)

## [!DNL Observability Insights] {#observability}

[!DNL Observability Insights] le permite supervisar actividades en Adobe Experience Platform mediante el uso de métricas estadísticas y notificaciones de eventos.

**Nuevas características**

| Función | Descripción |
| --- | --- |
| Notificaciones de eventos de Adobe I/O | [!DNL Observability Insights] aprovecha los eventos de Adobe I/O para crear notificaciones de eventos para varios servicios de Experience Platform. Las cargas de notificación se envían a un enlace web configurado que puede utilizar para automatizar más procesos descendentes. |

Consulte la [[!DNL Observability Insights] información general](../../observability/home.md) para obtener más información sobre el servicio.

## [!DNL Privacy Service] {#privacy}

Varias regulaciones legales y organizativas otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API de RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos de clientes personales o privados de aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normas de privacidad legales y organizativas.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Apoyo a LGPD (Brasil) | Ahora se pueden crear trabajos de privacidad bajo la [!DNL Lei Geral de Proteção de Dados] (LGPD). Estos trabajos se rastrean bajo el código de regulación `lgpd_bra`. |

Consulte la [Información general del Privacy Service](../../privacy-service/home.md) para obtener más información sobre el servicio.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus diferentes datos de clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Visor de perfiles | El visor de perfiles, en la interfaz de usuario de Platform, se ha actualizado para que sea un tablero con personalización completa. El usuario tiene ahora la opción de realizar las siguientes tareas: <ul><li>Actualice los atributos estándar y personalizados seleccionados en el widget de información básica.</li><li>Crear, editar y eliminar widgets personalizados</li><li>Cambiar el tamaño y reorganizar las utilidades</li></ul> |

Para obtener más información, consulte [!DNL Real-Time Customer Profile], incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] información, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de su [!DNL Real-Time Customer Profile] datos. Estos segmentos están configurados de forma centralizada y se mantienen en [!DNL Platform], lo que permite que cualquier aplicación de Adobe pueda acceder a ellas fácilmente.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Exportar trabajos | Se ha agregado un indicador para permitir que los segmentos se evalúen como parte de un trabajo de exportación. Como resultado, los usuarios pueden ejecutar tanto la segmentación como las exportaciones en un solo trabajo. |
| Combinar directivas | Se pueden incluir varias políticas de combinación en un único trabajo de segmentación por lotes. |

Para obtener más información, consulte [!DNL Segmentation Service], consulte la [Información general sobre la segmentación](../../segmentation/home.md)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Asignación automática | [!DNL Platform] proporciona recomendaciones inteligentes para la asignación automática durante el flujo de trabajo de ingesta de datos, en función de un esquema de destino o conjunto de datos seleccionado por el usuario. Puede ajustar manualmente las reglas flexibles de asignación automática para adaptarlas a sus casos de uso. |
| Mejoras en la experiencia de usuario | Los usuarios pueden acceder a las acciones de tablas en línea para acceder más fácilmente a las acciones principales, como agregar datos, editar la programación y agregar segmentos. Consulte la [monitorización de flujos de datos](../../sources/tutorials/ui/monitor.md) documento para obtener más información. |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
