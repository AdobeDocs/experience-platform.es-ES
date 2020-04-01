---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 10 de septiembre de 2019
doc-type: release notes
last-update: September 13, 2019
author: ens28527
translation-type: tm+mt
source-git-commit: 28a8fc496c85b334e89d0f0a130d3cc5c8956399

---


# Notas de la versión de Adobe Experience Platform

## Fecha de lanzamiento: 10 de septiembre de 2019

## Ingesta de datos

Adobe Experience Platform proporciona un completo conjunto de funciones para ingestar cualquier tipo y latencia de datos. La integración de datos de la plataforma de experiencia de Adobe proporciona varias alternativas para la ingesta de datos, incluidas las API por lotes, las API de flujo, los conectores nativos de Adobe, los socios de integración de datos o la interfaz de usuario de la plataforma de experiencia de Adobe.

**Nuevas funciones**

| Función | Descripción |
| ----------- | ---------- |
| Nuevo dominio para la transmisión por flujo continuo de la ingesta | El dominio `dcs.data.adobe.net` se ha movido al nuevo dominio común de recopilación de datos `dcs.adobedc.net`. Los usuarios deben actualizar sus implementaciones de acuerdo con la documentación revisada sobre la transmisión por secuencias de Adobe Experience Platform. Se ha actualizado toda la documentación relacionada con la transmisión por secuencias de Adobe Experience Platform para utilizar el nuevo dominio. |

Para obtener más información, visite la documentación [de la ingestión](../../ingestion/home.md)de datos.

## Área de trabajo de ciencia de datos

Adobe Experience Platform Data Science Workspace es un servicio totalmente gestionado dentro de la plataforma de experiencia que permite a los científicos de datos generar sin problemas perspectivas a partir de datos y contenido en las soluciones de Adobe y en los sistemas de terceros mediante la creación y la puesta en marcha de modelos de aprendizaje automático. Data Science Workspace está estrechamente integrado con Platform y potencia el ciclo de vida completo de la ciencia de datos, incluida la exploración y preparación de datos XDM, seguido del desarrollo y la operacionalización de modelos para enriquecer automáticamente el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Programación de servicios mediante la interfaz de usuario | Integrado con el servicio de orquestación de plataformas para automatizar la formación y la puntuación del modelo con programaciones definidas por el usuario mediante la interfaz de usuario. |
| Galería de servicios | Explore, supervise y acceda a los servicios de aprendizaje automático con la capacidad de programar trabajos automatizados de formación y puntuación, todo ello dentro de la Galería de servicios rediseñada. |
| JupyterLab 5.0.0 | Mejoras en la interfaz de usuario de JupyterLab. |

**Problemas conocidos**

* Actualmente no hay una forma accesible en la Galería de servicios de eliminar un servicio existente. Mientras tanto, consulte la referencia [de la API de aprendizaje automático de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei para eliminar un servicio existente a través de llamadas de API.
* La Galería de servicios no admite paginación para filtrar las ejecuciones de puntuación y formación de un servicio.
* Al configurar la formación o puntuación programada, se ejecuta en la Galería de servicios y, al establecer la frecuencia en hora, se evita que se aplique la programación.

Para obtener más información, visite Información general sobre [Data Science Workspace](../../data-science-workspace/home.md).

## Servicio de Consulta

El servicio de Consulta ofrece la posibilidad de utilizar SQL estándar para la consulta de datos en Adobe Experience Platform para admitir una variedad de casos de uso de análisis y gestiones de datos. Se trata de una herramienta sin servidor que le permite unir conjuntos de datos desde Data Lake y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, Área de trabajo de ciencia de datos o para su inserción en el Perfil del cliente en tiempo real.

Puede utilizar el servicio de Consulta para crear ecosistemas de análisis de datos, creando una imagen de los clientes en sus distintos canales de interacción. Estos canales pueden incluir sistemas de punto de venta, web, móviles o CRM.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Mejoras en el Editor de Consultas | Se Añadió una función de guardado que le permite guardar una consulta y trabajar en ella más tarde. Se ha Añadido una ficha &quot;Examinar&quot; en la interfaz de usuario del servicio de Consulta de la plataforma Adobe Experience que muestra consultas guardadas por los usuarios de la organización. Se ha implementado un panel &quot;Detalles de Consulta&quot; que muestra metadatos útiles sobre la consulta que se está viendo. |
| Nuevas funciones de atribución | Funciones definidas por Adobe en Consulta Service a consulta para atribución de canales con parámetros de caducidad. |
| Mejoras en la sintaxis SQL | Compatibilidad con sintaxis iLike. |
| Generar conjuntos de datos con un Esquema XDM definido | Se ha Añadido una nueva cláusula en Crear tabla como consultas de selección (CTAS) que permite especificar un esquema de destinatario. |

For more information, refer to the [Query Service documentation](../../query-service/home.md).