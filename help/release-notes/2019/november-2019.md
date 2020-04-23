---
title: 'Notas de la versión de Adobe Experience Platform '
description: Notas de la versión de la plataforma de experiencia 18 de noviembre de 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 817f994fc0622b1c46e98f8d773a4d91c1064824

---


# Notas de la versión de Adobe Experience Platform

## Fecha de la versión: 18 de noviembre de 2019

Nuevas funciones de Adobe Experience Platform:
* [Plataforma de datos de clientes en tiempo real](#rtcdp)
* [Destinos](#destinations)
* [Fuentes](#sources)

Actualizaciones de funciones existentes:
* [Área de trabajo de ciencia de datos](#dsw)
* [Sistema de modelo de datos de experiencia (XDM)](#xdm)
* [Perfil del cliente en tiempo real](#profile)
* [Servicio de segmentación](#segmentation)

## Real-time Customer Data Platform {#rtcdp}

Basada en la plataforma Adobe Experience, la plataforma de datos del cliente en tiempo real (CDP en tiempo real) de Adobe ayuda a las compañías a reunir datos conocidos y desconocidos para activar los perfiles del cliente con decisiones inteligentes durante todo el viaje del cliente. CDP en tiempo real combina múltiples fuentes de datos empresariales para crear perfiles unificados en tiempo real que se pueden utilizar para proporcionar experiencias personalizadas de uno a uno en todos los canales y dispositivos.

La plataforma de datos del cliente en tiempo real incluye herramientas para la administración de datos, la administración de identidades, la segmentación avanzada y la ciencia de datos, de modo que puede crear perfiles y definir audiencias, así como obtener perspectivas ricas y al mismo tiempo poder aplicar políticas estrictas de control de datos.

Adobe se conecta a un gran ecosistema de socios, sin mencionar las integraciones nativas con Adobe Experience Cloud, para que pueda activar estas audiencias sin problemas y ofrecer buenas experiencias de cliente en todos los canales, desde la personalización en el sitio o en la aplicación hasta el correo electrónico, los medios de pago, los centros de llamadas, los dispositivos conectados, etc.

Con CDP en tiempo real, puede:

* Lograr una única vista de su cliente con la recopilación de flujo continuo de datos de clientes de toda la empresa.
* Administre de manera responsable perfiles con control de privacidad y administración de confianza para identificadores conocidos y desconocidos.
* Genere perspectivas procesables y escale audiencias con AI y aprendizaje automático con tecnología Adobe Sensei y creados para especialistas en marketing.
* Ofrezca experiencias personalizadas en tiempo real en todos los canales y destinos.

Para obtener más información, consulte la documentación [de la plataforma de datos del cliente en tiempo real de](../../rtcdp/overview.md)Adobe.

**Funciones principales**

| Función | Descripción |
|---|---|
| Destinos | Integraciones prediseñadas con plataformas de destino admitidas por la plataforma de datos del cliente en tiempo real de Adobe que activan los datos a dichos socios de forma transparente. See [Destinations](#destinations) below for more information. |
| panel de métricas de Página de inicio | La página de inicio de la Plataforma de datos del cliente en tiempo real de Adobe incluye un panel de métricas que muestra información sobre perfiles y segmentos. La página de inicio también contiene enlaces con material didáctico. Consulte la sección sobre las métricas [de la plataforma de datos del cliente en tiempo](#real-time-customer-data-platform-metrics) real más abajo. |
| Fuentes | Puede ingerir datos de una variedad de fuentes, como soluciones de Adobe, almacenamientos basados en la nube, software de terceros y CRM. Consulte la sección [Fuentes](#sources) a continuación para obtener más información. |

**Métricas de la plataforma de datos del cliente en tiempo real**

La página de inicio de la Plataforma de datos del cliente en tiempo real (CDP en tiempo real) de Adobe, que incluye un panel de métricas, aparece cuando inicia sesión en CDP en tiempo real.

La página de inicio es sólo uno de los lugares en los que aparecen las tarjetas de métricas. CDP en tiempo real proporciona tarjetas de métricas a lo largo de toda la experiencia. Estas métricas le informan sobre las audiencias de datos, perfiles y segmentos del sistema.

Si no hay datos en el sistema cuando inicia sesión en CDP en tiempo real, no aparece el panel en la página de inicio. En este caso, la página de inicio proporciona material de aprendizaje para una primera experiencia de usuario. A medida que se recopilan los datos, el panel se actualiza automáticamente para mostrar información sobre esos datos.

Para obtener más información, consulte Información general sobre las métricas de la Plataforma de datos del cliente en tiempo [real](../../rtcdp/home-page-dashboards.md)

## Destinos {#destinations}

Los destinos son integraciones prediseñadas con plataformas de destino admitidas por la plataforma de datos del cliente en tiempo real de Adobe que activan los datos a dichos socios de forma transparente. Para obtener más información, lea el artículo de información general sobre [Destinations](../../rtcdp/destinations/destinations-overview.md) .

**Destinos disponibles**

Con la versión de noviembre, la plataforma de datos del cliente en tiempo real de Adobe admite los siguientes destinos:

* Publicidad: Google
* Mercadotecnia por correo electrónico: Adobe Campaign, Salesforce Marketing Cloud, Oracle Responsys, Oracle Eloqua

Consulte el catálogo [de](../../rtcdp/destinations/destinations-catalog.md) destino para obtener información sobre cada uno de los destinos.

**Limitaciones conocidas**

* El control para permitir programas de activación personalizados en el flujo [de](../../rtcdp/destinations/activate-destinations.md#activate-data) activación (paso de programación) no está disponible con la versión inicial.
* Actualmente no hay forma de editar o eliminar una configuración de destino. Para solucionar esta limitación, puede habilitar o deshabilitar el destino en la esquina superior derecha de la página [de detalles del](../../rtcdp/destinations/destination-details-page.md)destino.
* Actualmente no hay ninguna validación para los detalles de la cuenta, la ruta o las credenciales al conectarse a la cuenta de almacenamiento o destino. Asegúrese de que está introduciendo las credenciales correctas y la comprobación de dobles para detectar errores o errores ortográficos.
* No se han realizado renovaciones de credenciales con la versión inicial. Una vez que una cuenta ha caducado o necesita actualizarse, debe crear una nueva conexión de destino y reasignar los segmentos asignados anteriormente.

## Fuentes {#sources}

Adobe Experience Platform puede ingestar datos de fuentes externas y permitirle estructurarlos, etiquetarlos y mejorarlos mediante los servicios de plataforma. Puede ingestar datos de una variedad de fuentes, como soluciones de Adobe, almacenamiento basado en la nube, software de terceros y su sistema CRM.

La plataforma de experiencia proporciona una API RESTful y una interfaz de usuario interactiva que le permite configurar fácilmente las conexiones de origen para varios proveedores de datos. Estas conexiones de origen le permiten autenticarse en sus sistemas almacenamiento y servicios CRM, establecer tiempos para ejecuciones de ingestión y administrar el rendimiento de la ingesta de datos.

**Funciones principales**

| Función | Descripción |
| ---------- | ------------ |
| Interfaz de usuario de fuentes | Nueva interfaz de usuario para crear, ver y administrar conexiones de origen. |
| flujos de trabajo renovados para conectores CRM | Nuevo flujo de trabajo intuitivo de la interfaz de usuario para crear y administrar conectores de Microsoft Dynamics y Salesforce. |
| Compatibilidad con conectores para almacenamientos basados en la nube | Los conectores ahora pueden acceder a almacenamientos basados en la nube. Las nuevas fuentes incluyen Amazon S3, Azure Blob y servidores FTP/SFTP. |

**Problemas conocidos**

* Los conectores de origen para almacenamientos basados en la nube no admiten la ingestión de archivos comprimidos.

Para obtener más información sobre las fuentes, consulte Información general sobre [las fuentes](../../sources/home.md).

## Área de trabajo de ciencia de datos {#dsw}

Adobe Experience Platform Data Science Workspace permite a los científicos de datos generar sin problemas perspectivas a partir de datos y contenido en todas las aplicaciones de Adobe y sistemas de terceros mediante la creación y la puesta en marcha de modelos de aprendizaje automático. Data Science Workspace está estrechamente integrado con Platform y potencia el ciclo de vida completo de la ciencia de datos, incluida la exploración y preparación de datos XDM, seguido del desarrollo y la operacionalización de modelos para enriquecer automáticamente el Perfil del cliente en tiempo real con perspectivas de aprendizaje automático.

**Nuevas funciones**

| Función | Descripción |
| -----------| ---------- |
| Acceso a datos mediante el SDK de plataforma | Las fórmulas y los blocs de notas del iniciador previamente compilados en Python ahora utilizan el SDK de plataforma para acceder a los datos. |
| Compatibilidad con entornos limitados | Compatibilidad con la próxima funcionalidad de simulación de pruebas (actualmente en fase beta), incluida la capacidad de aislar blocs de notas y fórmulas en entornos limitados de desarrollo o producción. Consulte la descripción general [de los](../../sandboxes/home.md) entornos limitados para obtener más información. |

Para obtener más información, consulte la información general [de](../../data-science-workspace/home.md)Área de trabajo de ciencia de datos.

## Sistema de modelo de datos de experiencia (XDM) {#xdm}

La estandarización y la interoperabilidad son conceptos clave que sustentan la plataforma de experiencia. El modelo de datos de experiencia (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para que cualquier aplicación se comunique con los servicios de la plataforma Adobe Experience. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que ofrece perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y utilizar atributos de clientes para fines de personalización.

**Nuevas funciones**

| Función | Descripción |
| ---------- | ------------ |
| esquema de notificaciones | Nuevo esquema que representa los datos de notificación enviados durante el proceso de ingesta de datos. |
| esquemas de Adobe AdCloud DSP | Se han añadido cinco nuevos esquemas para representar los metadatos de la plataforma de demanda (DSP) de Adobe Advertising Cloud: Ubicación, Campaña, Paquete, Anunciante, Cuenta. |
| Mezcla de detalles de implementación de ExperienceEvent | Nueva combinación de ExperienceEvent que agrega un campo estándar para almacenar información sobre el software utilizado para recopilar el evento. |
| Mezcla de privacidad de Perfil | Nueva combinación de perfiles que agrega campos para aceptar señales generales de exclusión y de exclusión de ventas y uso compartido para el Perfil del cliente en tiempo real. |
| Restricciones de formato para `xdm:alternateDisplayInfo` | Los campos &quot;Título&quot; y &quot;Descripción&quot; para `xdm:alternateDisplayInfo` deben ser cadenas para pasar la validación. |
| Cambio de nombre: Perfil individual XDM | El &quot;título&quot; de la clase &quot;Perfil XDM&quot; se ha actualizado a &quot;Perfil individual XDM&quot;. El formato `$id` de la clase no ha cambiado. |

**Problemas conocidos**

* None.

Para obtener más información sobre cómo trabajar con XDM mediante la API del Registro de Esquema y la interfaz de usuario del Editor de Esquemas, lea la documentación [del sistema](../../xdm/home.md)XDM.

## Perfil del cliente en tiempo real {#profile}

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. Perfil le permite consolidar sus distintos datos de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes.

| Función | Descripción |
| -----------| ---------- |
| Mejoras en la búsqueda de Perfiles | Ahora los usuarios pueden buscar perfiles mediante descriptores de referencia y entidades relacionadas. |
| Limpiar datos para un conjunto de datos determinado | Ahora los usuarios pueden eliminar datos de un conjunto de datos o lote determinado mediante la API de trabajos del sistema de Perfil. |
| Mejoras en la consulta del Perfil de Edge | Las aplicaciones ahora pueden consulta el Perfil del borde según cualquiera de las identidades de un perfil determinado. |
| Configurar directivas de combinación por proyección | Las aplicaciones ahora pueden configurar políticas de combinación por proyección para generar una vista de los datos según una política de combinación específica. |
| Atributos calculados | Los atributos calculados calculan automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil a valores acumulados como &quot;compra total&quot;, &quot;valor de duración&quot; o &quot;estado del canal&quot; según un evento entrante, un evento entrante y datos de perfil, o un evento entrante, datos de perfil y eventos históricos. |

**Corrección de errores**

* lista simplificada de las estrategias de identificación de ID disponibles en el flujo de trabajo de creación de políticas de combinación.

**Problemas conocidos**

* None.

Para obtener más información sobre el Perfil del cliente en tiempo real, incluidos tutoriales y prácticas recomendadas para trabajar con datos de Perfil, lea la Descripción general [del Perfil del cliente en tiempo](../../profile/home.md)real.

## Servicio de segmentación {#segmentation}

El servicio de segmentación de la plataforma de experiencia de Adobe proporciona una interfaz de usuario y una API RESTful que le permite crear segmentos y generar audiencias a partir de los datos de Perfil de clientes en tiempo real. Estos segmentos se configuran y mantienen de forma centralizada en Platform, lo que los hace fácilmente accesibles para cualquier aplicación de Adobe.

El servicio de segmentación define un subconjunto particular de perfiles al describir los criterios que distinguen a un grupo comercializable de personas dentro de la base de clientes. Los segmentos pueden basarse en datos de registros (como información demográfica) o en eventos de series temporales que representen las interacciones de los clientes con su marca.

| Función | Descripción |
| -----------| ---------- |
| Segmentación programada | Los usuarios ahora pueden habilitar la evaluación programada de segmentos para todos los segmentos a través de la interfaz de usuario y la API. Una vez habilitados, todos los segmentos se evaluarán una vez al día. Esto no afecta a las capacidades de segmentación a petición que siguen funcionando como antes.<br/><br/>Nota: La función de segmentación programada no se puede usar en entornos limitados con más de cinco directivas de combinación para Perfil individual XDM. |
| Segmentación por flujo continuo | La compatibilidad con la evaluación continua de segmentos (segmentación de flujo) permite evaluar la mayoría de las reglas de segmentos a medida que los datos pasan a la plataforma. Esta función significa que la pertenencia a segmentos estará actualizada sin necesidad de ejecutar trabajos de segmentación programados. Se aplican algunas excepciones, como los segmentos que utilizan relaciones entre varias entidades o con cargas útiles enriquecidas. |
| Segmentos como bloques de creación | Al crear segmentos mediante la interfaz de usuario del Generador de segmentos, los usuarios ahora pueden utilizar segmentos definidos previamente como componentes básicos para segmentos adicionales. <ul><li>Haga referencia a la pertenencia a la audiencia actual: se actualiza a medida que las personas entran y salen de las audiencias.</li><li>Lógica de copia: tome la definición de segmento seleccionada y duplicado en el nuevo segmento.</li></ul> |
| Membresía en el segmento de Vista por Área de nombres de ID | La pertenencia a segmentos ahora se puede ver mediante la Área de nombres de ID (correo electrónico, ECID y recuento total). |
| Compatibilidad con RBAC | El Generador de segmentos ahora ofrece compatibilidad con controles de acceso y permisos básicos basados en roles. |
| Compatibilidad mejorada con el uso compartido de audiencias externas entre las soluciones de plataforma y Adobe | Ahora los usuarios pueden introducir metadatos de audiencia externos (que no sean de la plataforma de experiencia) en situaciones en las que el número de audiencias es grande o no se conoce a priori. Esta versión incluye acceso a los metadatos del Administrador de Audiencias para los clientes que han aprovisionado el conector de la solución. Estos metadatos de audiencia se pueden usar en el Generador de segmentos para crear nuevos segmentos de la plataforma de experiencia. <br/><br/> Además, los segmentos creados en la plataforma de experiencia estarán ahora disponibles para su uso en soluciones integradas de Adobe, incluidos Administrador de Audiencias, Destinatario y Ad Cloud. |

**Corrección de errores**

* Se ha corregido un problema que provocaba que la segmentación con varias entidades devolviera cero perfiles en caso de relaciones anidadas.
* Se corrigió un problema en el cual la lógica de exclusión devolvía resultados engañosos.
* Se ha mejorado la legibilidad de las carpetas de varias entidades. Ahora muestran el nombre descriptivo de la clase XDM.
* Se corrigió un problema intermitente en el cual aparecían varias copias de la misma carpeta XDM.
* Ahora se genera mensajería para informar al usuario si las estimaciones de segmentos no están disponibles para la directiva de combinación seleccionada.

**Problemas conocidos**

* None.

Para obtener más información sobre el servicio de segmentación, lea la información general [del servicio de](../../segmentation/home.md)segmentación.