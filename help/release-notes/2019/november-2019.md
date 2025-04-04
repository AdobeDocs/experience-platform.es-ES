---
title: Notas de la versión de noviembre de 2019 de Adobe Experience Platform
description: Las notas de la versión de noviembre de 2019 de Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 8%

---

# Notas de la versión de Adobe Experience Platform

**Fecha de lanzamiento: martes, 18 de noviembre de 2019**

Nuevas funciones de Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Actualizaciones de funciones existentes:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

Creado en Adobe Experience Platform, Real-Time Customer Data Platform (Real-Time CDP) ayuda a las empresas a reunir datos conocidos y desconocidos para activar perfiles de clientes con decisiones inteligentes a lo largo del recorrido del cliente. Real-Time CDP combina varias fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para ofrecer experiencias de cliente personalizadas en todos los canales y dispositivos.

[!DNL Real-Time Customer Data Platform] incluye herramientas para el control de datos, la administración de identidades, la segmentación avanzada y la ciencia de datos para que pueda generar perfiles y definir audiencias, así como obtener perspectivas enriquecidas a la vez que puede aplicar políticas estrictas de control de datos.

Adobe se conecta a un gran ecosistema de socios, por no hablar de las integraciones nativas con Adobe Experience Cloud, para que pueda activar sin problemas estas audiencias y ofrecer buenas experiencias de cliente en todos los canales, desde personalización en el sitio o en la aplicación hasta correo electrónico, medios de pago, centros de llamadas, dispositivos conectados y mucho más.

Con Real-Time CDP, puede:

* Consiga una única vista de su cliente con la recopilación de streaming de datos de clientes desde toda la empresa.
* Administre perfiles de forma responsable con control de confianza y controles de privacidad para identificadores conocidos y desconocidos.
* Genere perspectivas procesables y escale audiencias con IA y aprendizaje automático con tecnología Adobe Sensei y diseñados para especialistas en marketing.
* Ofrezca experiencias personalizadas en tiempo real en todos los canales y destinos.

Para obtener más información, consulte la [documentación de Real-Time Customer Data Platform](../../rtcdp/overview.md).

**Funciones principales**

| Función | Descripción |
|---|---|
| Destinos | Integraciones prediseñadas con plataformas de destino admitidas por [!DNL Real-Time Customer Data Platform] de Adobe que activan los datos a esos socios de forma práctica. Consulte [Destinos](#destinations) a continuación para obtener más información. |
| Panel de métricas de página de inicio | La página de inicio de Real-Time Customer Data Platform (Real-Time CDP) incluye un panel de métricas que muestra información sobre perfiles y segmentos. La página de inicio también contiene vínculos a materiales de aprendizaje. Consulte la sección sobre [métricas de Real-Time Customer Data Platform](#real-time-customer-data-platform-metrics) a continuación. |
| Fuentes | Puede introducir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y CRM. Consulte la sección [Fuentes](#sources) más abajo para obtener más información. |

**[!DNL Real-Time Customer Data Platform]métricas**

La página de inicio de Real-Time Customer Data Platform (Real-Time CDP), que incluye un panel de métricas, aparece al iniciar sesión en Real-Time CDP.

La página de inicio es solo uno de los lugares en los que aparecen las tarjetas de métricas. Real-Time CDP proporciona tarjetas de métricas en toda la experiencia. Estas métricas le informan sobre los datos, el perfil y las audiencias de segmentos en el sistema.

Si no hay datos en el sistema al iniciar sesión en Real-Time CDP, el panel de la página principal no aparece. En este caso, la página de inicio proporciona material de aprendizaje por primera vez para la experiencia del usuario. A medida que se recopilan los datos, el panel se actualiza automáticamente para mostrar información sobre esos datos.

Para obtener más información, consulte [Resumen de las métricas de Real-Time Customer Data Platform](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] son integraciones prediseñadas con plataformas de destino admitidas por Real-Time Customer Data Platform de Adobe que activan los datos a dichos socios de forma fluida. Para obtener más información, lea el artículo [Información general sobre destinos](../../destinations/home.md).

**Destinos disponibles**

Con la versión de noviembre, Real-Time Customer Data Platform de Adobe admite los siguientes destinos:

* Advertising: [!DNL Google]
* Marketing por correo electrónico: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Consulte el [catálogo de destino](../../destinations/catalog/overview.md) para obtener información sobre cada uno de los destinos.

**Limitaciones conocidas**

* El control para permitir programaciones de activación personalizadas en el flujo de activación (paso Programar) no está disponible con la versión inicial.
* Actualmente no hay forma de editar o eliminar una configuración de destino. Para solucionar esta limitación, puede habilitar o deshabilitar el destino en la esquina superior derecha de [página de detalles de destino](../../destinations/ui/destination-details-page.md).
* Actualmente no hay ninguna validación para los detalles, la ruta o las credenciales de la cuenta al conectarse a la cuenta de destino o de almacenamiento. Asegúrese de introducir las credenciales correctas y vuelva a comprobar si hay errores ortográficos o errores ortográficos.
* No se han implementado renovaciones de credenciales con la versión inicial. Una vez que una cuenta haya caducado o necesite actualizarse, debe crear una nueva conexión de destino y volver a asignar los segmentos asignados anteriormente.

## Fuentes {#sources}

Adobe Experience Platform puede ingerir datos de orígenes externos y, al mismo tiempo, estructurarlos, etiquetarlos y mejorarlos mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

[!DNL Experience Platform] proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar conexiones de origen para varios proveedores de datos con facilidad. Estas conexiones de origen le permiten autenticarse en sus sistemas de almacenamiento y servicios CRM, establecer tiempos para ejecuciones de ingesta y administrar el rendimiento de ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ---------- | ------------ |
| IU de orígenes | Nueva interfaz de usuario para crear, ver y administrar conexiones de origen. |
| Flujos de trabajo modificados para conectores CRM | Nuevo flujo de trabajo de IU intuitivo para crear y administrar los conectores [!DNL Microsoft Dynamics] y [!DNL Salesforce]. |
| Compatibilidad con conectores para almacenamiento basado en la nube | Los conectores ahora pueden acceder al almacenamiento basado en la nube. Los nuevos orígenes incluyen [!DNL Amazon S3], [!DNL Azure Blob] y servidores FTP/SFTP. |

**Problemas conocidos**

* Los conectores de Source para almacenamiento basado en la nube no admiten la ingesta de archivos comprimidos.

Para obtener más información sobre las fuentes, consulte [Resumen de fuentes](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] permite a los científicos de datos generar sin problemas perspectivas a partir de datos y contenido en aplicaciones de Adobe y sistemas de terceros mediante la creación y el funcionamiento de modelos de aprendizaje automático. [!DNL Data Science Workspace] está totalmente integrado con [!DNL Experience Platform] y potencia el ciclo vital de la ciencia de datos de extremo a extremo, incluida la exploración y preparación de datos XDM, seguida del desarrollo y la operacionalización de modelos para enriquecer automáticamente [!DNL Real-Time Customer Profile] con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Acceso a datos mediante [!DNL Experience Platform] SDK | Las fórmulas prediseñadas y los blocs de notas del iniciador de [!DNL Python] ahora usan [!DNL Experience Platform] SDK para obtener acceso a los datos. |
| Compatibilidad con zonas protegidas | Compatibilidad con las próximas funciones de zona protegida (actualmente en fase beta), incluida la capacidad de aislar blocs de notas y fórmulas en zonas protegidas de desarrollo o producción. Consulte la [información general sobre las zonas protegidas](../../sandboxes/home.md) para obtener más detalles. |

Para obtener más información, consulte la [descripción general de Data Science Workspace](../../data-science-workspace/home.md).

## Sistema [!DNL Experience Data Model] (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave detrás de [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación para comunicarse con servicios en Adobe Experience Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir sus públicos mediante segmentos y utilizar sus atributos para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| Esquema de notificación | Nuevo esquema que representa los datos de notificación enviados durante el proceso de ingesta de datos. |
| Esquemas de Adobe AdCloud DSP | Se han agregado cinco nuevos esquemas para representar los metadatos de la plataforma del lado de la demanda (DSP) de Adobe Advertising Cloud: Ubicación, Campaña, Paquete, Anunciante, Cuenta. |
| Grupos de campos de esquema Detalles de implementación de ExperienceEvent | Nuevos grupos de campos de ExperienceEvent que agregan un campo estándar para almacenar información sobre el software utilizado para recopilar el evento. |
| [!DNL Profile Privacy] grupos de campos | Nuevos grupos de campos de perfil que agregan campos para aceptar señales generales de exclusión y exclusión de ventas/uso compartido para [!DNL Real-Time Customer Profile]. |
| Restricciones de formato para `xdm:alternateDisplayInfo` | Los campos &quot;Título&quot; y &quot;Descripción&quot; de `xdm:alternateDisplayInfo` deben ser cadenas para pasar la validación. |
| Cambio de nombre: XDM [!DNL Individual Profile] | El &quot;título&quot; de la clase &quot;XDM [!DNL Profile]&quot; se ha actualizado a &quot;XDM [!DNL Individual Profile]&quot;. El `$id` formal de la clase no ha cambiado. |

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre cómo trabajar con XDM mediante la API [!DNL Schema Registry] y la interfaz de usuario [!DNL Schema Editor], lea la [documentación del sistema XDM](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Adobe Experience Platform le permite impulsar experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-Time Customer Profile], puede ver una vista integral de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos de clientes dispares en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

| Función | Descripción |
| -----------| ---------- |
| Mejoras en la búsqueda de [!DNL Profile] | Ahora los usuarios pueden buscar perfiles utilizando descriptores de referencia y entidades relacionadas. |
| Limpiar los datos de un conjunto de datos determinado | Los usuarios ahora pueden eliminar los datos de un conjunto de datos o lote determinado mediante la API de trabajos del sistema [!DNL Profile]. |
| Mejoras en las consultas de Edge [!DNL Profile] | Ahora las aplicaciones pueden consultar Edge [!DNL Profile] por cualquiera de las identidades de un perfil determinado. |
| Configurar políticas de combinación por proyección | Las aplicaciones ahora pueden configurar políticas de combinación por proyección para generar una vista de los datos regida por una política de combinación específica. |
| Atributos calculados | Los atributos calculados calculan automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados operan en el nivel de perfil para acumular valores como &quot;compra total&quot;, &quot;valor de duración&quot; o &quot;estado del canal&quot; en función de un evento entrante, un evento entrante y datos de perfil, o un evento entrante, datos de perfil y eventos históricos. |

**Corrección de errores**

* Lista simplificada de las estrategias de vinculación de ID disponibles en el flujo de trabajo de creación de políticas de combinación.

**Problemas conocidos**

* Ninguna.

Para obtener más información sobre [!DNL Real-Time Customer Profile], incluidos tutoriales y prácticas recomendadas para trabajar con datos de [!DNL Profile], lea [Información general del perfil del cliente en tiempo real](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] proporciona una interfaz de usuario y una API RESTful que le permiten generar segmentos y audiencias a partir de los datos de [!DNL Real-Time Customer Profile]. Estos segmentos se configuran centralmente y se mantienen en [!DNL Experience Platform], lo que hace que cualquier aplicación de Adobe pueda acceder a ellos fácilmente.

[!DNL Segmentation Service] define un subconjunto particular de perfiles mediante la descripción de los criterios que distinguen a un grupo comercializable de personas dentro de su base de clientes. Los segmentos pueden basarse en datos de registro (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| -----------| ---------- |
| Segmentación programada | Los usuarios ahora pueden habilitar la evaluación de segmentos programada para todos los segmentos a través de la interfaz de usuario y la API. Una vez activados, todos los segmentos se evaluarán una vez al día. Esto no afecta a las capacidades de segmentación bajo demanda que siguen funcionando como antes.<br/><br/>Nota: la característica de segmentación programada no se puede usar en zonas protegidas con más de cinco políticas de combinación para [!DNL XDM Individual Profile]. |
| Segmentación de streaming | La compatibilidad con la evaluación continua de segmentos (segmentación de flujo continuo) permite evaluar la mayoría de las reglas de segmentos a medida que los datos pasan a [!DNL Experience Platform]. Esta función significa que el abono de segmentos estará actualizado sin necesidad de ejecutar trabajos de segmentación programados. Se aplican algunas excepciones, como segmentos que utilizan relaciones de varias entidades o con cargas útiles enriquecidas. |
| Segmentos como componentes básicos | Al crear segmentos con la interfaz de usuario del Generador de segmentos, los usuarios ahora pueden utilizar segmentos definidos anteriormente como componentes básicos para segmentos adicionales. <ul><li>Miembros de la audiencia actual de referencia: se actualiza a medida que las personas entran y salen de las audiencias.</li><li>Copiar lógica: tome la definición de segmento seleccionada y duplique la definición en el nuevo segmento.</li></ul> |
| Ver abono de segmentos por área de nombres de ID | Ahora el área de nombres de ID puede ver la pertenencia al segmento (correo electrónico, ECID y recuento total). |
| Compatibilidad con RBAC | El Generador de segmentos ahora es compatible con los controles y permisos de acceso básicos basados en funciones. |
| Compatibilidad mejorada con el uso compartido de audiencias externas entre [!DNL Experience Platform] y las soluciones de Adobe | Los usuarios ahora pueden incluir metadatos de audiencia externos (distintos de [!DNL Experience Platform]) en escenarios donde el número de audiencias es grande o se desconoce a priori. Esta versión incluye acceso a metadatos de [!DNL Audience Manager] para clientes que han aprovisionado el conector de solución. Estos metadatos de audiencia se pueden usar en el Generador de segmentos para crear [!DNL Experience Platform] segmentos nuevos. <br/><br/> Además, los segmentos creados en [!DNL Experience Platform] ahora estarán disponibles para su uso en soluciones de Adobe integradas, incluidas [!DNL Audience Manager], [!DNL Target] y [!DNL Ad Cloud]. |

**Corrección de errores**

* Se ha corregido un problema que hacía que la segmentación de varias entidades devolviera cero perfiles en caso de relaciones anidadas.
* Se ha corregido un problema en el cual la lógica de exclusión devolvía resultados engañosos.
* Legibilidad mejorada para carpetas de varias entidades. Ahora muestran el nombre descriptivo de la clase XDM.
* Se ha corregido un problema intermitente por el que aparecían varias copias de la misma carpeta XDM.
* La mensajería ahora se produce para informar a un usuario si las estimaciones de segmentos no están disponibles para la política de combinación seleccionada.

**Problemas conocidos**

* Ninguna.

Para obtener más información acerca de [!DNL Segmentation Service], lea la [descripción general del servicio de segmentación](../../segmentation/home.md).
