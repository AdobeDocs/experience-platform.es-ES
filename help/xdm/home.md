---
keywords: Experience Platform;inicio;temas populares;XDM;sistema XDM;perfil individual XDM;ExperienceEvent XDM;Evento de experiencia XDM;experienceEvent;evento de experiencia;grupos de campos;grupo de campos;grupo de campos;evento de experiencia;evento de experiencia XDM;evento de experiencia XDM;evento de experiencia;evento de experiencias;evento de experiencias XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos Registro;Registro de esquemas;biblioteca de esquemas;Biblioteca de esquemas;esquema;datos de registros;serie temporal;serie temporal
solution: Experience Platform
title: Información general del sistema XDM
topic-legacy: overview
description: La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. Experience Data Model (XDM), impulsado por el Adobe, es un esfuerzo por estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: 58f6c5e3ac77070807f7486bf429493d14fdda9e
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---

# Información general del sistema XDM

>[!NOTE]
>
>El término &quot;mixin&quot; se ha actualizado a &quot;grupo de campos de esquema&quot; para promover la comprensión. Los grupos de campos son un conjunto de campos reutilizables para admitir casos de uso empresarial. Este cambio ahora se refleja en la API del Registro de esquemas, la interfaz de usuario de Adobe Experience Platform y en toda la documentación de Platform.

La estandarización y la interoperabilidad son conceptos clave detrás de Adobe Experience Platform. [!DNL Experience Data Model] (XDM), impulsado por el Adobe, es un esfuerzo para estandarizar los datos de experiencia del cliente y definir esquemas para la administración de experiencias del cliente.

XDM es una especificación públicamente documentada diseñada para mejorar el poder de las experiencias digitales. Proporciona estructuras y definiciones comunes para cualquier aplicación que se utilice para comunicarse con los servicios [!DNL Platform]. Al cumplir con los estándares XDM, todos los datos de experiencia del cliente pueden incorporarse a una representación común que puede proporcionar perspectivas de una manera más rápida e integrada. Puede obtener perspectivas valiosas a partir de las acciones de los clientes, definir audiencias de clientes a través de segmentos y expresar atributos del cliente con fines de personalización.

XDM es el marco básico que permite a Adobe Experience Cloud, con tecnología [!DNL Experience Platform], entregar el mensaje correcto a la persona adecuada, en el canal correcto, en el momento justo. Metodología en la que se crea [!DNL Experience Platform], Sistema XDM, operacionaliza [!DNL Experience Data Model] esquemas para su uso por los servicios [!DNL Platform].

Este documento proporciona información general sobre la función del sistema XDM en [!DNL Experience Platform].

## Esquemas XDM

[!DNL Experience Platform] utiliza esquemas para describir la estructura de los datos de una manera uniforme y reutilizable. Al definir los datos de manera uniforme en todos los sistemas, resulta más fácil conservar el significado y, por lo tanto, obtener valor de los datos.

Antes de poder introducir los datos en [!DNL Platform], se debe componer un esquema para describir la estructura de los datos y proporcionar restricciones al tipo de datos que se puede contener dentro de cada campo. Los esquemas constan de una clase base y de cero o más grupos de campos de esquema.

Para obtener más información sobre el modelo de composición de esquema, incluidos los principios de diseño y las prácticas recomendadas, consulte los [conceptos básicos de la composición de esquema](schema/composition.md).

### [!DNL Schema Registry] y [!DNL Schema Library]

El **[!DNL Schema Registry]** proporciona una interfaz de usuario y una API RESTful desde las que puede ver y administrar todos los recursos relacionados con el esquema en Adobe Experience Platform **[!DNL Schema Library]**. El [!DNL Schema Library] contiene los recursos estándar del sector que se ponen a su disposición por Adobe, así como los recursos de [!DNL Experience Platform] socios y proveedores cuyas aplicaciones utiliza. La interfaz de usuario y la API del Registro de esquemas también se pueden utilizar para crear y administrar nuevos esquemas y recursos que son exclusivos de su organización.

Para obtener una guía completa de las principales operaciones disponibles en [!DNL Schema Registry], consulte la [Guía para desarrolladores de Schema Registry](api/getting-started.md).

## Comportamientos de datos en el sistema XDM {#data-behaviors}

Los datos que se van a usar en [!DNL Experience Platform] se agrupan en dos tipos de comportamiento:

* **Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.
* **Datos** de series temporales: Proporciona una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirectamente.

Todos los esquemas XDM describen datos que pueden clasificarse como registros o series temporales. El comportamiento de los datos de un esquema se define mediante la clase del esquema, que se asigna a un esquema cuando se crea por primera vez. Las clases XDM describen el menor número de propiedades que debe contener un esquema para representar un comportamiento de datos determinado.

Aunque puede definir sus propias clases dentro de [!DNL Schema Registry], se recomienda utilizar las clases preferidas **[!DNL XDM Individual Profile]** y **[!DNL XDM ExperienceEvent]** para los datos de registros y series temporales, respectivamente. Estas clases se describen con más detalle a continuación.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] es una clase basada en registros que forma una representación singular de los atributos de sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o participaciones específicas, y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

Los perfiles menos identificados pueden consistir únicamente en señales de comportamiento anónimas, como las cookies del explorador. En este caso, los datos de perfil dispersos se utilizan para crear una base de información en la que se recopilan y almacenan los intereses y preferencias del perfil anónimo. Estos identificadores pueden ser más detallados a lo largo del tiempo, ya que el sujeto se registra en las notificaciones, suscripciones, compras, etc. Este aumento en los atributos de perfil puede resultar en un asunto identificado y permitir un mayor grado de participación objetivo.

A medida que un perfil de consumidor sigue creciendo, se convierte en un sólido repositorio de la información personal, la información de identificación, los detalles de contacto y las preferencias de comunicación de un individuo.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produjo un evento (o conjunto de eventos), incluyendo el punto en el tiempo y la identidad del sujeto involucrado. Los eventos de experiencia son registros de hechos de lo que ha sucedido, por lo que son inmutables y representan lo que ha sucedido sin agregación ni interpretación. Son esenciales para el análisis del dominio de tiempo, ya que se pueden utilizar para analizar los cambios que se producen en una ventana de tiempo determinada y para comparar entre varias ventanas de tiempo a fin de rastrear tendencias.

Los eventos de experiencia pueden ser explícitos o implícitos. Los eventos explícitos son acciones humanas directamente observables que se producen durante un punto del recorrido. Los eventos implícitos son eventos que se producen sin una acción humana directa, pero que siguen estando relacionados con un individuo. Algunos ejemplos de eventos implícitos pueden ser el envío programado de boletines de correo electrónico o el voltaje de la batería que alcanza un cierto umbral.

Aunque no todos los eventos se clasifican fácilmente en todas las fuentes de datos, es extremadamente valioso armonizar eventos similares en tipos similares siempre que sea posible para su procesamiento.

![Recorrido del cliente de ExperienceEvent](images/overview/experience-event-journey.png)

## Esquemas XDM y servicios [!DNL Experience Platform]

[!DNL Experience Platform] es independiente del esquema, lo que significa que cualquier esquema que se ajuste al estándar XDM está disponible para su uso por parte de los  [!DNL Platform] servicios. A continuación se describen con más detalle las formas en que los distintos servicios [!DNL Platform] utilizan esquemas.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] es el sistema de registro de los  [!DNL Experience Platform] recursos y sus esquemas relacionados. [!DNL Catalog] no son los archivos o directorios que contienen datos, sino que contienen los metadatos y las descripciones de esos archivos y directorios.

[!DNL Catalog] los datos se almacenan en  [!DNL Data Lake], un almacén de datos muy granular que contiene todos los datos administrados por  [!DNL Platform], independientemente del formato de archivo o el origen.

Para empezar a ingerir datos en [!DNL Experience Platform], se crea un conjunto de datos con [!DNL Catalog Service]. El conjunto de datos hace referencia a un esquema XDM que describe la estructura de los datos que se van a introducir. Si se crea un conjunto de datos sin un esquema, [!DNL Experience Platform] derivará un &quot;esquema observado&quot; inspeccionando el tipo y el contenido de los campos de datos ingestados. A continuación, se realiza el seguimiento de los conjuntos de datos en [!DNL Catalog] y se almacenan en [!DNL Data Lake] junto con los esquemas y esquemas observados en los que se basan.

Para obtener más información sobre [!DNL Catalog], consulte la [información general del Servicio de catálogo](../catalog/home.md). Para obtener más información sobre la ingesta de datos de Adobe Experience Platform, consulte [Data Ingestion overview](../ingestion/home.md).

### [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] permite utilizar SQL estándar para consultar los datos [!DNL Experience Platform] con el fin de admitir muchos casos de uso diferentes.

Una vez compuesto un esquema y creado un conjunto de datos que hace referencia a ese esquema, los datos se incorporan y almacenan en [!DNL Data Lake]. Con [!DNL Query Service], puede unirse a cualquier conjunto de datos en [!DNL Data Lake] y capturar los resultados de la consulta como un nuevo conjunto de datos para usar en sistemas de informes, aprendizaje automático o para su incorporación a [!DNL Real-time Customer Profile].

Para obtener más información sobre [!DNL Query Service], consulte la [Introducción del servicio de consulta](../query-service/home.md).

### [!DNL Real-time Customer Profile]

El perfil del cliente en tiempo real proporciona un perfil de cliente centralizado para la administración de experiencias personalizadas y con un público objetivo. Cada perfil contiene datos agregados en todos los sistemas, así como cuentas con marca de tiempo procesables de eventos que involucran al individuo que han tenido lugar en cualquiera de los sistemas que utiliza con [!DNL Experience Platform].

[!DNL Real-time Customer Profile] consume datos con formato de esquema basados en las  [!DNL XDM Individual Profile] clases  [!DNL XDM ExperienceEvent] o y responde a consultas basadas en esos datos. [!DNL Profile] no admite el uso de esquemas basados en otras clases.

[!DNL Profile] mantiene una instancia de cada perfil del cliente, combinando los datos para formar una &quot;única fuente de verdad&quot; para el individuo. Estos datos unificados se representan con lo que se conoce como &quot;vista de unión&quot;. Una vista de unión agrega los campos de todos los esquemas que implementan la misma clase en un esquema único.  Al componer un esquema mediante la interfaz de usuario o la API, puede activar el esquema para utilizarlo con [!DNL Real-time Customer Profile] y etiquetarlo para incluirlo en la vista de unión. El esquema etiquetado participará después en la definición del esquema que se va a alimentar con [!DNL Profile].

Como [!DNL XDM Individual Profile] y [!DNL XDM ExperienceEvent] los datos se incorporan y administran mediante [!DNL Catalog], se déclencheur [!DNL Real-time Customer Profile] que comiencen a introducir datos que se hayan habilitado para su uso. Cuantas más interacciones y detalles se incorporen, más robustos se vuelven los perfiles individuales.

[!DNL XDM Individual Profile] los datos de ayudan a informar y potenciar las acciones en cualquier integración de soluciones de canal o Adobe, y cuando se asocian con un historial rico de datos de comportamiento e interacción, estos datos se utilizan para impulsar el aprendizaje automático. La API [!DNL Real-time Customer Profile] también se puede utilizar para enriquecer la funcionalidad de soluciones de terceros, CRM y soluciones propietarias.

Consulte la [Descripción general del perfil del cliente en tiempo real](../profile/home.md) para obtener más información.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] utiliza aprendizaje automático e inteligencia artificial para obtener perspectivas de los datos almacenados dentro de [!DNL Experience Platform]. [!DNL Data Science Workspace] permite a los científicos de datos crear fórmulas basadas en XDM Individual  [!DNL Profile] y en  [!DNL XDM ExperienceEvent] datos sobre clientes y sus actividades, lo que facilita predicciones como la compra de propensión y ofertas recomendadas que es probable que el individuo aprecie y utilice.

Con [!DNL Data Science Workspace], los científicos de datos pueden crear fácilmente API de servicios inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otras soluciones de Adobe, incluidas Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y dirigidas.

Para obtener más información sobre el uso de [!DNL Experience Platform] datos para potenciar perspectivas, consulte la [información general de Data Science Workspace](../data-science-workspace/home.md).

## Pasos siguientes y recursos adicionales

Ahora que comprende mejor el papel de los esquemas a través de [!DNL Experience Platform], está listo para empezar a componer los suyos. Para complementar su aprendizaje, comience leyendo la documentación sugerida y vea el siguiente vídeo.

Para aprender los principios de diseño y las prácticas recomendadas para componer esquemas que se van a utilizar con [!DNL Experience Platform], comience por leer los [conceptos básicos de la composición del esquema](schema/composition.md). Para obtener instrucciones paso a paso sobre cómo crear un esquema, consulte los tutoriales sobre la creación de un esquema [con la API](tutorials/create-schema-api.md) o [con la interfaz de usuario](tutorials/create-schema-ui.md).

Para reforzar su comprensión de [!DNL XDM System] en [!DNL Experience Platform], vea el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
