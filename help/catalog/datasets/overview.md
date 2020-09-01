---
keywords: Experience Platform;home;popular topics;data location;Data Location;Data management;data management;Lineage;lineage;data type;data types;Data types;Data type
solution: Experience Platform
title: Introducción a los conjuntos de datos
topic: datasets
description: Este documento proporciona información general de alto nivel sobre los conjuntos de datos en Experience Platform.
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 2%

---


# Introducción a los conjuntos de datos

Todos los datos que se ingieren correctamente en Adobe Experience Platform se conservan dentro de los [!DNL Data Lake] conjuntos de datos. Un conjunto de datos es un almacenamiento y una construcción de administración para una colección de datos, generalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

Este documento proporciona información general de alto nivel sobre los conjuntos de datos de [!DNL Experience Platform].

## Creación de conjuntos de datos y seguimiento de metadatos

[!DNL Catalog Service] es el sistema de registro para la ubicación y el linaje de los datos dentro [!DNL Experience Platform], y se utiliza para crear y administrar conjuntos de datos. [!DNL Catalog] rastrea los metadatos de cada conjunto de datos, que incluye una referencia al esquema [!DNL Experience Data Model] (XDM) al que se ajusta el conjunto de datos (explicado en la siguiente sección) y el número de registros ingeridos en ese conjunto de datos.

Consulte la descripción general [del servicio de](../home.md) catálogos para obtener más información.

## Imponer restricciones en los datos del conjunto de datos

[!DNL Experience Data Model] (XDM) es el marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. Todos los datos que se ingieren en [!DNL Platform] deben cumplir un esquema XDM predefinido para poder persistir en el [!DNL Data Lake] conjunto de datos.

Todos los conjuntos de datos contienen una referencia al esquema XDM que restringe el formato y la estructura de los datos que pueden almacenar. Si se intenta cargar datos en un conjunto de datos que no se ajusta al esquema XDM del conjunto de datos, se producirá un error en la ingestión.

Para obtener más información sobre XDM, consulte la descripción general [del sistema](../../xdm/home.md)XDM.

## Ingreso de datos en conjuntos de datos

La ingestión de datos de Adobe Experience Platform representa los múltiples métodos mediante los cuales [!DNL Platform] ingesta datos de diversas fuentes. Independientemente del método de ingestión, todos los datos ingestados correctamente se convierten en archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Estos archivos por lotes se agregan luego a conjuntos de datos dedicados y se mantienen dentro de los [!DNL Data Lake].

Para obtener más información, consulte la descripción general [de la inserción de](../../ingestion/home.md) datos.

## Aplicación de etiquetas de uso a conjuntos de datos

Adobe Experience Platform [!DNL Data Governance] le permite administrar los datos de los clientes para garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos. El [!DNL Data Governance] marco permite aplicar etiquetas de uso para categorizar los datos según las políticas de uso que se aplican a dichos datos.

Las etiquetas de uso de datos se pueden aplicar a conjuntos de datos completos o a campos de conjuntos de datos individuales. Las etiquetas agregadas en el nivel de conjunto de datos son heredadas por todos los campos dentro de ese conjunto de datos.

Consulte la información general [de Gobierno de](../../data-governance/home.md) datos para obtener más información sobre el servicio. Para ver los pasos sobre cómo trabajar con etiquetas de uso en [!DNL Platform], consulte las siguientes guías:

* [Administrar etiquetas en la interfaz de usuario](../../data-governance/labels/user-guide.md)
* [Administrar etiquetas de conjuntos de datos en la API](../../data-governance/labels/dataset-api.md)

## Conjuntos de datos en servicios [!DNL Platform] descendentes

Una vez que los datasets se han utilizado para almacenar datos ingestados, estos datasets los utilizan los servicios [!DNL Platform] descendentes para actualizar los perfiles de los clientes, obtener perspectivas a través del aprendizaje automático y mucho más.

A continuación se muestra una lista de servicios de flujo descendente que utilizan conjuntos de datos para diversas operaciones. Consulte la documentación de cada servicio para obtener más información.

* [[!DNL Data Access API]](../../data-access/home.md): Permite acceder y descargar el contenido de los archivos almacenados en los conjuntos de datos.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Permite unir identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [[!Perfil del cliente en tiempo real de DNL]](../../profile/home.md): Aprovecha [!DNL Identity Service] para crear perfiles detallados de clientes a partir de sus conjuntos de datos en tiempo real. [!DNL Real-time Customer Profile] extrae datos de los perfiles del cliente [!DNL Data Lake] y los mantiene en su propio almacén de datos independiente.
* [Servicio](../../segmentation/home.md)de segmentación de Adobe Experience Platform: Le permite generar segmentos y audiencias a partir de sus [!DNL Real-time Customer Profile] datos. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro del [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Utiliza aprendizaje automático e inteligencia artificial para descubrir perspectivas en grandes conjuntos de datos.
* [Servicio](../../query-service/home.md)de Consulta de Adobe Experience Platform: Permite utilizar SQL estándar para consulta de datos en [!DNL Experience Platform], unir cualquier conjunto de datos dentro del [!DNL Data Lake] y capturar los resultados de consulta como un nuevo conjunto de datos para su uso en sistema de informes, [!DNL Data Science Workspace]o [!DNL Real-time Customer Profile].
* [Servicio](../../decisioning-service/home.md)de decisiones de Adobe Experience Platform: Aprovecha [!DNL Real-time Customer Profile] para determinar la opción más probable que un cliente elegirá a partir de un conjunto de opciones, en función de los datos de comportamiento que [!DNL Profile] extraen de conjuntos de datos habilitados.

## Pasos siguientes

Al leer este documento, se le han presentado los usos principales de los conjuntos de datos en [!DNL Experience Platform], así como los diversos [!DNL Platform] servicios que utilizan conjuntos de datos. Para obtener más información sobre las muchas formas en que se utilizan los conjuntos de datos en [!DNL Platform], consulte la documentación del servicio vinculada a través de esta información general.

Para ver los pasos sobre cómo interactuar con conjuntos de datos dentro de la [!DNL Experience Platform] interfaz de usuario, consulte la guía [del usuario de](user-guide.md)conjuntos de datos.