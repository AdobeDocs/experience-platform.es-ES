---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Introducción a los conjuntos de datos
topic: datasets
translation-type: tm+mt
source-git-commit: dcdd94a3a13a13b4104e57b74ecf613bc316b0af
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 2%

---


# Introducción a los conjuntos de datos

Todos los datos que se ingieren correctamente en la plataforma de Adobe Experience se mantienen en el lago de datos como conjuntos de datos. Un conjunto de datos es un almacenamiento y una construcción de administración para una colección de datos, generalmente una tabla, que contiene un esquema (columnas) y campos (filas). Los conjuntos de datos también contienen metadatos que describen varios aspectos de los datos que almacenan.

Este documento proporciona información general de alto nivel sobre los conjuntos de datos en la plataforma de experiencias.

## Creación de conjuntos de datos y seguimiento de metadatos

El servicio de catálogos es el sistema de registro para la ubicación y linaje de datos dentro de la plataforma de experiencias y se utiliza para crear y administrar conjuntos de datos. Catalog rastrea los metadatos de cada conjunto de datos, que incluye una referencia al esquema del Modelo de datos de experiencia (XDM) al que se ajusta el conjunto de datos (que se explica en la siguiente sección) y el número de registros ingeridos en ese conjunto de datos.

Consulte la descripción general [del servicio de](../home.md) catálogos para obtener más información.

## Imponer restricciones en los datos del conjunto de datos

El modelo de datos de experiencia (XDM) es el marco estandarizado mediante el cual Platform organiza los datos de experiencia del cliente. Todos los datos que se ingieren en la plataforma deben cumplir con un esquema XDM predefinido para que pueda persistir en el Data Lake como un conjunto de datos.

Todos los conjuntos de datos contienen una referencia al esquema XDM que restringe el formato y la estructura de los datos que pueden almacenar. Si se intenta cargar datos en un conjunto de datos que no se ajusta al esquema XDM del conjunto de datos, se producirá un error en la ingestión.

Para obtener más información sobre XDM, consulte la descripción general [del sistema](../../xdm/home.md)XDM.

## Ingreso de datos en conjuntos de datos

La ingestión de datos de la plataforma de experiencia de Adobe representa los múltiples métodos mediante los cuales la plataforma ingesta datos de diversas fuentes. Independientemente del método de ingestión, todos los datos ingestados correctamente se convierten en archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad. Estos archivos por lotes se agregan luego a conjuntos de datos dedicados y persisten dentro del lago de datos.

Para obtener más información, consulte la descripción general [de la inserción de](../../ingestion/home.md) datos.

## Aplicación de etiquetas de uso a conjuntos de datos

El Gobierno de datos de la plataforma Adobe Experience le permite administrar los datos de los clientes para garantizar el cumplimiento de las normativas, restricciones y políticas aplicables al uso de los datos. Utilizando el etiquetado y cumplimiento del uso de datos (DULE) como su marco de trabajo principal, el Gobierno de datos permite aplicar etiquetas de uso para categorizar los datos según las políticas de uso que se aplican a esos datos.

Las etiquetas de uso de datos se pueden aplicar a conjuntos de datos completos o a campos de conjuntos de datos individuales. Las etiquetas agregadas en el nivel de conjunto de datos son heredadas por todos los campos dentro de ese conjunto de datos.

Consulte la información general [de](../../data-governance/home.md) Administración de datos para obtener más información sobre el servicio. Para ver los pasos sobre cómo trabajar con etiquetas de uso en [!DNL Platform], consulte las siguientes guías:

* [Administrar etiquetas en la interfaz de usuario](../../data-governance/labels/user-guide.md)
* [Administrar etiquetas en la API](../../data-governance/labels/api.md)

## Conjuntos de datos en los servicios de plataformas descendentes

Una vez que los datasets se han utilizado para almacenar datos ingestados, los servicios de plataforma descendentes utilizan esos datasets para actualizar los perfiles de los clientes, obtener perspectivas a través del aprendizaje automático y mucho más.

A continuación se muestra una lista de servicios de flujo descendente que utilizan conjuntos de datos para diversas operaciones. Consulte la documentación de cada servicio para obtener más información.

* [API](../../data-access/home.md)de acceso a datos: Permite acceder y descargar el contenido de los archivos almacenados en los conjuntos de datos.
* [Servicio](../../identity-service/home.md)de identidad de Adobe Experience Platform: Permite unir identidades entre dispositivos y sistemas, vinculando conjuntos de datos en función de los campos de identidad definidos por los esquemas XDM a los que se ajustan.
* [Perfil](../../profile/home.md)del cliente en tiempo real: Aprovecha Identity Service para crear perfiles detallados de clientes a partir de sus conjuntos de datos en tiempo real. El cliente en tiempo real extrae datos del Data Lake y mantiene los perfiles de los clientes en su propio almacén de datos independiente.
* [Servicio](../../segmentation/home.md)de segmentación de la plataforma Adobe Experience: Le permite generar segmentos y audiencias a partir de los datos de Perfil del cliente en tiempo real. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro del Data Lake.
* [Espacio de trabajo](../../data-science-workspace/home.md)de ciencias de datos de la plataforma de Adobe Experience: Utiliza aprendizaje automático e inteligencia artificial para descubrir perspectivas en grandes conjuntos de datos.
* [Servicio](../../query-service/home.md)de Consulta de la plataforma Adobe Experience: Le permite utilizar SQL estándar para la consulta de datos en la plataforma de experiencia, uniendo cualquier conjunto de datos dentro de Data Lake y capturando los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, Área de trabajo de ciencia de datos o Perfil de clientes en tiempo real.
* [Servicio](../../decisioning-service/home.md)de decisiones de Adobe Experience Platform: Aprovecha el Perfil del cliente en tiempo real para determinar la opción más probable que tomará un cliente a partir de un conjunto de opciones, en función de los datos de comportamiento que el Perfil extrae de los conjuntos de datos habilitados.

## Pasos siguientes

Al leer este documento, se le han presentado los usos principales de los conjuntos de datos en la plataforma de experiencia, así como los diversos servicios de la plataforma que utilizan conjuntos de datos. Para obtener más información sobre las muchas formas en que se utilizan los conjuntos de datos en la plataforma, consulte la documentación del servicio vinculada a través de esta información general.

Para ver los pasos sobre cómo interactuar con conjuntos de datos en la interfaz de usuario de la plataforma de experiencia, consulte la guía [del usuario de](user-guide.md)conjuntos de datos.