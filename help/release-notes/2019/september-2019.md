---
title: 'Notas de la versión de Adobe Experience Platform: septiembre de 2019'
description: Las notas de la versión de septiembre de 2019 de Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: 863889984e5e77770638eb984e129e720b3d4458
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: miércoles, 10 de septiembre de 2019**

Actualizaciones de las funciones existentes en Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para introducir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de streaming, los conectores de Adobe nativos, los socios de integración de datos o la interfaz de usuario de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
| ----------- | ---------- |
| Nuevo dominio para la ingesta de transmisión | El dominio `dcs.data.adobe.net` se ha movido al nuevo dominio común de recopilación de datos `dcs.adobedc.net`. Los usuarios deben actualizar sus implementaciones según la documentación revisada de ingesta de transmisión de Adobe Experience Platform. Toda la documentación relacionada con la introducción de la transmisión por secuencias de Adobe Experience Platform se ha actualizado para utilizar el nuevo dominio. |

Para obtener más información, visite la [Documentación de ingesta de datos](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] es un servicio totalmente administrado en [!DNL Experience Platform] que permite a los científicos de datos generar sin problemas perspectivas a partir de datos y contenido en soluciones de Adobe y sistemas de terceros mediante la creación y puesta en funcionamiento de modelos de aprendizaje automático. [!DNL Data Science Workspace] está totalmente integrado con [!DNL Platform] y potencia el ciclo vital de la ciencia de datos de extremo a extremo, incluida la exploración y preparación de datos XDM, seguida del desarrollo y la operacionalización de modelos para enriquecer automáticamente [!DNL Real-Time Customer Profile] con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Programación de servicios mediante la interfaz de usuario | Integrado con el servicio de orquestación [!DNL Platform] para automatizar la formación y puntuación del modelo con programaciones definidas por el usuario mediante la interfaz de usuario. |
| [!DNL Service Gallery] | Examine, supervise y acceda a los servicios de aprendizaje automático con la capacidad de programar trabajos de puntuación y formación automatizados, todo ello dentro de los [!DNL Service Gallery] rediseñados. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] mejoras en la IU. |

**Problemas conocidos**

* Actualmente no hay ninguna forma accesible en [!DNL Service Gallery] de eliminar un servicio existente. Mientras tanto, consulte la [referencia de la API de aprendizaje automático de Sensei](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) para eliminar un servicio existente mediante llamadas a la API.
* [!DNL Service Gallery] no tiene compatibilidad de paginación para filtrar las ejecuciones de puntuación y aprendizaje de un servicio.
* Al configurar la formación programada o las ejecuciones de puntuación a través de [!DNL Service Gallery], establecer la frecuencia en cada hora evita que se aplique la programación.

Para obtener más información, visite [Información general de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] proporciona la capacidad de usar SQL estándar para consultar datos en Adobe Experience Platform con el fin de admitir una variedad de casos de uso de análisis y administración de datos. Es una herramienta sin servidor que le permite unirse a conjuntos de datos de [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, [!DNL Data Science Workspace], o para su ingesta en [!DNL Real-Time Customer Profile].

Puede usar [!DNL Query Service] para generar ecosistemas de análisis de datos creando una imagen de los clientes en sus diversos canales de interacción. Estos canales pueden incluir sistemas de puntos de venta, web, móviles o CRM.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Mejoras en [!DNL Query Editor] | Se ha añadido una función de guardado que le permite guardar una consulta y trabajar en ella más adelante. Se ha agregado una ficha &quot;Examinar&quot; a la interfaz de usuario [!DNL Query Service] en Adobe Experience Platform que muestra las consultas guardadas por los usuarios de su organización. Se ha implementado un panel &quot;Detalles de la consulta&quot; que muestra metadatos útiles sobre la consulta que se está viendo. |
| Nuevas funciones de atribución | Funciones definidas por el Adobe en [!DNL Query Service] para consultar la atribución de canal con parámetros de caducidad. |
| Mejoras en la sintaxis SQL | Compatibilidad con la sintaxis iLike. |
| Generar conjuntos de datos con un esquema XDM definido | Se ha añadido una nueva cláusula en Crear tabla como consultas de selección (CTAS) que le permite especificar un esquema de destino. |

Para obtener más información, consulte la [documentación del servicio de consultas](../../query-service/home.md).
