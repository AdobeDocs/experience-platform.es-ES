---
keywords: Experience Platform;inicio;temas populares;XDM;sistema XDM;perfil individual XDM;ExperienceEvent XDM;Evento de experiencia XDM;experienceEvent;evento de experiencia;grupos de campos;grupo de campos;grupo de campos;evento de experiencia;evento de experiencia XDM;evento de experiencia XDM;evento de experiencia;evento de experiencias;evento de experiencias XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos Registro;Registro de esquemas;biblioteca de esquemas;Biblioteca de esquemas;esquema;datos de registros;serie temporal;serie temporal
solution: Experience Platform
title: Información general del sistema XDM
topic-legacy: overview
description: La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. Experience Data Model (XDM), impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 9fda5dad7b7e29c88598ff299c26277a015277a6
workflow-type: tm+mt
source-wordcount: '1993'
ht-degree: 2%

---

# Información general del sistema XDM

>[!NOTE]
>
>El término &quot;mixin&quot; se ha actualizado al esquema &quot;grupo de campos&quot; para promover la comprensión. Los grupos de campos son un conjunto de campos reutilizables para admitir casos de uso empresarial. Este cambio ahora se refleja en la API del Registro de esquemas, la interfaz de usuario de Adobe Experience Platform y en toda la documentación de Platform.

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes que permiten a cualquier aplicación comunicarse con los servicios de Platform. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente pueden incorporarse a una representación común que puede proporcionar perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y expresar atributos del cliente con fines de personalización.

XDM es el marco fundamental que permite a Adobe Experience Cloud, con tecnología de Experience Platform, entregar el mensaje correcto a la persona adecuada, en el canal correcto, exactamente en el momento adecuado. La metodología en la que se crea el Experience Platform, el sistema XDM, operacionaliza los [!DNL Experience Data Model] esquemas para su uso por los servicios de Platform.

Este documento proporciona una visión general de la función del sistema XDM dentro de Experience Platform.

## Esquemas XDM

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en Platform, se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase base y de cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte los [conceptos básicos de la composición de esquema](schema/composition.md).

### Componentes XDM estándar

XDM proporciona una sólida recopilación de grupos de campos estándar y tipos de datos, que están diseñados para capturar conceptos comunes y casos de uso en diferentes industrias. Experience Platform le permite filtrar estos componentes por sector, lo que le permite construir de forma rápida y segura esquemas que respondan mejor a sus necesidades empresariales particulares.

Al crear esquemas en la interfaz de usuario del Experience Platform, los grupos de campos enumerados se muestran con una métrica de popularidad. Esta métrica se determina según la frecuencia con la que otros usuarios de Platform emplean el grupo de campos en sus esquemas. Cuanto mayor sea el número, más popular será el grupo de campos. De forma predeterminada, los resultados se muestran de los más populares a los menos populares, lo que le mantiene informado de las tendencias de modelado de datos de su sector.

![Popularidad del grupo de campos](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform proporciona una interfaz de usuario y una API RESTful desde la cual puede ver y administrar todos los recursos relacionados con el esquema en el Experience Platform **[!DNL Schema Library]**. El [!DNL Schema Library] contiene componentes XDM estándar que se ponen a su disposición por Adobe, así como recursos de socios Experience Platform y proveedores cuyas aplicaciones utiliza.

Con el espacio de trabajo [!DNL Schema Registry API] o [!UICONTROL Esquemas] en la interfaz de usuario de Platform, también puede crear y administrar nuevos esquemas y recursos que sean exclusivos de su organización.

Para obtener más información sobre cómo administrar e interactuar con esquemas en Platform, consulte la siguiente documentación:

* [Guía de interfaz de usuario de XDM](./ui/overview.md)
* [Guía de API del Registro de Esquemas](./api/overview.md)

## Comportamientos de datos en el sistema XDM {#data-behaviors}

Los datos que se van a usar en el Experience Platform se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirectamente.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el menor número de propiedades que debe contener un esquema para representar un comportamiento de datos determinado.

Aunque puede definir sus propias clases dentro de [!DNL Schema Registry], se recomienda utilizar las clases preferidas **[!UICONTROL XDM Individual Profile]** y **[!UICONTROL XDM ExperienceEvent]** para los datos de registros y series temporales, respectivamente. Estas clases se describen con más detalle a continuación.

### [!UICONTROL Perfil individual XDM] {#xdm-individual-profile}

[!UICONTROL XDM Individual ] Profiles es una clase basada en registros que forma una representación singular de los atributos de sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o participaciones específicas, y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

Los perfiles menos identificados pueden consistir únicamente en señales de comportamiento anónimas, como las cookies del explorador. En este caso, los datos de perfil dispersos se utilizan para crear una base de información en la que se recopilan y almacenan los intereses y preferencias del perfil anónimo. Estos identificadores pueden ser más detallados a lo largo del tiempo, ya que el sujeto se registra en las notificaciones, suscripciones, compras, etc. Este aumento en los atributos de perfil puede resultar en un asunto identificado y permitir un mayor grado de participación objetivo.

A medida que un perfil sigue creciendo, se convierte en un sólido repositorio de la información personal, la información de identificación, los detalles de contacto y las preferencias de comunicación de un individuo.

Para obtener más información sobre la estructura y el caso de uso de los campos proporcionados por la clase, consulte la [[!UICONTROL XDM Individual Profile] guía de referencia](./classes/individual-profile.md) .

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produjo un evento (o conjunto de eventos), incluyendo el punto en el tiempo y la identidad del sujeto involucrado. Los eventos de experiencia son registros fácticos inmutables de lo que ocurrió en ese momento, que representan lo que ocurrió sin agregación ni interpretación. Son esenciales para el análisis del dominio de tiempo, ya que se pueden utilizar para analizar los cambios que se producen en una ventana de tiempo determinada y para comparar entre varias ventanas de tiempo a fin de rastrear tendencias.

Los eventos de experiencia pueden ser explícitos o implícitos. Los eventos explícitos son acciones humanas directamente observables que se producen durante un punto del recorrido. Los eventos implícitos son eventos que se producen sin una acción humana directa, pero que siguen estando relacionados con un individuo. Algunos ejemplos de eventos implícitos pueden ser el envío programado de boletines de correo electrónico o el voltaje de la batería que alcanza un cierto umbral.

Aunque no todos los eventos se clasifican fácilmente en todas las fuentes de datos, es extremadamente valioso armonizar eventos similares en tipos similares siempre que sea posible para su procesamiento.

![Recorrido del cliente de ExperienceEvent](images/overview/experience-event-journey.png)

Consulte la [[!UICONTROL Guía de referencia de ExperienceEvent] XDM](./classes/experienceevent.md) para obtener más información sobre la estructura y el caso de uso de los campos proporcionados por la clase.

## Esquemas XDM y servicios de Experience Platform

Experience Platform no depende del esquema, lo que significa que cualquier esquema que se ajuste al estándar XDM está disponible para los servicios de Platform. A continuación se describen con más detalle las formas en que los distintos servicios de Platform utilizan esquemas.

### Servicio de catálogo, ingesta de datos y lago de datos

El servicio de catálogo es el sistema de registro de los recursos del Experience Platform y sus esquemas relacionados. El catálogo no contiene los archivos de datos o directorios reales, sino que contiene los metadatos y las descripciones de esos archivos y directorios.

Los datos del catálogo se almacenan en el lago de datos, un almacén de datos muy granular que contiene todos los datos administrados por Platform, independientemente del origen o el formato de archivo.

Para empezar a ingerir datos en Experience Platform, puede utilizar el servicio de catálogo para crear un conjunto de datos. El conjunto de datos hace referencia a un esquema XDM que describe la estructura de los datos que se van a introducir. Si se crea un conjunto de datos sin un esquema, el Experience Platform deriva un &quot;esquema observado&quot; inspeccionando el tipo y el contenido de los campos de datos introducidos. A continuación, se realiza el seguimiento de los conjuntos de datos en el catálogo y se almacenan en el lago de datos junto con los esquemas y esquemas observados en los que se basan.

Para obtener más información sobre Catálogo, consulte la [Descripción general del Servicio de Catálogo](../catalog/home.md). Para obtener más información sobre la ingesta de datos de Adobe Experience Platform, consulte [Data Ingestion overview](../ingestion/home.md).

### Servicio de consultas

El servicio de consulta de Adobe Experience Platform le permite utilizar SQL estándar para consultar los datos del Experience Platform y admitir muchos casos de uso diferentes.

Una vez compuesto un esquema y creado un conjunto de datos que hace referencia a ese esquema, los datos se incorporan y almacenan en el lago de datos. Con el servicio de consulta, puede unirse a cualquier conjunto de datos en el lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para su uso en sistemas de informes, aprendizaje automático o para su incorporación al perfil del cliente en tiempo real.

Consulte [Información general del servicio de consulta](../query-service/home.md) para obtener más información sobre el servicio.

### Perfil del cliente en tiempo real

El perfil del cliente en tiempo real proporciona un perfil de cliente centralizado para la administración de experiencias personalizadas y con un público objetivo. Cada perfil contiene datos agregados en todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que involucran al individuo que han tenido lugar en cualquiera de los sistemas que utiliza con el Experience Platform.

El perfil del cliente en tiempo real consume datos con formato de esquema basados en las clases [!UICONTROL XDM Individual Profile] y [!UICONTROL XDM ExperienceEvent] y responde a consultas basadas en esos datos. El perfil no admite el uso de esquemas basados en otras clases.

El sistema mantiene una instancia de cada perfil del cliente, combinando los datos para formar una &quot;única fuente de verdad&quot; para el individuo. Estos datos unificados se representan con lo que se conoce como &quot;esquema de unión&quot; (también denominado &quot;vista de unión&quot;). Un esquema de unión agrega los campos de todos los esquemas que implementan la misma clase en un esquema único.  Al componer un esquema mediante la interfaz de usuario o la API, puede habilitar el esquema para utilizarlo con el perfil del cliente en tiempo real y etiquetarlo para su inclusión en la unión. El esquema etiquetado participará después en la definición del esquema que se va a enviar a Perfil.

Como los datos de [!UICONTROL XDM Individual Profile] y [!UICONTROL XDM ExperienceEvent] se incorporan en el lago de datos, el perfil del cliente en tiempo real ingesta cualquier dato que se haya habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más robustos se vuelven los perfiles individuales.

[!UICONTROL Los ] perfiles individuales de XDM ayudan a informar y potenciar las acciones en cualquier integración de producto de canal o Adobe. Cuando se asocia con un historial rico de datos de comportamiento e interacción, estos datos se pueden utilizar para impulsar el aprendizaje automático. La API de perfil de cliente en tiempo real también se puede utilizar para enriquecer la funcionalidad de soluciones de terceros, CRM y soluciones propietarias.

Consulte la [Descripción general del perfil del cliente en tiempo real](../profile/home.md) para obtener más información.

### Data Science Workspace

Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para obtener perspectivas de los datos almacenados en el Experience Platform. Data Science Workspace permite a los científicos de datos crear fórmulas basadas en datos de [!UICONTROL XDM Individual Profile] y [!UICONTROL XDM ExperienceEvent] sobre clientes y sus actividades, facilitando predicciones como la compra de inclinación y ofertas recomendadas que el individuo probablemente apreciará y utilizará.

Con Data Science Workspace, los científicos de datos pueden crear fácilmente API de servicio inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otras soluciones de Adobe, incluidas Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y dirigidas.

Para obtener más información sobre el uso de datos de Experience Platform para impulsar perspectivas, consulte la [información general de Data Science Workspace](../data-science-workspace/home.md).

## Pasos siguientes y recursos adicionales

Ahora que comprende mejor el papel de los esquemas a través del Experience Platform, está listo para empezar a componer los suyos.

Para aprender los principios de diseño y las prácticas recomendadas para componer esquemas que se van a utilizar con el Experience Platform, comience por leer los [conceptos básicos de la composición del esquema](schema/composition.md). Para obtener instrucciones paso a paso sobre cómo crear un esquema, consulte los tutoriales sobre la creación de un esquema [con la API](tutorials/create-schema-api.md) o [con la interfaz de usuario](tutorials/create-schema-ui.md).

Para reforzar su comprensión de [!DNL XDM System] en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
