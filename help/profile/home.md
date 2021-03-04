---
keywords: Experience Platform;perfil;perfil de cliente en tiempo real;solución de problemas;API;perfil unificado;perfil unificado;unificado;perfil;rtcp;gráficos XDM
title: Información general del perfil del cliente en tiempo real
topic: guía
description: El perfil del cliente en tiempo real es un almacén de entidades de búsqueda genérica que combina datos de varios activos de datos empresariales y, a continuación, proporciona acceso a esos datos en forma de perfiles de cliente individuales y eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 0%

---


# Información general del [!DNL Real-time Customer Profile]

Adobe Experience Platform le permite ofrecer experiencias coordinadas, coherentes y relevantes a sus clientes independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente al combinar datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar los datos de sus clientes en una vista unificada que ofrece una cuenta procesable con marca de tiempo de cada interacción con los clientes. Esta descripción general le ayudará a comprender la función y el uso de [!DNL Real-time Customer Profile] en [!DNL Experience Platform].

## [!DNL Profile] en Experience Platform

La relación entre el perfil del cliente en tiempo real y otros servicios dentro de Experience Platform se resalta en el siguiente diagrama:

![](images/profile-overview/profile-in-platform.png)

## Explicación de los perfiles

[!DNL Real-time Customer Profile] combina datos de varios sistemas empresariales y, a continuación, proporciona acceso a esos datos en forma de perfiles de clientes con eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales. Las siguientes secciones destacan algunos de los conceptos principales que debe comprender para crear y mantener perfiles de forma eficaz dentro de Platform.

### Almacenamiento de datos de perfil

Aunque [!DNL Real-time Customer Profile] procesa los datos ingestados y utiliza Adobe Experience Platform [!DNL Identity Service] para combinar los datos relacionados mediante la asignación de identidad, mantiene sus propios datos en el almacén de datos [!DNL Profile]. El almacén [!DNL Profile] es independiente de los datos del catálogo en el lago de datos y de los datos [!DNL Identity Service] en el gráfico de identidad.

El Almacenamiento de perfiles utiliza una infraestructura de Microsoft Azure Cosmos DB y Platform Data Lake utiliza el almacenamiento de Microsoft Azure Data Lake.

### Protecciones de perfil

Experience Platform proporciona una serie de protecciones que le ayudan a evitar la creación de esquemas del [Modelo de datos de experiencia (XDM)](../xdm/home.md) que el Perfil del cliente en tiempo real no puede admitir. Esto incluye límites leves que resultarán en una degradación del rendimiento, así como límites duros que resultarán en errores y averías del sistema. Para obtener más información, incluida una lista de directrices y ejemplos de casos de uso, consulte la documentación de [Protección de perfil](guardrails.md).

### (Beta) Panel de perfiles {#profile-dashboard}

>[!IMPORTANT]
>
>La funcionalidad del panel está actualmente en fase beta y no está disponible para todos los usuarios. La documentación y las funciones están sujetas a cambios.

La interfaz de usuario de Experience Platform proporciona un tablero en el que puede ver información importante sobre los datos del perfil del cliente en tiempo real, tal como se capturan durante una instantánea diaria. Para obtener información sobre cómo acceder y trabajar con el tablero [!DNL Profile] en la interfaz de usuario, así como información detallada sobre las métricas mostradas en el tablero, consulte la [Guía de la interfaz de usuario del tablero de perfil](ui/profile-dashboard.md).

### Fragmentos de perfil frente a perfiles combinados {#profile-fragments-vs-merged-profiles}

Cada perfil de cliente individual está compuesto por varios fragmentos de perfil que se han combinado para formar una sola vista de ese cliente. Por ejemplo, si un cliente interactúa con la marca a través de varios canales, su organización tendrá varios fragmentos de perfil relacionados con ese único cliente que aparecerán en varios conjuntos de datos. Cuando estos fragmentos se incorporan a Platform, se combinan para crear un perfil único para ese cliente.

Cuando los datos de múltiples fuentes entran en conflicto (por ejemplo, un fragmento enumera al cliente como &quot;soltero&quot; mientras que el otro lo enumera como &quot;casado&quot;), la [política de combinación](#merge-policies) determina qué información se debe priorizar e incluir en el perfil del individuo. Por lo tanto, es probable que el número total de fragmentos de perfil dentro de Platform siempre sea mayor que el número total de perfiles combinados, ya que cada perfil está compuesto por varios fragmentos.

### Registrar datos

Un perfil es una representación de un asunto, una organización o un individuo, compuesta por muchos atributos (también conocidos como datos de registro). Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellido y dirección de correo electrónico. Con [!DNL Experience Platform], puede personalizar perfiles para que utilicen datos específicos relevantes para su negocio. La clase estándar [!DNL Experience Data Model] (XDM), [!DNL XDM Individual Profile], es la clase preferida sobre la que se crea un esquema al describir datos de registros de clientes y proporciona la integración de datos a muchas interacciones entre los servicios de Platform. Para obtener más información sobre cómo trabajar con esquemas en [!DNL Experience Platform], comience leyendo la [información general del sistema XDM](../xdm/home.md).

### Eventos de series temporales

Los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto realizó una acción directa o indirectamente, así como datos que detallan el propio evento. Representados por la clase de esquema estándar XDM ExperienceEvent, los datos de series temporales pueden describir eventos como elementos que se agregan a un carro, vínculos en los que se hace clic y vídeos vistos. Los datos de series temporales se pueden utilizar para basar las reglas de segmentación en y se puede acceder a los eventos de forma individual en el contexto de un perfil.

### Identidades

Cada empresa quiere comunicarse con sus clientes de una manera que se sienta personal. Sin embargo, uno de los desafíos de ofrecer experiencias digitales relevantes a los clientes es comprender cómo unir sus datos desconectados, lo que a menudo se propaga a través de diferentes canales digitales, como tabletas, teléfonos móviles y portátiles. [!DNL Identity Service] le permite crear una imagen completa de su cliente vinculando identidades de varios canales y creando un gráfico de identidad para cada cliente. Visite la [información general del servicio de identidad](../identity-service/home.md) para obtener más información.

### Combinar directivas

Al unir fragmentos de datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se utilizarán para crear el perfil del cliente. Cuando hay datos conflictivos de varios conjuntos de datos, la política de combinación determinará cómo se deben tratar esos datos y qué valor se debe utilizar. Con las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar las políticas existentes y establecer una directiva de combinación predeterminada para su organización.

Para obtener más información sobre cómo trabajar con políticas de combinación utilizando la API [!DNL Real-time Customer Profile], consulte la [guía de extremo de directivas de combinación](api/merge-policies.md). Para trabajar con políticas de combinación utilizando la interfaz de usuario [!DNL Experience Platform], consulte la [guía de la interfaz de usuario de directivas de combinación](ui/merge-policies.md).

### Esquemas de unión {#profile-fragments-and-union-schemas}

Una de las características clave de [!DNL Real-time Customer Profile] es la capacidad de unificar los datos de varios canales. Cuando se utiliza [!DNL Real-time Customer Profile] para acceder a una entidad, puede proporcionarle una vista combinada de todos los fragmentos de perfil de esa entidad en todos los conjuntos de datos, denominados &quot;vista de unión&quot; y posibles gracias a lo que se conoce como esquema de unión.

Para obtener más información sobre los esquemas de unión, incluido cómo acceder a los esquemas de unión en la interfaz de usuario, visite la [guía de la interfaz de usuario del esquema de unión](ui/union-schema.md).

### (Alpha) Atributos calculados

>[!IMPORTANT]
>
>La funcionalidad de atributo calculada está en alfa. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados son funciones que se utilizan para acumular datos de nivel de evento en atributos de nivel de perfil. Estas funciones se calculan automáticamente para que se puedan utilizar en toda la segmentación, activación y personalización. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con elementos como el valor de compra de por vida, el tiempo entre compras o el número de aperturas de aplicaciones, sin que sea necesario realizar cálculos complejos manualmente cada vez que se necesite la información. Para obtener más información sobre los atributos calculados, incluida la comprensión de la función que los atributos calculados juegan en Adobe Experience Platform, comience por leer la [información general de los atributos calculados](computed-attributes/overview.md).

## Perfiles y segmentos

Adobe Experience Platform [!DNL Segmentation Service] produce las audiencias necesarias para impulsar las experiencias para sus clientes individuales. Cuando se crea un segmento de audiencia, el ID de ese segmento se agrega a la lista de pertenencia a segmentos para todos los perfiles aptos. Las reglas de segmentos se crean y aplican a los datos [!DNL Real-time Customer Profile] mediante las API de RESTful y la interfaz de usuario del Generador de segmentos. Para obtener más información sobre la segmentación, comience leyendo la [información general del Servicio de segmentación](../segmentation/home.md).

### Incorporación por secuencias y segmentación por secuencias

La entrada en tiempo real es posible a través de un proceso llamado ingesta de flujo continuo. A medida que se incorporan los datos de perfil y serie temporal, [!DNL Real-time Customer Profile] decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo llamado segmentación de flujo continuo, antes de combinarlos con los datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos instantáneamente y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca. Durante la ingesta, los datos también se someten a validación para garantizar que se introduzcan correctamente y se ajusten al esquema en el que se basa el conjunto de datos. Para obtener más información sobre qué validación se realiza durante la ingesta, comience por leer la [descripción general de la calidad de la ingesta de datos](../ingestion/quality/overview.md).

## Proyecciones perimetrales

Para ofrecer experiencias coordinadas, coherentes y personalizadas a sus clientes en varios canales en tiempo real, es necesario disponer fácilmente de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. Adobe Experience Platform permite este acceso en tiempo real a los datos mediante lo que se conoce como perímetros. Un Edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Por ejemplo, las aplicaciones de Adobe, como Adobe Target y Adobe Campaign, utilizan perímetros para ofrecer experiencias de cliente personalizadas en tiempo real. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que se pondrá a disposición en el borde. Para obtener más información y empezar a trabajar con proyecciones mediante la API [!DNL Real-time Customer Profile], consulte la [guía de puntos finales de proyección de Edge](api/edge-projections.md).

## Ingesta de datos en [!DNL Profile]

[!DNL Platform] se puede configurar para enviar datos de registros y series temporales a  [!DNL Profile], admitiendo la ingesta de flujo en tiempo real y la ingesta por lotes. Para obtener más información, consulte el tutorial que describe cómo [agregar datos al perfil del cliente en tiempo real](tutorials/add-profile-data.md).

>[!NOTE]
>
>Los datos recopilados a través de las soluciones de Adobe, incluidas [!DNL Analytics Cloud], [!DNL Marketing Cloud] y [!DNL Advertising Cloud], se transfieren a [!DNL Experience Platform] y se incorporan a [!DNL Profile].

### Métricas de ingesta de perfiles

Observability Insights permite exponer métricas clave en Adobe Experience Platform. Además de las estadísticas de uso de [!DNL Experience Platform] y los indicadores de rendimiento para varias funcionalidades de [!DNL Platform] , existen métricas específicas relacionadas con el perfil que permiten conocer las tasas de solicitudes entrantes, las tasas de ingesta exitosas, los tamaños de registro ingeridos y mucho más. Para obtener más información, comience por leer la [información general de la API de Observability Insights](../observability/api/overview.md) y para obtener una lista completa de las métricas del Perfil del cliente en tiempo real, consulte la documentación sobre [métricas disponibles](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] y [!DNL Privacy]

[!DNL Data governance] es una serie de estrategias y tecnologías que se utilizan para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos.

En cuanto al acceso a los datos, el control de datos desempeña un papel clave en [!DNL Experience Platform] a varios niveles:
* Etiquetado del uso de los datos
* Políticas de acceso a los datos
* Control de acceso de datos para acciones de marketing

[!DNL Data governance] se administra en varios puntos. Entre ellas, decidir qué datos se introducen en [!DNL Platform] y qué datos se pueden acceder después de la ingesta para una acción de marketing determinada. Para obtener más información, comience por leer la [información general del control de datos](../data-governance/home.md).

### Gestión de solicitudes de exclusión y privacidad de datos

[!DNL Experience Platform] permite a los clientes enviar solicitudes de exclusión relacionadas con el uso y almacenamiento de sus datos en  [!DNL Real-time Customer Profile]. Para obtener más información sobre cómo se gestionan las solicitudes de exclusión, consulte la documentación sobre [cumplimiento de las solicitudes de exclusión](../segmentation/honoring-opt-outs.md).

## Pasos siguientes y recursos adicionales

Para obtener más información sobre cómo trabajar con datos de [!DNL Real-time Customer Profile] mediante la interfaz de usuario de Experience Platform o la API de perfil, comience por leer la [Guía del desarrollador de la ](ui/user-guide.md) o la [Guía del desarrollador de API](api/overview.md), respectivamente.