---
keywords: Experience Platform;inicio;temas populares;XDM;sistema XDM;perfil individual de XDM;XDM ExperienceEvent;XDM ExperienceEvent;evento de experiencia;evento de experiencia;grupos de campos;grupos de campos;grupo de campos;grupo de campos;evento de experiencia;evento de experiencia XDM;evento de experiencia;XDM ExperienceEvent;experienceEvent;experienceevent;evento de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;biblioteca de esquemas;esquema;datos de registro;serie temporal;serie temporal
solution: Experience Platform
title: Información general del sistema XDM
description: La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. El modelo de datos de experiencia (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '2083'
ht-degree: 4%

---

# Información general del sistema XDM

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsado por Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación documentada públicamente y diseñada para mejorar la potencia de las experiencias digitales. Proporciona estructuras y definiciones comunes que permiten que cualquier aplicación utilice para comunicarse con los servicios de Platform. Al adherirse a los estándares XDM, todos los datos de experiencia del cliente se pueden incorporar en una representación común que puede ofrecer perspectivas de una manera más rápida e integrada. Puede obtener información valiosa de las acciones de los clientes, definir las audiencias de los clientes mediante segmentos y expresar los atributos del cliente con fines de personalización.

XDM es el marco de trabajo básico que permite a Adobe Experience Cloud, con tecnología de Experience Platform, enviar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento exacto. La metodología en la que se crea Experience Platform, el sistema XDM, pone en funcionamiento [!DNL Experience Data Model] esquemas para su uso en los servicios de Platform.

Obtenga información acerca de la función que desempeña el sistema XDM en Experience Platform.

## Esquemas XDM

Experience Platform utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de forma coherente en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir datos en Platform, se debe crear un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se pueden contener en cada campo. Los esquemas constan de una clase base y cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición de esquemas, incluidos los principios de diseño y las prácticas recomendadas, consulte la [conceptos básicos de composición de esquemas](schema/composition.md).

### Componentes XDM estándar

XDM proporciona una colección sólida de grupos de campos y tipos de datos estándar, que están pensados para capturar conceptos y casos de uso comunes en diferentes industrias. Experience Platform le permite filtrar estos componentes por sector, lo que le permite crear de forma rápida y segura esquemas que mejor se ajusten a sus necesidades empresariales específicas.

Al construir esquemas en la interfaz de usuario del Experience Platform, los grupos de campos enumerados se muestran con una métrica de popularidad. Esta métrica está determinada por la frecuencia con la que otros usuarios de Platform emplean el grupo de campos en sus esquemas. Cuanto mayor sea el número, más popular será el grupo de campos. De forma predeterminada, los resultados se muestran de los más populares a los menos populares, lo que le mantiene informado de las tendencias de modelado de datos en su industria.

![Popularidad de grupo de campos](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform proporciona una interfaz de usuario y una API RESTful desde las cuales puede ver y administrar todos los recursos relacionados con esquemas en el Experience Platform **[!DNL Schema Library]**. El [!DNL Schema Library] contiene componentes XDM estándar que Adobe pone a su disposición, así como recursos de socios y proveedores Experience Platform cuyas aplicaciones utiliza.

Uso del [!DNL Schema Registry API] o el [!UICONTROL Esquemas] Workspace en la IU de Platform, también puede crear y administrar nuevos esquemas y recursos que sean únicos para su organización.

Para obtener más información sobre cómo administrar e interactuar con esquemas en Platform, consulte la siguiente documentación:

* [Guía de IU de XDM](./ui/overview.md)
* [Guía de API de Registro de esquemas](./api/overview.md)

## Comportamientos de datos en el sistema XDM {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Comportamientos de datos"
>abstract="Los datos que se van a usar en Experience Platform se agrupan en tres tipos de comportamiento: registro, serie temporal y ad hoc. Los esquemas de registro proporcionan información sobre los atributos de un asunto, mientras que los esquemas de series temporales capturan una instantánea del sistema en el momento en que se realizó una acción. Los esquemas ad hoc capturan campos que son áreas de nombres para uso exclusivo de un conjunto de datos. Consulte la documentación para obtener más información sobre los comportamientos de los datos en Platform."

Los datos que se van a utilizar en Experience Platform se agrupan en tres tipos de comportamiento:

* **Registro**: Proporciona información sobre los atributos de un asunto. Un sujeto podría ser una organización o un individuo.
* **Serie temporal**: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción, directa o indirectamente.
* **Ad hoc**: captura campos con un espacio de nombres para que los utilice un solo conjunto de datos. Los esquemas ad hoc se utilizan en varios flujos de trabajo de ingesta de datos para Experience Platform, incluida la ingesta de archivos CSV y la creación de determinados tipos de conexiones de origen.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el número más pequeño de propiedades que debe contener un esquema para representar un comportamiento de datos determinado.

Aunque puede definir sus propias clases dentro de la variable [!DNL Schema Registry]No obstante, se recomienda utilizar las clases estándar **[!UICONTROL Perfil individual de XDM]** y **[!UICONTROL ExperienceEvent de XDM]** para datos de registros y series temporales, respectivamente. Estas clases se describen con más detalle a continuación.

>[!NOTE]
>
>No hay clases estándar basadas en el comportamiento ad hoc. Los procesos de Platform que los utilizan generan automáticamente esquemas ad hoc, pero también se pueden [creado manualmente con la API de Registro de esquemas](./tutorials/ad-hoc.md).

### [!UICONTROL Perfil individual de XDM] {#xdm-individual-profile}

[!UICONTROL Perfil individual de XDM] es una clase basada en registros que forma una representación singular de los atributos de los sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o compromisos específicos y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

Los perfiles menos identificados solo pueden consistir en señales de comportamiento anónimas, como las cookies del explorador. En este caso, los escasos datos de perfil se utilizan para crear una base de información en la que se recopilan y almacenan los intereses y preferencias del perfil anónimo. Estos identificadores pueden ser más detallados con el tiempo a medida que el sujeto se suscribe a notificaciones, suscripciones, compras, etc. Este aumento en los atributos del perfil puede dar como resultado final la identificación de un sujeto y permitir un mayor grado de participación segmentada.

A medida que un perfil crece, se convierte en un repositorio sólido de la información personal de una persona, la información de identificación, los detalles de contacto y las preferencias de comunicación.

Consulte la [[!UICONTROL Perfil individual de XDM] guía de referencia](./classes/individual-profile.md) para obtener más información sobre la estructura y el caso de uso de los campos proporcionados por la clase.

### [!UICONTROL ExperienceEvent de XDM] {#xdm-experience-event}

ExperienceEvent de XDM es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produjo un evento (o conjunto de eventos), incluido el momento y la identidad del sujeto involucrado. Los Eventos de experiencia son registros fácticos e inmutables de lo que ocurrió en ese momento, y representan lo que sucedió sin agregación ni interpretación. Son esenciales para el análisis en el dominio del tiempo, ya que se pueden utilizar para analizar los cambios que se producen en un intervalo de tiempo determinado y para comparar varias ventanas de tiempo con el fin de rastrear las tendencias.

Los eventos de experiencia pueden ser explícitos o implícitos. Los eventos explícitos son acciones humanas directamente observables que tienen lugar durante un punto de un recorrido. Los eventos implícitos son eventos que se producen sin una acción humana directa, pero que siguen estando relacionados con un individuo. Ejemplos de eventos implícitos pueden incluir el envío programado de boletines de correo electrónico o el voltaje de la batería que alcanza un determinado umbral.

Aunque no todos los eventos se clasifican fácilmente en todas las fuentes de datos, es extremadamente valioso armonizar eventos similares en tipos similares siempre que sea posible para el procesamiento.

![Recorrido del cliente de ExperienceEvent](images/overview/experience-event-journey.png)

Consulte la [[!UICONTROL ExperienceEvent de XDM] guía de referencia](./classes/experienceevent.md) para obtener más información sobre la estructura y el caso de uso de los campos proporcionados por la clase.

## Esquemas XDM y servicios de Experience Platform

Experience Platform no depende del esquema, lo que significa que cualquier esquema que se ajuste al estándar XDM está disponible para los servicios de Platform. A continuación, se describen más detalladamente las formas en que los distintos servicios de Platform utilizan esquemas.

### Servicio de catálogo, ingesta de datos y lago de datos

El servicio de catálogo es el sistema de registro para los recursos de Experience Platform y sus esquemas relacionados. El catálogo no contiene los archivos o directorios de datos reales, sino que contiene los metadatos y las descripciones de esos archivos y directorios.

Los datos del catálogo se almacenan en el lago de datos, un almacén de datos muy granular que contiene todos los datos administrados por Platform, independientemente del origen o el formato de archivo.

Para empezar a ingerir datos en Experience Platform, puede utilizar el servicio de catálogo para crear un conjunto de datos. El conjunto de datos hace referencia a un esquema XDM que describe la estructura de los datos que se van a introducir. Si se crea un conjunto de datos sin un esquema, Experience Platform deriva un &quot;esquema observado&quot; inspeccionando el tipo y el contenido de los campos de datos introducidos. A continuación, se realiza el seguimiento de los conjuntos de datos en el catálogo y se almacenan en el lago de datos junto con los esquemas y esquemas observados en los que se basan.

Para obtener más información sobre el catálogo, consulte la [Resumen del servicio de catálogo](../catalog/home.md). Para obtener más información sobre la ingesta de datos de Adobe Experience Platform, consulte la [Resumen de ingesta de datos](../ingestion/home.md).

### Servicio de consultas

Adobe Experience Platform Query Service permite utilizar SQL estándar para consultar los datos del Experience Platform para admitir muchos casos de uso diferentes.

Una vez que se ha compuesto un esquema y se ha creado un conjunto de datos que hace referencia a ese esquema, los datos se incorporan y almacenan en el lago de datos. Con el servicio de consulta, puede unirse a cualquier conjunto de datos del lago de datos y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en el sistema de informes, el aprendizaje automático o para su inserción en el perfil del cliente en tiempo real.

Consulte la [Introducción al servicio de consultas](../query-service/home.md) para obtener más información sobre el servicio.

### Perfil del cliente en tiempo real

El Perfil del cliente en tiempo real proporciona un perfil de consumidor centralizado para la administración de experiencias personalizada y dirigida. Cada perfil contiene datos agregados de todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que implican a la persona que ha tenido lugar en cualquiera de los sistemas que utiliza con Experience Platform.

El perfil del cliente en tiempo real consume datos con formato de esquema basados en el [!UICONTROL Perfil individual de XDM] y [!UICONTROL ExperienceEvent de XDM] y responde a consultas basadas en esos datos. El perfil no admite el uso de esquemas basados en otras clases.

El sistema mantiene una instancia de cada perfil del cliente, combinando los datos para formar una &quot;única fuente fiable&quot; para el individuo. Estos datos unificados se representan con lo que se conoce como &quot;esquema de unión&quot; (a veces denominado &quot;vista de unión&quot;). Un esquema de unión agrega los campos de todos los esquemas que implementan la misma clase en un único esquema.  Al maquetar un esquema mediante la interfaz de usuario o la API de, puede activar el esquema para utilizarlo con el perfil del cliente en tiempo real y etiquetarlo para incluirlo en la unión. El esquema etiquetado participará en la definición del esquema que se envía al perfil.

Como [!UICONTROL Perfil individual de XDM] y [!UICONTROL ExperienceEvent de XDM] Si los datos de se incorporan al lago de datos, el perfil del cliente en tiempo real ingiere cualquier dato que se haya habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más sólidos se volverán los perfiles individuales.

[!UICONTROL Perfil individual de XDM] Los datos de ayudan a informar y potenciar las acciones en cualquier canal o integración de productos de Adobe. Cuando se asocian con un historial completo de datos de comportamiento e interacción, estos datos se pueden utilizar para potenciar el aprendizaje automático. La API del perfil del cliente en tiempo real también se puede utilizar para enriquecer la funcionalidad de las soluciones de terceros, CRM y soluciones propietarias.

Consulte la [Resumen del perfil del cliente en tiempo real](../profile/home.md) para obtener más información.

### Data Science Workspace

El espacio de trabajo de ciencia de datos de Adobe Experience Platform utiliza aprendizaje automático e inteligencia artificial para obtener perspectivas de los datos almacenados en Experience Platform. El espacio de trabajo de ciencia de datos permite a los científicos de datos crear fórmulas basadas en [!UICONTROL Perfil individual de XDM] y [!UICONTROL ExperienceEvent de XDM] datos sobre los clientes y sus actividades, lo que facilita predicciones como la tendencia a comprar y ofertas recomendadas que el usuario probablemente aprecie y utilice.

Con Data Science Workspace, los científicos de datos pueden crear fácilmente API de servicio inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otras soluciones de Adobe, incluidas Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y específicas.

Para obtener más información sobre el uso de datos de Experience Platform para potenciar las perspectivas, consulte la [Resumen de Data Science Workspace](../data-science-workspace/home.md).

## Pasos siguientes y recursos adicionales

Ahora que comprende mejor el papel de los esquemas a lo largo de Experience Platform, está listo para empezar a componer los suyos propios.

Para conocer los principios de diseño y las prácticas recomendadas para componer esquemas que se van a utilizar con Experience Platform, comience leyendo el [conceptos básicos de composición de esquemas](schema/composition.md). Para obtener instrucciones paso a paso sobre cómo crear un esquema, consulte los tutoriales sobre la creación de un esquema [uso de la API](tutorials/create-schema-api.md) o [uso de la interfaz de usuario](tutorials/create-schema-ui.md).

Para reforzar su comprensión de [!DNL XDM System] en Experience Platform, vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
