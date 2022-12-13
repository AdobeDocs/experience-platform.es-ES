---
keywords: Experience Platform;inicio;temas populares;ubicación de datos;ubicación de datos;administración de datos;administración de datos;idioma;linaje;tipo de datos;tipos de datos;tipos de datos;tipo de datos
solution: Experience Platform
title: Información general sobre conjuntos de datos
topic-legacy: datasets
description: Este documento proporciona información general de alto nivel sobre los conjuntos de datos en Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '784'
ht-degree: 9%

---

# Información general sobre conjuntos de datos

Todos los datos que se incorporan correctamente en Adobe Experience Platform se conservan dentro del [!DNL Data Lake] como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

Este documento proporciona información general de alto nivel sobre los conjuntos de datos en [!DNL Experience Platform].

## Creación de conjuntos de datos y seguimiento de metadatos

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de los datos [!DNL Experience Platform], y se utiliza para crear y administrar conjuntos de datos. [!DNL Catalog] rastrea los metadatos de cada conjunto de datos, lo que incluye una referencia a la variable [!DNL Experience Data Model] (XDM) el esquema al que se ajusta el conjunto de datos (explicado en la sección siguiente) y el número de registros introducidos en ese conjunto de datos.

Consulte la [Información general del servicio de catálogo](../home.md) para obtener más información.

## Implementación de restricciones en los datos del conjunto de datos

[!DNL Experience Data Model] (XDM) es el marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente. Todos los datos que se incorporan en [!DNL Platform] debe ajustarse a un esquema XDM predefinido para que pueda persistir en el [!DNL Data Lake] como conjunto de datos.

Todos los conjuntos de datos contienen una referencia al esquema XDM que restringe el formato y la estructura de los datos que pueden almacenar. Si se intenta cargar datos en un conjunto de datos que no se ajuste al esquema XDM del conjunto de datos, la ingesta fallará.

Para obtener más información sobre XDM, consulte la [Información general del sistema XDM](../../xdm/home.md).

## Ingesta de datos en conjuntos de datos

La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] Ingesta datos de varias fuentes. Independientemente del método de ingesta, todos los datos introducidos correctamente se convierten en archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. A continuación, estos archivos por lotes se añaden a conjuntos de datos dedicados y se mantienen dentro del [!DNL Data Lake].

Consulte la [Información general sobre la ingesta de datos](../../ingestion/home.md) para obtener más información.

## Aplicación de etiquetas de uso a conjuntos de datos

La administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes para garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. El marco de control de datos le permite aplicar etiquetas de uso para categorizar los datos según las políticas de uso que se apliquen a esos datos.

>[!IMPORTANT]
>
>La aplicación de etiquetas en el nivel de conjunto de datos solo se admite para casos de uso de control de datos. Si intenta crear directivas de acceso para los datos, debe [aplicar etiquetas al esquema](../../xdm/tutorials/labels.md) en el que se basa el conjunto de datos. Consulte la descripción general sobre [control de acceso basado en atributos](../../access-control/abac/overview.md) para obtener más información.

Las etiquetas de uso de datos se pueden aplicar a conjuntos de datos completos o a campos de conjuntos de datos individuales. Las etiquetas agregadas en el nivel de conjunto de datos las heredan todos los campos dentro de ese conjunto de datos.

Consulte la [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información sobre el servicio. Para ver los pasos sobre cómo trabajar con etiquetas de uso en [!DNL Platform], consulte las siguientes guías:

* [Administrar etiquetas en la interfaz de usuario](../../data-governance/labels/user-guide.md)
* [Administrar etiquetas de conjuntos de datos en la API](../../data-governance/labels/dataset-api.md)

## Conjuntos de datos en el flujo descendente [!DNL Platform] servicios

Una vez que se han utilizado los conjuntos de datos para almacenar datos ingestados, esos conjuntos de datos se utilizan después en el flujo descendente [!DNL Platform] servicios para actualizar perfiles de clientes, obtener perspectivas a través del aprendizaje automático, etc.

A continuación se muestra una lista de servicios descendentes que utilizan conjuntos de datos para diversas operaciones. Consulte la documentación de cada servicio para obtener más información.

* [[!DNL Data Access API]](../../data-access/home.md): Permite acceder y descargar el contenido de los archivos almacenados en conjuntos de datos.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): Agrupa identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Aprovechamientos [!DNL Identity Service] para crear perfiles de cliente detallados a partir de sus conjuntos de datos en tiempo real. [!DNL Real-time Customer Profile] extrae datos de [!DNL Data Lake] y mantienen los perfiles de los clientes en su propio almacén de datos independiente.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): Permite generar segmentos y generar audiencias a partir de [!DNL Real-time Customer Profile] datos. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro del [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utiliza aprendizaje automático e inteligencia artificial para descubrir perspectivas en conjuntos de datos grandes.
* [Servicio de consultas de Adobe Experience Platform](../../query-service/home.md): Permite utilizar SQL estándar para consultar datos en [!DNL Experience Platform], uniendo cualquier conjunto de datos dentro de la variable [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en los informes, [!DNL Data Science Workspace]o [!DNL Real-time Customer Profile].
* [Servicio de destinos de Adobe Experience Platform](../../destinations/home.md): Permite [exportar conjuntos de datos](/help/destinations/ui/export-datasets.md) al almacenamiento en la nube o a los destinos de marketing por correo electrónico que desee, para actividades de creación de informes o de ciencia de datos.

## Pasos siguientes

Al leer este documento, se le han introducido los usos principales de los conjuntos de datos en [!DNL Experience Platform], así como los distintos [!DNL Platform] servicios que utilizan conjuntos de datos. Para obtener más información sobre las distintas formas en que se utilizan los conjuntos de datos en [!DNL Platform], consulte la documentación del servicio vinculada a través de esta descripción general.

Para ver los pasos sobre cómo interactuar con conjuntos de datos dentro de la variable [!DNL Experience Platform] La interfaz de usuario de puede consultar la [guía del usuario de conjuntos de datos](user-guide.md).
