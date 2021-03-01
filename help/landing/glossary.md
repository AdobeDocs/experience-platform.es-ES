---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Glosario de Adobe Experience Platform
topic: introducción
description: Un glosario de terminología importante en Experience Platform.
translation-type: tm+mt
source-git-commit: 5575d5e45bddcc007dcf78720cd7a7e20475f78c
workflow-type: tm+mt
source-wordcount: '7139'
ht-degree: 1%

---


# Glosario de Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Control de acceso**: El control de acceso basado en roles permite a los administradores asignar acceso y permisos a los usuarios de Experience Platform. Los permisos incluyen la capacidad de vista y/o uso de funciones de Experience Platform, como crear entornos limitados, definir esquemas y administrar conjuntos de datos.

**ID** de clave de acceso: Un ID de clave de acceso es un identificador único asociado a una clave de acceso secreto  [!DNL Amazon] S3. El ID de la clave de acceso y la clave de acceso secreto se utilizan juntos para firmar [!DNL Amazon Web Services] solicitudes (AWS).

**Acción**: En  [!DNL Platform Launch]concreto, una acción es un tipo específico de componente de regla que define lo que debe suceder después de que se produzca un evento y se evalúen y pasen las condiciones.

**Activar**: Activar es la acción que realiza un usuario para asignar un segmento o perfiles a un destino como  [!DNL Oracle Eloqua],  [!DNL Google] o  [!DNL Salesforce Marketing Cloud].

**Actividad**: En  [!DNL Offer Decisioning], una actividad contiene la lógica que informa la selección de una oferta.

**Administrador**: Uno o más individuos de su organización que pueden configurar y personalizar permisos para Experience Platform en Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso de su organización. A través de la consola, los administradores pueden otorgar permisos de acceso a grupos de usuarios para diversas funciones de la plataforma, como &quot;Administrar conjuntos de datos&quot;, &quot;Conjuntos de datos de Vista&quot; o &quot;Administrar Perfiles&quot;.

**Adobe Experience Platform**: Adobe Experience Platform estandariza los datos y el contenido en toda la empresa, lo que potencia los perfiles de los consumidores en tiempo real, permite la ciencia de datos y acelera la velocidad de contenido para impulsar la personalización de la experiencia en todo el recorrido del cliente.

**Adobe Experience Platform Launch**:  [!DNL Platform Launch] es un ecosistema de administración de etiquetas y SDK, integrado con Experience Platform y  [!DNL Experience Cloud] aplicaciones. [!DNL Platform Launch] proporciona herramientas para implementar, unificar y administrar integraciones de análisis, marketing y publicidad necesarias para potenciar las experiencias relevantes de los clientes en todos los dispositivos cliente.

**Servicio** de Consulta de Adobe Experience Platform: Permite a los analistas de datos realizar consultas de eventos y perfiles para su uso en análisis y aprendizaje automático. Con el servicio de Consulta, los científicos y analistas de datos pueden extraer todos sus conjuntos de datos almacenados en el Experience Platform (incluidos datos de comportamiento, así como puntos de venta, administración de la relación con los clientes (CRM), etc.) y realizar consultas en dichos conjuntos de datos para responder preguntas específicas sobre los datos.

**Servicio** de segmentación de Adobe Experience Platform: Permite generar segmentos y audiencias a partir de los datos de Perfil de clientes en tiempo real. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro del Data Lake.

**Servicios** inteligentes de Adobe: Los servicios inteligentes, como Attribution AI y AI del cliente, son modelos de aprendizaje automático basados en inteligencia artificial que están diseñados específicamente y requieren que el Experience Platform los ejecute y funcione.

**Adobe I/O**: Adobe I/O forma parte de Experience Platform y proporciona acceso a todo lo que los desarrolladores necesitan para integrar, ampliar y personalizar la plataforma, incluidas las API, los eventos, la consola para desarrolladores y las útiles herramientas.

**Adobe Sensei**: Adobe Sensei es el sistema de inteligencia que impulsa al Experience Platform. También ofrece un conjunto de servicios de IA que empoderan a las marcas para mejorar su capacidad de ofrecer experiencias personalizadas y en tiempo real a los clientes.

**Cubo** Amazon S3:  [!DNL Amazon S3] los cubos son los contenedores fundamentales para los datos almacenados en el  [!DNL Amazon] ecosistema. Los contenedores contienen objetos, cada objeto se almacena y recupera mediante una clave exclusiva asignada por el desarrollador.

**Conector** Amazon S3: El conector  [!DNL Amazon] S3 permite a los clientes del Experience Platform conectarse y acceder de forma segura a sus datos  [!DNL Amazon] S3.

**Anexar estrategia** de guardado: La estrategia de almacenamiento &quot;anexar&quot; es una opción que se utiliza al especificar datos de terceros para realizar la ingesta a través de una conexión y anexar datos o filas nuevos al final del conjunto de datos. Las filas ingestadas anteriormente no se tocan y solo las filas creadas desde la última ejecución programada se transfieren al Experience Platform. Todas las filas que se cambiaron en el sistema de origen permanecen sin cambios en el Experience Platform.

**Matriz**: Las matrices se utilizan para elementos ordenados con el mismo tipo de datos.

**Inteligencia** artificial: La inteligencia artificial es una teoría y un desarrollo de sistemas informáticos capaces de realizar tareas que normalmente requieren inteligencia humana, como la percepción visual, el reconocimiento del habla, la toma de decisiones y la traducción entre idiomas.

**Atributos**: Los atributos son características especificadas que representan un perfil.

**Combinación** de atributos: Al definir una directiva de combinación mediante la API de Perfil de cliente en tiempo real, el  `attributeMerge` objeto indica la forma en que la directiva de combinación dará prioridad a los atributos de perfil en caso de conflictos de datos. Es equivalente a seleccionar un [!UICONTROL método de combinación] al definir una directiva de combinación en la interfaz de usuario de la plataforma.

**Attribution AI**:  [!DNL Attribution AI] es un servicio inteligente con tecnología de Adobe Sensei que ofrece funciones algorítmicas de atribución de múltiples canales en todo el ciclo de vida del cliente.

**Audiencia**: Una audiencia es el conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

**Tamaño** de audiencia: Un tamaño de audiencia es el número total de perfiles que cumplen los criterios de una definición de segmento y cumplen los requisitos para pertenecer a la audiencia.

**Instantánea** de audiencia: Una instantánea de audiencia captura todos los perfiles que cumplen los criterios del segmento en el momento de la segmentación.

## B

**Relleno** posterior: Para los orígenes programados, la opción de relleno permite la ingestión de datos históricos.

**Período** de relleno: El período de relleno es una opción para establecer el período de tiempo necesario para la ingesta de datos históricos de terceros mediante una conexión de origen. Al seleccionar un período de relleno de &quot;para siempre&quot;, se ingesta el historial completo de los datos de origen al Experience Platform.

**Lote**: Un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Los conjuntos de datos están compuestos de varios lotes.

**Id** de lote: Un ID de lote es un identificador generado por Adobes para un lote de datos.

**Ingesta** por lotes: La ingestión por lotes permite ingerir datos en Experience Platform como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad.

**Segmentación** por lotes: La segmentación por lotes es una alternativa a un proceso de selección de datos en curso y mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, este segmento se guarda y almacena para que pueda exportarse para su uso.

**Generar**: En  [!DNL Platform Launch], una compilación es un archivo o conjunto de archivos que contiene todas las configuraciones y el código necesarios para ejecutar la lógica empresarial contenida en una biblioteca, lo que le permite implementar esa biblioteca en su sitio web o aplicación móvil.

**Herramientas** de inteligencia empresarial: Las herramientas de inteligencia empresarial (BI) están integradas principalmente con  [!DNL Experience Platform Query Service]. Las herramientas de inteligencia comercial son tipos de software de aplicaciones que recopilan y procesan grandes cantidades de datos no estructurados de sistemas internos y externos.

## C

**Tapa**: En  [!DNL Offer Decisioning], en las reglas de decisiones se utiliza el límite de frecuencia (también conocido como límite de frecuencia) para definir cuántas veces se presenta una oferta. Existen dos tipos de mayúsculas: cuántas veces se puede proponer una oferta en la audiencia de destinatario combinada (denominada &quot;Cap global&quot;) y cuántas veces se puede proponer una oferta al mismo usuario final (denominada &quot;Cap de Perfil&quot;).

**Catálogo**: En el contexto de las fuentes y los destinos, un catálogo es una galería con conexiones disponibles a aplicaciones de Adobe y tecnologías de terceros. No debe confundirse con [!DNL Catalog Service].

**[!DNL Catalog Service]**::  [!DNL Catalog Service] (a veces llamado  [!DNL Catalog]) es el sistema de registro para la ubicación y linaje de datos dentro de Adobe Experience Platform. Aunque todos los datos que se ingestan en Experience Platform se almacenan en el lago de datos como archivos y directorios, [!DNL Catalog] guarda los metadatos y la descripción de esos archivos y directorios para fines de búsqueda, monitoreo y administración de datos.

**Clase**: En el Modelo de datos de experiencia (XDM), una clase define el conjunto más pequeño de campos utilizados para generar un esquema y define el comportamiento base del objeto comercial que representa el esquema.

**Cliente**: Un cliente es una herramienta o aplicación externa que se conecta  [!DNL Query Service] mediante el protocolo PostgreSQL o la API HTTP.

**Colección**: En  [!DNL Offer Decisioning], las colecciones son subconjuntos de ofertas basados en condiciones predefinidas definidas definidas por un especialista en marketing, como la categoría de la oferta.

**Combinar con la acción** de mercadotecnia PII: Acción de marketing que combina cualquier información de identificación personal (PII) con datos anónimos. Los contratos para datos provenientes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de esos datos con datos directamente identificables.

**Interfaz** de línea de comandos: Una interfaz de línea de comandos es una herramienta basada en texto a la que se puede conectar  [!DNL Query Service] para la ejecución de consultas sin procesar.

**Composición**: Una composición es un grupo de componentes que se forman juntos para formar el esquema.

**Condición**: En  [!DNL Platform Launch], una condición es un componente de regla que evalúa una afirmación lógica que debe devolver  `true` o  `false`. Todas las condiciones deben evaluarse como `true` y todas las condiciones de excepción deben evaluarse como `false` antes de que se ejecute ninguna acción en la regla.

**Consola**: En  [!DNL Query Service], la consola proporciona información sobre el estado y el funcionamiento de una consulta. La consola muestra el estado de la conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error que resulten de dichas consultas.

**Etiquetas** de contrato (&quot;C&quot;): Las etiquetas de uso de datos de contrato (&quot;C&quot;) se utilizan para categorizar los datos que tienen obligaciones contractuales o que están relacionados con las políticas de administración de datos de un cliente.

**Etiqueta** de contrato C1: Una etiqueta de uso de datos de  `C1` contrato especifica que los datos solo se pueden exportar desde Adobe Experience Cloud en un formulario agregado sin incluir identificadores individuales o de dispositivo. Por ejemplo, los datos que se originaron en las redes sociales.

**Etiqueta** de contrato C2: Una etiqueta de uso de datos de  `C2` contrato especifica los datos que no se pueden exportar a terceros. Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la exportación de datos desde donde se recopilaron originalmente. Por ejemplo: los contratos de redes sociales suelen restringir la transferencia de datos que se reciben de ellos. C2 es más restrictivo que C1, que sólo requiere agregación y datos anónimos.

**Etiqueta** de contrato C3: Una etiqueta de uso de datos de  `C3` contrato especifica los datos que no se pueden combinar ni utilizar de otro modo con información directamente identificable. Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la combinación o utilización de esos datos con información directamente identificable. Por ejemplo, los contratos para datos provenientes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros a menudo incluyen prohibiciones contractuales específicas sobre el uso de datos directamente identificables.

**Etiqueta** de contrato C4: Una etiqueta de uso de datos de  `C4` contrato especifica que los datos no se pueden usar para dirigir anuncios o contenido, ya sea en el sitio o entre sitios. C4 es la etiqueta más restrictiva, ya que engloba las etiquetas C5, C6 y C7.

**Etiqueta** de contrato C5: Una etiqueta de uso de datos de  `C5` contrato especifica que los datos no se pueden utilizar para dirigir anuncios o contenido basado en intereses a través de sitios. La segmentación o personalización basada en intereses se produce si se cumplen las tres condiciones siguientes: Los datos recopilados in situ se utilizan para hacer inferencias sobre el interés del usuario; se utiliza en otro contexto, como en otro sitio o aplicación; y se utiliza para seleccionar qué contenido o anuncios se ofrecen en función de esas inferencias.

**Etiqueta** de contrato C6: Una etiqueta de uso de datos de  `C6` contrato especifica que los datos no se pueden usar para la segmentación de publicidad en el sitio. El objetivo de publicidad en el sitio incluye la selección y el envío de anuncios en los sitios web de la organización, o en las aplicaciones, o bien para medir el envío y la efectividad de dichos anuncios. Esto incluye el uso de datos recopilados anteriormente en el sitio sobre el interés de los usuarios por seleccionar publicidades, procesar datos sobre qué publicidades se mostraron, cuándo y dónde se mostraron y si los usuarios realizaron alguna acción relacionada con la publicidad, como seleccionar una publicidad o realizar una compra.

**Etiqueta** de contrato C7: Una etiqueta de uso de datos de  `C7` contrato especifica que los datos no se pueden usar para dirigir el contenido en el sitio. La segmentación de contenido en el sitio incluye la selección y el envío de contenido en los sitios web de la organización o en las aplicaciones, o bien para medir el envío y la efectividad de dicho contenido. Esto incluye la información recopilada anteriormente sobre el interés de los usuarios por seleccionar contenido, el procesamiento de datos sobre qué contenido se mostró, la frecuencia o el tiempo que se mostró, cuándo y dónde se mostró, y si los usuarios realizaron alguna acción relacionada con el contenido, como seleccionar contenido.

**Etiqueta** de contrato C8: Una etiqueta de uso de datos de  `C8` contrato especifica que los datos no se pueden utilizar para medir los sitios web o las aplicaciones de la organización. Esto no incluye la segmentación basada en intereses, que es la recopilación de información sobre el uso que hace de este servicio para personalizar posteriormente el contenido y/o la publicidad en otros contextos.

**Etiqueta** de contrato C9: Una etiqueta de uso de datos de  `C9` contrato especifica que los datos no se pueden usar en flujos de trabajo de ciencia de datos. Algunos contratos incluyen prohibiciones explícitas de los datos utilizados para la ciencia de datos. A veces se expresan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado.

**Etiqueta** de contrato C10: Una etiqueta de uso de datos de  `C10` contrato especifica que los datos no se pueden utilizar para la activación de identidad vinculada. Algunas directivas de uso de datos restringen el uso de datos de identidad vinculados para la personalización. La etiqueta `C10` se aplica automáticamente a los segmentos si sus políticas de combinación utilizan la opción &quot;gráfico privado&quot;.

**Columna** Fecha de creación: La selección de una columna Fecha de creación es una opción al especificar datos de terceros mediante una conexión de origen. Cuando se selecciona la estrategia de guardar datos anexados y el esquema del conjunto de datos contiene varios campos de fecha, debe elegir entre el esquema disponible para especificar una columna de clave Fecha de creación. La opción Fecha de creación no está disponible cuando se selecciona la estrategia de sobrescritura de guardar.

**Crear tabla como selección**: Crear tabla como Seleccionar (CTAS) es un comando SQL que, cuando se ejecuta como parte de una consulta SQL completa y válida, indicará  [!DNL Query Service] que se mantengan los resultados de la consulta en un conjunto de datos. Puede crear un nuevo conjunto de resultados, sobrescribir resultados anteriores o anexar a resultados anteriores.

**Datos** entre sitios: Los datos entre sitios son la combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio.

**Acción** de mercadotecnia de objetivo entre sitios: Acción de mercadotecnia que utiliza datos para la segmentación de anuncios entre sitios. La combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas, se denomina datos entre sitios. Los datos entre sitios generalmente se recopilan y procesan para hacer inferencias sobre los intereses de los clientes.

**Área de nombres** de identidad personalizada: Su organización puede crear Áreas de nombres de identidad personalizadas para representar las identidades de una organización o un caso empresarial específicos.

**Etiquetas** personalizadas: Las etiquetas de uso de datos personalizadas le permiten crear y aplicar etiquetas específicas a campos de datos que satisfagan necesidades comerciales específicas.

**AI** del cliente: La API del cliente es un servicio inteligente con tecnología de Adobe Sensei que enriquece los perfiles del cliente con las propiedades basadas en la IA y potencia la segmentación del cliente y los esfuerzos de determinación de objetivos.

## D

**Diccionario** de datos: En  [!DNL Platform Launch], un diccionario de datos (también conocido como mapa de datos) es un conjunto de elementos de datos definidos dentro de una propiedad.

**Elemento** de datos: En  [!DNL Platform Launch], un elemento de datos es un puntero que se utiliza dentro de reglas y extensiones para señalar a un fragmento de datos específico que existe en el dispositivo cliente.

**Ingesta** de datos: La ingestión de datos es el proceso de agregar datos de una fuente al Experience Platform. Los datos se pueden ingerir en la plataforma de diversas maneras, incluyendo flujo continuo, lotes o agregación mediante conectores de origen.

**Capa** de datos: En  [!DNL Platform Launch]realidad, una capa de datos es una estructura de datos que existe en el dispositivo cliente y que contiene metadatos sobre el contexto en el que se ve una página o pantalla.

**Administración** de datos: La gobernanza de los datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos se ajusten a las normas y políticas institucionales en materia de utilización de los datos.

**Socios** de integración de datos: Los socios de integración de datos simplifican y automatizan la carga y transformación de volúmenes masivos de datos de más de 200 fuentes a Experience Platform sin necesidad de escribir código.

**Etiquetas** de conjunto de datos: Las etiquetas de uso de datos se pueden agregar a los conjuntos de datos. Todos los campos dentro de ese conjunto de datos heredarán las etiquetas del conjunto de datos.

**Área de trabajo** de ciencias de datos:  [!DNL Data Science Workspace] dentro de Experience Platform permite a los clientes crear modelos de aprendizaje automático utilizando datos en aplicaciones de plataforma y Adobe para crear segmentos inteligentes, generar perspectivas y proporcionar predicciones, lo que le permite mejorar considerablemente las experiencias digitales de los usuarios finales.

**Fuente** de datos: Un origen de datos es un origen de datos designado por el usuario. Ejemplos de una fuente de datos son una aplicación móvil, eventos de perfil y/o experiencia, eventos de perfil de sitios web o una CRM.

**Administrador** de datos: Un administrador de datos es la persona responsable de la administración, supervisión y ejecución de los activos de datos de una organización. Un administrador de datos también garantiza que las políticas de gobernanza de los datos estén salvaguardadas y mantenidas para cumplir con las regulaciones y políticas organizativas del gobierno.

**Flujo** de datos: Un flujo de datos es un conjunto o una colección de mensajes que comparten el mismo esquema y que se envían por el mismo origen.

**Tipo** de datos: Un tipo de datos es un recurso XDM reutilizable que define un campo de tipo de objeto que contiene varias propiedades en una representación jerárquica.

**Etiquetas** de uso de datos: Las etiquetas de uso de datos permiten clasificar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las normativas y políticas corporativas. Las etiquetas de uso de datos agregadas a un conjunto de datos se heredan o se aplican a todos los campos dentro de ese conjunto de datos. Las etiquetas de uso de datos también se pueden aplicar directamente a los campos.

**Flujo de datos**: Un flujo de datos es un flujo virtual de datos que fluye a la plataforma desde un origen y hacia los destinos.

**Ejecución** de flujo de datos: Una ejecución de flujo de datos es un flujo de datos que aterriza en el Experience Platform según una programación especificada por el usuario.

**Conjunto de datos**: Un conjunto de datos es un almacenamiento y una construcción de administración para una colección de datos, generalmente una tabla, que contiene un esquema (columnas) y campos (filas).

**ID** de conjunto de datos: Identificador generado por Adobes para un conjunto de datos ingerido.

**Resultado** del conjunto de datos: El resultado del conjunto de datos proporciona un mecanismo para determinar la opción &quot;Crear tabla como selección&quot; que se utilizará para una  [!DNL Query Service] ejecución en particular.

**Columna** Delta: Una columna delta permite seleccionar un campo de datos de origen para representar una marca de hora para la ingestión incremental.

**Estrategia** de ahorro de Delta: La estrategia de guardado delta es una opción para ingerir datos de terceros a través de una conexión de origen. La opción permite al usuario especificar que las filas de datos de origen nuevas o modificadas se ingerirán en el Experience Platform. Las filas nuevas se agregan al final del conjunto de datos y las filas cambiadas se actualizan en el conjunto de datos del Experience Platform.

**Descriptor**: En el Modelo de datos de experiencia (XDM), un descriptor es un conjunto adicional de metadatos relacionados con el esquema que describe un comportamiento específico de un campo. El Experience Platform puede utilizar los descriptores para comprender el comportamiento de esquema deseado, como la relación entre dos esquemas.

**Destino**: Un destino es un término general para cualquier extremo, como una aplicación de Adobe, una plataforma de publicidad, un servicio de almacenamiento en la nube o un servicio de marketing, donde se activa y se entrega una audiencia.

**Categoría** de destino: Una categoría de destino es un grupo de destinos que tienen características similares.

**Catálogo** de destino: Un catálogo de destino es una lista de destinos disponibles en Experience Platform.

**Reglas** de llamada directa: En  [!DNL Platform Launch]realidad, una regla de llamada directa es una regla que se ejecuta cuando se llama directamente desde la página, omitiendo los sistemas de búsqueda y detección de eventos.

**Nombre** para mostrar: En el Modelo de datos de experiencia (XDM), un nombre para mostrar es un nombre práctico para un campo que se muestra en la interfaz de usuario.

## E

**Oferta** elegible: Una oferta elegible puede ofrecerse de manera coherente a un perfil, ya que cumple las limitaciones definidas antes de su establecimiento.

**Reglas de elegibilidad**: En  [!DNL Offer Decisioning], las reglas de elegibilidad se aplican a un perfil relacionado con restricciones de calendario, programación y límite.

**Acción** de mercadotecnia de objetivo de correo electrónico: Acción de marketing que utiliza datos en campañas de segmentación de correo electrónico.

**Código** incrustado: En  [!DNL Platform Launch], el código incrustado es una etiqueta de secuencia de comandos colocada en el HTML de un sitio o entorno. El código incrustado indica al explorador dónde recuperar la compilación.

**Lista desglosada**: Una lista desglosada (enumeración) es un campo XDM limitado a un conjunto de valores predefinidos.

**Entorno**: En  [!DNL Platform Launch], un entorno es un conjunto de instrucciones de implementación que especifica el envío de host y el formato de archivo de una compilación. Una biblioteca debe estar emparejada con un entorno para poder crearla.

**Diagnósticos** de errores: Los diagnósticos de errores permiten generar mensajes de error detallados para lotes ingestados. El umbral de error permite configurar el porcentaje de errores aceptables antes de que falle un lote.

**Evento**: En  [!DNL Platform Launch], un evento es un tipo específico de componente de regla, que es un déclencheur que se produce en un dispositivo cliente para iniciar la ejecución de una regla.

**Entidades** de evento: En el contexto del modelado de datos, las entidades de evento representan conceptos relacionados con las acciones que puede realizar un cliente, eventos del sistema o cualquier otro concepto en el que desee rastrear los cambios con el tiempo. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la clase [!DNL XDM ExperienceEvent].

**Eventos**: Los eventos son los datos de comportamiento asociados a un perfil.

**El modelo de datos de experiencia (XDM)** [!DNL Experience Data Model]  (XDM) es un entorno de código abierto que utiliza esquemas estándar para unificar datos para su uso con aplicaciones de Experience Platform y Adobe Experience Cloud. XDM estandariza la forma en que se estructuran los datos y acelera y simplifica el proceso de obtener perspectivas a partir de cantidades masivas de datos.

**Experimento**: Un experimento es el proceso de crear un modelo entrenado formando la instancia con una porción de muestra de datos de producción activos. Esto es diferente de un modelo entrenado que se prueba con un conjunto de datos de prueba de retención. Esto también es diferente del concepto de un experimento en algunos marcos de aprendizaje automático donde en realidad significa un proyecto de modelado de muestra.

**Evento** de experiencias: Un Evento de experiencias representa una instantánea del sistema cuando se produce una interacción o un evento relacionado con una experiencia del cliente. Los Eventos de experiencias son registros inmutables de los hechos de lo que ocurrió y representan lo que ocurrió sin agregación ni interpretación. En el Modelo de datos de experiencia (XDM), la clase [!DNL XDM ExperienceEvent] captura este concepto.

**Extensión**: En  [!DNL Platform Launch], una extensión es un paquete de funcionalidad agregado a una  [!DNL Platform Launch] propiedad. Una extensión suele centrarse en una solución de marketing o análisis concreta y proporciona las herramientas necesarias para implementar esa tecnología en un entorno de cliente.

**Paquete** de extensión: En  [!DNL Platform Launch], un paquete de extensión es un archivo ZIP creado y cargado por un desarrollador de extensiones que proporciona todo lo necesario para que  [!DNL Platform Launch] los usuarios instalen la extensión dentro de su propiedad. Un paquete de extensión contiene un manifiesto que especifica información sobre la extensión, el código HTML/JavaScript necesario para que los usuarios finales puedan configurar el comportamiento de la extensión [!DNL Platform Launch] y el código JavaScript ejecutable enviado al entorno del cliente (si es necesario).

## F

**Ofertas** de reserva: Una oferta de reserva es la oferta predeterminada que se muestra cuando un usuario final no cumple los requisitos para ninguna de las ofertas de la colección utilizada.

**Asignación** de funciones: La asignación de funciones se refiere al proceso de asignación de características de datos a funciones de entrada y destinatario que requiere un modelo de aprendizaje automático.

**Campo**: Un campo es el elemento de nivel más bajo de un conjunto de datos, tal como se define en el esquema XDM del conjunto de datos. Cada campo tiene un nombre para fines de referencia y un tipo para indicar el tipo de datos que contiene. Los tipos de campo pueden incluir (pero no están limitados a) entero, número, cadena, booleano y objeto.

**Etiquetas** de campo: Las etiquetas de campo son etiquetas de control de datos que se heredan de un conjunto de datos o se aplican directamente a un campo.

**Nombre** del campo: Se utiliza un nombre de campo para hacer referencia al valor de un campo en consultas y servicios posteriores.

**Frecuencia**: En  [!DNL Query Service], la frecuencia determina con qué frecuencia se ejecutará una consulta programada recurrente.

## G

**Geofence**: Una geofence es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software déclencheur una respuesta cuando un dispositivo móvil entra o sale de un área en particular.

**RGPD (Reglamento General de Protección de Datos)**: El Reglamento General de Protección de Datos (RGPD) es un marco jurídico que establece directrices para la recogida y el tratamiento de la información personal de las personas en la Unión Europea (UE). El RGPD establece los principios de gestión de datos y los derechos de la persona y abarca todas las compañías que se ocupan de los datos de los ciudadanos de la UE.

## H

**Host**: En  [!DNL Platform Launch], un host especifica la ubicación, el dominio y las credenciales de usuario necesarias para  [!DNL Platform Launch] entregar una compilación.

## I

**Identidad**: Una identidad es un identificador que representa exclusivamente a un cliente individual, como un ID de cookie, un ID de dispositivo o un ID de correo electrónico.

**Campos** de identidad: Los campos de identidad son campos XDM que se utilizan para unir información sobre clientes individuales provenientes de varias fuentes de datos. Se debe definir una sola identidad principal para que el esquema se pueda utilizar en el Perfil del cliente en tiempo real.

**Etiquetas** de identidad (&quot;I&quot;): Las etiquetas de uso de datos de identidad (&quot;I&quot;) se utilizan para categorizar los datos que pueden identificar o contactar a una persona específica.

**Gráfico** de identidad: Un gráfico de identidad es un mapa de relaciones entre identidades vinculadas y vinculadas que existen para un cliente individual. Cada gráfico de identidad se actualiza en tiempo casi real con la actividad del cliente. La estructura común de las relaciones de identidad en sus datos está representada por el [!UICONTROL Gráfico privado], que sirve como modelo estructural para cada gráfico de identidad individual.

**Área de nombres** de identidad: Una Área de nombres de identidad define el contexto de un identificador, como una dirección de correo electrónico o un ID de CRM.

**Servicio** de identidad:  [!DNL Experience Platform Identity Service] permite crear y administrar tipos de identidad, lo que le permite vincular identidades de cliente entre dispositivos y canales. La capacidad del servicio de vincular identidades permite que el Perfil del cliente en tiempo real proporcione una representación completa de cada cliente individual.

**Vinculación** de identidad: El proceso de identificación de fragmentos de datos y su unión para formar un registro de perfil completo es el proceso de identificación de dichos fragmentos.

**Símbolo** de identidad: Un símbolo de identidad es una abreviatura de una Área de nombres de identidad que puede utilizarse como referencia en las API.

**Valor** de identidad: Un valor de identidad, combinado con una Área de nombres de identidad, es un identificador que representa un individuo, una organización o un recurso únicos. Al hacer coincidir los datos de registro entre fragmentos de perfil, el valor de Área de nombres e identidad debe coincidir.

**Etiqueta** de uso de datos I1: La etiqueta de uso de  `I1` datos se utiliza para clasificar datos que pueden identificar o contactar directamente con una persona específica en lugar de con un dispositivo.

**Etiqueta** de uso de datos I2: La etiqueta de uso de  `I2` datos se utiliza para clasificar los datos que pueden utilizarse en combinación con cualquier otro dato para identificar indirectamente a una persona concreta o ponerse en contacto con ella.

**Organización** de IMS: Una organización de IMS (a veces denominada organización de IMS) es el nombre utilizado para identificar una compañía o un grupo específico dentro de una compañía entre productos de Adobe. Los administradores pueden configurar y administrar el acceso y los permisos de las funciones para los usuarios de una organización.

**Ingesta**: Consulte ingestión de datos.

**Programación** de ingestión: Un programa de ingestión proporciona opciones basadas en el tiempo al realizar la ingesta de un origen a un Experience Platform.

**Función** de entrada: Se especifica una función de entrada en la asignación de funciones y la utiliza un modelo de aprendizaje automático para realizar predicciones.

**[!DNL Intelligent Services]**::  [!DNL Intelligent Services] como  [!DNL Attribution AI] y  [!DNL Customer AI] son modelos de aprendizaje automático basados en inteligencia artificial que requieren que el Experience Platform (o las aplicaciones creadas sobre la plataforma, como la Plataforma de datos del cliente en tiempo real) se ejecuten y funcionen.

**Personalización** o segmentación basada en intereses: La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes:

1. Los datos recopilados en el sitio se utilizan para hacer inferencias sobre el interés del usuario.
1. Los datos se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio).
1. Los datos se utilizan para seleccionar qué contenido o anuncios se ofrecen en función de esas inferencias.

## J

**[!DNL JupyterLab]**:: Una interfaz de código abierto basada en web para Project  [!DNL Jupyter] que se integra en la interfaz de usuario de la plataforma.

**[!DNL Jupyter Notebook]**:: Integrados con JupyterLab, los portátiles Jupyter le permiten realizar tareas de limpieza y transformación de datos, simulación numérica, modelado estadístico, visualización de datos, aprendizaje automático y mucho más en los datos de sus Experience Platform en una variedad de idiomas como Python, Scala y PySpark.

## K

## L

**Biblioteca**: En  [!DNL Platform Launch], una biblioteca es un conjunto de lógica empresarial que contiene instrucciones sobre cómo debe comportarse la  [!DNL Platform Launch] biblioteca en el dispositivo cliente.

**Entidades** de búsqueda: En el contexto del modelado de datos, las entidades de búsqueda representan conceptos que pueden relacionarse con una persona individual, pero que no pueden utilizarse directamente para identificar a la persona. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en clases de modelo de datos de experiencia (XDM) personalizadas.

## M

**Aprendizaje automático (ML)**: El aprendizaje automático es el campo de estudio que permite a las computadoras aprender sin programarse explícitamente.

**Modelo** de aprendizaje automático: Un modelo de aprendizaje automático es un ejemplo de una fórmula de aprendizaje automático que se enseña utilizando datos históricos y configuraciones para resolver un caso de uso comercial. En Adobe Experience Platform Data Science Workspace, los modelos de aprendizaje automático se denominan fórmulas.

**Asignación**: La asignación de datos es el proceso de asignación de campos de datos de origen a campos de destinatario relacionados en un destino.

**Acción** de mercadotecnia: En el marco de la administración de datos, una acción de mercadotecnia (también conocida como caso de uso de mercadotecnia) es una acción que realiza un consumidor de datos de Experience Platform, para la cual es necesario verificar las infracciones de las políticas de uso de datos.

**Método** de combinación: Al definir una directiva de combinación mediante la interfaz de usuario de la plataforma, el método de combinación especifica cómo se debe priorizar los fragmentos de datos cuando se produce un conflicto. Al utilizar la API de Perfil del cliente en tiempo real para definir una directiva de combinación, el método de combinación se determina mediante el objeto `attributeMerge`.

**Combinar directiva**: Las políticas de combinación son reglas que el Experience Platform utiliza para determinar cómo se combinarán los fragmentos de datos del cliente de varias fuentes para crear un perfil individual. Cuando se produce un conflicto de datos, la política de combinación determina qué datos deben priorizarse para su inclusión en el perfil.

**Mezcla**: En el Modelo de datos de experiencia (XDM), una combinación permite a los usuarios ampliar los campos reutilizables para definir uno o varios atributos que se van a incluir en un esquema.

**Módulo**: En  [!DNL Platform Launch], un módulo es un fragmento de JavaScript ejecutable proporcionado por una extensión, que realiza acciones en un entorno del cliente sin necesidad de crear una regla.

## N

**Simulador de pruebas** no de producción: Los entornos limitados que no son de producción son entornos limitados que generalmente se utilizan para experimentos de desarrollo, pruebas o ensayos. A diferencia de los entornos limitados de producción, los entornos limitados que no son de producción pueden restablecerse y eliminarse.

**[!DNL Notebooks]**::  [!DNL Notebooks] se crean mediante  [!DNL Jupyter Notebook] y se pueden ejecutar para realizar análisis de datos.

## O

**Oferta**: Una oferta es un mensaje de marketing que contiene una propuesta comercial o de ventas a un cliente (potencial). Las ofertas suelen tener reglas específicas que determinan quién puede verlas o recibirlas.

**[!DNL Offer Decisioning]**::  [!DNL Offer Decisioning] permite a los especialistas en marketing administrar reglas y modelos formados de propuestas de oferta cuando interactúan con usuarios finales en función de los datos recopilados en canales y aplicaciones.

**Biblioteca** de ofertas: La biblioteca de ofertas es una biblioteca central que se utiliza para administrar ofertas, reglas de decisión y actividades personalizadas y de reserva.

**Acción** de mercadotecnia de personalización en el sitio: Acción de marketing que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer inferencias sobre los intereses de los usuarios y se utiliza para seleccionar qué contenido o publicidades se ofrecen en base a esas inferencias.

**Acción** de mercadotecnia de objetivo en el sitio: Acción de mercadotecnia que utiliza datos para los anuncios en el sitio, incluida la selección y el envío de los anuncios en los sitios web o las aplicaciones de la organización, o para medir el envío y la efectividad de dichos anuncios.

**Sobrescribir estrategia** de guardado: La estrategia de almacenamiento &quot;Sobrescribir&quot; es una opción para la ingesta de datos de terceros a través de una conexión, donde puede especificar si los datos ingestados se sobrescribirán en una programación específica.

## P

**Administración** parcial: La ingestión parcial permite la ingestión de registros válidos de datos de lote dentro de un umbral de error especificado. Los diagnósticos de errores para los registros fallidos se pueden descargar o acceder a ellos en [!UICONTROL Información general de la ejecución de flujo de datos de Monitoreo] o [!UICONTROL Fuentes].

**Archivos** de parquet: Un archivo de parquet es un formato de archivo de almacenamiento en columnas con estructuras de datos anidadas complejas. Los archivos de parqué son necesarios para agregar datos para rellenar un conjunto de datos de esquema.

**Ofertas** personalizadas: Una oferta personalizada es un mensaje de marketing personalizable basado en reglas de elegibilidad y restricciones.

**Ubicaciones**: una ubicación es la ubicación o el contexto en el que aparece una oferta para un usuario final.

**Área de trabajo** Directivas: Espacio de trabajo en la interfaz de usuario de la plataforma que permite a los administradores de datos vista y administrar las directivas y etiquetas de uso de datos de su organización.

**Política**: Una directiva de uso de datos es una regla que especifica las acciones de marketing que están restringidas en función de la aplicación de etiquetas de uso aplicadas a los datos de la plataforma.

**Aplicación** de políticas: Permite aplicar políticas de uso de datos con acciones de marketing aplicadas para evitar operaciones de datos que constituyan infracciones de política dentro de una organización.

**Clave** principal: Una clave principal es una designación en un esquema para identificar de manera exclusiva todos los registros.

**Prioridad**: En  [!DNL Offer Decisioning], la prioridad se utiliza para clasificar ofertas que cumplen todas las restricciones, como la elegibilidad, el calendario y el límite.

**Gráfico** de identidad privada: El gráfico de identidad privada (a veces denominado gráfico privado) es un mapa privado de las relaciones entre identidades vinculadas y vinculadas que se construye en base a los datos de origen y que solo es visible por su organización. Sólo existe un gráfico privado para cada organización y sirve como modelo estructural para los gráficos de identidad individuales generados para cada cliente que interactúa con su marca.

**Perfil** del producto: Los perfiles de producto permiten a los administradores otorgar acceso al usuario a todos o a un subconjunto de servicios asociados con el Experience Platform.

**Entorno limitado** de producción: Un simulador para pruebas de producción es un simulador para pruebas destinado a utilizarse en el entorno de producción. A diferencia de los entornos limitados que no son de producción, los entornos limitados de producción no se pueden restaurar ni eliminar.

**Perfil**: No debe confundirse con el Perfil del cliente en tiempo real como servicio, un perfil es una representación completa de un cliente individual, creada a partir de datos de series temporales y registros combinados de múltiples fuentes.

**Acceso** de perfil: El  `/entities` punto final de la API de Perfil del cliente en tiempo real le permite acceder a los datos de registro y a los eventos de serie temporal en el almacén de datos de Perfil. Consulte también: Entidades perfil

**Datos** de perfil: Los datos de perfil se refieren a cualquier dato que se encuentre dentro del almacén de datos de Perfil.

**Almacén** de datos de perfil: El almacén de datos de Perfil (a veces llamado almacén de Perfiles) es un sistema de almacenamiento de datos independiente del lago de datos, que utiliza el Perfil de clientes en tiempo real para crear y almacenar perfiles.

**Entidades** de perfil: Las entidades de perfil representan atributos relacionados con una persona individual, normalmente un cliente. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la clase [!DNL XDM Individual Profile]. Consulte también: Acceso a perfil

**Exportación** de perfil:  [!DNL Profile] export es uno de los dos tipos de destinos en Experience Platform. [!DNL Profile] export genera un archivo que contiene perfiles y atributos, y utiliza datos PII sin procesar con correo electrónico para integrarlos con las plataformas de automatización de correo electrónico y mercadotecnia.

**Fragmento** de perfil: Un fragmento de perfil es la información de perfil para una sola identidad de la lista de identidades que existen para un cliente en particular.

**ID** de perfil: Un ID de perfil es un identificador generado automáticamente asociado a un tipo de identidad y representa un perfil.

**Propiedad**: En  [!DNL Platform Launch], una propiedad es un contenedor de todo lo necesario para implementar un conjunto de etiquetas.

## Q

**Consulta**: Las consultas son solicitudes de datos de tablas de bases de datos.

**Editor** de consultas: El Editor de consultas es una herramienta para escribir, validar y enviar sentencias SQL en  [!DNL Query Service].

## R

**Plataforma** de datos de clientes en tiempo real:  [!DNL Real-time Customer Data Platform] aúna datos conocidos y desconocidos de clientes para crear perfiles de clientes confiables con integración simplificada, segmentación inteligente y activación en tiempo real en todo el recorrido de clientes digitales.

**Perfil** del cliente en tiempo real: El Perfil del cliente en tiempo real (a veces llamado Perfil) proporciona una vista holística de cada cliente individual mediante la combinación de datos de varios canales, incluidos los de Internet, sin conexión, CRM y terceros. Perfil le permite consolidar los datos de sus clientes en perfiles individuales que ofrecen cuentas procesables con marca de hora de cada interacción con los clientes.

**Fórmula**: Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa procesos específicos de aprendizaje automático, algoritmos de IA, lógica de procesamiento y parámetros de configuración necesarios para crear y ejecutar un modelo capacitado y, por lo tanto, ayudan a resolver problemas comerciales específicos.

**Registro**: Un registro son datos que se mantienen como filas en un conjunto de datos.

**Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.

**Periodicidad**: En  [!DNL Query Service], una periodicidad define si una consulta está programada para ejecutarse solo una vez o de forma recurrente.

**Representación**: En  [!DNL Offer Decisioning]realidad, una representación es información que un canal utiliza para mostrar una oferta, como ubicación o idioma.

**Recurso**: En  [!DNL Platform Launch], un recurso es un término genérico que hace referencia a las opciones que el  [!DNL Platform Launch] usuario puede configurar dentro del entorno del cliente, incluidas las extensiones, los elementos de datos y las reglas.

**Control de acceso** basado en roles: El control de acceso basado en roles permite a los administradores asignar acceso y permisos a los usuarios de Experience Platform. Los permisos incluyen la capacidad de vista y/o uso de funciones de Experience Platform, como crear entornos limitados, definir esquemas y administrar conjuntos de datos.

**Regla**: En  [!DNL Platform Launch], una regla es una colección de componentes que define un conjunto específico de eventos, condiciones y acciones que deben agruparse lógicamente.

**Componente** de regla: En  [!DNL Platform Launch], los componentes de regla son los eventos, las condiciones y las acciones que conforman una regla.

**Tiempo de ejecución**: Runtime especifica un entorno de tiempo de ejecución para una fórmula de aprendizaje automático. [!DNL Python], R,  [!DNL Spark], PySpark y los tiempos de ejecución de Tensorflow le permiten introducir una URL en una imagen de Docker para un origen de fórmula.

## S

**Datos** de muestra: Los datos de muestra son una previsualización de un archivo de datos, normalmente las primeras 100 filas, que proporciona a un científico de datos o a un ingeniero una idea del esquema o los datos que hay en el archivo de datos.

**Simulador para pruebas**: Un simulador de pruebas es una construcción virtual que divide una sola instancia de Plataforma en un entorno virtual independiente para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

**Restablecimiento** de Simulador para pruebas: Un restablecimiento del entorno limitado elimina todos los datos, incluidos los datos, perfiles y segmentos dentro de un entorno limitado. Los reajustes del Simulador para pruebas pueden afectar a los datos que están conectados a destinos internos o externos.

**Mezclador** de Simulador para pruebas: El control del conmutador de simulador de pruebas en Experience Platform permite a los usuarios navegar entre los entornos limitados a los que tienen acceso. Si se cambia un simulador para pruebas, todo el contenido cambiará y puede alterar el acceso a las funciones en función de los permisos.

**Programar**: Una programación es una especificación definida por el usuario sobre la frecuencia o cadencia de la ingestión de datos desde una fuente de datos de terceros a Adobe Experience Platform.

**Puntuación**: La puntuación es el proceso de generación de perspectivas a partir de datos mediante un modelo capacitado.

**Esquema**: Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. Un esquema consta de una clase y una mezcla opcional y se utiliza para crear conjuntos de datos y conjuntos de datos. Un esquema puede incluir atributos de comportamiento, marcas de hora, identidades, definiciones de atributos, relaciones, etc.

**Biblioteca** de esquemas: La biblioteca de Esquemas contiene recursos XDM estándar del sector disponibles por Adobe, así como recursos personalizados definidos por su organización.

**Registro** de esquemas: El Registro de Esquemas proporciona una interfaz de usuario y una API RESTful que se utilizan para la vista y administración de todos los recursos relacionados con el esquema en la Biblioteca de Esquemas.

**Clave** de acceso secreta: Una clave de acceso secreto es una clave  [!DNL Amazon] S3 que se utiliza junto con el ID de clave de acceso para firmar solicitudes de AWS.

**Segmento**: Un segmento es un conjunto de reglas que incluye atributos y datos de evento que califican una cantidad de perfiles para convertirse en una audiencia.

**Generador** de segmentos: El  [!DNL Segment Builder] es un entorno de desarrollo visual que se utiliza para generar definiciones de segmentos. Sirve como un componente común de todas las aplicaciones que utilizan el servicio de segmentación por Experience Platform.

**Definición** del segmento: Una definición de segmento es el conjunto de reglas utilizado para describir las características o el comportamiento clave de una audiencia de destinatario. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia que cumplen los requisitos para un segmento.

**Método** de evaluación de segmentos: Existen dos métodos de evaluación de segmentos: programado y bajo demanda. La evaluación programada permite un programa recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que la evaluación a petición implica la creación de un trabajo de segmento para generar la audiencia inmediatamente.

**Exportación** de segmentos: La exportación de segmentos es uno de los dos tipos de destinos en Experience Platform. Con la exportación de segmentos, puede enviar los perfiles que califican y se han asignado al destino. Utiliza ID de segmento y usuario y datos seudónimos, y normalmente se integra con las redes sociales y otras plataformas de destinatario de medios digitales.

**ID** del segmento: Un ID de segmento es un identificador generado automáticamente asociado a un segmento.

**Membresía** del segmento: La pertenencia a segmentos muestra los segmentos de los que forma parte actualmente un perfil.

**Reglas** de segmento: Las reglas de segmentos definen las condiciones que determinan si un perfil cumple los requisitos para un segmento.

**Segmentación**: La segmentación es el proceso de dividir un gran grupo de clientes, clientes potenciales o consumidores en grupos más pequeños que comparten atributos similares y responderán de manera similar a estrategias de mercadotecnia específicas.

**Marco** Sensei ML: Sensei ML Framework es un marco de aprendizaje automático (ML) unificado que aprovecha los datos Experience Platform para empoderar a los científicos de datos para el desarrollo de servicios de inteligencia basados en ML de una manera más rápida, escalable y reutilizable.

**Etiquetas** sensibles (&quot;S&quot;): Las etiquetas sensibles (&quot;S&quot;) se utilizan para categorizar los datos considerados sensibles, como distintos tipos de datos de comportamiento o geográficos que se desean marcar como sensibles.

**Servicios**: Un potente entorno para la operacionalización de servicios AI y ML mediante el aprovechamiento de Adobe Intelligent Services. Los servicios ofrecen experiencias personalizadas en tiempo real o ofrecen servicios inteligentes personalizados.

**Acción** de mercadotecnia de personalización de identidad única: Acción de marketing que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer inferencias sobre los intereses de los usuarios y se utiliza para seleccionar qué contenido o publicidades se ofrecen en base a esas inferencias.

**Etiqueta** de uso de datos S1: Se utiliza una etiqueta de uso de  `S1` datos para clasificar datos que especifican la latitud y la longitud que pueden utilizarse para determinar la ubicación exacta de un dispositivo.

**Etiqueta** de uso de datos S2: Se utiliza una etiqueta de uso de  `S2` datos para clasificar los datos que pueden utilizarse para determinar un área de geofence definida de forma amplia.

**Fuente**: Un origen es un término general para cualquier conector de entrada en Platform. Consulte también: Conector de origen

**Atributo** de origen: Un atributo de origen es un campo del conjunto de datos de origen. Los atributos de origen se asignan a los campos de esquema de destinatario.

**Catálogo** de origen: El catálogo de origen es la lista de los conectores de origen disponibles en el Experience Platform.

**Categoría** de origen: Una categoría de origen es un grupo de fuentes que tienen características similares.

**Conector** de origen: Los conectores de origen (también conocidos como fuentes) ayudan a los usuarios a ingerir fácilmente datos de varias fuentes, lo que permite estructurar, etiquetar y mejorar los datos mediante servicios de Experience Platform. Los datos se pueden ingerir desde una variedad de fuentes, como almacenamiento basado en la nube, software de terceros y sistemas CRM.

**Conexión** de flujo continuo: Una conexión de flujo continuo es un punto final único proporcionado por Adobe y vinculado a la organización de IMS de un cliente para transmitir datos a Experience Platform.

**Área de nombres** de identidad estándar: Las Áreas de nombres de identidad estándar son Áreas de nombres de identidad predefinidas proporcionadas por Adobe, que representan soluciones estándares del sector que se utilizan comúnmente para identificar a los clientes.

**Transmisión por secuencias**: La ingestión por flujo continuo le permite enviar datos desde dispositivos del lado del cliente y del servidor al Experience Platform en tiempo real.

**Segmentación** de flujo continuo: La segmentación por flujo continuo es un proceso continuo de selección de datos que actualiza segmentos en respuesta a la actividad del usuario. Una vez creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes a [!DNL Real-time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan con regularidad, lo que garantiza que la audiencia de destinatarios siga siendo relevante.

**Vista** del sistema: La Vista del sistema es una representación visual de los conjuntos de datos de origen que fluyen  [!DNL Real-time Customer Profile] a los destinos.

## T

**Funciones** de destinatario: En la asignación de funciones, una función de destinatario es la función que predice un modelo.

**Datos** de series temporales: Los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto de registro realizó una acción directa o indirecta.

**Modelo** capacitado: Un modelo capacitado representa el resultado ejecutable de un proceso de capacitación de modelos, en el que se aplicó un conjunto de datos de capacitación a la instancia del modelo. Un modelo capacitado mantendrá una referencia a cualquier servicio Web inteligente que se cree a partir de él. Un modelo entrenado es adecuado para la puntuación y la creación de un servicio Web inteligente.

**Token**: Un token es un tipo de seguridad de autenticación de dos factores que puede utilizarse para autorizar el uso de servicios informáticos con  [!DNL Query Service].

## U

**Esquema** de unión: Un esquema de unión es una consolidación de esquemas que comparten la misma clase y para los que se ha habilitado  [!DNL Real-time Customer Profile]. Pueden existir varios esquemas de unión para una organización, pero sólo puede haber un esquema de unión por clase.

## V

## W

## X

**XDM**: Consulte Modelo de datos de experiencia (XDM).

**Evento** de decisión XDM: El Evento de decisiones XDM es una clase basada en series temporales que se utiliza para recoger observaciones sobre el resultado y el contexto de una actividad de decisión. Esto incluye información sobre cómo se tomó la decisión, cuándo se tomó, qué opciones se propusieron (y se eligieron) y qué estado contextual existió que influyó en la decisión o pudo observarse durante el proceso de decisión.

**XDM ExperienceEvent**: XDM ExperienceEvent es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produce un evento (o conjunto de eventos), incluido el punto en el tiempo y la identidad del sujeto involucrado. Consulte también: Evento de experiencias

**Perfil** individual XDM: XDM  [!DNL Individual Profile] es una clase basada en registros que forma una representación singular de los atributos de los sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o participaciones específicas, y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

**Sistema** XDM: El sistema XDM representa la estructura que opera esquemas XDM para su uso en servicios de Experience Platform descendentes.

## Y

## Z
