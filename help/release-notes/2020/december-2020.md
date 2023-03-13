---
title: Notas de la versión de Adobe Experience Platform, diciembre de 2020
description: Notas de la versión de diciembre de 2020 de Adobe Experience Platform.
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

Los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Estos flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, al servicio de identidad y perfil y a destinos.

**Característica principal**

| Función | Descripción |
| ------- | ----------- |
| Transparencia para flujos de datos | Puede monitorizar los flujos de datos de fuentes y destinos. Para obtener más información, lea la [tutorial sobre fuentes de monitorización](../../dataflows/ui/monitor-sources.md) o el [tutorial sobre supervisión de destinos](../../dataflows/ui/monitor-destinations.md). |

Para obtener más información sobre los flujos de datos, lea la [resumen de flujos de datos](../../dataflows/home.md).

## [!DNL Data Science Workspace] {#dsw}

El espacio de trabajo de ciencia de datos utiliza aprendizaje automático e inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, el espacio de trabajo de ciencia de datos le ayuda a hacer predicciones utilizando su contenido y sus recursos de datos en soluciones de Adobe.

**Funciones principales**

| Función | Descripción |
| --- | ---|
| Complemento del paquete Adobe Experience Platform Intelligence | El complemento del paquete Adobe Experience Platform Intelligence es una actualización de Data Science Workspace que desbloquea funciones clave adicionales como: <li> Experimentación y evaluación de modelos impulsados por la IU.</li><li> Capacidad para implementar y poner en funcionamiento modelos con formación programada y trabajos de inferencia.</li><li> Compatibilidad con el aprendizaje profundo en modelos Tensorflow (GPU Compute).</li><li> Equipo distribuido basado en Spark para entrenar y puntuar con conjuntos de datos grandes (10 MM + filas).</li><li>Y más</li> |

Para obtener más información sobre el complemento del paquete Adobe Experience Platform Intelligence, consulte la documentación sobre [Acceso y funciones de Data Science Workspace](../../data-science-workspace/access-features-dsw.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ------- | ----------- |
| Actualización de los detalles de cuenta y conexión para orígenes de flujo continuo | Ahora puede actualizar los nombres, descripciones y credenciales de las conexiones de flujo continuo existentes utilizando [!DNL Flow Service] API y la IU de. Para obtener más información, consulte el tutorial sobre [actualización de conexiones mediante la API](../../sources/tutorials/api/update.md) y [edición de detalles de la cuenta mediante la IU](../../sources/tutorials/ui/monitor.md). |
| Eliminar flujos de datos | Ahora, los flujos de datos de streaming que contienen errores o se han vuelto innecesarios se pueden eliminar mediante el [!DNL Flow Service] API y la IU de. Para obtener más información, consulte el tutorial sobre [eliminación de flujos de datos mediante la API](../../sources/tutorials/api/delete-dataflows.md) y [eliminación de flujos de datos mediante la IU](../../sources/tutorials/ui/delete.md). |

Para obtener más información sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
