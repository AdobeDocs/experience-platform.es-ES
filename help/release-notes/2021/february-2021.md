---
title: 'Notas de la versión de Adobe Experience Platform: febrero de 2021'
description: Las notas de la versión de febrero de 2021 de Adobe Experience Platform.
doc-type: release notes
last-update: February 24, 2021
author: ens70167
exl-id: 8c3142af-4021-4f7e-acbd-c5277dd188d1
source-git-commit: f9917d6a6de81f98b472cff9b41f1526ea51cdae
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 22%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de publicación: jueves, 24 de febrero de 2021**

Nuevas funciones de Adobe Experience Platform:

- [Paneles (Beta)](#dashboards)

Actualizaciones de las funciones existentes en Adobe Experience Platform:

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Dataflows]](#dataflows)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM) System]](#xdm)
- [[!DNL Identity Service]](#identity)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Paneles (Beta) {#dashboards}

Adobe Experience Platform proporciona varios paneles a través de los cuales puede ver información importante acerca de los datos de su organización, tal y como se captura durante las instantáneas diarias.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Perfiles, segmentos, destinos y tableros de uso de licencias (Beta) | **Nota: Actualmente, la funcionalidad de tablero está en versión beta y no está disponible para todos los usuarios. La documentación y las funcionalidades están sujetas a cambios.**<br/><br/> Los paneles proporcionan informes listos para usar sobre los datos de su organización y están integrados directamente en el flujo de trabajo del experto en marketing dentro de Platform. Estos paneles están disponibles sin necesidad de soporte de TI adicional ni el tiempo y esfuerzo que, de lo contrario, tomaría exportar y procesar los datos con el diseño y la implementación de almacenamiento de datos adicional. |

## [!DNL Data Science Workspace] {#dsw}

El espacio de trabajo de ciencia de datos utiliza aprendizaje automático e inteligencia artificial para crear perspectivas a partir de sus datos. Integrado en Adobe Experience Platform, el espacio de trabajo de ciencia de datos le ayuda a hacer predicciones utilizando su contenido y sus recursos de datos en soluciones de Adobe.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Portátil JupyterLab EDA | El cuaderno de Python de análisis exploratorio de datos (EDA) ya está disponible en Jupyterlab. Este bloc de notas está diseñado para ayudarle a descubrir patrones en los datos, comprobar la sanidad de los datos y resumir los datos relevantes para los modelos predictivos. Consulte el tutorial sobre [explorar datos basados en web para modelos predictivos](../../data-science-workspace/jupyterlab/eda-notebook.md) para obtener más información. |

Para obtener información más general sobre Data Science Workspace, consulte la [Resumen de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Dataflows] {#dataflows}

En Adobe Experience Platform, los datos se incorporan desde una amplia variedad de fuentes, se analizan dentro de Experience Platform y se activan en una amplia variedad de destinos. Platform facilita el proceso de seguimiento de este flujo de datos potencialmente no lineal al proporcionar transparencia a los flujos de datos.

Los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Estos flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, donde luego los utiliza [!DNL Identity Service] y [!DNL Real-Time Customer Profile] antes de activarse finalmente en [!DNL Destinations].

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Nuevo panel de monitorización | Ahora puede utilizar el panel de monitorización para lograr transparencia entre servicios e información procesable para las ingestas de datos de origen. El nuevo panel de monitorización proporciona una vista completa de los datos procesados a partir de [!DNL Data Lake] hasta [!DNL Identity Service] y a [!DNL Profile], a la vez que le permite monitorizar las tasas de ingesta, los éxitos y los errores. Consulte el tutorial sobre [monitorización de flujos de datos de origen en la IU](../../dataflows/ui/monitor-sources.md) para obtener más información. |

Para obtener información más general sobre los flujos de datos, consulte la [resumen de flujos de datos](../../dataflows/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones generadas previamente con plataformas de destino que permiten la activación perfecta de datos de Adobe Experience Platform. Puede utilizar los destinos para activar los datos conocidos y desconocidos para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

**Nuevos destinos**

| Destino | Descripción |
| ----------- | ----------- |
| [[!DNL LinkedIn Matched Audiences]](../../destinations/catalog/social/linkedin.md) | El [!DNL LinkedIn Matched Audiences] permite activar audiencias en el [!DNL LinkedIn] plataforma social. |

Para obtener información más general sobre los destinos, consulte la [información general sobre destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM) System] {#xdm}

La estandarización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Interfaz de usuario de búsqueda actualizada | Las funcionalidades de búsqueda mejoradas ahora están disponibles en el [!UICONTROL Examinar] en la pestaña [!UICONTROL Esquemas] espacio de trabajo y el cuadro de diálogo de selección del grupo de campos esquema en [!DNL Schema Editor].<br><br>Al buscar un término anteriormente, los resultados solo incluirían recursos XDM cuyo nombre coincida con la consulta de búsqueda. Ahora, además de los recursos cuyo nombre coincida con la consulta, también se incluirán los recursos que contengan atributos individuales que coincidan con el término. Esto le permite buscar recursos XDM en función de los atributos que contienen en lugar de por el nombre del recurso.<br><br>Consulte los documentos sobre [exploración de recursos XDM](../../xdm/ui/explore.md) y [administración de esquemas](../../xdm/ui/resources/schemas.md) en la IU de para obtener más información. |

Para obtener información más general sobre XDM, consulte la [Información general del sistema XDM](../../xdm/home.md).

## [!DNL Identity Service] {#identity}

Para ofrecer experiencias digitales relevantes, es necesario tener una comprensión completa de su cliente. Esto se hace más difícil cuando los datos del cliente se fragmentan en sistemas dispares, lo que provoca que cada cliente individual parezca tener varias &quot;identidades&quot;.

Adobe Experience Platform [!DNL Identity Service] le ayuda a obtener una mejor vista de sus clientes y de su comportamiento al unir identidades entre dispositivos y sistemas, lo que le permite ofrecer experiencias digitales personales impactantes en tiempo real.

**Nuevas funciones**

| Función | Descripción |
| --- | --- |
| Visualizador de gráficos de identidad | El visor de gráficos de identidad le permite validar y visualizar identidades vinculadas en la interfaz de usuario, lo que permite mejorar la depuración y la transparencia. Consulte la [documento del visualizador de gráficos de identidad](../../identity-service/features/identity-graph-viewer.md) para obtener más información. |

Para obtener información más general sobre [!DNL Identity Service], consulte la [Introducción al servicio de identidad](../../identity-service/home.md).

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el perfil del cliente en tiempo real, puede ver una vista integral de cada cliente individual combinando datos de varios canales, incluidos los canales en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de los clientes en una vista unificada, lo que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

**Nuevas funciones**

| Función | Descripción |
| ------- | ----------- |
| Atributos calculados (Alpha) | ***Nota: Actualmente, esta funcionalidad está en formato alfa y no está disponible para todos los usuarios. La documentación y las funcionalidades están sujetas a cambios.*** <br/><br/>Los atributos calculados son funciones que se utilizan para agregar datos de nivel de evento en atributos de nivel de perfil. A continuación, puede utilizar los agregados en la segmentación, activación y personalización. Algunos ejemplos de estas funciones incluyen count, sum, average, min, max, true/false. Actualmente, los atributos calculados solo están disponibles mediante API. |

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] data, comience por leer el [Resumen del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

Adobe Experience Platform puede introducir datos de fuentes externas, al tiempo que le permite estructurar, etiquetar y mejorar esos datos mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

Experience Platform proporciona una API RESTful y una IU interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse y conectarse a sistemas de almacenamiento externos y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Nuevas fuentes**

| Función | Descripción |
| --- | --- |
| [!DNL Google PubSub] | Ahora puede conectarse [!DNL Google PubSub] hasta [!DNL Experience Platform] uso del [!DNL Flow Service] API para la IU de. Consulte la [[!DNL Google PubSub] descripción general del conector](../../sources/connectors/cloud-storage/google-pubsub.md) para obtener más información. |
| [!DNL Oracle Object Storage] | Ahora puede conectarse [!DNL Oracle Object Storage] hasta [!DNL Experience Platform] uso del [!DNL Flow Service] API para la IU de. Consulte la [[!DNL Oracle Object Storage] descripción general del conector](../../sources/connectors/cloud-storage/oracle-object-storage.md) para obtener más información. |

Para obtener información más general sobre las fuentes, consulte la [información general de orígenes](../../sources/home.md).
