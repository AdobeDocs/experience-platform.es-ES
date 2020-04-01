---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Sistema de modelo de datos de experiencia (XDM)
topic: overview
translation-type: tm+mt
source-git-commit: c07f926a71447e840c692ed15e85c9e02f1106ab

---


# Descripción general del sistema XDM

La estandarización y la interoperabilidad son conceptos clave que subyacen a Adobe Experience Platform. El modelo de datos de experiencia (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de la experiencia del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación que se pueda utilizar para comunicarse con los servicios de la Plataforma. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar a una representación común que puede ofrecer perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas de las acciones de los clientes, definir audiencias de clientes a través de segmentos y expresar atributos de clientes para fines de personalización.

XDM es el marco de base que permite a Adobe Experience Cloud, con la tecnología de Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto y en el momento preciso. La metodología en la que se basa la plataforma de experiencia, Sistema **** XDM, hace operativos los esquemas del modelo de datos de experiencia para que los utilicen los servicios de plataforma.

Este documento proporciona una visión general de la función del sistema XDM en la plataforma de experiencia.

## esquemas XDM

La plataforma de experiencias utiliza esquemas para describir la estructura de los datos de forma coherente y reutilizable. Al definir los datos de manera consistente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de que los datos se puedan ingerir en la plataforma, se debe crear un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se pueden incluir en cada campo. Los Esquemas consisten en una clase base y cero o más mezclas.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios y las prácticas recomendadas de diseño, consulte los [conceptos básicos de la composición](schema/composition.md)de esquemas.

### Registro de Esquemas y Biblioteca de Esquemas

El Registro **de** Esquema proporciona una interfaz de usuario y una API RESTful desde la que puede realizar la vista y la gestión de todos los recursos relacionados con el esquema en la biblioteca **de** Esquemas de la plataforma de experiencia de Adobe. La biblioteca de Esquemas contiene los recursos estándar del sector que Adobe pone a su disposición, así como los recursos de los socios y proveedores de la plataforma de experiencia cuyas aplicaciones utilice. La interfaz de usuario y la API del Registro de Esquema también se pueden usar para crear y administrar nuevos esquemas y recursos que son exclusivos de su organización.

Para obtener una guía completa de las principales operaciones disponibles en el Registro de Esquemas, consulte la guía [para desarrolladores del Registro de](api/getting-started.md)Esquemas.

## Comportamientos de datos en el sistema XDM {#data-behaviors}

Los datos destinados a utilizarse en la plataforma de experiencia se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema lo define la **clase** del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el menor número de propiedades que debe contener un esquema para representar un comportamiento de datos concreto.

Aunque puede definir sus propias clases dentro del Registro de Esquemas, se recomienda utilizar las clases preferidas **XDM Individual Perfil** y **XDM ExperienceEvent** para los datos de registros y series temporales, respectivamente. Estas clases se describen con más detalle a continuación.

### Perfil individual XDM

El Perfil individual XDM es una clase basada en registros que forma una representación única de los atributos de los sujetos identificados y parcialmente identificados. Los Perfiles altamente identificados pueden utilizarse para comunicaciones personales o participaciones específicas, y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

Los perfiles menos identificados pueden consistir únicamente en señales conductuales anónimas como las cookies del explorador. En este caso, los datos de perfil dispersos se utilizan para crear una base de información en la que se recopilan y almacenan los intereses y preferencias del perfil anónimo. Estos identificadores pueden ser más detallados con el tiempo a medida que el sujeto se registra para recibir notificaciones, suscripciones, compras, etc. Este aumento en los atributos del perfil puede resultar en un asunto identificado y permitir un mayor grado de compromiso objetivo.

A medida que el perfil de los consumidores sigue creciendo, se convierte en un sólido repositorio de la información personal, la información de identificación, los datos de contacto y las preferencias de comunicación de un individuo.

### XDM ExperienceEvent

XDM ExperienceEvent es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produce un evento (o conjunto de eventos), incluido el punto en el tiempo y la identidad del sujeto involucrado. Los Eventos de experiencias son registros de hechos de lo que ocurrió, por lo que son inmutables y representan lo que ocurrió sin agregación ni interpretación. Son fundamentales para el análisis de dominio de tiempo, ya que se pueden utilizar para analizar los cambios que se producen en una ventana de tiempo determinada y para comparar varias ventanas de tiempo para rastrear tendencias.

Los Eventos de experiencias pueden ser explícitos o implícitos. Los eventos explícitos son acciones humanas directamente observables que tienen lugar durante un período de un viaje. Los eventos implícitos son eventos que se crían sin una acción humana directa, pero que siguen estando relacionados con una persona. Algunos ejemplos de eventos implícitos pueden incluir el envío programado de boletines informativos por correo electrónico o la tensión de la batería que alcanza un determinado umbral.

Aunque no todos los eventos se clasifican fácilmente en todas las fuentes de datos, resulta extremadamente valioso armonizar eventos similares en tipos similares cuando sea posible para su procesamiento.

![Viaje del cliente de ExperienceEvent](images/overview/experience-event-journey.png)

## esquemas XDM y servicios de la plataforma de experiencia

La plataforma de experiencia no depende del esquema, lo que significa que cualquier esquema que se ajuste al estándar XDM está disponible para su uso por los servicios de plataforma. A continuación se detallan las formas en que los distintos servicios de la Plataforma utilizan esquemas.

### Servicio de catálogo, Data Ingestion y Data Lake

El servicio de catálogo es el sistema de registro de los recursos de la plataforma de experiencia y sus esquemas relacionados. El catálogo no es los archivos o directorios reales que contienen datos, sino que contiene los metadatos y las descripciones de esos archivos y directorios.

Los datos del catálogo se almacenan en Data Lake, un almacén de datos muy granular que contiene todos los datos administrados por la plataforma, independientemente del formato de archivo o origen.

Para empezar a ingerir datos en la plataforma de experiencias, se crea un conjunto de datos mediante el servicio de catálogos. El conjunto de datos hace referencia a un esquema XDM que describe la estructura de los datos que se van a ingestar. Si se crea un conjunto de datos sin un esquema, la plataforma de experiencia obtendrá un &quot;esquema observado&quot; inspeccionando el tipo y el contenido de los campos de datos ingestados. Los conjuntos de datos se rastrean en el catálogo y se almacenan en el Data Lake junto con los esquemas y esquemas observados en los que se basan.

Para obtener más información sobre Catálogo, consulte la descripción general [del servicio de](../catalog/home.md)catálogos. Para obtener más información sobre la ingestión de datos de la plataforma Adobe Experience, consulte la información general [sobre la introducción](../ingestion/home.md)de datos.

### Servicio de Consulta

El servicio de Consulta de la plataforma de experiencia de Adobe le permite utilizar SQL estándar para la consulta de datos de la plataforma de experiencias para admitir muchos casos de uso diferentes.

Después de que se haya compuesto un esquema y se haya creado un conjunto de datos que haga referencia a ese esquema, los datos se ingieren y almacenan en el Data Lake. Con el servicio de Consulta, puede unirse a cualquier conjunto de datos en Data Lake y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistema de informes, aprendizaje automático o para su inserción en el Perfil del cliente en tiempo real.

Para obtener más información sobre el servicio de Consulta, consulte la introducción [del servicio de](../query-service/home.md)Consulta.

### Perfil del cliente en tiempo real

El Perfil de clientes en tiempo real proporciona un perfil de consumo centralizado para la administración personalizada y dirigida de la experiencia. Cada perfil contiene datos agregados en todos los sistemas, así como cuentas con marca de hora procesables de eventos que involucran a personas individuales que han tenido lugar en cualquiera de los sistemas que se utilizan con la plataforma de experiencia.

El Perfil del cliente en tiempo real consume datos con formato de esquema basados en las clases XDM Individual Perfil o XDM ExperienceEvent y responde a consultas basadas en esos datos. Perfil no admite el uso de esquemas basados en otras clases.

Perfil mantiene una instancia de cada perfil de cliente, combinando los datos para formar una &quot;única fuente de verdad&quot; para el individuo. Estos datos unificados se representan usando lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un solo esquema.  Al componer un esquema mediante la interfaz de usuario o la API, puede activar el esquema para utilizarlo con el Perfil del cliente en tiempo real y etiquetarlo para incluirlo en la vista de unión. El esquema etiquetado participará entonces en la definición de esquema que se alimenta con Perfil.

A medida que el Perfil individual XDM y los datos XDM ExperienceEvent se transfieren y administran mediante el catálogo, se activa el Perfil del cliente en tiempo real para empezar a ingestar datos que se han habilitado para su uso. Cuanto más interacciones y detalles se ingieran, más robustos se volverán los perfiles individuales.

Los datos de Perfil individual XDM ayudan a informar y potenciar las acciones en cualquier integración de soluciones de canal o Adobe, y cuando se combinan con un historial rico de datos de comportamiento e interacción, estos datos se utilizan para impulsar el aprendizaje automático. La API de Perfil del cliente en tiempo real también puede utilizarse para enriquecer la funcionalidad de soluciones de terceros, CRM y soluciones propietarias.

Consulte la descripción general [del Perfil del cliente en tiempo](../profile/home.md) real para obtener más información.

### Área de trabajo de ciencia de datos

Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados en la plataforma de experiencia. Data Science Workspace permite a los científicos de datos crear fórmulas basadas en datos de XDM Individual Perfil y XDM ExperienceEvent sobre clientes y sus actividades, lo que facilita predicciones como la tendencia de compra y ofertas recomendadas que el individuo probablemente apreciará y utilizará.

Con Data Science Workspace, los científicos de datos pueden crear fácilmente API de servicios inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otras soluciones de Adobe, incluidas Adobe Destinatario y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y con objetivos.

Para obtener más información sobre el uso de los datos de la plataforma de experiencia para obtener perspectivas, consulte la descripción general [de Área de trabajo](../data-science-workspace/home.md)de Data Science.

### Servicio de decisiones

El servicio de toma de decisiones permite configurar decisiones de oferta personalizadas en aplicaciones integradas en la plataforma. Las Ofertas pueden ser recomendaciones de productos, componentes de contenido para una experiencia web, secuencias de comandos de conversación y acciones a realizar.

El servicio de decisiones aprovecha los datos de Perfil del cliente en tiempo real y, por lo tanto, solo es compatible con conjuntos de datos basados en esquemas que implementan la clase XDM Individual Perfil o XDM ExperienceEvent.

Consulte la información general [del servicio de](../decisioning-service/home.md) decisiones para obtener más información.

## Pasos siguientes

Ahora que comprende mejor el papel de los esquemas en toda la plataforma de experiencia, está preparado para crear su propio inicio.

Para aprender los principios de diseño y las prácticas recomendadas para la composición de esquemas que se utilizarán con la plataforma de experiencias, lea los [conceptos básicos de la composición](schema/composition.md)de esquemas. Para obtener instrucciones paso a paso sobre cómo crear un esquema, consulte los tutoriales sobre cómo crear un esquema [con la API](tutorials/create-schema-api.md) o [con la interfaz](tutorials/create-schema-ui.md)de usuario.