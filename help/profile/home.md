---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Información general sobre el Perfil del cliente en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]sobre validación

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con [!DNL Real-time Customer Profile], puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. [!DNL Profile] le permite consolidar sus datos dispares de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes. Esta información general le ayudará a comprender la función y el uso de [!DNL Real-time Customer Profile] en [!DNL Experience Platform].

## Explicación [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] es un almacén de entidades de búsqueda genérico que combina datos de varios recursos de datos empresariales y, a continuación, proporciona acceso a esos datos en forma de perfiles de clientes individuales y eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales.

### [!DNL Profile] almacén de datos

Aunque [!DNL Real-time Customer Profile] procesa datos ingestados y utiliza Adobe Experience Platform [!DNL Identity Service] para combinar datos relacionados mediante asignación de identidad, mantiene sus propios datos en el [!DNL Profile] almacén. En otras palabras, el [!DNL Profile] almacén es independiente de [!DNL Catalog] los datos ([!DNL Data Lake]) y los [!DNL Identity Service] datos (gráfico de identidad).

### [!DNL Profile] y [!DNL Platform] servicios

La relación entre [!DNL Real-time Customer Profile] y otros servicios dentro de [!DNL Experience Platform] se resalta en el siguiente diagrama:

![Relación entre Perfil y otros servicios de Experience Platform.](images/profile-overview/profile-in-platform.png)

### Perfiles y datos de registro

Un perfil es una representación de un sujeto, una organización o una persona, también denominada datos de registro. Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellidos y dirección de correo electrónico. Con [!DNL Experience Platform], puede personalizar perfiles para utilizar tipos de datos relevantes para su empresa. La clase estándar [!DNL Experience Data Model] (XDM) [!DNL Individual Profile] es la clase preferida en la que se genera un esquema al describir datos de registros de clientes y proporciona la información integral a muchas interacciones entre los servicios de plataforma. Para obtener más información sobre cómo trabajar con esquemas en [!DNL Experience Platform], lea la descripción general [del sistema](../xdm/home.md)XDM.

### Eventos de series temporales

Los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto realizó una acción, ya sea directa o indirectamente, así como datos que detallan el propio evento. Representados por la clase de esquema estándar XDM ExperienceEvent, los datos de series temporales pueden describir eventos como elementos que se agregan a un carro, vínculos en los que se hace clic y vídeos vistos. Los datos de series temporales pueden utilizarse para basar las reglas de segmentación en y se puede acceder a los eventos de forma individual en el contexto de un perfil.

### Identidades

Cada empresa quiere comunicarse con sus clientes de una manera que se sienta personal. Sin embargo, uno de los desafíos de ofrecer experiencias digitales relevantes a los clientes es comprender cómo unir sus datos desconectados, lo que a menudo se extiende a través de diferentes canales digitales, como tabletas, teléfonos móviles y portátiles. [!DNL Identity Service] le permite unir la imagen completa de su cliente vinculando identidades de varios canales, creando un gráfico de identidad para cada cliente, lo que le permite comprenderlas mejor. Visite la información general [del servicio de](../identity-service/home.md) identidad para obtener más información.

### Segmentación

Adobe Experience Platform [!DNL Segmentation Service] produce las audiencias necesarias para potenciar las experiencias de sus clientes individuales. Cuando se crea un segmento de audiencia, el ID de ese segmento se agrega a la lista de pertenencias a segmentos para todos los perfiles que cumplen los requisitos. Las reglas de segmentos se generan y aplican a los [!DNL Real-time Customer Profile] datos mediante las API de RESTful y la interfaz de usuario del Generador de segmentos. Para obtener más información sobre la segmentación, lea la información general [del servicio de](../segmentation/home.md)segmentación.

### Fragmentos de perfil y esquemas de unión {#profile-fragments-and-union-schemas}

Una de las características clave de [!DNL Real-time Customer Profile] es la capacidad de unificar datos de varios canales. Cuando [!DNL Real-time Customer Profile] se utiliza para acceder a una entidad, puede suministrarle una vista combinada de todos los fragmentos de perfil de dicha entidad en todos los conjuntos de datos, denominados vistas de unión y posibles mediante lo que se conoce como esquema de unión. [!DNL Real-time Customer Profile] los datos se combinan entre fuentes cuando su ID accede a una entidad o perfil o se exportan como un segmento. Para obtener más información sobre el acceso a perfiles y vistas de unión mediante la [!DNL Real-time Customer Profile] API, visite la guía [de extremo de](api/entities.md)entidades.

### Combinar directivas

Al reunir datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales, las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para obtener más información sobre cómo trabajar con directivas de combinación mediante la [!DNL Real-time Customer Profile] API, consulte la guía [de extremo de directivas de](api/merge-policies.md)combinación. Para trabajar con directivas de combinación mediante la [!DNL Experience Platform] IU, consulte la guía [del usuario de directivas de](ui/merge-policies.md)combinación.

### (Alfa) Configuración de atributos calculados

>[!IMPORTANT]
>La funcionalidad de atributo calculada que se describe en este documento está en alfa. La documentación y las funciones están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos. Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Para obtener más información sobre los atributos calculados e instrucciones paso a paso para trabajar con ellos mediante la [!DNL Real-time Customer Profile] API, consulte la guía [de extremo de atributos](api/computed-attributes.md)calculados. Esta guía le ayudará a comprender mejor la función que los atributos calculados desempeñan en Adobe Experience Platform, e incluye ejemplos de llamadas de API para realizar operaciones CRUD básicas.

## Componentes en tiempo real

Esta sección presenta los componentes que permiten [!DNL Real-time Customer Profile] actualizar y supervisar los datos de registros y series temporales en tiempo real.

### Transmisión de flujo continuo y de ingestión

La entrada en tiempo real es posible a través de un proceso llamado transmisión de la ingesta. A medida que se ingieren datos de series temporales y perfiles, decide incluir o excluir automáticamente esos datos de segmentos mediante un proceso continuo denominado segmentación por flujo continuo, antes de combinarlos con datos existentes y actualizar la vista de unión. [!DNL Real-time Customer Profile] Como resultado, puede realizar cálculos instantáneamente y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca. Mientras se ingieren, los datos también se someten a validación para garantizar que se ingieran correctamente y se ajusten al esquema en el que se basa el conjunto de datos. Para obtener más información sobre la validación que se realiza durante la ingestión, lea la descripción general [de la calidad de la ingestión de](../ingestion/quality/overview.md)datos.

### Configuraciones y destinos de proyección de Edge

Para ofrecer a sus clientes experiencias coordinadas, coherentes y personalizadas en varios canales en tiempo real, es necesario disponer de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. Adobe Experience Platform permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como bordes. Un edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Por ejemplo, las aplicaciones de Adobe como Adobe Target y Adobe Campaign utilizan bordes para ofrecer experiencias personalizadas al cliente en tiempo real. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde. Para obtener más información y empezar a trabajar con proyecciones mediante la [!DNL Real-time Customer Profile] API, consulte la guía [de puntos finales de proyección de](api/edge-projections.md)Edge.

## Añadir datos a [!DNL Real-time Customer Profile]

[!DNL Platform] puede configurarse para enviar el registro y los datos de la serie temporal a [!DNL Profile], admitiendo la transmisión de flujo continuo en tiempo real y la ingestión por lotes. Para obtener más información, consulte el tutorial que describe cómo [agregar datos al Perfil](tutorials/add-profile-data.md)del cliente en tiempo real.

>[!NOTE]
>
>Los datos recopilados a través de soluciones de Adobe, incluidos [!DNL Analytics Cloud], [!DNL Marketing Cloud]y [!DNL Advertising Cloud], fluyen [!DNL Experience Platform] y se ingieren en [!DNL Profile].

### [!DNL Profile] métricas de ingestión

Las perspectivas de visibilidad le permiten exponer métricas clave en Adobe Experience Platform. Además de [!DNL Platform] las estadísticas de uso y los indicadores de rendimiento para diversas [!DNL Platform] funcionalidades, existen métricas específicas [!DNL Profile]relacionadas que le permiten conocer mejor las tasas de solicitudes entrantes, las tasas de ingestión exitosas, los tamaños de registro ingestados y mucho más. Para obtener más información, lea la información general [de](../observability/home.md)Perspectivas de la capacidad de observación y, para obtener una lista completa de [!DNL Profile] las métricas, consulte la documentación sobre las métricas [](../observability/metrics.md)disponibles.

## [!DNL Data governance] y [!DNL Privacy]

[!DNL Data governance] es una serie de estrategias y tecnologías utilizadas para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos.

En lo que se refiere al acceso a los datos, la gobernanza de los datos desempeña un papel clave en [!DNL Experience Platform] varios niveles:
* Etiquetado de uso de datos
* Directivas de acceso a datos
* Control de acceso de datos para acciones de marketing

[!DNL Data governance] se administra en varios puntos. Éstos incluyen decidir en qué datos se ingieren [!DNL Platform] y en qué datos se puede acceder después de la ingestión para una acción de mercadotecnia determinada. Para obtener más información, comience por leer la información general [sobre la administración de](../data-governance/home.md)datos.

### Gestión de solicitudes de exclusión y de privacidad de datos

[!DNL Experience Platform] permite a los clientes enviar solicitudes de exclusión relacionadas con el uso y el almacenamiento de sus datos en [!DNL Real-time Customer Profile]. Para obtener más información sobre cómo se gestionan las solicitudes de exclusión, consulte la documentación sobre el [cumplimiento de las solicitudes](../segmentation/honoring-opt-outs.md)de exclusión.

## [!DNL Profile] guías

[!DNL Experience Platform] dispone de una serie de directrices que deben seguirse para su uso eficaz [!DNL Profile].

| Sección | Límite |
| ------- | -------- |
| [!DNL Profile] esquema de unión | Un máximo de **20** datasets puede contribuir al esquema de [!DNL Profile] unión. |
| Relaciones con varias entidades | Se puede crear un máximo de **5** relaciones de varias entidades. |
| Profundidad de JSON para asociación de varias entidades | La profundidad máxima de JSON es **4**. |
| Datos de series temporales | Los datos de series temporales **no están** permitidos en entidades [!DNL Profile] no personales. |
| Relaciones de esquema de personas que no son personas | Las relaciones de esquema con personas que no son personas **no están** permitidas. |
| Fragmento de perfil | El tamaño máximo recomendado de un fragmento de perfil es de **10 kB**.<br><br> El tamaño máximo absoluto de un fragmento de perfil es de **1 MB**. |
| Entidad no personal | El tamaño total máximo de una entidad individual no personal es de **200 MB**. |
| Conjuntos de datos por entidad no personal | Se puede asociar un máximo de **1** conjunto de datos a una entidad que no sea personal. |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>Una entidad no personal hace referencia a cualquier clase XDM que **no forme** parte de [!DNL Profile].

## Próximos pasos y recursos adicionales

Para obtener más información sobre [!DNL Real-time Customer Profile], siga leyendo la documentación y complementando su aprendizaje en el siguiente vídeo o explorando otros tutoriales [de vídeo](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)Experience Platform.

>[!WARNING]
>La interfaz de usuario que [!DNL Platform] se muestra en el siguiente vídeo no está actualizada. Consulte la guía [del usuario de Perfil del cliente en tiempo](ui/user-guide.md) real para obtener las capturas de pantalla y las funciones más recientes de la interfaz de usuario.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)