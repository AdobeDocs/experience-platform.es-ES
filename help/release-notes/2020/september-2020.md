---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 9 de septiembre de 2020
doc-type: release notes
last-update: September 8, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 64b6b59923d549cdcbf35d2e375529aec8cf81b8
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 9 de septiembre de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!Gobierno de datos DNL]](#governance)
* [[!Destinos DNL]](#destinations)
* [[!Fuentes DNL]](#sources)

## [!DNL Data Governance] {#governance}

La Administración de datos de Adobe Experience Platform es una serie de estrategias y tecnologías utilizadas para administrar los datos de los clientes y garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Desempeña un papel clave en [!DNL Experience Platform] varios niveles, incluyendo catalogación, linaje de datos, etiquetado de uso de datos, políticas de acceso a datos e controles de acceso en datos para acciones de mercadotecnia.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Mejoras en la interfaz de usuario de etiquetado de conjuntos de datos | Se han agregado varios controles de filtrado y clasificación nuevos a la interfaz de usuario de etiquetado de conjuntos de datos para facilitar el trabajo con esquemas grandes: <ul><li>Ordene los campos por orden alfabético en función de la ruta completa del esquema.</li><li>Realice búsquedas parciales en los nombres de ruta de campo.</li><li>Filtre campos sin etiquetas, una etiqueta seleccionada o una categoría de etiqueta.</li></ul> |

Consulte la información general [de Gobierno de](../../data-governance/home.md) datos para obtener más información sobre el servicio.

## Destinos {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras en los recursos | Los usuarios pueden acceder a las acciones de tabla en línea para acceder más fácilmente a las acciones principales, como agregar datos, editar la programación y agregar segmentos. Consulte el documento del espacio de trabajo [de](../../rtcdp/destinations/destinations-workspace.md) destinos para obtener más información. |

Para obtener más información, visite la descripción general de [destinos](../../rtcdp/destinations/destinations-overview.md)

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Asignación automática | [!DNL Platform] proporciona recomendaciones inteligentes para la asignación automática durante el flujo de trabajo de inserción de datos, en función de un esquema de destinatario o conjunto de datos seleccionados por el usuario. Puede ajustar manualmente las reglas de asignación automática flexibles para adaptarlas a sus casos de uso. |
| Mejoras en los recursos | Los usuarios pueden acceder a las acciones de tabla en línea para acceder más fácilmente a las acciones principales, como agregar datos, editar la programación y agregar segmentos. Consulte el documento de flujos de datos de [supervisión](../../sources/tutorials/ui/monitor.md) para obtener más información. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.