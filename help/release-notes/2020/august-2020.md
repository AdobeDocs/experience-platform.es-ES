---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 1d9c8cbf273e9aef13e34df91a98b6c08180c8ff
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 5%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 12 de agosto de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!Espacio de trabajo de ciencias de datos DNL]](#dsw)
- [!DNL Destinations](#destinations)
- [[!Fuentes DNL]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para generar perspectivas a partir de los datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a realizar predicciones mediante el uso de contenido y recursos de datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de VM en [!DNL JupyterLab] | Se mejoró la estabilidad de las máquinas [!DNL JupyterLab notebook] virtuales de larga ejecución. |

Para obtener más información sobre [!DNL JupyterLab], consulte la guía del [[!DNL JupyterLab] usuario](../../data-science-workspace/jupyterlab/overview.md).

## Destinos {#destinations}

En la plataforma [de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe, los destinos son integraciones prediseñadas con plataformas de destino que activan los datos a dichos socios de forma transparente.

**Nuevos destinos**

Hay nuevos destinos disponibles donde puede activar los datos de Adobe Experience Platform. Consulte a continuación los detalles:

| Destino | Descripción |
|--- | ---|
| [!DNL Google Customer Match] | La coincidencia de clientes de Google le permite utilizar sus datos en línea y sin conexión para comunicarse con sus clientes y volver a interactuar con ellos en las propiedades que posee y opera Google, como: [!DNL Search], [!DNL Shopping], Gmail y YouTube. <br><br> Visite la [!DNL Google Customer Match] página [](/help/rtcdp/destinations/google-customer-match-destination.md) del catálogo de destinos para obtener más información sobre el destino y cómo configurarlo en Adobe Real-time CDP. |

**Nuevas funciones**

| Función | Descripción |
|------- | -----------|
| Editor de nombres de archivo personalizado | Actualice el flujo de trabajo de activación de datos para los destinos de marketing por correo electrónico y los destinos de almacenamiento en la nube que le permiten editar el nombre de los archivos exportados. Para obtener más información, consulte el paso [](/help/rtcdp/destinations/activate-destinations.md#configure) Configurar del flujo de trabajo de activación. |
| Atributos recomendados | Actualice el flujo de trabajo de activación de datos para los destinos de marketing por correo electrónico y los destinos de almacenamiento en la nube que muestran los atributos recomendados para agregarlos a los archivos exportados. Para obtener más información, consulte el paso [](/help/rtcdp/destinations/activate-destinations.md#select-attributes) Seleccionar atributos en el flujo de trabajo de activación. |

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Supervisión de la ejecución de flujo | Los usuarios pueden supervisar todas las ejecuciones de flujo y ver una vista detallada de cada ejecución, incluido el estado de finalización, la duración de la ejecución, la lista de archivos procesados, los errores y las métricas. Consulte el documento de flujos de datos de [supervisión](../../sources/tutorials/ui/monitor.md) para obtener más información. |
| Actualización de cuentas | Los usuarios pueden actualizar las credenciales, el nombre y la descripción de cualquier cuenta existente para proporcionar información más significativa y corregir cualquier error que se haya creado. |
| Notificaciones de ejecución de flujo | Los usuarios pueden suscribirse a los eventos y registrar los enlaces web para recibir notificaciones en tiempo real sobre el estado, las métricas y los errores relacionados con las ejecuciones de flujo. |
| Mejoras en el catálogo de la interfaz de usuario | Actualizaciones en la pantalla del catálogo de fuentes para facilitar el acceso a las acciones principales de los objetos seleccionados. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.
