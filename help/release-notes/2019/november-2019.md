---
title: Notas de la versión de Adobe Experience Platform
description: Notas de la versión del Experience Platform 18 de noviembre de 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 5f120a716cc3396ef7749463bb6052a8ced2fbb4
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 2%

---


# Notas de la versión de Adobe Experience Platform

**Fecha de la versión: 18 de noviembre de 2019**

Nuevas funciones de Adobe Experience Platform:
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Actualizaciones de funciones existentes:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

Integrada en Adobe Experience Platform, la plataforma de datos del cliente en tiempo real (CDP en tiempo real) ayuda a las compañías a reunir datos conocidos y desconocidos para activar los perfiles del cliente con decisiones inteligentes durante todo el viaje del cliente. CDP en tiempo real combina múltiples fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para proporcionar experiencias personalizadas de uno a uno en todos los canales y dispositivos.

[!DNL Real-time Customer Data Platform] incluye herramientas para la administración de datos, la administración de identidades, la segmentación avanzada y la ciencia de datos para que pueda crear perfiles y definir audiencias, así como obtener perspectivas ricas y poder aplicar políticas estrictas de gobernanza de datos.

Adobe se conecta a un gran ecosistema de socios, por no hablar de integraciones nativas con Adobe Experience Cloud, para que pueda activar estas audiencias sin problemas y ofrecer buenas experiencias de cliente en todos los canales, desde la personalización in situ o en la aplicación hasta el correo electrónico, los medios de pago, los centros de llamadas, los dispositivos conectados, etc.

Con CDP en tiempo real, puede:

* Lograr una única vista de su cliente con la recopilación de flujo continuo de datos de clientes de toda la empresa.
* Administre de manera responsable perfiles con control de privacidad y administración de confianza para identificadores conocidos y desconocidos.
* Genere perspectivas procesables y audiencias de escala con AI y aprendizaje automático con tecnología Adobe Sensei y creados para especialistas en marketing.
* Ofrezca experiencias personalizadas en tiempo real en todos los canales y destinos.

Para obtener más información, consulte la documentación [de la Plataforma de datos del cliente en tiempo](../../rtcdp/overview.md)real.

**Funciones principales**

| Función | Descripción |
|---|---|
| Destinos | Integraciones prediseñadas con plataformas de destino admitidas por los Adobes [!DNL Real-time Customer Data Platform] que activan datos a dichos socios de una manera transparente. See [Destinations](#destinations) below for more information. |
| Panel de métricas de página de inicio | La página de inicio de la Plataforma de datos del cliente en tiempo real (CDP en tiempo real) incluye un panel de métricas que muestra información sobre perfiles y segmentos. La página de inicio también contiene enlaces con material didáctico. Consulte la sección sobre las métricas [de la plataforma de datos del cliente en tiempo](#real-time-customer-data-platform-metrics) real más abajo. |
| Fuentes | Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamientos basados en la nube, software de terceros y CRM. Consulte la sección [Fuentes](#sources) a continuación para obtener más información. |

**[!DNL Real-time Customer Data Platform]métricas**

La página de inicio de la Plataforma de datos del cliente en tiempo real (CDP en tiempo real), que incluye un panel de métricas, aparece cuando inicia sesión en CDP en tiempo real.

La página de inicio es sólo uno de los lugares en los que aparecen las tarjetas de métricas. CDP en tiempo real proporciona tarjetas de métricas a lo largo de toda la experiencia. Estas métricas le informan sobre las audiencias de datos, perfiles y segmentos del sistema.

Si no hay datos en el sistema cuando inicia sesión en CDP en tiempo real, no aparece el panel en la página de inicio. En este caso, la página de inicio proporciona material de aprendizaje para una primera experiencia de usuario. A medida que se recopilan los datos, el panel se actualiza automáticamente para mostrar información sobre esos datos.

Para obtener más información, consulte Información general sobre las métricas de la Plataforma de datos del cliente en tiempo [real](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino admitidas por la plataforma de datos del cliente en tiempo real de Adobe que activan los datos a dichos socios de forma transparente. Para obtener más información, lea el artículo de información general sobre [Destinations](../../destinations/home.md) .

**Destinos disponibles**

Con la versión de noviembre, la plataforma de datos del cliente en tiempo real de Adobe admite los siguientes destinos:

* Publicidad: [!DNL Google]
* Mercadotecnia por correo electrónico: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consulte el catálogo [de](../../destinations/catalog/overview.md) destino para obtener información sobre cada uno de los destinos.

**Limitaciones conocidas**

* El control para permitir programas de activación personalizados en el flujo [de](../../destinations/ui/activate-destinations.md#activate-data) activación (paso de programación) no está disponible con la versión inicial.
* Actualmente no hay forma de editar o eliminar una configuración de destino. Para solucionar esta limitación, puede habilitar o deshabilitar el destino en la esquina superior derecha de la página [de detalles del](../../destinations/ui/destination-details-page.md)destino.
* Actualmente no hay ninguna validación para los detalles de la cuenta, la ruta o las credenciales al conectarse a la cuenta de almacenamiento o destino. Asegúrese de que está introduciendo las credenciales correctas y la comprobación de dobles para detectar errores o errores ortográficos.
* No se han realizado renovaciones de credenciales con la versión inicial. Una vez que una cuenta ha caducado o necesita actualizarse, debe crear una nueva conexión de destino y reasignar los segmentos asignados anteriormente.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de fuentes externas y, al mismo tiempo, puede estructurarlos, etiquetarlos y mejorarlos mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse en sus sistemas almacenamiento y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ---------- | ------------ |
| Interfaz de usuario de fuentes | Nueva interfaz de usuario para crear, ver y administrar conexiones de origen. |
| Flujos de trabajo renovados para conectores CRM | Nuevo flujo de trabajo intuitivo de la interfaz de usuario para crear y gestionar [!DNL Microsoft Dynamics] y [!DNL Salesforce] conectores. |
| Compatibilidad con conectores para almacenamientos basados en la nube | Los conectores ahora pueden acceder a almacenamientos basados en la nube. Las nuevas fuentes incluyen servidores [!DNL Amazon S3], [!DNL Azure Blob]y FTP/SFTP. |

**Problemas conocidos**

* Los conectores de origen para almacenamientos basados en la nube no admiten la ingestión de archivos comprimidos.

Para obtener más información sobre las fuentes, consulte Información general sobre [las fuentes](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] permite a los científicos de datos generar sin problemas perspectivas a partir de datos y contenido en aplicaciones de Adobe y sistemas de terceros mediante la creación y la puesta en marcha de modelos de aprendizaje automático. [!DNL Data Science Workspace] está estrechamente integrado con [!DNL Platform] y potencia el ciclo de vida completo de la ciencia de datos, incluida la exploración y preparación de datos XDM, seguido del desarrollo y la operacionalización de modelos para enriquecerse automáticamente [!DNL Real-time Customer Profile] con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Acceso a datos mediante [!DNL Platform] SDK | Las fórmulas y los blocs de notas del iniciador previamente compilados en [!DNL Python] ahora utilizan [!DNL Platform] SDK para acceder a los datos. |
| Compatibilidad con entornos limitados | Compatibilidad con la próxima funcionalidad de simulación de pruebas (actualmente en fase beta), incluida la capacidad de aislar blocs de notas y fórmulas en entornos limitados de desarrollo o producción. See the [sandboxes overview](../../sandboxes/home.md) for more information. |

Para obtener más información, consulte la información general [de](../../data-science-workspace/home.md)Área de trabajo de ciencia de datos.

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de Adobe Experience Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Esquema de notificaciones | Nuevo esquema que representa los datos de notificación enviados durante el proceso de ingesta de datos. |
| Esquemas de DSP de Adobe AdCloud | Se han agregado cinco nuevos esquemas para representar los metadatos de la plataforma de demanda (DSP) de Adobe Advertising Cloud: Ubicación, Campaña, Paquete, Anunciante, Cuenta. |
| Mezcla de detalles de implementación de ExperienceEvent | Nueva combinación de ExperienceEvent que agrega un campo estándar para almacenar información sobre el software utilizado para recopilar el evento. |
| [!DNL Profile Privacy] mezcla | Nueva mezcla de perfiles que agrega campos para aceptar señales generales de exclusión y de exclusión de ventas y uso compartido para [!DNL Real-time Customer Profile]. |
| Restricciones de formato para `xdm:alternateDisplayInfo` | Los campos &quot;Título&quot; y &quot;Descripción&quot; para `xdm:alternateDisplayInfo` deben ser cadenas para pasar la validación. |
| Cambio de nombre: XDM [!DNL Individual Profile] | El &quot;título&quot; de la clase &quot;XDM [!DNL Profile]&quot; se ha actualizado a &quot;XDM [!DNL Individual Profile]&quot;. El formato `$id` de la clase no ha cambiado. |

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre cómo trabajar con XDM mediante la [!DNL Schema Registry] API y la interfaz de usuario, lea la documentación [!DNL Schema Editor] del sistema [](../../xdm/home.md)XDM.

## [!DNL Real-time Customer Profile] {#profile}

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos dispares de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

| Función | Descripción |
| -----------| ---------- |
| Mejoras en la [!DNL Profile] búsqueda | Ahora los usuarios pueden buscar perfiles mediante descriptores de referencia y entidades relacionadas. |
| Limpiar datos para un conjunto de datos determinado | Ahora los usuarios pueden eliminar datos de un conjunto de datos o lote determinado mediante la API de trabajos [!DNL Profile] del sistema. |
| Mejoras en la consulta [!DNL Profile] de Edge | Las aplicaciones ahora pueden consulta de Edge [!DNL Profile] por cualquiera de las identidades de un perfil determinado. |
| Configurar directivas de combinación por proyección | Las aplicaciones ahora pueden configurar políticas de combinación por proyección para generar una vista de los datos según una política de combinación específica. |
| Atributos calculados | Los atributos calculados calculan automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil a valores acumulados como &quot;compra total&quot;, &quot;valor de duración&quot; o &quot;estado del canal&quot; según un evento entrante, un evento entrante y datos de perfil, o un evento entrante, datos de perfil y eventos históricos. |

**Corrección de errores**

* Lista simplificada de las estrategias de identificación de ID disponibles en el flujo de trabajo de creación de políticas de combinación.

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre [!DNL Real-time Customer Profile]los tutoriales y las prácticas recomendadas para trabajar con [!DNL Profile] datos, lea la Información general sobre el Perfil del cliente en tiempo [real](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API RESTful que le permite generar segmentos y audiencias a partir de sus [!DNL Real-time Customer Profile] datos. Estos segmentos están configurados y mantenidos de forma centralizada en [!DNL Platform], lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

[!DNL Segmentation Service] define un subconjunto concreto de perfiles describiendo los criterios que distinguen a un grupo comercializable de personas dentro de la base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| -----------| ---------- |
| Segmentación programada | Los usuarios ahora pueden habilitar la evaluación programada de segmentos para todos los segmentos a través de la interfaz de usuario y la API. Una vez habilitados, todos los segmentos se evaluarán una vez al día. Esto no afecta a las capacidades de segmentación a petición que siguen funcionando como antes.<br/><br/>Nota: La función de segmentación programada no se puede usar en entornos limitados con más de cinco directivas de combinación para [!DNL XDM Individual Profile]. |
| Segmentación por flujo continuo | La compatibilidad con la evaluación continua de segmentos (segmentación de flujo) permite evaluar la mayoría de las reglas de segmentos a medida que pasan los datos [!DNL Platform]. Esta función significa que la pertenencia a segmentos estará actualizada sin necesidad de ejecutar trabajos de segmentación programados. Se aplican algunas excepciones, como los segmentos que utilizan relaciones entre varias entidades o con cargas útiles enriquecidas. |
| Segmentos como bloques de creación | Al crear segmentos mediante la interfaz de usuario del Generador de segmentos, los usuarios ahora pueden utilizar segmentos definidos previamente como componentes básicos para segmentos adicionales. <ul><li>Haga referencia a la pertenencia a la audiencia actual: se actualiza a medida que las personas entran y salen de las audiencias.</li><li>Lógica de copia: tome la definición de segmento seleccionada y duplicado en el nuevo segmento.</li></ul> |
| Membresía del segmento de vista por Área de nombres de ID | La pertenencia a segmentos ahora se puede ver mediante la Área de nombres de ID (correo electrónico, ECID y recuento total). |
| Compatibilidad con RBAC | El Generador de segmentos ahora ofrece compatibilidad con controles de acceso y permisos básicos basados en roles. |
| Compatibilidad mejorada con el uso compartido de audiencias externas entre las soluciones [!DNL Platform] y Adobe | Ahora los usuarios pueden introducir metadatos de audiencia externos (no[!DNL Experience Platform]) en situaciones en las que el número de audiencias es grande o no se conoce a priori. Esta versión incluye el acceso a los metadatos para los clientes que han aprovisionado el conector de la solución. [!DNL Audience Manager] Estos metadatos de audiencia se pueden usar en el Generador de segmentos para crear nuevos [!DNL Experience Platform] segmentos. <br/><br/> Además, los segmentos creados en [!DNL Experience Platform] estarán ahora disponibles para su uso en soluciones de Adobe integradas, incluidas [!DNL Audience Manager], [!DNL Target]y [!DNL Ad Cloud]. |

**Corrección de errores**

* Se ha corregido un problema que provocaba que la segmentación con varias entidades devolviera cero perfiles en caso de relaciones anidadas.
* Se corrigió un problema en el cual la lógica de exclusión devolvía resultados engañosos.
* Se ha mejorado la legibilidad de las carpetas de varias entidades. Ahora muestran el nombre descriptivo de la clase XDM.
* Se corrigió un problema intermitente en el cual aparecían varias copias de la misma carpeta XDM.
* Ahora se genera mensajería para informar al usuario si las estimaciones de segmentos no están disponibles para la directiva de combinación seleccionada.

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre [!DNL Segmentation Service], lea la información general [del servicio](../../segmentation/home.md)de segmentación.