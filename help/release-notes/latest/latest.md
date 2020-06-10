---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 10 de junio de 2020
doc-type: release notes
last-update: June 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: b6cfdf56c20065bdc3e8a9fedf6007ddd74eaeaa
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 10 de junio de 2020**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [Área de trabajo de ciencia de datos](#dsw)
- [Fuentes](#sources)

## Área de trabajo de ciencia de datos {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para generar perspectivas a partir de los datos. Integrado en la plataforma Adobe Experience, el espacio de trabajo de ciencia de datos le ayuda a realizar predicciones con su contenido y recursos de datos en todas las soluciones de Adobe.

Data Science Workspace ha estado trabajando en nuevas formas de permitir mejores experiencias y predicciones mediante el uso de aprendizaje automático en tiempo real. El aprendizaje automático en tiempo real permite crear, probar e implementar modelos de aprendizaje automático personalizados o importados preformados en formatos de modelo interoperables estándar del sector para la puntuación/activación en tiempo real mediante un punto final de API.

Tenga en cuenta que el aprendizaje automático en tiempo real se encuentra en fase alfa y aún se está desarrollando.

| Función | Descripción |
|--- | ---|
| Iniciador de HTML en tiempo real de JupyterLab | JupyterLab Launcher ahora incluye un ordenador portátil Python para aprendizaje automático en tiempo real (Alpha). |

Para obtener más información sobre el alfa de aprendizaje automático en tiempo real, consulte la descripción general [de aprendizaje automático en tiempo](../../data-science-workspace/real-time-machine-learning/home.md)real.

## Fuentes {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Compatibilidad adicional de API e interfaz de usuario para sistemas de almacenamiento en la nube | Nuevo conector de origen para HDFS de Apache |
| Compatibilidad adicional de API e interfaz de usuario con bases de datos | Nuevo conector de origen para Couchbase. |

Para obtener más información sobre las fuentes, consulte la descripción general [de](../../sources/home.md)las fuentes.
