---
keywords: Experience Platform;inicio;temas populares;CJA;análisis de recorrido;análisis de recorrido del cliente;orquestación de campaña;orquestación;recorrido del cliente;recorrido;orquestación de recorrido;capacidad;región
title: Flujo de trabajo de ejemplo completo de Adobe Experience Platform
description: Conozca el flujo de trabajo completo básico para Adobe Experience Platform de alto nivel.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Flujo de trabajo de ejemplo completo de Adobe Experience Platform

Adobe Experience Platform es el sistema más potente, flexible y abierto del mercado para crear y administrar soluciones completas que mejoren la experiencia del cliente. Platform les permite a las organizaciones centralizar y estandarizar los datos y el contenido de los clientes de cualquier sistema y aplicar la ciencia de datos y el aprendizaje automático para mejorar en gran medida el diseño y el envío de las experiencias personalizadas enriquecidas.

Platform, que se basa en las API de RESTful, expone toda la funcionalidad del sistema a los desarrolladores, lo que permite integrar fácilmente las soluciones empresariales con herramientas familiares. Platform le permite obtener una vista integral de sus clientes mediante la ingesta de datos de clientes, la segmentación de datos a las audiencias a las que desea dirigirse y la activación de estas audiencias en un destino externo. El siguiente tutorial muestra un flujo de trabajo completo con todos los pasos desde la ingesta a través de fuentes hasta la activación de audiencia a través de destinos.

![Flujo de trabajo de extremo a extremo del Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Primeros pasos

Este flujo de trabajo completo utiliza varios servicios de Adobe Experience Platform. A continuación se muestra una lista de los servicios que se utilizan en este flujo de trabajo con vínculos a sus descripciones generales:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco estandarizado mediante el cual [!DNL Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que sus datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): Proporciona una vista completa de los clientes y su comportamiento al unir identidades entre dispositivos y sistemas.
- [Fuentes](../sources/home.md): [!DNL Experience Platform] permite la ingesta de datos desde varias fuentes, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] permite dividir los datos almacenados en [!DNL Experience Platform] que se relaciona con individuos (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.
- [Conjuntos de datos](../catalog/datasets/overview.md): la construcción de almacenamiento y administración para la persistencia de datos en [!DNL Experience Platform].
- [Destinos](../destinations/home.md): los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing entre canales, campañas por correo electrónico, publicidad segmentada y muchos otros casos de uso.

## Creación de un esquema XDM

Antes de introducir datos en Platform, primero debe crear un esquema XDM para describir la estructura de esos datos. Cuando introduzca los datos en el siguiente paso, asignará los datos entrantes a este esquema. Para aprender a crear un esquema XDM de ejemplo, lea el tutorial sobre [creación de un esquema con el Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

El tutorial anterior muestra cómo establecer campos de identidad para los esquemas. Un campo de identidad representa un campo que se puede utilizar para identificar a una persona individual relacionada con un registro o un evento de serie temporal. Los campos de identidad son un componente crucial en la forma en que se construyen los gráficos de identidad de los clientes en Platform, lo que en última instancia afecta a la forma en que el Perfil del cliente en tiempo real combina fragmentos de datos dispares para obtener una vista completa del cliente. Para obtener más información sobre cómo ver gráficos de identidad en Platform, consulte el tutorial sobre [cómo utilizar el visualizador de gráficos de identidad](../identity-service/ui/identity-graph-viewer.md).

Debe habilitar el esquema para utilizarlo en el perfil del cliente en tiempo real, de modo que los perfiles de los clientes se puedan crear a partir de los datos basados en el esquema. Consulte la sección sobre [habilitar un esquema para el perfil](../xdm/ui/resources/schemas.md#profile) en la guía de la interfaz de usuario de esquemas para obtener más información.

## Ingesta de datos en Platform

Una vez creado un esquema XDM, puede empezar a introducir los datos en el sistema.

Todos los datos introducidos en Platform se almacenan en conjuntos de datos individuales al ingerirlos. Un conjunto de datos es una colección de registros de datos que se asignan a un esquema XDM específico. Antes de que los datos puedan ser utilizados por [!DNL Real-Time Customer Profile], el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas sobre cómo habilitar un conjunto de datos para el perfil, consulte la [Guía de IU de conjuntos de datos](../catalog/datasets/user-guide.md#enable-profile) y el [tutorial de API de configuración de conjuntos de datos](../profile/tutorials/dataset-configuration.md). Una vez configurado el conjunto de datos, puede empezar a introducir datos en él.

Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras. Por ejemplo, puede introducir los datos utilizando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Puede encontrar una lista completa de las fuentes disponibles en la [descripción general de conectores de origen](../sources/home.md).

Si utiliza Amazon S3 como conector de origen, puede seguir las instrucciones del tutorial de API sobre [creación de un conector de Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) o el tutorial de la IU sobre [creación de un conector de Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) para obtener información sobre cómo crear, conectarse e introducir datos dentro del conector.

Para obtener instrucciones más detalladas sobre los conectores de origen, lea la [descripción general de conectores de origen](../sources/home.md). Para obtener más información sobre Flow Service, la API en la que se basan las fuentes, lea la [Referencia de API de Flow Service](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Una vez que los datos se llevan a Platform a través del conector de origen y se almacenan en el conjunto de datos habilitado para perfiles, los perfiles de cliente se crean automáticamente en función de los datos de identidad configurados en el esquema XDM.

Al cargar datos en un nuevo conjunto de datos por primera vez, o al configurar un nuevo proceso de ETL o fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente y de que los perfiles generados contienen los datos esperados. Para obtener más información sobre cómo acceder a los perfiles de los clientes en la interfaz de usuario de Platform, consulte [Guía de la IU del perfil del cliente en tiempo real](../profile/ui/user-guide.md). Para obtener más información sobre cómo acceder a los perfiles mediante la API de perfil del cliente en tiempo real, consulte la guía de [uso del extremo de entidades](../profile/api/entities.md).

## Evaluación de los datos

Una vez que haya generado correctamente perfiles a partir de los datos ingeridos, puede evaluar los datos mediante la segmentación. La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de personas desde el almacén de perfiles, con el fin de distinguir un grupo comercializable de personas de su base de clientes. Para obtener más información sobre la segmentación, lea la [resumen del servicio de segmentación](../segmentation/home.md).

### Creación de una definición de segmento

Para empezar, debe crear una definición de segmento para agrupar a los clientes y crear la audiencia de destino. Una definición de segmento es un conjunto de reglas que puede utilizar para definir la audiencia a la que desea dirigirse. Para crear una definición de segmento, puede seguir las instrucciones de la guía de la interfaz de usuario sobre el uso de [Generador de segmentos](../segmentation/ui/segment-builder.md) o el tutorial de API sobre [creación de segmentos](../segmentation/tutorials/create-a-segment.md).

Una vez que haya creado una definición de segmento, asegúrese de tomar nota del ID de definición del segmento.

### Evaluación de la definición del segmento

Después de crear la definición del segmento, puede crear un trabajo de segmento para evaluar el segmento como una instancia única o crear una programación para evaluar el segmento de forma continua.

Para evaluar una definición de segmento bajo demanda, puede crear un trabajo de segmento. Un trabajo de segmentación es un proceso asíncrono que crea un nuevo segmento de audiencia basado en la definición del segmento referido y las políticas de combinación. Una política de combinación es un conjunto de reglas que Platform utiliza para determinar qué datos se utilizarán para crear perfiles de clientes y qué datos se priorizarán cuando haya discrepancias entre las fuentes. Para aprender a trabajar con las políticas de combinación, consulte la [guía de IU de políticas de combinación](../profile/merge-policies/ui-guide.md).

Una vez creado y evaluado el trabajo de segmentación, puede obtener información sobre el segmento, como el tamaño de la audiencia o los errores que pueden haberse producido durante el procesamiento. Para obtener información sobre cómo crear un trabajo de segmentación, incluidos todos los detalles que necesita proporcionar, lea la [guía para desarrolladores de trabajos de segmentación](../segmentation/api/segment-jobs.md).

Para evaluar una definición de segmento de forma continua, puede crear y activar una programación. Una programación es una herramienta que se puede utilizar para ejecutar automáticamente un trabajo de segmento una vez al día a una hora especificada. Para obtener información sobre cómo crear y habilitar una programación, puede seguir las instrucciones de la guía de API en la [extremo de programaciones](../segmentation/api/schedules.md).

## Exportación de los datos evaluados

Después de crear el trabajo de segmento único o la programación en curso, puede crear un trabajo de exportación de segmentos para exportar los resultados a un conjunto de datos o exportar los resultados a un destino. Las secciones siguientes proporcionan directrices sobre ambas opciones.

### Exportar los datos evaluados a un conjunto de datos

Después de crear el trabajo de segmento único o la programación en curso, puede exportar los resultados creando un trabajo de exportación de segmentos. Un trabajo de exportación de segmentos es una tarea asincrónica que envía información sobre la audiencia evaluada a un conjunto de datos.

Antes de crear un trabajo de exportación, primero debe crear un conjunto de datos al que exportar los datos. Para obtener información sobre cómo crear un conjunto de datos, lea la sección sobre [creación de un conjunto de datos de destinatario](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) en el tutorial sobre la evaluación de un segmento, asegúrese de anotar el ID del conjunto de datos después de la creación. Después de crear un conjunto de datos, puede crear un trabajo de exportación. Para aprender a crear un trabajo de exportación, puede seguir las instrucciones de la guía de API en la [extremo de trabajos de exportación](../segmentation/api/export-jobs.md).

### Exportar los datos evaluados a un destino

Como alternativa, después de crear el trabajo de segmentación única o la programación en curso, puede exportar los resultados a un destino. Un destino es un punto final, como una aplicación de Adobe en un servicio externo, donde se puede activar y enviar una audiencia. Puede encontrar una lista completa de los destinos disponibles en la [catálogo de destinos](../destinations/catalog/overview.md).

Para obtener instrucciones sobre cómo activar datos en destinos de marketing por lotes o por correo electrónico, consulte el tutorial sobre [Obtenga información sobre cómo activar datos de audiencia en destinos de exportación de perfiles por lotes mediante la IU de Platform](../destinations/ui/activate-batch-profile-destinations.md) y el [guía sobre cómo conectarse a destinos por lotes y activar datos mediante la API de Flow Service](../destinations/api/connect-activate-batch-destinations.md).

## Monitorización de las actividades de datos de Platform

Platform le permite hacer un seguimiento de cómo se procesan los datos mediante el uso de flujos de datos, que son representaciones de trabajos que mueven datos entre los distintos componentes de Platform. Estos flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, donde luego los utiliza [!DNL Identity Service] y [!DNL Real-Time Customer Profile] antes de activarse finalmente en los destinos. El panel de monitorización le proporciona una representación visual del recorrido de un flujo de datos. Para obtener información sobre cómo monitorizar los flujos de datos dentro de la interfaz de usuario de Platform, consulte los tutoriales de [monitorización de flujos de datos para orígenes](../dataflows/ui/monitor-sources.md) y [monitorización de flujos de datos para destinos](../dataflows/ui/monitor-destinations.md).

También puede monitorizar las actividades de la Platform mediante el uso de métricas estadísticas y notificaciones de eventos mediante [!DNL Observability Insights]. Puede suscribirse a las notificaciones de alerta a través de la interfaz de usuario de Platform o enviarlas a un webhook configurado. Para obtener más información sobre cómo ver, habilitar, deshabilitar y suscribirse a las alertas disponibles en la interfaz de usuario de Experience Platform, consulte la [[!UICONTROL Alertas] Guía de IU](../observability/alerts/ui.md). Para obtener más información sobre cómo recibir alertas a través de webhooks, consulte la guía de [suscripción a notificaciones de eventos de Adobe I/O](../observability/alerts/subscribe.md).

## Pasos siguientes

Al leer este tutorial, se le ha dado una introducción básica a un flujo completo simple para Platform. Para obtener más información sobre Adobe Experience Platform, lea la [Información general de plataforma](./home.md). Para obtener más información sobre el uso de la IU de Platform y la API de Platform, lea la [Guía de IU de Platform](./ui-guide.md) y el [Guía de API de Platform](./api-guide.md) respectivamente.
