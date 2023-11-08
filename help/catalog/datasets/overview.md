---
keywords: Experience Platform;inicio;temas populares;ubicación de datos;Ubicación de datos;Administración de datos;Administración de datos;Linaje;linaje;tipo de datos;tipos de datos;Tipos de datos;Tipo de datos
solution: Experience Platform
title: Resumen de conjuntos de datos
description: Este documento proporciona información general de alto nivel sobre los conjuntos de datos en Experience Platform.
user-guide-description: Obtenga información general de alto nivel sobre los conjuntos de datos en Experience Platform con esta guía. Obtenga información sobre cómo crearlos, aplicar restricciones en los datos e ingerirlos en conjuntos de datos aquí.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 8%

---

# Información general sobre conjuntos de datos

Todos los datos que se incorporan correctamente a Adobe Experience Platform se conservan dentro de la variable [!DNL Data Lake] como conjuntos de datos. Un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

Este documento proporciona información general de alto nivel sobre los conjuntos de datos en [!DNL Experience Platform].

## Creación de conjuntos de datos y metadatos de seguimiento

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de datos dentro de [!DNL Experience Platform]y se utilizan para crear y administrar conjuntos de datos. [!DNL Catalog] rastrea los metadatos de cada conjunto de datos, que incluye una referencia a la variable [!DNL Experience Data Model] El esquema (XDM) al que se ajusta el conjunto de datos (explicado en la siguiente sección) y el número de registros introducidos en ese conjunto de datos.

Consulte la [Resumen del servicio de catálogo](../home.md) para obtener más información.

## Aplicar restricciones a datos de conjuntos de datos

[!DNL Experience Data Model] (XDM) es el marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. Todos los datos que se incorporan a [!DNL Platform] debe ajustarse a un esquema XDM predefinido para poder persistir en [!DNL Data Lake] como un conjunto de datos.

Todos los conjuntos de datos contienen una referencia al esquema XDM que restringe el formato y la estructura de los datos que pueden almacenar. Si se intentan cargar datos en un conjunto de datos que no se ajusta al esquema XDM del conjunto de datos, la ingesta fallará.

Para obtener más información sobre XDM, consulte [Información general del sistema XDM](../../xdm/home.md).

## Ingesta de datos en conjuntos de datos

La ingesta de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] ingiere datos de varias fuentes. Independientemente del método de ingesta, todos los datos introducidos correctamente se convierten en archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Estos archivos por lotes se añaden a continuación a conjuntos de datos dedicados y se mantienen en el [!DNL Data Lake].

Consulte la [Resumen de ingesta de datos](../../ingestion/home.md) para obtener más información.

## Etiquetas aplicadas a conjuntos de datos de esquemas

Administración de datos de Adobe Experience Platform le permite administrar los datos de los clientes para garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. El marco de trabajo de control de datos le permite aplicar etiquetas de uso para categorizar los datos según las políticas de uso que se apliquen a esos datos. Las etiquetas se pueden aplicar a esquemas individuales, campos dentro de esos esquemas y conjuntos de datos individuales completos. Cuando las etiquetas se aplican directamente a un esquema, esas etiquetas se propagan a todos los conjuntos de datos existentes y futuros basados en ese esquema.

>[!IMPORTANT]
>
>Las etiquetas ya no se pueden aplicar a campos de nivel de conjunto de datos. Este flujo de trabajo ha quedado obsoleto y favorece la aplicación de etiquetas en el nivel de esquema. Cualquier etiqueta aplicada anteriormente en el nivel de objeto del conjunto de datos seguirá siendo compatible mediante la IU de Platform hasta el 31 de mayo de 2024. Para garantizar que las etiquetas sean coherentes en todos los esquemas, cualquier etiqueta adjunta anteriormente a campos de nivel de conjunto de datos debe migrarse al nivel de esquema durante el próximo año. Consulte la sección sobre [migración de etiquetas aplicadas anteriormente](../../data-governance/e2e.md#migrate-labels) para obtener instrucciones sobre cómo hacerlo.

Consulte la [Resumen de gobernanza de datos](../../data-governance/home.md) para obtener más información sobre el servicio. Para ver los pasos sobre cómo trabajar con etiquetas de uso en [!DNL Platform], consulte las siguientes guías:

* [Administración de etiquetas en la IU](../../data-governance/labels/user-guide.md)
* [Administrar etiquetas de conjuntos de datos en la API](../../data-governance/labels/dataset-api.md)

## Conjuntos de datos en flujo descendente [!DNL Platform] servicios

Una vez que se han utilizado conjuntos de datos para almacenar datos ingeridos, esos conjuntos de datos se utilizan en el flujo descendente [!DNL Platform] servicios para actualizar perfiles de clientes, obtener perspectivas a través del aprendizaje automático y mucho más.

A continuación se muestra una lista de servicios descendentes que utilizan conjuntos de datos para diversas operaciones. Consulte la documentación de cada servicio para obtener más información.

* [[!DNL Data Access API]](../../data-access/home.md): Permite acceder y descargar el contenido de los archivos almacenados en los conjuntos de datos.
* [Servicio de identidad de Adobe Experience Platform](../../identity-service/home.md): vincula identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Aprovecha [!DNL Identity Service] para crear perfiles detallados de los clientes a partir de los conjuntos de datos en tiempo real. [!DNL Real-Time Customer Profile] extrae datos del [!DNL Data Lake] y mantiene los perfiles de los clientes en su propio almacén de datos independiente.
* [Servicio de segmentación de Adobe Experience Platform](../../segmentation/home.md): Permite generar segmentos y audiencias a partir de [!DNL Real-Time Customer Profile] datos. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro de la [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): utiliza el aprendizaje automático y la inteligencia artificial para descubrir perspectivas en grandes conjuntos de datos.
* [Adobe Experience Platform Query Service](../../query-service/home.md): permite utilizar SQL estándar para consultar datos en [!DNL Experience Platform], uniendo cualquier conjunto de datos dentro de [!DNL Data Lake] y captura de resultados de consultas como un nuevo conjunto de datos para su uso en sistemas de informes, [!DNL Data Science Workspace], o [!DNL Real-Time Customer Profile].
* [Servicio Destinos de Adobe Experience Platform](../../destinations/home.md): le permite [exportar conjuntos de datos](/help/destinations/ui/export-datasets.md) a los destinos de marketing por correo electrónico o almacenamiento en la nube que desee, para actividades de informes o ciencia de datos.

## Pasos siguientes

Al leer este documento, se le ha presentado los usos principales de los conjuntos de datos en [!DNL Experience Platform], así como los distintos [!DNL Platform] servicios que utilizan conjuntos de datos. Para obtener más información sobre las muchas formas en que se utilizan los conjuntos de datos en [!DNL Platform], consulte la documentación del servicio vinculada a lo largo de esta descripción general.

Para ver los pasos sobre cómo interactuar con conjuntos de datos dentro de [!DNL Experience Platform] IU, consulte la [guía del usuario de conjuntos de datos](user-guide.md).
