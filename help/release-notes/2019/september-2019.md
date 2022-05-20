---
title: Notas de la versión de Adobe Experience Platform, septiembre de 2019
description: Notas de la versión de septiembre de 2019 para Adobe Experience Platform.
doc-type: release notes
last-update: September 13, 2019
author: ens28527
exl-id: 7f503046-a3b4-4fdb-833c-4205b6e9fa04
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 5%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de versión: 10 de septiembre de 2019**

Actualizaciones de funciones existentes en Adobe Experience Platform:

* [[!DNL Data Ingestion]](#ingestion)
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Query Service]](#query)

## [!DNL Data Ingestion] {#ingestion}

Adobe Experience Platform proporciona un completo conjunto de funciones para ingerir cualquier tipo y latencia de datos. Adobe Experience Platform [!DNL Data Ingestion] proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de transmisión, los conectores de Adobe nativos, los socios de integración de datos o la IU de Adobe Experience Platform.

**Nuevas funciones**

| Función | Descripción |
| ----------- | ---------- |
| Nuevo dominio para la transmisión por secuencias de ingesta | La variable `dcs.data.adobe.net` se ha trasladado al nuevo dominio común de recopilación de datos `dcs.adobedc.net`. Los usuarios deben actualizar sus implementaciones según la documentación revisada de ingesta de flujo continuo de Adobe Experience Platform. Toda la documentación relacionada con la ingesta de flujo continuo de Adobe Experience Platform se ha actualizado para utilizar el nuevo dominio. |

Para obtener más información, consulte la [Documentación de ingesta de datos](../../ingestion/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] es un servicio completamente administrado dentro de [!DNL Experience Platform] que permite a los científicos de datos generar perspectivas a partir de datos y contenido sin problemas en soluciones de Adobe y sistemas de terceros creando y operacionalizando modelos de aprendizaje automático. [!DNL Data Science Workspace] está estrechamente integrado con [!DNL Platform] y potencia el ciclo de vida completo de la ciencia de datos, incluida la exploración y preparación de datos XDM, seguido del desarrollo y la operacionalización de modelos para enriquecer automáticamente [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Programación de servicios mediante la interfaz de usuario | Integrado con [!DNL Platform] Servicio de organización para automatizar la formación y puntuación del modelo con programas definidos por el usuario mediante la interfaz de usuario. |
| [!DNL Service Gallery] | Examine, supervise y acceda a los servicios de aprendizaje automático con la capacidad de programar trabajos automatizados de formación y puntuación, todo ello dentro del nuevo diseño [!DNL Service Gallery]. |
| [!DNL JupyterLab] 5.0.0 | [!DNL JupyterLab] Mejoras en la interfaz de usuario. |

**Problemas conocidos**

* Actualmente no hay manera accesible en la variable [!DNL Service Gallery] para eliminar un servicio existente. Mientras tanto, consulte la [Referencia de la API de aprendizaje automático de Sensei](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para eliminar un servicio existente mediante llamadas a la API.
* La variable [!DNL Service Gallery] no es compatible con paginación para filtrar las ejecuciones de capacitación y puntuación de un Servicio.
* Al configurar la formación o puntuación programada, se ejecuta a través de la variable [!DNL Service Gallery], establecer la frecuencia en por hora evita que se aplique la programación.

Para obtener más información, consulte la [Información general de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Query Service] {#query}

[!DNL Query Service] proporciona la capacidad de usar SQL estándar para consultar datos en Adobe Experience Platform para admitir una variedad de casos de uso de análisis y administración de datos. Es una herramienta sin servidor que le permite unir conjuntos de datos desde la variable [!DNL Data Lake] y captar los resultados de la consulta como un nuevo conjunto de datos para su uso en los informes, [!DNL Data Science Workspace]o para su ingesta en [!DNL Real-time Customer Profile].

Puede usar [!DNL Query Service] para crear ecosistemas de análisis de datos, crear una imagen de los clientes en sus distintos canales de interacción. Estos canales pueden incluir sistemas de puntos de venta, web, móviles o CRM.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Mejoras en [!DNL Query Editor] | Se ha agregado una función de guardado que permite guardar una consulta y trabajar en ella más adelante. Se ha añadido la pestaña &quot;Examinar&quot; a la sección [!DNL Query Service] interfaz de usuario de Adobe Experience Platform que muestra las consultas guardadas por los usuarios de su organización. Se ha implementado un panel &quot;Detalles de consulta&quot; que muestra metadatos útiles sobre la consulta que se está viendo. |
| Nuevas funciones de atribución | funciones definidas por Adobe en [!DNL Query Service] para consultar la atribución de canal con parámetros de caducidad. |
| Mejoras en la sintaxis SQL | Compatibilidad con sintaxis iLike. |
| Generar conjuntos de datos con un esquema XDM definido | Se ha añadido una nueva cláusula en las consultas Crear tabla como selección (CTAS) que permite especificar un esquema de objetivo. |

Para obtener más información, consulte [Documentación del servicio de consultas](../../query-service/home.md).
