---
title: Notas de la versión de Adobe Experience Platform, diciembre de 2020
description: Notas de la versión de diciembre de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: December 9, 2020
author: ens60013 & ens72471
exl-id: 89d631f1-1b11-4a18-98e1-08e1d5bd8b0d
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 9 de diciembre de 2020**

Nuevas funciones de Adobe Experience Platform:

- [[!DNL Dataflows]](#dataflows)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Sources]](#sources)

## [!DNL Dataflows] {#dataflows}

Los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Estos flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a ID y servicio de perfil y a destinos.

**Característica clave**

| Función | Descripción |
| ------- | ----------- |
| Transparencia para flujos de datos | Puede controlar los flujos de datos para las fuentes y los destinos. Para obtener más información, lea la [tutorial sobre fuentes de monitorización](../../dataflows/ui/monitor-sources.md) o [tutorial sobre la monitorización de destinos](../../dataflows/ui/monitor-destinations.md). |

Para obtener más información sobre los flujos de datos, lea la [información general sobre flujos de datos](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe.

**Funciones principales**

| Función | Descripción |
| --- | ---|
| complemento del paquete Adobe Experience Platform Intelligence | El complemento del paquete de Adobe Experience Platform Intelligence es una actualización de Data Science Workspace que desbloquea funciones clave adicionales como: <li> Experimentación y evaluación del modelo impulsado por la interfaz de usuario.</li><li> Capacidad para implementar y operacionalizar modelos con trabajos programados de capacitación e inferencias.</li><li> Compatibilidad con el aprendizaje profundo en modelos de Tensorflow (GPU Compute).</li><li> Cálculo distribuido basado en chispas para entrenar y puntuar con conjuntos de datos grandes (10 MM + filas).</li><li>Y más</li> |

Para obtener más información sobre el complemento del paquete Adobe Experience Platform Intelligence, consulte la documentación de [Acceso y funciones de Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Actualizar los detalles de cuenta y conexión para las fuentes de flujo continuo | Ahora puede actualizar los nombres, las descripciones y las credenciales de las conexiones de flujo continuo existentes mediante la función [!DNL Flow Service] y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre [actualización de conexiones mediante la API](../../sources/tutorials/api/update.md) y [edición de los detalles de la cuenta mediante la interfaz de usuario](../../sources/tutorials/ui/monitor.md). |
| Eliminar flujos de datos | Los flujos de datos de flujo continuo que contienen errores o que se han vuelto innecesarios ahora se pueden eliminar mediante la función [!DNL Flow Service] y la interfaz de usuario. Para obtener más información, consulte el tutorial sobre [eliminación de flujos de datos mediante la API](../../sources/tutorials/api/delete-dataflows.md) y [eliminación de flujos de datos mediante la interfaz de usuario](../../sources/tutorials/ui/delete.md). |

Para obtener más información sobre las fuentes, consulte la [información general sobre fuentes](../../sources/home.md).
