---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión del Experience Platform 10 de septiembre de 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 5%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: 10 de septiembre de 2019**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [!DNL Data Ingestion](#ingestion)
* [!DNL Data Science Workspace](#dsw)
* [!DNL Query Service](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] ofrece varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de flujo, los conectores nativos de Adobe, los socios de integración de datos o la interfaz de usuario de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
| ----------- | ---------- |
| Nuevo dominio para la transmisión por flujo continuo de la ingesta | El dominio `dcs.data.adobe.net` se ha movido al nuevo dominio común de recopilación de datos `dcs.adobedc.net`. Los usuarios deben actualizar sus implementaciones de acuerdo con la documentación revisada sobre la transmisión de flujo continuo de Adobe Experience Platform. Se ha actualizado toda la documentación relacionada con la ingesta de flujo continuo de Adobes Experience Platform para utilizar el nuevo dominio. |

Para obtener más información, visite la documentación [de la ingestión](../../ingestion/home.md)de datos.

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] es un servicio totalmente gestionado dentro del [!DNL Experience Platform] cual permite a los científicos de datos generar sin problemas perspectivas a partir de datos y contenido en todas las soluciones de Adobe y sistemas de terceros mediante la creación y la puesta en marcha de modelos de aprendizaje automático. [!DNL Data Science Workspace] está estrechamente integrado con [!DNL Platform] y potencia el ciclo de vida completo de la ciencia de datos, incluida la exploración y preparación de datos XDM, seguido del desarrollo y la operacionalización de modelos para enriquecerse automáticamente [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Programación de servicios mediante la interfaz de usuario | Integrado con [!DNL Platform] el servicio de orquestación para automatizar la formación y la puntuación del modelo con programaciones definidas por el usuario mediante la interfaz de usuario. |
| [!DNL Service Gallery] | Explore, supervise y acceda a los servicios de aprendizaje automático con la capacidad de programar trabajos automatizados de formación y puntuación, todo ello dentro del nuevo diseño [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Mejoras en la interfaz de usuario. |

**Problemas conocidos**

* Actualmente no hay una forma accesible en la [!DNL Service Gallery] para eliminar un servicio existente. Mientras tanto, consulte la referencia [de la API de aprendizaje automático de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei para eliminar un servicio existente a través de llamadas de API.
* El [!DNL Service Gallery] no tiene soporte de paginación para filtrar las ejecuciones de puntuación y formación de un Servicio.
* Al configurar la formación programada o la puntuación se ejecuta a través del [!DNL Service Gallery], si se establece la frecuencia en cada hora se evita que se aplique la programación.

Para obtener más información, visite Información general sobre [Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] proporciona la capacidad de usar SQL estándar para consulta de datos en Adobe Experience Platform para admitir una variedad de casos de uso de análisis y gestión de datos. It is a serverless tool that allows you to join datasets from the [!DNL Data Lake] and capture the query results as a new dataset for use in reporting, [!DNL Data Science Workspace], or for ingestion into [!DNL Real-time Customer Profile].

You can use [!DNL Query Service] to build data analysis ecosystems, creating a picture of customers across their various interaction channels. Estos canales pueden incluir sistemas de punto de venta, web, móviles o CRM.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Mejoras en [!DNL Query Editor] | Se Añadió una función de guardado que le permite guardar una consulta y trabajar en ella más tarde. Se ha Añadido una ficha &quot;Examinar&quot; en la interfaz de usuario del [!DNL Query Service] Adobe Experience Platform que muestra consultas guardadas por los usuarios de la organización. Se ha implementado un panel &quot;Detalles de Consulta&quot; que muestra metadatos útiles sobre la consulta que se está viendo. |
| Nuevas funciones de atribución | Funciones definidas por Adobe en [!DNL Query Service] consulta para atribución de canales con parámetros de caducidad. |
| Mejoras en la sintaxis SQL | Compatibilidad con sintaxis iLike. |
| Generar conjuntos de datos con un Esquema XDM definido | Se ha Añadido una nueva cláusula en Crear tabla como consultas de selección (CTAS) que permite especificar un esquema de destinatario. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).