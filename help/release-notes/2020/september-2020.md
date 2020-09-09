---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 9 de septiembre de 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 9a9b1294507986723c1e4d1230a854630131be3a
workflow-type: tm+mt
source-wordcount: '805'
ht-degree: 4%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 9 de septiembre de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!Gobierno de datos DNL]](#governance)
- [[!Destinos DNL]](#destinations)
- [[!Privacy Service DNL]](#privacy)
- [[!DNL Perfil del cliente en tiempo real]](#profile)
- [[!Servicio de segmentación DNL]](#segmentation)
- [[!Fuentes DNL]](#sources)

## [!DNL Data Governance] {#governance}

La Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías utilizadas para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] varios niveles, incluyendo catalogación, linaje de datos, etiquetado de uso de datos, políticas de acceso a datos e controles de acceso en datos para acciones de mercadotecnia.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en la interfaz de usuario de etiquetado de conjuntos de datos | Se han agregado varios controles de filtrado y clasificación nuevos a la interfaz de usuario de etiquetado de conjuntos de datos para facilitar el trabajo con esquemas grandes: <ul><li>Ordene los campos por orden alfabético en función de la ruta completa del esquema.</li><li>Realice búsquedas parciales en los nombres de ruta de campo.</li><li>Filtre campos sin etiquetas, una etiqueta seleccionada o una categoría de etiqueta.</li></ul> |

Consulte la información general [de Gobierno de](../../data-governance/home.md) datos para obtener más información sobre el servicio.

## Destinos {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en los recursos | Los usuarios pueden acceder a las acciones de tabla en línea para acceder más fácilmente a las acciones principales, como agregar datos, editar la programación y agregar segmentos. Consulte el documento del espacio de trabajo [de](../../rtcdp/destinations/destinations-workspace.md) destinos para obtener más información. |

Para obtener más información, visite la descripción general de [destinos](../../rtcdp/destinations/destinations-overview.md)

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos dispares de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

| Función | Descripción |
| ------- | ----------- |
| Visor de perfiles | El visor de perfil, en la interfaz de usuario de la plataforma, se ha actualizado para que sea un panel con personalización total. El usuario tiene ahora la opción de realizar las siguientes tareas: <ul><li>Actualice los atributos estándar y personalizados seleccionados en la utilidad de información básica.</li><li>Creación, edición y eliminación de widgets personalizados</li><li>Cambiar el tamaño y reorganizar los widgets</li></ul> |

Para obtener más información sobre [!DNL Real-time Customer Profile]tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] datos, lea la descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## Servicio de segmentación {#segmentation}

El servicio de segmentación de Adobe Experience Platform proporciona una interfaz de usuario y una API de RESTful que le permite generar segmentos y audiencias a partir de sus [!DNL Real-time Customer Profile] datos. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform], lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto concreto de perfiles describiendo los criterios que distinguen a un grupo comercializable de personas dentro de la base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Trabajos de exportación | Se agregó un indicador para permitir que los segmentos se evalúen como parte de un trabajo de exportación. Como resultado, los usuarios pueden ejecutar tanto la segmentación como las exportaciones en un solo trabajo. |
| Combinar directivas | Se pueden incluir varias directivas de combinación en un único trabajo de segmentación por lotes. |

Para obtener más información sobre [!DNL Segmentation Service], consulte la información general [de segmentación](../../segmentation/home.md)

## [!DNL Privacy Service] {#privacy}

Varios reglamentos legales y organizativos otorgan a los usuarios el derecho de acceder a sus datos personales o eliminarlos de sus almacenes de datos si así lo solicitan. Adobe Experience Platform [!DNL Privacy Service] proporciona una API RESTful y una interfaz de usuario para ayudarle a administrar estas solicitudes de datos de sus clientes. Con [!DNL Privacy Service], puede enviar solicitudes para acceder y eliminar datos personales o privados de clientes desde las aplicaciones de Adobe Experience Cloud, lo que facilita el cumplimiento automatizado de las normativas legales y de privacidad de la organización.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Apoyo a LGPD (Brasil) | Ahora se pueden crear empleos de privacidad bajo la regulación de Brasil [!DNL Lei Geral de Proteção de Dados] (LGPD, por sus siglas en inglés). Estos trabajos son rastreados bajo el código de regulación `lgpd_bra`. |

Consulte la descripción general [del](../../privacy-service/home.md) Privacy Service para obtener más información sobre el servicio.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Asignación automática | [!DNL Platform] proporciona recomendaciones inteligentes para la asignación automática durante el flujo de trabajo de inserción de datos, en función de un esquema de destinatario o conjunto de datos seleccionados por el usuario. Puede ajustar manualmente las reglas de asignación automática flexibles para adaptarlas a sus casos de uso. |
| Mejoras en los recursos | Los usuarios pueden acceder a las acciones de tabla en línea para acceder más fácilmente a las acciones principales, como agregar datos, editar la programación y agregar segmentos. Consulte el documento de flujos de datos de [supervisión](../../sources/tutorials/ui/monitor.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.
