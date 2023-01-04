---
keywords: Experience Platform;inicio;temas populares;CJA;análisis de recorrido;análisis de recorrido del cliente;organización de campañas;organización;recorrido del cliente;recorrido;orquestación de recorrido;capacidad;región
title: Flujo de trabajo de ejemplo completo de Adobe Experience Platform
topic-legacy: getting started
description: Conozca el flujo de trabajo básico de principio a fin para Adobe Experience Platform en un nivel superior.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1836'
ht-degree: 3%

---

# Flujo de trabajo de ejemplo completo de Adobe Experience Platform

Adobe Experience Platform es el sistema más potente, flexible y abierto del mercado para crear y administrar soluciones completas que mejoren la experiencia del cliente. Platform les permite a las organizaciones centralizar y estandarizar los datos y el contenido de los clientes de cualquier sistema y aplicar la ciencia de datos y el aprendizaje automático para mejorar en gran medida el diseño y el envío de las experiencias personalizadas enriquecidas.

Basada en las API de RESTful, Platform expone toda la funcionalidad del sistema a los desarrolladores, lo que permite la fácil integración de las soluciones empresariales mediante herramientas familiares. Platform le permite obtener una vista holística de sus clientes mediante la ingesta de datos de sus clientes, la segmentación de sus datos en las audiencias a las que desee dirigirse y la activación de estas audiencias en un destino externo. El siguiente tutorial muestra un flujo de trabajo completo que muestra todos los pasos, desde la ingesta a través de fuentes hasta la activación de audiencias mediante destinos.

![Experience Platform de flujo de trabajo completo](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Primeros pasos

Este flujo de trabajo completo utiliza varios servicios de Adobe Experience Platform. A continuación se muestra una lista de los servicios que se utilizan en este flujo de trabajo con vínculos a sus descripciones generales:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente. Para utilizar mejor la segmentación, asegúrese de que los datos se incorporan como perfiles y eventos según el [prácticas recomendadas para el modelado de datos](../xdm/schema/best-practices.md).
- [[!DNL Identity Service]](../identity-service/home.md): Proporciona una vista completa de sus clientes y su comportamiento al unir identidades entre dispositivos y sistemas.
- [Fuentes](../sources/home.md): [!DNL Experience Platform] permite la ingesta de datos de varias fuentes, al mismo tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] permite dividir los datos almacenados en [!DNL Experience Platform] que se relaciona con individuos (como clientes, posibles clientes, usuarios u organizaciones) en grupos más pequeños.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.
- [Conjuntos de datos](../catalog/datasets/overview.md): La construcción de almacenamiento y administración para la persistencia de datos en [!DNL Experience Platform].
- [Destinos](../destinations/home.md): Los destinos son integraciones prediseñadas con aplicaciones de uso común que permiten la activación perfecta de datos de Platform para campañas de marketing multicanal, campañas de correo electrónico, publicidad de destino y muchos otros casos de uso.

## Creación de un esquema XDM

Antes de ingerir datos en Platform, primero debe crear un esquema XDM para describir la estructura de esos datos. Al introducir los datos en el siguiente paso, asignará los datos entrantes a este esquema. Para aprender a crear un esquema XDM de ejemplo, lea el tutorial sobre [creación de un esquema con el Editor de esquemas](../xdm/tutorials/create-schema-ui.md).

El tutorial anterior muestra cómo definir los campos de identidad para los esquemas. Un campo de identidad representa un campo que puede utilizarse para identificar a una persona individual relacionada con un registro o un evento de serie temporal. Los campos de identidad son un componente crucial de la forma en que se construyen los gráficos de identidad de los clientes en Platform, que en última instancia afecta a cómo el perfil del cliente en tiempo real combina distintos fragmentos de datos para obtener una vista completa del cliente. Para obtener más información sobre cómo ver los gráficos de identidad en Platform, consulte el tutorial sobre [cómo utilizar el visor de gráficos de identidad](../identity-service/ui/identity-graph-viewer.md).

Debe habilitar el esquema para utilizarlo en el perfil del cliente en tiempo real de modo que los perfiles del cliente se puedan crear a partir de los datos basados en el esquema. Consulte la sección sobre [activación de un esquema para Perfil](../xdm/ui/resources/schemas.md#profile) en la guía de la interfaz de usuario de esquemas para obtener más información.

## Ingesta de datos en Platform

Una vez creado un esquema XDM, puede empezar a introducir los datos en el sistema.

Todos los datos introducidos en Platform se almacenan en conjuntos de datos individuales tras su incorporación. Un conjunto de datos es una colección de registros de datos que se asignan a un esquema XDM específico. Antes de que sus datos puedan ser utilizados por [!DNL Real-Time Customer Profile], el conjunto de datos en cuestión debe configurarse específicamente. Para obtener instrucciones completas sobre cómo habilitar un conjunto de datos para Perfil, consulte la [Guía de la interfaz de usuario de conjuntos de datos](../catalog/datasets/user-guide.md#enable-profile) y [tutorial de API de configuración del conjunto de datos](../profile/tutorials/dataset-configuration.md). Una vez configurado el conjunto de datos, puede empezar a introducir datos en él.

Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras. Por ejemplo, puede ingerir los datos utilizando [Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md). Puede encontrar una lista completa de las fuentes disponibles en la [información general sobre conectores de origen](../sources/home.md).

Si utiliza Amazon S3 como conector de origen, puede seguir las instrucciones del tutorial de API en [creación de un conector Amazon S3](../sources/tutorials/api/create/cloud-storage/s3.md) o el tutorial de IU en [creación de un conector Amazon S3](../sources/tutorials/ui/create/cloud-storage/s3.md) para aprender a crear, conectar e introducir datos en el conector.

Para obtener instrucciones más detalladas sobre conectores de origen, lea la [información general sobre conectores de origen](../sources/home.md). Para obtener más información sobre el servicio de flujo, la API de la que se basan las fuentes, lea la [Referencia de la API del servicio de flujo](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Una vez que los datos llegan a Platform a través del conector de origen y se almacenan en el conjunto de datos habilitado para perfil, los perfiles de cliente se crean automáticamente en función de los datos de identidad configurados en el esquema XDM.

Al cargar datos en un nuevo conjunto de datos por primera vez, o al configurar un nuevo proceso de ETL o una fuente de datos, se recomienda comprobar cuidadosamente los datos para asegurarse de que se han cargado correctamente y que los perfiles generados contienen los datos esperados. Para obtener más información sobre cómo acceder a los perfiles de cliente en la interfaz de usuario de Platform, consulte la [Guía de la interfaz de usuario del perfil del cliente en tiempo real](../profile/ui/user-guide.md). Para obtener más información sobre cómo acceder a perfiles mediante la API de perfil de cliente en tiempo real, consulte la guía de [uso del extremo de entidades](../profile/api/entities.md).

## Evaluar los datos

Una vez que haya generado correctamente perfiles a partir de los datos introducidos, puede evaluar los datos mediante la segmentación. La segmentación es el proceso de definir atributos o comportamientos específicos compartidos por un subconjunto de individuos desde el almacén de perfiles para distinguir un grupo comercializable de personas de su base de clientes. Para obtener más información sobre la segmentación, lea la [información general del servicio de segmentación](../segmentation/home.md).

### Crear una definición de segmento

Para empezar, debe crear una definición de segmento para agrupar los clientes con el fin de crear la audiencia de destino. Una definición de segmento es un conjunto de reglas que puede utilizar para definir la audiencia a la que desea dirigirse. Para crear una definición de segmento, puede seguir las instrucciones de la guía de IU sobre el uso de [Generador de segmentos](../segmentation/ui/segment-builder.md) o el tutorial de API en [creación de segmentos](../segmentation/tutorials/create-a-segment.md).

Una vez que haya creado una definición de segmento, asegúrese de tener en cuenta el ID de definición de segmento.

### Evaluar la definición del segmento

Después de crear su definición de segmento, puede crear un trabajo de segmento para evaluar el segmento como una instancia única o crear una programación para evaluar el segmento de forma continua.

Para evaluar una definición de segmento según demanda, puede crear un trabajo de segmento. Un trabajo de segmento es un proceso asincrónico que crea un nuevo segmento de audiencia basado en las políticas de combinación y definición de segmento referidas. Una política de combinación es un conjunto de reglas que Platform utiliza para determinar qué datos se utilizarán para crear perfiles de clientes y qué datos se priorizarán cuando haya discrepancias entre las fuentes. Para aprender a trabajar con políticas de combinación, consulte la [guía de interfaz de usuario de políticas de combinación](../profile/merge-policies/ui-guide.md).

Una vez creado y evaluado el trabajo del segmento, puede obtener información sobre el segmento, como el tamaño de la audiencia o los errores que puedan haberse producido durante el procesamiento. Para aprender a crear un trabajo de segmento, incluidos todos los detalles que necesita proporcionar, lea la [guía para desarrolladores de empleo de segmentos](../segmentation/api/segment-jobs.md).

Para evaluar una definición de segmento de forma continua, puede crear y habilitar una programación. Una programación es una herramienta que se puede utilizar para ejecutar automáticamente un trabajo de segmento una vez al día a una hora especificada. Para aprender a crear y habilitar una programación, puede seguir las instrucciones de la guía de API en la [extremo de programaciones](../segmentation/api/schedules.md).

## Exportar los datos evaluados

Después de crear su trabajo de segmento único o su programación continua, puede crear un trabajo de exportación de segmento para exportar los resultados a un conjunto de datos o exportar los resultados a un destino. Las secciones siguientes proporcionan directrices sobre ambas opciones.

### Exportar los datos evaluados a un conjunto de datos

Después de crear su trabajo de segmento de una sola vez o su programación continua, puede exportar los resultados creando un trabajo de exportación de segmento. Un trabajo de exportación de segmentos es una tarea asincrónica que envía información sobre la audiencia evaluada a un conjunto de datos.

Antes de crear un trabajo de exportación, primero debe crear un conjunto de datos para exportar los datos a. Para aprender a crear un conjunto de datos, lea la sección sobre [creación de un conjunto de datos de destino](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) en el tutorial sobre la evaluación de un segmento, asegúrese de anotar el ID del conjunto de datos después de la creación. Después de crear un conjunto de datos, puede crear un trabajo de exportación. Para aprender a crear un trabajo de exportación, puede seguir las instrucciones de la guía de API en la [exportar extremo de trabajos](../segmentation/api/export-jobs.md).

### Exportar los datos evaluados a un destino

Como alternativa, después de crear su trabajo de segmento único o su programación en curso, puede exportar los resultados a un destino. Un destino es un punto final, como una aplicación de Adobe en un servicio externo, en el que se puede activar y enviar una audiencia. Puede encontrar una lista completa de los destinos disponibles en la [catálogo de destinos](../destinations/catalog/overview.md).

Para obtener instrucciones sobre cómo activar datos en destinos de marketing por lotes o por correo electrónico, consulte el tutorial sobre [activación de datos de audiencia en destinos de exportación de perfiles por lotes mediante la interfaz de usuario de Platform](../destinations/ui/activate-batch-profile-destinations.md) y [guía sobre cómo conectarse a destinos de lote y activar datos mediante la API de servicio de flujo](../destinations/api/connect-activate-batch-destinations.md).

## Monitorización de las actividades de datos de Platform

Platform le permite rastrear cómo se procesan los datos mediante flujos de datos, que son representaciones de trabajos que mueven datos a través de los distintos componentes de Platform. Estos flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, donde los utiliza [!DNL Identity Service] y [!DNL Real-Time Customer Profile] antes de activarse finalmente en los destinos. El panel de monitorización proporciona una representación visual del recorrido de un flujo de datos. Para obtener información sobre cómo monitorizar los flujos de datos dentro de la interfaz de usuario de Platform, consulte los tutoriales sobre [monitorización de flujos de datos de fuentes](../dataflows/ui/monitor-sources.md) y [monitorización de flujos de datos en destinos](../dataflows/ui/monitor-destinations.md).

También puede supervisar las actividades de Platform mediante el uso de métricas estadísticas y notificaciones de eventos mediante [!DNL Observability Insights]. Puede suscribirse a las notificaciones de alerta a través de la interfaz de usuario de Platform o enviarlas a un enlace web configurado. Para obtener más información sobre cómo ver, habilitar, deshabilitar y suscribirse a las alertas disponibles desde la interfaz de usuario del Experience Platform, consulte la [[!UICONTROL Alertas] Guía de la interfaz de usuario](../observability/alerts/ui.md). Para obtener más información sobre cómo recibir alertas a través de los enlaces web, consulte la guía de [suscripción a las notificaciones de eventos de Adobe I/O](../observability/alerts/subscribe.md).

## Pasos siguientes

Al leer este tutorial, se le ha dado una introducción básica a un flujo simple de extremo a extremo para Platform. Para obtener más información sobre Adobe Experience Platform, lea la [Información general de plataforma](./home.md). Para obtener más información sobre el uso de la interfaz de usuario de Platform y la API de plataforma, lea la [Guía de la interfaz de usuario de Platform](./ui-guide.md) y [Guía de API de plataforma](./api-guide.md) respectivamente.
