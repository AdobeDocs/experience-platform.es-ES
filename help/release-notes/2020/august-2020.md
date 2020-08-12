---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 10 de agosto de 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 89531ad458bd41720090ef2c429376af4460d7c0
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 7%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 12 de agosto de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!Espacio de trabajo de ciencias de datos DNL]](#dsw)
- [[!Fuentes DNL]](#sources)

## [!DNL Data Science Workspace] {#dsw}

[!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para generar perspectivas a partir de los datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a realizar predicciones mediante el uso de contenido y recursos de datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Mejoras de VM en [!DNL JupyterLab] | Se mejoró la estabilidad de las máquinas [!DNL JupyterLab notebook] virtuales de larga ejecución. |

Para obtener más información sobre [!DNL JupyterLab], consulte la guía del [[!DNL JupyterLab] usuario](../../data-science-workspace/jupyterlab/overview.md).

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
