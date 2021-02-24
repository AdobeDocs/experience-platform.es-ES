---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform del 24 de febrero de 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
translation-type: tm+mt
source-git-commit: 7142d13b144f34d92087affe101c5ccfcb52d90e
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 6%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 24 de febrero de 2021**

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Sources]](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de los datos. Integrado en Adobe Experience Platform, Área de trabajo de ciencia de datos le ayuda a realizar predicciones con sus recursos de contenido y datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Portátil JupyterLab EDA | El portátil Python de análisis de datos exploratoria (EDA) ya está disponible en Jupyterlab. Este bloc de notas está diseñado para ayudarle a descubrir patrones en los datos, comprobar la integridad de los datos y resumir los datos relevantes para modelos predictivos. Consulte el tutorial sobre [exploración de datos basados en Web para modelos predictivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obtener más información. |

Para obtener información más general sobre el área de trabajo de ciencias de datos, consulte la [información general del área de trabajo de ciencias de datos](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

En Adobe Experience Platform, los datos se ingieren desde una amplia variedad de fuentes, se analizan en el Experience Platform y se activan en una amplia variedad de destinos. La plataforma facilita el proceso de seguimiento de este flujo potencialmente no lineal de datos al proporcionar transparencia con flujos de datos.

Los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Estos flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destinatario, donde luego se utilizan [!DNL Identity Service] y [!DNL Real-time Customer Profile] antes de activarse en [!DNL Destinations].

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Nuevo panel de supervisión | Ahora puede utilizar el panel de supervisión para la transparencia entre servicios y perspectivas procesables para las ingestas de datos de origen. El nuevo panel de monitoreo proporciona una vista integral de los datos procesados de [!DNL Data Lake] a [!DNL Identity Service] y a [!DNL Profile], a la vez que le permite monitorear las tasas de ingestión, los éxitos y los errores. Consulte el tutorial sobre [monitoreo de flujos de datos de origen en la interfaz de usuario](../../dataflows/ui/monitor-sources.md) para obtener más información. |

Para obtener información más general sobre flujos de datos, consulte la [información general de flujos de datos](../../dataflows/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Interfaz de usuario de búsqueda actualizada | Las funciones de búsqueda mejoradas ahora están disponibles en la ficha [!UICONTROL Examinar] del espacio de trabajo [!UICONTROL Esquemas] y en el cuadro de diálogo de selección de mezcla de [!DNL Schema Editor].<br><br>Al buscar un término anteriormente, los resultados solo incluirían recursos XDM cuyo nombre coincida con la consulta de búsqueda. Ahora, además de los recursos cuyo nombre coincide con la consulta, también se incluirán los recursos que contengan atributos individuales que coincidan con el término. Esto le permite buscar recursos XDM en función de los atributos que contienen en lugar de por el nombre del recurso.<br><br>Consulte los documentos para  [explorar ](../../xdm/ui/explore.md) los recursos XDM y  [administrar ](../../xdm/ui/resources/schemas.md) esquemas en la interfaz de usuario para obtener más información. |

Para obtener información más general sobre XDM, consulte la [información general del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de los clientes se fragmentan en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de su cliente y su comportamiento al unir identidades entre dispositivos y sistemas, permitiéndole ofrecer experiencias digitales personales y impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Visor de gráficos de identidad | El visor de gráficos de identidad le permite validar y visualizar identidades que se unen en la interfaz de usuario, lo que permite mejorar la depuración y la transparencia. Consulte el [documento del visor de gráficos de identidad](../../identity-service/ui/identity-graph-viewer.md) para obtener más información. |

Para obtener más información general sobre [!DNL Identity Service], consulte la [información general del servicio de identidad](../../identity-service/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Nuevas fuentes**

| Función | Descripción |
| --- | --- |
| [!DNL Google PubSub] | Ahora puede conectar [!DNL Google PubSub] a [!DNL Experience Platform] mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [[!DNL Google PubSub] descripción general del conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obtener más información. |
| [!DNL Oracle Object Storage] | Ahora puede conectar [!DNL Oracle Object Storage] a [!DNL Experience Platform] mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [[!DNL Oracle Object Storage] descripción general del conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obtener más información. |

Para obtener información más general sobre las fuentes, consulte la [información general de las fuentes](../../sources/home.md).
