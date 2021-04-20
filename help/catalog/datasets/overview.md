---
keywords: Experience Platform;inicio;temas populares;ubicación de datos;ubicación de datos;administración de datos;administración de datos;idioma;linaje;tipo de datos;tipos de datos;tipos de datos;tipo de datos
solution: Experience Platform
title: Información general sobre conjuntos de datos
topic: datasets
description: Este documento proporciona información general de alto nivel sobre los conjuntos de datos en Experience Platform.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---


# Información general sobre conjuntos de datos

Todos los datos que se incorporan correctamente en Adobe Experience Platform se mantienen dentro de [!DNL Data Lake] como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una recopilación de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

Este documento proporciona información general de alto nivel sobre los conjuntos de datos en [!DNL Experience Platform].

## Creación de conjuntos de datos y seguimiento de metadatos

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de los datos dentro de  [!DNL Experience Platform], y se utiliza para crear y administrar conjuntos de datos. [!DNL Catalog] rastrea los metadatos de cada conjunto de datos, que incluyen una referencia al esquema  [!DNL Experience Data Model] (XDM) al que se ajusta el conjunto de datos (explicado en la siguiente sección) y el número de registros ingeridos en ese conjunto de datos.

Consulte la [Descripción general del servicio de catálogo](../home.md) para obtener más información.

## Implementación de restricciones en los datos del conjunto de datos

[!DNL Experience Data Model] (XDM) es el marco estandarizado mediante el cual se  [!DNL Platform] organizan los datos de experiencia del cliente. Todos los datos que se incorporan en [!DNL Platform] deben ajustarse a un esquema XDM predefinido para que pueda persistir en [!DNL Data Lake] como conjunto de datos.

Todos los conjuntos de datos contienen una referencia al esquema XDM que restringe el formato y la estructura de los datos que pueden almacenar. Si se intenta cargar datos en un conjunto de datos que no se ajuste al esquema XDM del conjunto de datos, la ingesta fallará.

Para obtener más información sobre XDM, consulte [Información general del sistema XDM](../../xdm/home.md).

## Ingesta de datos en conjuntos de datos

La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] ingesta datos de varias fuentes. Independientemente del método de ingesta, todos los datos introducidos correctamente se convierten en archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. A continuación, estos archivos por lotes se añaden a conjuntos de datos dedicados y se mantienen dentro de [!DNL Data Lake].

Consulte la [información general sobre la ingesta de datos](../../ingestion/home.md) para obtener más información.

## Aplicación de etiquetas de uso a conjuntos de datos

Adobe Experience Platform [!DNL Data Governance] le permite administrar los datos de los clientes para garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. El marco [!DNL Data Governance] le permite aplicar etiquetas de uso para categorizar los datos según las políticas de uso que se aplican a esos datos.

Las etiquetas de uso de datos se pueden aplicar a conjuntos de datos completos o a campos de conjuntos de datos individuales. Las etiquetas agregadas en el nivel de conjunto de datos las heredan todos los campos dentro de ese conjunto de datos.

Consulte [Información general sobre la administración de datos](../../data-governance/home.md) para obtener más información sobre el servicio. Para ver los pasos sobre cómo trabajar con etiquetas de uso en [!DNL Platform], consulte las siguientes guías:

* [Administrar etiquetas en la interfaz de usuario](../../data-governance/labels/user-guide.md)
* [Administrar etiquetas de conjuntos de datos en la API](../../data-governance/labels/dataset-api.md)

## Conjuntos de datos en servicios descendentes [!DNL Platform]

Una vez que los conjuntos de datos se han utilizado para almacenar datos ingestados, los servicios descendentes [!DNL Platform] utilizan esos conjuntos de datos para actualizar los perfiles de los clientes, obtener perspectivas mediante el aprendizaje automático y mucho más.

A continuación se muestra una lista de servicios descendentes que utilizan conjuntos de datos para diversas operaciones. Consulte la documentación de cada servicio para obtener más información.

* [[!DNL Data Access API]](../../data-access/home.md): Permite acceder y descargar el contenido de los archivos almacenados en conjuntos de datos.
* [Servicio de ID de Adobe Experience Platform](../../identity-service/home.md): Agrupa identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Aprovecha  [!DNL Identity Service] para crear perfiles de cliente detallados a partir de sus conjuntos de datos en tiempo real. [!DNL Real-time Customer Profile] extrae datos de  [!DNL Data Lake] y mantiene los perfiles de cliente en su propio almacén de datos independiente.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): Permite crear segmentos y generar audiencias a partir de los  [!DNL Real-time Customer Profile] datos. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro de [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utiliza aprendizaje automático e inteligencia artificial para descubrir perspectivas en conjuntos de datos grandes.
* [Servicio de consultas de Adobe Experience Platform](../../query-service/home.md): Permite utilizar SQL estándar para consultar datos en  [!DNL Experience Platform], unir cualquier conjunto de datos dentro de  [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en informes,  [!DNL Data Science Workspace] o  [!DNL Real-time Customer Profile].

## Pasos siguientes

Al leer este documento, se le han introducido los usos principales de los conjuntos de datos en [!DNL Experience Platform], así como los diversos servicios [!DNL Platform] que utilizan conjuntos de datos. Para obtener más información sobre las muchas formas en que se utilizan los conjuntos de datos en [!DNL Platform], consulte la documentación del servicio vinculada a través de esta descripción general.

Para ver los pasos sobre cómo interactuar con conjuntos de datos dentro de la [!DNL Experience Platform] interfaz de usuario, consulte la [guía del usuario de conjuntos de datos](user-guide.md).