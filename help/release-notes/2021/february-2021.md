---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform para el 24 de febrero de 2021.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 7%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: 24 de febrero de 2021**

Nuevas funciones de Adobe Experience Platform:

- [Tableros (Beta)](#dashboards)

Actualizaciones de funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## (Beta) Tableros {#dashboards}

Adobe Experience Platform proporciona varios tableros a través de los cuales puede ver información importante sobre los datos de su organización, tal como se captura durante las instantáneas diarias.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Perfiles, segmentos, destinos y tableros de uso de licencias (Beta) | **Nota: La funcionalidad del panel está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.**<br/><br/> Los tableros proporcionan informes integrados sobre los datos de su organización y están integrados directamente en el flujo de trabajo de los especialistas en marketing dentro de Platform. Estos tableros están disponibles sin necesidad de soporte de TI adicional o sin el tiempo y esfuerzo que de otro modo se necesitarían para exportar y procesar datos con diseño e implementación adicionales de almacenamiento de datos. |

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, Data Science Workspace le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Portátil JupyterLab EDA | El bloc de notas Python de análisis de datos exploratorios (EDA) ya está disponible en Jupyterlab. Este bloc de notas está diseñado para ayudarle a descubrir patrones en los datos, comprobar la solidez de los datos y resumir los datos relevantes para los modelos predictivos. Consulte el tutorial sobre [exploración de datos basados en web para modelos predictivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obtener más información. |

Para obtener información más general sobre Data Science Workspace, consulte [Información general sobre Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

En Adobe Experience Platform, los datos se incorporan a partir de una amplia variedad de fuentes, se analizan en el Experience Platform y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia con flujos de datos.

Los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Estos flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, donde se utilizan en [!DNL Identity Service] y [!DNL Real-time Customer Profile] antes de activarse en [!DNL Destinations].

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Nuevo panel de monitorización | Ahora puede utilizar el panel de monitorización para la transparencia entre servicios y perspectivas procesables para la ingesta de datos de origen. El nuevo panel de monitorización proporciona una vista completa de los datos procesados de [!DNL Data Lake] a [!DNL Identity Service] y a [!DNL Profile], a la vez que le permite monitorizar las tasas de ingesta, los éxitos y los errores. Consulte el tutorial sobre [monitorización de flujos de datos de origen en la interfaz de usuario](../../dataflows/ui/monitor-sources.md) para obtener más información. |

Para obtener información más general sobre los flujos de datos, consulte la [descripción general de los flujos de datos](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar destinos para activar los datos conocidos y desconocidos en campañas de marketing en canales múltiples, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | La conexión [!DNL LinkedIn Matched Audiences] permite activar audiencias en la plataforma social [!DNL LinkedIn]. |

Para obtener información más general sobre los destinos, consulte [información general sobre destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Interfaz de usuario de búsqueda actualizada | Las funciones de búsqueda mejoradas ahora están disponibles en la pestaña [!UICONTROL Browse] del espacio de trabajo [!UICONTROL Schemas] y en el cuadro de diálogo de selección del grupo de campos de esquema en [!DNL Schema Editor].<br><br>Al buscar un término anteriormente, los resultados solo incluirían recursos XDM cuyo nombre coincida con la consulta de búsqueda. Ahora, además de los recursos cuyo nombre coincide con la consulta, también se incluyen los recursos que contienen atributos individuales que coinciden con el término. Esto le permite buscar recursos XDM en función de los atributos que contienen en lugar de por el nombre del recurso.<br><br>Consulte los documentos sobre la  [exploración de los ](../../xdm/ui/explore.md) recursos XDM y la  [administración de ](../../xdm/ui/resources/schemas.md) esquemas en la interfaz de usuario para obtener más información. |

Para obtener información más general sobre XDM, consulte [Información general del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

La entrega de experiencias digitales relevantes requiere una comprensión completa de su cliente. Esto se hace más difícil cuando los datos de sus clientes están fragmentados en distintos sistemas, lo que hace que cada cliente individual parezca tener múltiples &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor visión de su cliente y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales y impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Visor de gráficos de identidad | El visor de gráficos de identidad permite validar y visualizar identidades vinculadas en la interfaz de usuario, lo que permite mejorar la depuración y la transparencia. Consulte el [documento del visor de gráficos de identidad](../../identity-service/ui/identity-graph-viewer.md) para obtener más información. |

Para obtener información más general sobre [!DNL Identity Service], consulte la [descripción general del servicio de identidad](../../identity-service/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de los clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Atributos calculados (alfa) | ***Nota: Esta funcionalidad se encuentra en fase alfa y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.*** <br/><br/>Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. A continuación, puede utilizar los agregados en segmentación, activación y personalización. Algunos ejemplos de estas funciones son count, sum, average, min, max, true/false. Actualmente, los atributos calculados están disponibles solo mediante API. Para obtener más información, consulte la [descripción general de los atributos calculados](../../profile/computed-attributes/overview.md). |

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos [!DNL Profile], lea en primer lugar la [información general del Perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas, al mismo tiempo que le permite estructurarlos, etiquetarlos y mejorarlos mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas fuentes**

| Función | Descripción |
| --- | --- |
| [!DNL Google PubSub] | Ahora puede conectar [!DNL Google PubSub] a [!DNL Experience Platform] mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [[!DNL Google PubSub] descripción general del conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obtener más información. |
| [!DNL Oracle Object Storage] | Ahora puede conectar [!DNL Oracle Object Storage] a [!DNL Experience Platform] mediante la API [!DNL Flow Service] o la interfaz de usuario. Consulte la [[!DNL Oracle Object Storage] descripción general del conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obtener más información. |

Para obtener información más general sobre las fuentes, consulte [sources overview](../../sources/home.md).
