---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Información general sobre el Perfil del cliente en tiempo real
topic: guide
translation-type: tm+mt
source-git-commit: 50e6b39c1eb0bda4f3b30991515fb1c13fa9ff87

---


# Información general sobre el Perfil del cliente en tiempo real

Adobe Experience Platform le permite dirigir experiencias coordinadas, coherentes y relevantes para sus clientes, independientemente de dónde o cuándo interactúen con su marca. Con el Perfil del cliente en tiempo real, puede ver una vista holística de cada cliente individual que combina datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. Perfil le permite consolidar sus distintos datos de clientes en una vista unificada que ofrece una cuenta procesable con marca de hora de cada interacción con los clientes. Esta descripción general le ayudará a comprender la función y el uso del Perfil del cliente en tiempo real en la plataforma de experiencia.

## Explicación del Perfil del cliente en tiempo real

El Perfil de clientes en tiempo real es un almacén de entidades de búsqueda genérico que combina datos de diversos activos de datos empresariales y, a continuación, proporciona acceso a esos datos en forma de perfiles de clientes individuales y eventos de series temporales relacionados. Esta función permite a los especialistas en marketing impulsar experiencias coordinadas, coherentes y relevantes con sus audiencias en varios canales, como se resume en el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12&enable10seconds=on&speedcontrol=on)

### Almacén de datos de Perfil

Aunque el Perfil de clientes en tiempo real procesa datos ingestados y utiliza el servicio de identidad de Adobe Experience Platform para combinar datos relacionados mediante la asignación de identidades, mantiene sus propios datos en el almacén de Perfiles. En otras palabras, el almacén de Perfiles es independiente de los datos del catálogo (Data Lake) y de los datos del servicio de identidad (Identity Service).

### Servicios de Perfil y plataforma

La relación entre el Perfil del cliente en tiempo real y otros servicios dentro de la plataforma de experiencia se resalta en el diagrama siguiente:

![Relación entre Perfil y otros servicios de la plataforma de experiencias.](images/profile-overview/profile-in-platform.png)

### Perfiles y datos de registro

Un perfil es una representación de un sujeto, una organización o una persona, también denominada datos de registro. Por ejemplo, el perfil de un producto puede incluir un SKU y una descripción, mientras que el perfil de una persona contiene información como nombre, apellidos y dirección de correo electrónico. Con la plataforma de experiencia, puede personalizar perfiles para utilizar tipos de datos relevantes para su empresa. La clase de Perfil individual estándar del Modelo de datos de experiencia (XDM) es la clase preferida sobre la que se debe crear un esquema al describir datos de registros de clientes y proporciona la información integral a muchas interacciones entre los servicios de plataforma. Para obtener más información sobre cómo trabajar con esquemas en la plataforma de experiencias, lea la descripción general [del sistema](../xdm/home.md)XDM.

### eventos de series temporales

Los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto realizó una acción, directa o indirectamente, así como datos que detallan el propio evento. Representados por la clase de esquema estándar XDM ExperienceEvent, los datos de series temporales pueden describir eventos como elementos que se agregan a un carro, vínculos en los que se hace clic y vídeos vistos. Los datos de series temporales pueden utilizarse para basar las reglas de segmentación en y se puede acceder a los eventos de forma individual en el contexto de un perfil.

### Identidades

Cada empresa quiere comunicarse con sus clientes de una manera que se sienta personal. Sin embargo, uno de los desafíos de ofrecer experiencias digitales relevantes a los clientes es comprender cómo unir sus datos desconectados, lo que a menudo se extiende a través de diferentes canales digitales, como tabletas, teléfonos móviles y portátiles. El servicio de identidad le permite unir la imagen completa de su cliente vinculando identidades de varios canales, creando un gráfico de identidad para cada cliente, lo que le permite comprenderlas mejor. Visite la información general [del servicio de](../identity-service/home.md) identidad para obtener más información.

### Segmentación

El servicio de segmentación de la plataforma de experiencia de Adobe genera las audiencias necesarias para potenciar las experiencias de sus clientes individuales. Cuando se crea un segmento de audiencia, el ID de ese segmento se agrega a la lista de pertenencias a segmentos para todos los perfiles que cumplen los requisitos. Las reglas de segmentos se generan y aplican a los datos de Perfil del cliente en tiempo real mediante las API de RESTful y la interfaz de usuario del Generador de segmentos. Para obtener más información sobre la segmentación, lea la información general [del servicio de](../segmentation/home.md)segmentación.

### Fragmentos de Perfil y vistas de unión {#profile-fragments-and-union-schemas}

Una de las características clave del Perfil del cliente en tiempo real es la capacidad de unificar datos de varios canales. Cuando se utiliza el Perfil de cliente en tiempo real para acceder a una entidad, puede proporcionarle una vista combinada de todos los fragmentos de perfil de dicha entidad en todos los conjuntos de datos, denominada vista de unión. Los datos de Perfil del cliente en tiempo real se combinan entre fuentes cuando su ID accede a una entidad o perfil o se exportan como un segmento. Para obtener más información sobre el acceso a perfiles y vistas de unión, visite la subguía para desarrolladores de la API de Perfil del cliente en tiempo real sobre [entidades, también conocida como &quot;Acceso a Perfil&quot;](api/entities.md).

### Combinar directivas

Al reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales, las políticas de combinación son las reglas que utiliza la Plataforma para determinar cómo se priorizarán los datos y qué datos se combinarán para crear esa vista unificada. Mediante las API de RESTful o la interfaz de usuario, puede crear nuevas políticas de combinación, administrar políticas existentes y establecer una directiva de combinación predeterminada para su organización. Para obtener más información sobre cómo trabajar con políticas de combinación mediante API, consulte la guía [de](api/merge-policies.md) combinación de políticas de Perfil del cliente en tiempo real o la guía [del usuario de directivas de](ui/merge-policies.md) combinación para ver cómo trabajar con políticas de combinación mediante la interfaz de usuario de la plataforma.

## Componentes en tiempo real

Esta sección presenta los componentes que permiten al Perfil del cliente en tiempo real actualizar y supervisar los datos de registros y series temporales en tiempo real.

### Transmisión de flujo continuo y de ingestión

La entrada en tiempo real es posible a través de un proceso llamado transmisión de la ingesta. A medida que se ingieren datos de series temporales y de perfiles, el Perfil del cliente en tiempo real decide automáticamente incluir o excluir esos datos de los segmentos a través de un proceso continuo denominado segmentación por flujo, antes de combinarlos con datos existentes y actualizar la vista de unión. Como resultado, puede realizar cálculos instantáneamente y tomar decisiones para ofrecer experiencias mejoradas e individualizadas a los clientes a medida que interactúan con su marca. Mientras se ingieren, los datos también se someten a validación para garantizar que se ingieran correctamente y se ajusten al esquema en el que se basa el conjunto de datos. Para obtener más información sobre la validación que se realiza durante la ingestión, lea la descripción general [de la calidad de la ingestión de](../ingestion/quality/overview.md)datos.

### Proyecciones de Edge

Para ofrecer a sus clientes experiencias coordinadas, coherentes y personalizadas en varios canales en tiempo real, es necesario disponer de los datos adecuados y actualizarlos continuamente a medida que se produzcan cambios. Adobe Experience Platform permite este acceso en tiempo real a los datos mediante el uso de lo que se conoce como bordes. Un edge es un servidor ubicado geográficamente que almacena datos y los hace fácilmente accesibles para las aplicaciones. Por ejemplo, las aplicaciones de Adobe como Adobe Destinatario y Adobe Campaign utilizan bordes para ofrecer experiencias personalizadas al cliente en tiempo real. Los datos se dirigen a un borde mediante una proyección, con un destino de proyección que define el borde al que se enviarán los datos y una configuración de proyección que define la información específica que estará disponible en el borde.

Para obtener más información y empezar a trabajar con los bordes y las proyecciones, consulte la subguía [Proyecciones](api/edge-projections.md)perimetrales de la API de Perfil del cliente en tiempo real.

## Administración de datos y privacidad

La administración de datos es una serie de estrategias y tecnologías utilizadas para administrar los datos de los clientes y garantizar el cumplimiento de las regulaciones, restricciones y políticas aplicables al uso de los datos.

En lo que se refiere al acceso a los datos, la gobernanza de los datos desempeña un papel clave en la plataforma de experiencias en varios niveles:
* Etiquetado de uso de datos
* Directivas de acceso a datos
* Control de acceso de datos para acciones de marketing

La administración de datos se administra en varios puntos. Éstos incluyen decidir qué datos se ingieren en la plataforma y qué datos son accesibles después de la ingestión para una acción de mercadotecnia determinada. Para obtener más información, comience por leer la información general [sobre la administración de](../data-governance/home.md)datos.

### Gestión de solicitudes de exclusión y de privacidad de datos

Experience Platform permite a los clientes enviar solicitudes de exclusión relacionadas con el uso y el almacenamiento de sus datos en tiempo real con Perfil del cliente. Para obtener más información sobre cómo se gestionan las solicitudes de exclusión, consulte la documentación sobre el [cumplimiento de las solicitudes](../segmentation/honoring-opt-outs.md)de exclusión.

## Añadir datos al Perfil del cliente en tiempo real

La plataforma se puede configurar para enviar el registro y los datos de la serie temporal al Perfil, lo que permite la transmisión en tiempo real de la ingesta por lotes y de la ingesta por secuencias. Para obtener más información, consulte el tutorial que describe cómo [agregar datos al Perfil](tutorials/add-profile-data.md)del cliente en tiempo real.

>[!Note]
>Los datos recopilados a través de las soluciones de Adobe, incluidas Analytics Cloud, Marketing Cloud y Advertising Cloud, entran en la plataforma de Experience y se ingieren en Perfil.

## Crear segmentos de audiencia

La piedra angular de su campaña de mercadotecnia es su audiencia. El Perfil de clientes en tiempo real proporciona las herramientas para segmentar la base de clientes en audiencias que consisten en miembros que cumplen los criterios precisos que usted necesita. Con la segmentación, puede aislar los miembros de la audiencia mediante criterios como:

* Clientes para los que ha pasado una semana desde la última compra.
* Clientes para los que la suma de las compras es buena en más de $10,000.
* Los clientes que han visto un número determinado de campañas de marketing únicas desde una lista predefinida, especificadas por su ID de Campaña, y las han explorado en un plazo de 30 minutos.

Para comenzar con la segmentación, consulte la información general [de la](../segmentation/home.md)segmentación.

## (Alfa) Configuración de atributos calculados

>[!IMPORTANT]
>La funcionalidad de atributo calculada que se describe en este documento está en alfa. La documentación y la funcionalidad están sujetas a cambios.

Los atributos calculados permiten calcular automáticamente el valor de los campos en función de otros valores, cálculos y expresiones. Los atributos calculados funcionan en el nivel de perfil, lo que significa que se pueden acumulados valores en todos los registros y eventos. Cada atributo calculado contiene una expresión, o &quot;regla&quot;, que evalúa los datos entrantes y almacena el valor resultante en un atributo de perfil o en un evento. Estos cálculos le ayudan a responder fácilmente preguntas relacionadas con aspectos como el valor de compra de por vida, el tiempo entre compras o la cantidad de aperturas de aplicaciones, sin necesidad de realizar cálculos complejos manualmente cada vez que se necesita la información. Para obtener más información sobre los atributos calculados e instrucciones paso a paso para trabajar con ellos, consulte la [subguía de la API de Perfil de clientes en tiempo real sobre atributos](api/computed-attributes.md)calculados. Esta guía le ayudará a comprender mejor la función que los atributos calculados desempeñan en la plataforma Adobe Experience, e incluye ejemplos de llamadas de API para realizar operaciones CRUD básicas mediante la API de Perfil del cliente en tiempo real.