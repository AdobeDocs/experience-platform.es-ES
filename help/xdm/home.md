---
keywords: Experience Platform;inicio;temas populares;XDM;sistema XDM;perfil individual XDM;evento de experiencia XDM;evento de experiencia XDM;Evento de experiencias;evento de experiencia;evento de experiencias;mezclas;combinación;combinación;evento de experiencias;Evento de experiencias XDM;evento de experiencia XDM;evento de experiencia;evento de experiencia XDM;evento de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;Modelo de datos;Registro de esquemas;Registro de Esquemas;esquema biblioteca de ;Esquema biblioteca;esquema;datos de registros;serie temporal;serie temporal
solution: Experience Platform
title: Información general del sistema XDM
topic: overview
description: 'La estandarización y la interoperabilidad son conceptos clave para Adobe Experience Platform. El modelo de datos de experiencia (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente. '
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 2%

---


# Descripción general del sistema XDM

La estandarización y la interoperabilidad son conceptos clave para Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación que se pueda utilizar para comunicarse con los servicios [!DNL Platform]. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que puede ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y expresar atributos de clientes para fines de personalización.

XDM es el marco fundamental que permite a Adobe Experience Cloud, con la tecnología [!DNL Experience Platform], entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento preciso. Metodología en la que [!DNL Experience Platform] se crea, Sistema XDM, hace operativos [!DNL Experience Data Model] esquemas para su uso por los servicios [!DNL Platform].

Este documento proporciona una visión general de la función del sistema XDM dentro de [!DNL Experience Platform].

## Esquemas XDM

[!DNL Experience Platform] utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Para poder ingerir datos en [!DNL Platform], se debe crear un esquema que describa la estructura de los datos y proporcione restricciones al tipo de datos que se pueden incluir en cada campo. Los esquemas consisten en una clase base y cero o más mezclas.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte los [conceptos básicos de la composición de esquema](schema/composition.md).

### [!DNL Schema Registry] y [!DNL Schema Library]

El **[!DNL Schema Registry]** proporciona una interfaz de usuario y una API RESTful desde la cual puede realizar la vista y administración de todos los recursos relacionados con el esquema en Adobe Experience Platform **[!DNL Schema Library]**. El [!DNL Schema Library] contiene recursos estándar de la industria que se ponen a su disposición por Adobe, así como recursos de [!DNL Experience Platform] socios y proveedores cuyas aplicaciones se utilizan. La interfaz de usuario y la API del Registro de Esquema también se pueden usar para crear y administrar nuevos esquemas y recursos que son exclusivos de su organización.

Para obtener una guía completa de las principales operaciones disponibles en [!DNL Schema Registry], consulte la [guía para desarrolladores de Esquema Registry](api/getting-started.md).

## Comportamientos de datos en el sistema XDM {#data-behaviors}

Los datos destinados a utilizarse en [!DNL Experience Platform] se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema lo define la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el menor número de propiedades que debe contener un esquema para representar un comportamiento de datos concreto.

Aunque puede definir sus propias clases dentro de [!DNL Schema Registry], se recomienda utilizar las clases preferidas **[!DNL XDM Individual Profile]** y **[!DNL XDM ExperienceEvent]** para los datos de registros y series temporales, respectivamente. Estas clases se describen con más detalle a continuación.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] es una clase basada en registros que forma una representación singular de los atributos de los sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o participaciones específicas, y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

Los perfiles menos identificados pueden consistir únicamente en señales conductuales anónimas como las cookies del explorador. En este caso, los datos de perfil dispersos se utilizan para crear una base de información en la que se recopilan y almacenan los intereses y preferencias del perfil anónimo. Estos identificadores pueden ser más detallados con el tiempo a medida que el sujeto se registra para recibir notificaciones, suscripciones, compras, etc. Este aumento en los atributos del perfil puede resultar en un asunto identificado y permitir un mayor grado de compromiso objetivo.

A medida que el perfil de los consumidores sigue creciendo, se convierte en un sólido repositorio de la información personal, la información de identificación, los datos de contacto y las preferencias de comunicación de un individuo.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produce un evento (o conjunto de eventos), incluido el punto en el tiempo y la identidad del sujeto involucrado. Los Eventos de experiencias son registros de hechos de lo que ocurrió, por lo que son inmutables y representan lo que ocurrió sin agregación ni interpretación. Son fundamentales para el análisis de dominio de tiempo, ya que se pueden utilizar para analizar los cambios que se producen en una ventana de tiempo determinada y para comparar varias ventanas de tiempo para rastrear tendencias.

Los Eventos de experiencias pueden ser explícitos o implícitos. Los eventos explícitos son acciones humanas directamente observables que tienen lugar durante un momento del recorrido. Los eventos implícitos son eventos que se crían sin una acción humana directa, pero que siguen estando relacionados con una persona. Algunos ejemplos de eventos implícitos pueden incluir el envío programado de boletines informativos por correo electrónico o la tensión de la batería que alcanza un determinado umbral.

Aunque no todos los eventos se clasifican fácilmente en todas las fuentes de datos, resulta extremadamente valioso armonizar eventos similares en tipos similares cuando sea posible para su procesamiento.

![Recorrido del cliente de ExperienceEvent](images/overview/experience-event-journey.png)

## Esquemas XDM y [!DNL Experience Platform] servicios

[!DNL Experience Platform] no depende del esquema, lo que significa que cualquier esquema que se ajuste al estándar XDM está disponible para su uso por  [!DNL Platform] los servicios. A continuación se detallan las formas en que los diferentes servicios [!DNL Platform] utilizan esquemas.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] es el sistema de registro de  [!DNL Experience Platform] los activos y sus esquemas conexos. [!DNL Catalog] no son los archivos o directorios reales que contienen datos, sino que contienen los metadatos y las descripciones de esos archivos y directorios.

[!DNL Catalog] los datos se almacenan en el  [!DNL Data Lake], un almacén de datos altamente granular que contiene todos los datos administrados por  [!DNL Platform], independientemente del formato de archivo o origen.

Para empezar a ingerir datos en [!DNL Experience Platform], se crea un conjunto de datos mediante [!DNL Catalog Service]. El conjunto de datos hace referencia a un esquema XDM que describe la estructura de los datos que se van a ingestar. Si se crea un conjunto de datos sin un esquema, [!DNL Experience Platform] obtendrá un &quot;esquema observado&quot; inspeccionando el tipo y el contenido de los campos de datos ingestados. Los conjuntos de datos se rastrean en [!DNL Catalog] y se almacenan en [!DNL Data Lake] junto con los esquemas y esquemas observados en los que se basan.

Para obtener más información sobre [!DNL Catalog], consulte la [información general del servicio de catálogo](../catalog/home.md). Para obtener más información sobre la ingestión de datos de Adobe Experience Platform, consulte la [información general sobre la ingestión de datos](../ingestion/home.md).

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] le permite utilizar datos estándar de SQL para la consulta [!DNL Experience Platform] a fin de admitir muchos casos de uso diferentes.

Después de que se haya compuesto un esquema y se haya creado un conjunto de datos que haga referencia a ese esquema, los datos se ingieren y almacenan en [!DNL Data Lake]. Mediante [!DNL Query Service], puede unir cualquier conjunto de datos en [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, aprendizaje automático o para su ingestión en [!DNL Real-time Customer Profile].

Para obtener más información sobre [!DNL Query Service], consulte la [Introducción al servicio de Consulta](../query-service/home.md).

### [!DNL Real-time Customer Profile]

El Perfil de clientes en tiempo real proporciona un perfil de consumo centralizado para la administración personalizada y dirigida de la experiencia. Cada perfil contiene datos agregados en todos los sistemas, así como cuentas con marca de hora procesables de eventos que involucran a personas individuales que han tenido lugar en cualquiera de los sistemas que utiliza con [!DNL Experience Platform].

[!DNL Real-time Customer Profile] consume datos con formato de esquema basados en las  [!DNL XDM Individual Profile]   [!DNL XDM ExperienceEvent] clases o y responde a consultas basadas en esos datos. [!DNL Profile] no admite el uso de esquemas basados en otras clases.

[!DNL Profile] mantiene una instancia de cada perfil de cliente, combinando los datos para formar una &quot;única fuente de verdad&quot; para el individuo. Estos datos unificados se representan usando lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un solo esquema.  Al componer un esquema mediante la interfaz de usuario o la API, puede activar el esquema para utilizarlo con [!DNL Real-time Customer Profile] y etiquetarlo para incluirlo en la vista de unión. El esquema etiquetado participará luego en la definición de esquema que se está alimentando a [!DNL Profile].

Dado que [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent] datos son ingestados y administrados por [!DNL Catalog], el déclencheur [!DNL Real-time Customer Profile] es comenzar a ingerir datos habilitados para su uso. Cuanto más interacciones y detalles se ingieran, más robustos se volverán los perfiles individuales.

[!DNL XDM Individual Profile] los datos ayudan a informar y potenciar las acciones en cualquier integración de soluciones de canal o Adobe, y cuando se combinan con un historial rico de datos de comportamiento e interacción, estos datos se utilizan para impulsar el aprendizaje automático. La API [!DNL Real-time Customer Profile] también puede utilizarse para enriquecer la funcionalidad de soluciones de terceros, CRM y soluciones propietarias.

Consulte la [información general del Perfil del cliente en tiempo real](../profile/home.md) para obtener más información.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados dentro de [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en XDM Individual  [!DNL Profile] y  [!DNL XDM ExperienceEvent] datos sobre los clientes y sus actividades, lo que facilita predicciones como la propensión a comprar y ofertas recomendadas que el individuo probablemente apreciará y usará.

Con [!DNL Data Science Workspace], los científicos de datos pueden crear fácilmente API de servicios inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otras soluciones de Adobe, incluidas Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y dirigidas.

Para obtener más información sobre el uso de [!DNL Experience Platform] datos para generar perspectivas, consulte la [información general de Área de trabajo de ciencias de datos](../data-science-workspace/home.md).

## Próximos pasos y recursos adicionales

Ahora que comprende mejor el papel de los esquemas a través de [!DNL Experience Platform], está listo para el inicio de componer el suyo propio. Para seguir complementando su aprendizaje, lea la documentación sugerida y vea el siguiente vídeo.

Para aprender los principios de diseño y las prácticas recomendadas para la composición de esquemas que se utilizarán con [!DNL Experience Platform], comience por leer los [conceptos básicos de la composición de esquemas](schema/composition.md). Para obtener instrucciones paso a paso sobre cómo crear un esquema, consulte los tutoriales sobre cómo crear un esquema [mediante la API](tutorials/create-schema-api.md) o [mediante la interfaz de usuario](tutorials/create-schema-ui.md).

Para reforzar su comprensión de [!DNL XDM System] en [!DNL Experience Platform], vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

