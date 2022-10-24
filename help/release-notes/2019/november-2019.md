---
title: Notas de la versión de Adobe Experience Platform, noviembre de 2019
description: Notas de la versión de noviembre de 2019 para Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 2%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 18 de noviembre de 2019**

Nuevas funciones de Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Actualizaciones de funciones existentes:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Basado en Adobe Experience Platform, Real-time Customer Data Platform (Real-Time CDP) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes en todo el recorrido de clientes. Real-Time CDP combina varias fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para ofrecer experiencias personalizadas de cliente personalizadas y personalizadas en todos los canales y dispositivos.

[!DNL Real-Time Customer Data Platform] incluye herramientas para el control de datos, la administración de identidades, la segmentación avanzada y la ciencia de datos para que pueda crear perfiles y definir audiencias, así como obtener perspectivas enriquecidas, al tiempo que puede aplicar políticas estrictas de control de datos.

El Adobe se conecta a un gran ecosistema de socios, sin mencionar las integraciones nativas con Adobe Experience Cloud, de modo que puede activar sin problemas estas audiencias y ofrecer buenas experiencias de cliente en todos los canales, desde la personalización en el sitio o en la aplicación hasta el correo electrónico, los medios de pago, los centros de llamadas, los dispositivos conectados, etc.

Con Real-Time CDP, puede:

* Obtenga una sola vista de su cliente con la recopilación de flujo continuo de datos de clientes desde toda la empresa.
* Administre de forma responsable perfiles con controles de privacidad y control de gobernanza de confianza para identificadores conocidos y desconocidos.
* Genere perspectivas procesables y escale audiencias con IA y aprendizaje automático equipado con Adobe Sensei y creado para especialistas en marketing.
* Ofrezca experiencias personalizadas en tiempo real en todos los canales y destinos.

Para obtener más información, consulte la [Documentación de Real-time Customer Data Platform](../../rtcdp/overview.md).

**Funciones principales**

| Función | Descripción |
|---|---|
| Destinos | Integraciones creadas previamente con plataformas de destino admitidas por el Adobe [!DNL Real-Time Customer Data Platform] que activan los datos para esos socios de una manera sencilla. Consulte [Destinos](#destinations) más abajo para obtener más información. |
| Panel de métricas de la página principal | La página de inicio de Real-time Customer Data Platform (Real-Time CDP) incluye un tablero de métricas que muestra información sobre perfiles y segmentos. La página de inicio también contiene vínculos a material de aprendizaje. Consulte la sección sobre [Métricas de Real-time Customer Data Platform](#real-time-customer-data-platform-metrics) más abajo. |
| Fuentes | Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y CRM. Consulte la [Fuentes](#sources) para obtener más información. |

**[!DNL Real-Time Customer Data Platform]métricas**

La página de inicio de Real-time Customer Data Platform (Real-Time CDP), que incluye un tablero de métricas, aparece cuando inicia sesión en Real-Time CDP.

La página de inicio es solo uno de los lugares en los que aparecen las tarjetas de métricas. Real-Time CDP proporciona tarjetas de métricas a lo largo de toda la experiencia. Estas métricas le informan sobre los datos, el perfil y las audiencias de segmento del sistema.

Si no hay datos en el sistema cuando inicia sesión en Real-Time CDP, no aparece el tablero de la página principal. En este caso, la página principal proporciona material de aprendizaje para una primera experiencia de usuario. A medida que se recopilan los datos, el tablero se actualiza automáticamente para mostrar información sobre esos datos.

Para obtener más información, consulte la [Información general sobre las métricas de Real-time Customer Data Platform](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino admitidas por Real-time Customer Data Platform de Adobe que activan los datos a dichos socios de una manera sencilla. Para obtener más información, lea la [Información general sobre destinos](../../destinations/home.md) artículo.

**Destinos disponibles**

Con la versión de noviembre, Real-time Customer Data Platform de Adobe admite los siguientes destinos:

* Advertising: [!DNL Google]
* Marketing por correo electrónico: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consulte la [catálogo de destino](../../destinations/catalog/overview.md) para obtener información sobre cada uno de los destinos.

**Limitaciones conocidas**

* El control para permitir programas de activación personalizados en el flujo de activación (paso de programación) no está disponible con la versión inicial.
* Actualmente no hay forma de editar o eliminar una configuración de destino. Para solucionar esta limitación, puede habilitar o deshabilitar el destino en la esquina superior derecha del [página de detalles de destino](../../destinations/ui/destination-details-page.md).
* Actualmente no hay ninguna validación para los detalles de la cuenta, la ruta o las credenciales al conectarse a su cuenta de destino o almacenamiento. Asegúrese de que está introduciendo las credenciales correctas y compruebe dos veces si hay errores ortográficos o errores ortográficos.
* No se han realizado renovaciones de credenciales con la versión inicial. Una vez que una cuenta ha caducado o necesita actualizarse, debe crear una nueva conexión de destino y volver a asignar los segmentos asignados anteriormente.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, permitirle estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API de RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse en sus sistemas de almacenamiento y servicios CRM, establecer tiempos para ejecutar la ingesta y administrar el rendimiento de la ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ---------- | ------------ |
| Interfaz de usuario de fuentes | Nueva interfaz de usuario para crear, ver y administrar conexiones de origen. |
| Flujos de trabajo modificados para conectores CRM | Nuevo flujo de trabajo intuitivo de la interfaz de usuario para la creación y administración [!DNL Microsoft Dynamics] y [!DNL Salesforce] conectores. |
| Compatibilidad con conectores para almacenamiento en la nube | Los conectores ahora pueden acceder a las tiendas basadas en la nube. Las nuevas fuentes incluyen [!DNL Amazon S3], [!DNL Azure Blob]y servidores FTP/SFTP. |

**Problemas conocidos**

* Los conectores de origen para almacenamiento basado en la nube no admiten la ingesta de archivos comprimidos.

Para obtener más información sobre las fuentes, consulte [Resumen de fuentes](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] permite a los científicos de datos generar perspectivas a partir de datos y contenido en todas las aplicaciones de Adobe y sistemas de terceros mediante la creación y operación de modelos de aprendizaje automático. [!DNL Data Science Workspace] está estrechamente integrado con [!DNL Platform] y potencia el ciclo de vida completo de la ciencia de datos, incluida la exploración y preparación de datos XDM, seguido del desarrollo y la operacionalización de modelos para enriquecer automáticamente [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Acceso a datos mediante [!DNL Platform] SDK | Fórmulas creadas previamente y portátiles de lanzador en [!DNL Python] ahora use [!DNL Platform] SDK para acceder a datos. |
| Compatibilidad con entornos limitados | Compatibilidad con la próxima funcionalidad de entorno limitado (actualmente en versión beta), incluida la capacidad de aislar blocs de notas y fórmulas en entornos limitados de desarrollo o producción. Consulte la [información general sobre los entornos limitados](../../sandboxes/home.md) para obtener más información. |

Para obtener más información, consulte la [Información general de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrezca perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes con fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Esquema de notificación | Nuevo esquema que representa los datos de notificación enviados durante el proceso de ingesta de datos. |
| Esquemas de DSP de Adobe AdCloud | Se han agregado cinco nuevos esquemas para representar los metadatos de la plataforma (DSP) del lado de la demanda de Adobe Advertising Cloud: Ubicación, Campaña, Paquete, Anunciante, Cuenta. |
| Grupos de campos de esquema de detalles de implementación de ExperienceEvent | Nuevos grupos de campos de ExperienceEvent que agregan un campo estándar para almacenar información sobre el software utilizado para recopilar el evento. |
| [!DNL Profile Privacy] grupos de campos | Nuevos grupos de campos de perfil que agregan campos para aceptar señales de exclusión generales y de exclusión de ventas/uso compartido para [!DNL Real-time Customer Profile]. |
| Restricciones de formato para `xdm:alternateDisplayInfo` | Los campos &quot;Título&quot; y &quot;Descripción&quot; para `xdm:alternateDisplayInfo` deben ser cadenas para pasar la validación. |
| Cambio de nombre: XDM [!DNL Individual Profile] | El &quot;título&quot; de &quot;XDM&quot; [!DNL Profile]&quot; la clase se ha actualizado a &quot;XDM [!DNL Individual Profile]&quot;. El `$id` de la clase no ha cambiado. |

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre cómo trabajar con XDM mediante la variable [!DNL Schema Registry] API y [!DNL Schema Editor] interfaz de usuario, lea la [Documentación del sistema XDM](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes, independientemente de dónde o cuándo interactúen con su marca. con [!DNL Real-time Customer Profile], puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus diferentes datos de clientes en una vista unificada, que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes.

| Función | Descripción |
| -----------| ---------- |
| Mejoras en [!DNL Profile] búsqueda | Los usuarios ahora pueden buscar perfiles mediante descriptores de referencia y entidades relacionadas. |
| Limpiar los datos de un conjunto de datos determinado | Los usuarios ahora pueden eliminar los datos de un conjunto de datos o lote determinado mediante el [!DNL Profile] API de trabajos del sistema. |
| Edge [!DNL Profile] mejoras en las consultas | Las aplicaciones ahora pueden consultar Edge [!DNL Profile] por cualquiera de las identidades de un perfil determinado. |
| Configurar directivas de combinación por proyección | Las aplicaciones ahora pueden configurar políticas de combinación por proyección para generar una vista de los datos según se rija por una política de combinación específica. |
| Atributos calculados | Los atributos calculados calculan automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados operan en el nivel de perfil para agregar valores como &quot;compra total&quot;, &quot;valor de duración&quot; o &quot;estado de canal&quot; en función de un evento entrante, un evento entrante y datos de perfil, o un evento entrante, datos de perfil y eventos históricos. |

**Corrección de errores**

* Lista simplificada de estrategias de vinculación de ID disponibles en el flujo de trabajo de creación de directivas de combinación.

**Problemas conocidos**

* Ninguna.

Para obtener más información, consulte [!DNL Real-time Customer Profile], incluidos tutoriales y prácticas recomendadas para trabajar con [!DNL Profile] información, lea la [Información general del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API de RESTful que le permiten crear segmentos y generar audiencias a partir de su [!DNL Real-time Customer Profile] datos. Estos segmentos están configurados de forma centralizada y se mantienen en [!DNL Platform], lo que permite que cualquier aplicación de Adobe pueda acceder a ellas fácilmente.

[!DNL Segmentation Service] define un subconjunto de perfiles determinado describiendo los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| -----------| ---------- |
| Segmentación programada | Los usuarios ahora pueden habilitar la evaluación programada de segmentos para todos los segmentos a través de la interfaz de usuario y la API. Una vez habilitados, todos los segmentos se evaluarán una vez al día. Esto no afecta a las capacidades de segmentación bajo demanda que siguen funcionando como antes.<br/><br/>Nota: La función de segmentación programada no se puede usar en entornos limitados con más de cinco directivas de combinación para [!DNL XDM Individual Profile]. |
| Segmentación por transmisión | La compatibilidad con la evaluación continua de segmentos (segmentación de flujo continuo) permite evaluar la mayoría de las reglas de segmentos a medida que se pasan los datos [!DNL Platform]. Esta función significa que la pertenencia a segmentos estará actualizada sin necesidad de ejecutar trabajos de segmentación programados. Se aplican algunas excepciones, como segmentos que utilizan relaciones de varias entidades o con cargas útiles enriquecidas. |
| Segmentos como componentes básicos | Al crear segmentos mediante la interfaz de usuario del Generador de segmentos, los usuarios ahora pueden utilizar segmentos definidos previamente como componentes básicos para segmentos adicionales. <ul><li>Haga referencia a la pertenencia a la audiencia actual: se actualiza a medida que las personas entran y salen de las audiencias.</li><li>Copiar lógica: tome la definición de segmento seleccionada y duplíquela en el nuevo segmento.</li></ul> |
| Ver la pertenencia a segmentos por espacio de nombres de ID | Ahora, la pertenencia a segmentos se puede ver mediante el espacio de nombres del ID (correo electrónico, ECID y recuento total). |
| Compatibilidad con RBAC | El Generador de segmentos ahora es compatible con los controles y permisos de acceso básicos basados en funciones. |
| Compatibilidad mejorada con el uso compartido de audiencias externas entre [!DNL Platform] y soluciones de Adobe | Los usuarios ahora pueden introducir elementos externos (no externos)[!DNL Experience Platform]) metadatos de audiencia en escenarios en los que el número de audiencias es grande o no se conoce a priori. Esta versión incluye el acceso a [!DNL Audience Manager] metadatos para clientes que han aprovisionado el conector de soluciones. Estos metadatos de audiencia se pueden usar en el Generador de segmentos para crear [!DNL Experience Platform] segmentos. <br/><br/> Además, los segmentos creados en [!DNL Experience Platform] ya estará disponible para su uso en soluciones de Adobe integradas, incluidas [!DNL Audience Manager], [!DNL Target]y [!DNL Ad Cloud]. |

**Corrección de errores**

* Se ha corregido un problema que provocaba que la segmentación de varias entidades devolviera cero perfiles en caso de relaciones anidadas.
* Se ha corregido un problema en el cual la lógica de exclusión devolvía resultados confusos.
* Se ha mejorado la legibilidad de las carpetas de varias entidades. Ahora muestran el nombre descriptivo de la clase XDM.
* Se ha corregido un problema intermitente en el que aparecían varias copias de la misma carpeta XDM.
* Ahora se genera un mensaje para informar al usuario si las estimaciones de segmentos no están disponibles para la política de combinación seleccionada.

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre [!DNL Segmentation Service], lea la [Información general del servicio de segmentación](../../segmentation/home.md).
