---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Glosario de Adobe Experience Platform
description: Un glosario de terminología importante en Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: 6327f5e6cb64a46c502613dd6074d84ed1fdd32b
workflow-type: tm+mt
source-wordcount: '7929'
ht-degree: 0%

---

# Glosario de Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Control de acceso**: El control de acceso basado en roles permite a los administradores asignar acceso y permisos a los usuarios del Experience Platform. Los permisos incluyen la capacidad de ver o utilizar funciones de Experience Platform, como la creación de entornos limitados, la definición de esquemas y la administración de conjuntos de datos.

**Acceso a ID de clave**: Un ID de clave de acceso es un identificador único asociado a un [!DNL Amazon] Clave de acceso secreta S3. El ID de clave de acceso y la clave de acceso secreta se utilizan juntos para firmar [!DNL Amazon Web Services] (AWS).

**Acción**: En el contexto de las etiquetas, una acción es un tipo específico de componente de regla que define lo que debe suceder después de que se produzca un evento y se evalúen y pasen las condiciones.

**Activar**: Activar es la acción que realiza un usuario para asignar un segmento o perfiles a un destino como [!DNL Oracle Eloqua], [!DNL Google]o [!DNL Salesforce Marketing Cloud].

**Actividad**: En [!DNL Offer Decisioning], una actividad contiene la lógica que indica la selección de una oferta.

**Administrador**: Una o más personas de su organización que pueden configurar y personalizar permisos para Experience Platform en Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console proporciona una ubicación central para administrar las autorizaciones de productos de Adobe y el acceso para su organización. A través de la consola, los administradores pueden otorgar a grupos de usuarios permisos de acceso para diversas funcionalidades de la plataforma, como &quot;Administrar conjuntos de datos&quot;, &quot;Ver conjuntos de datos&quot; o &quot;Administrar perfiles&quot;.

**Adobe Experience Platform**: Adobe Experience Platform estandariza los datos y el contenido en toda la empresa, lo que potencia los perfiles de los consumidores en tiempo real, permite la ciencia de datos y acelera la velocidad de contenido para impulsar la personalización de la experiencia en todo el recorrido de los clientes.

**Servicio de consultas de Adobe Experience Platform**: Permite a los analistas de datos consultar eventos y perfiles para utilizarlos en análisis y aprendizaje automático. Con el servicio de consulta, los científicos y analistas de datos pueden extraer todos sus conjuntos de datos almacenados en el Experience Platform (incluidos los datos de comportamiento, así como el punto de venta (POS), la administración de la relación con los clientes (CRM) y más) y consultar esos conjuntos de datos para responder preguntas específicas sobre los datos.

**Servicio de segmentación de Adobe Experience Platform**: Permite generar segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro del lago de datos.

**Servicios inteligentes de Adobe**: Los servicios inteligentes, como el Attribution AI y la Customer AI, son modelos de aprendizaje automático basados en la inteligencia artificial que están diseñados especialmente y que requieren que el Experience Platform los ejecute y funcione.

**Adobe I/O**: Adobe I/O forma parte del Experience Platform y proporciona acceso a todo lo que los desarrolladores necesitan para integrar, ampliar y personalizar Platform, incluidas las API, los eventos, la consola del desarrollador y las útiles herramientas.

**Adobe Sensei**: Adobe Sensei es el marco de inteligencia que impulsa al Experience Platform. También proporciona un conjunto de servicios de IA que permite a las marcas mejorar su capacidad para ofrecer experiencias personalizadas en tiempo real a los clientes.

**Bucket Amazon S3**: [!DNL Amazon S3] los contenedores son los contenedores de base para los datos almacenados en la variable [!DNL Amazon] ecosistema. Los contenedores contienen objetos, cada objeto se almacena y recupera utilizando una clave única asignada por el desarrollador.

**Conector Amazon S3**: La variable [!DNL Amazon] El conector S3 permite a los clientes del Experience Platform conectarse y acceder de forma segura a sus [!DNL Amazon] Datos S3.

**APA**: La variable [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promueve y protege la privacidad de las personas y regula la forma en que los organismos y organizaciones gubernamentales australianos administran la información personal. La variable [!DNL Privacy Act] incluye los principios aplicables a las organizaciones del sector privado. Por ejemplo, a las personas se les otorga el derecho de entender por qué se recopila la información personal y cómo se utilizará, la capacidad de acceder, borrar sus datos y corregir la información personal.

**Anexar estrategia de guardar**: La estrategia de guardado &quot;anexar&quot; es una opción que se utiliza al especificar datos de terceros para su ingesta a través de una conexión y anexar datos o filas nuevos al final del conjunto de datos. Las filas anidadas anteriormente permanecen inalteradas y solo las filas creadas desde la última ejecución programada se incorporan al Experience Platform. Las filas cambiadas en el sistema de origen permanecen sin cambios en el Experience Platform.

**Matriz**: Las matrices se utilizan para elementos ordenados con el mismo tipo de datos.

**Inteligencia artificial**: La inteligencia artificial es una teoría y el desarrollo de sistemas informáticos que son capaces de realizar tareas que normalmente requieren inteligencia humana, como la percepción visual, el reconocimiento del habla, la toma de decisiones y la traducción entre idiomas.

**Atributos**: Los atributos son características especificadas que representan un perfil.

**Combinación de atributos**: Al definir una directiva de combinación mediante la API de perfil de cliente en tiempo real, la variable `attributeMerge` indica la forma en que la política de combinación priorizará los atributos de perfil en caso de conflictos de datos. Equivale a seleccionar una [!UICONTROL Método Merge] al definir una política de combinación en la interfaz de usuario de Platform.

**Attribution AI**: [!DNL Attribution AI] es un servicio inteligente con tecnología de Adobe Sensei que ofrece funcionalidades de atribución algorítmica multicanal a lo largo de todo el ciclo de vida del cliente.

**Audiencia**: Una audiencia es el conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

**Tamaño de la audiencia**: Un tamaño de audiencia es el número total de perfiles que cumplen los criterios de una definición de segmento y cumplen los requisitos para pertenecer a una audiencia.

**Instantánea de audiencia**: Una instantánea de audiencia captura todos los perfiles que cumplen los criterios del segmento en el momento de la segmentación.

## B

**Relleno**: Para los orígenes programados, la opción de relleno permite la ingesta de datos históricos.

**Período de relleno**: El periodo de relleno es una opción para establecer el periodo de ingesta de datos históricos de terceros a través de una conexión de origen. Si se selecciona un periodo de relleno de &quot;para siempre&quot;, se introducirá todo el historial de los datos de origen en el Experience Platform.

**Lote**: Un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Los conjuntos de datos están compuestos por varios lotes.

**ID de lote**: Un ID de lote es un identificador generado por Adobe para un lote de datos.

**Ingesta por lotes**: La ingesta por lotes permite introducir datos en el Experience Platform como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad.

**Segmentación por lotes**: La segmentación por lotes es una alternativa a un proceso continuo de selección de datos y mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creado, este segmento se guarda y se almacena para que se pueda exportar para su uso.

**Generar**: En el contexto de las etiquetas, una compilación es un archivo o conjunto de archivos que contienen todas las configuraciones y el código necesarios para ejecutar la lógica empresarial contenida en una biblioteca, lo que le permite implementar esa biblioteca en su sitio web o aplicación móvil.

**Herramientas de inteligencia empresarial**: Las herramientas de inteligencia empresarial (BI) están integradas principalmente con [!DNL Experience Platform Query Service]. Las herramientas de BI son tipos de software de aplicación que recopilan y procesan grandes cantidades de datos no estructurados de sistemas internos y externos.

## C

**Restricción**: En [!DNL Offer Decisioning], el límite (también conocido como límite de frecuencia) se utiliza en las reglas de toma de decisiones para definir cuántas veces se presenta una oferta. Existen dos tipos de mayúsculas: cuántas veces se puede proponer una oferta en la audiencia de destino combinada (denominada &quot;límite global&quot;) y cuántas veces se puede proponer una oferta al mismo usuario final (denominada &quot;límite de perfil&quot;).

**Catálogo**: En el contexto de las fuentes y los destinos, un catálogo es una galería con conexiones disponibles a aplicaciones de Adobe y tecnologías de terceros. No confundir con [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (a veces se llama [!DNL Catalog]) es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos introducidos en el Experience Platform se almacenan en el lago de datos como archivos y directorios, [!DNL Catalog] contiene los metadatos y la descripción de esos archivos y directorios con fines de búsqueda, supervisión y control de datos.

**CCPA**: La variable [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) mejora los derechos de privacidad y la protección del consumidor para los residentes de California, Estados Unidos. La CCPA otorga nuevos derechos de privacidad de datos a los residentes de California, incluido el derecho a acceder y eliminar sus datos personales, a saber si sus datos personales se venden o revelan (y a quién) y el derecho a no participar en la venta de sus datos a terceros.

**Clase**: En Experience Data Model (XDM), una clase define el conjunto de campos más pequeño utilizado para crear un esquema y define el comportamiento base del objeto de negocio que representa el esquema.

**Cliente**: Un cliente es una herramienta o aplicación externa que se conecta a [!DNL Query Service] via [!DNL PostgreSQL] protocolo o API HTTP.

**Colección**: En [!DNL Offer Decisioning], las colecciones son subconjuntos de ofertas basadas en condiciones predefinidas definidas definidas por un especialista en marketing, como la categoría de la oferta.

**Combinación con la acción de marketing PII**: Acción de marketing que combina cualquier información de identificación personal (PII) con datos anónimos. Los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de dichos datos con datos directamente identificables.

**Interfaz de línea de comandos**: Una interfaz de línea de comandos es una herramienta basada en texto que puede utilizarse para conectarse a [!DNL Query Service] para la ejecución de consultas sin procesar.

**Composición**: Una composición es una agrupación de componentes que se forman juntos para formar el esquema.

**Condición**: En el contexto de las etiquetas, una condición es un componente de regla que evalúa una instrucción lógica que debe devolver `true` o `false`. Todas las condiciones deben evaluarse como `true` y todas las condiciones de excepción deben evaluarse como `false` antes de ejecutar ninguna acción en la regla.

**Consola**: En [!DNL Query Service], la consola proporciona información sobre el estado y el funcionamiento de una consulta. La consola muestra el estado de conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error que resulten de esas consultas.

**Etiquetas de contrato (&quot;C&quot;)**: Las etiquetas de uso de datos del contrato (&quot;C&quot;) se utilizan para categorizar los datos que tienen obligaciones contractuales o que están relacionados con las políticas de control de datos de su organización.

**CPRA**: La variable [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) amplía y modifica partes del [!DNL California Consumer Privacy Act (CCPA)]. La variable [!DNL CPRA] establece una nueva base para la privacidad de datos de los consumidores en California, al aumentar los derechos de los consumidores y ampliar el tipo de datos abarcados por una definición más amplia de información personal confidencial. Además, la variable [!DNL CPRA] estableció la Agencia de Protección de la Privacidad de California, una nueva agencia dedicada a implementar y aplicar las reglas de privacidad de datos.

**Etiqueta de contrato C1**: A `C1` la etiqueta de uso de datos de contrato especifica que los datos solo se pueden exportar desde Adobe Experience Cloud en un formulario agregado sin incluir identificadores individuales o de dispositivo. Por ejemplo, datos que se originaron en redes sociales.

**Etiqueta de contrato C2**: A `C2` la etiqueta de uso de datos de contrato especifica los datos que no se pueden exportar a un tercero. Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la exportación de datos desde donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales a menudo restringen la transferencia de datos que usted recibe de ellos. C2 es más restrictivo que C1, que solo requiere agregación y datos anónimos.

**Etiqueta de contrato C3**: A `C3` la etiqueta de uso de datos del contrato especifica los datos que no se pueden combinar ni utilizar de otro modo con información directamente identificable. Algunos proveedores de datos tienen cláusulas en sus contratos que prohíben la combinación o el uso de esos datos con información directamente identificable. Por ejemplo, los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de datos directamente identificables.

**Etiqueta de contrato C4**: A `C4` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para dirigir anuncios o contenido, ya sea en el sitio o entre sitios. C4 es la etiqueta más restrictiva, ya que engloba las etiquetas C5, C6 y C7.

**Etiqueta de contrato C5**: A `C5` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para la segmentación entre sitios de contenido o anuncios basados en intereses. La segmentación o personalización basada en intereses se produce si se cumplen las tres condiciones siguientes: Los datos recopilados en el sitio se utilizan para hacer inferencias sobre el interés del usuario; se utiliza en otro contexto, como en otro sitio o aplicación; y se usa para seleccionar qué contenido o anuncios se ofrecen en función de esas inferencias.

**Etiqueta de contrato C6**: A `C6` la etiqueta de uso de datos de contrato especifica que los datos no se pueden usar para la segmentación de anuncios en el sitio. La segmentación de anuncios en el sitio incluye la selección y entrega de anuncios en los sitios web de la organización, o aplicaciones, o para medir la entrega y efectividad de dichos anuncios. Esto incluye el uso de datos en el sitio recopilados anteriormente sobre el interés de los usuarios por seleccionar publicidades, procesar datos sobre qué publicidades se mostraron, cuándo y dónde se mostraron y si los usuarios realizaron alguna acción relacionada con el anuncio, como seleccionar un anuncio o realizar una compra.

**Etiqueta de contrato C7**: A `C7` la etiqueta de uso de datos de contrato especifica que los datos no se pueden usar para segmentar el contenido en el sitio. La segmentación de contenido en el sitio incluye la selección y entrega de contenido en los sitios web de la organización, o en las aplicaciones, o para medir la entrega y efectividad de dicho contenido. Esto incluye información recopilada anteriormente sobre el interés de los usuarios por seleccionar contenido, el procesamiento de datos sobre qué contenido se mostró, la frecuencia o el tiempo que se mostró, cuándo y dónde se mostró y si los usuarios realizaron alguna acción relacionada con el contenido, como seleccionar contenido.

**Etiqueta de contrato C8**: A `C8` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para medir los sitios web o las aplicaciones de su organización. Esto no incluye la segmentación basada en intereses, que es la recopilación de información sobre el uso de este servicio para personalizar posteriormente el contenido o la publicidad en otros contextos.

**Etiqueta de contrato C9**: A `C9` la etiqueta de uso de datos de contrato especifica que los datos no se pueden utilizar en flujos de trabajo de ciencia de datos. Algunos contratos incluyen prohibiciones explícitas sobre los datos utilizados para la ciencia de datos. A veces se expresan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado.

**Etiqueta de contrato C10**: A `C10` la etiqueta de uso de datos de contrato especifica que los datos no se pueden usar para la activación de identidad vinculada. Algunas políticas de uso de datos restringen el uso de datos de identidad vinculados para la personalización. La variable `C10` se aplica automáticamente a los segmentos si sus políticas de combinación utilizan la opción &quot;gráfico privado&quot;.

**Columna Fecha de creación**: La selección de una columna Fecha de creación es una opción al especificar datos de terceros mediante una conexión de origen. Cuando se selecciona la estrategia de guardar datos adjuntos y el esquema del conjunto de datos contiene varios campos de fecha, debe elegir entre el esquema disponible para especificar una columna de clave Fecha de creación . La opción Fecha de creación no está disponible cuando se selecciona la estrategia de sobrescritura y guardado.

**Crear tabla como seleccione**: Crear tabla como Seleccionar (CTAS) es un comando SQL que, cuando se ejecuta como parte de una consulta SQL completa y válida, ordena [!DNL Query Service] para mantener los resultados de la consulta en un conjunto de datos. Puede crear un nuevo conjunto de resultados, sobrescribir resultados anteriores o anexar a resultados anteriores.

**Datos entre sitios**: Los datos entre sitios son la combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio.

**Acción de marketing de objetivos entre sitios**: Acción de marketing que utiliza datos para la segmentación de anuncios entre sitios. La combinación de datos de varios sitios, incluida una combinación de datos en el sitio y datos fuera del sitio o una combinación de datos de varias fuentes fuera del sitio, se denomina datos entre sitios. Los datos entre sitios suelen recopilarse y procesarse para hacer inferencias sobre los intereses de los clientes.

**Área de nombres de identidad personalizada**: Su organización puede crear áreas de nombres de identidad personalizadas para representar identidades de una organización o un caso empresarial específicos.

**Etiquetas personalizadas**: Las etiquetas de uso de datos personalizadas le permiten crear y aplicar etiquetas específicas a campos de datos que satisfagan necesidades comerciales específicas.

**Customer AI**: Customer AI es un servicio inteligente de Adobe Sensei que enriquece los perfiles de los clientes con tendencias basadas en AI y potencia la segmentación de clientes y los esfuerzos de determinación de objetivos.

## D

**Diario**: En el contexto de las exportaciones de archivos programadas, programa las exportaciones de archivos completas o incrementales una vez al día, todos los días, desde la fecha de inicio hasta la fecha de finalización a la hora especificada por el usuario.

**Diccionario de datos**: En el contexto de las etiquetas, un diccionario de datos (también conocido como mapa de datos) es un conjunto de elementos de datos definidos dentro de una propiedad.

**Elemento de datos**: En el contexto de las etiquetas, un elemento de datos es un puntero que se utiliza dentro de las reglas y extensiones para señalar a un fragmento de datos específico que existe en el dispositivo cliente.

**Ingesta de datos**: El consumo de datos es el proceso de adición de datos de una fuente a un Experience Platform. Los datos se pueden ingerir en Platform de varias maneras, incluso mediante flujo continuo, lotes o mediante conectores de origen.

**Capa de datos**: En el contexto de las etiquetas, una capa de datos es una estructura de datos que existe en el dispositivo cliente y que contiene metadatos sobre el contexto en el que se ve una página o pantalla.

**Administración de datos**: La gobernanza de los datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos se ajusten a las normas y políticas de la organización con respecto al uso de los datos.

**Socios de integración de datos**: Los socios de integración de datos simplifican y automatizan la carga y transformación de volúmenes masivos de datos de más de 200 fuentes a Experience Platform sin necesidad de escribir código.

**Etiquetas de conjuntos de datos**: Las etiquetas de uso de datos se pueden agregar a conjuntos de datos. Todos los campos dentro de ese conjunto de datos heredarán las etiquetas del conjunto de datos.

**Data Science Workspace**: [!DNL Data Science Workspace] en Experience Platform permite a los clientes crear modelos de aprendizaje automático utilizando datos en aplicaciones de plataforma y Adobe para crear segmentos inteligentes, generar perspectivas y proporcionar predicciones, lo que le permite mejorar en gran medida las experiencias digitales de los usuarios finales.

**Fuente de datos**: Una fuente de datos es un origen de datos designado por el usuario. Algunos ejemplos de fuentes de datos son una aplicación móvil, eventos de perfil o experiencia, eventos de perfil de sitio web o un CRM.

**Administrador de datos**: Un gestor de datos es la persona responsable de la administración, supervisión y aplicación de los activos de datos de una organización. Un gestor de datos también garantiza que las políticas de control de datos se salvaguarden y se mantengan para cumplir con las regulaciones gubernamentales y las políticas organizativas.

**Flujo de datos**: Un flujo de datos es un conjunto o una colección de mensajes que comparten el mismo esquema y que se envían desde el mismo origen.

**Tipo de datos**: Un tipo de datos es un recurso XDM reutilizable que define un campo de tipo de objeto que contiene varias propiedades en una representación jerárquica.

**Etiquetas de uso de datos**: Las etiquetas de uso de datos le permiten clasificar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las regulaciones y políticas corporativas. Las etiquetas de uso de datos agregadas a un conjunto de datos se heredan o aplican a todos los campos dentro de ese conjunto de datos. Las etiquetas de uso de datos también se pueden aplicar directamente a los campos.

**Flujo de datos**: Un flujo de datos es una canalización virtual de datos que fluye a Platform desde un origen y hacia los destinos.

**Ejecución de flujo de datos**: Una ejecución de flujo de datos es un flujo de datos que llega en Experience Platform en función de una programación especificada por el usuario.

**Conjunto de datos**: Un conjunto de datos es una construcción de almacenamiento y administración para una recopilación de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas).

**ID de conjunto de datos**: Identificador generado por Adobe para un conjunto de datos ingerido.

**Salida de conjunto de datos**: El resultado del conjunto de datos proporciona un mecanismo para determinar qué se utilizará la opción &quot;Crear tabla como selección&quot; para un [!DNL Query Service] ejecute.

**Clave de deduplicación**: Clave principal definida por el usuario que determina la identidad por la cual los usuarios desean que sus perfiles se dedupliquen. &#x200B;

**Columna Delta**: Una columna delta permite seleccionar un campo de datos de origen para representar una marca de tiempo para la ingesta incremental.

**Estrategia de ahorro Delta**: La estrategia de guardado delta es una opción para la ingesta de datos de terceros a través de una conexión de origen. La opción permite al usuario especificar que se incorporan al Experience Platform filas de datos de origen nuevas o modificadas. Se agregan nuevas filas al final del conjunto de datos y las filas cambiadas se actualizan en el conjunto de datos en el Experience Platform.

**Descriptor**: En Experience Data Model (XDM), un descriptor es un conjunto adicional de metadatos relacionados con el esquema que describe un comportamiento específico de un campo. El Experience Platform puede utilizar los descriptores para comprender el comportamiento de esquema deseado, como la relación entre dos esquemas.

**Destino**: Un destino es un término general para cualquier extremo, como una aplicación de Adobe, una plataforma publicitaria, un servicio de almacenamiento en la nube o un servicio de marketing, donde se activa y envía una audiencia.

**Categoría de destino**: Una categoría de destino es un grupo de destinos que tienen características similares.

**Catálogo de destino**: Un catálogo de destino es una lista de destinos disponibles en Experience Platform.

**Reglas de llamada directa**: En el contexto de las etiquetas, una regla de llamada directa es una regla que se ejecuta cuando se llama directamente desde la página, omitiendo los sistemas de detección de eventos y búsqueda.

**Nombre para mostrar**: En el Modelo de datos de experiencia (XDM), un nombre para mostrar es un nombre descriptivo para un campo que se muestra en la interfaz de usuario.

## E

**Oferta apta**: Una oferta apta se puede ofrecer de forma coherente a un perfil, ya que cumple las restricciones definidas por adelantado.

**Reglas de elegibilidad**: En [!DNL Offer Decisioning], las reglas de idoneidad se aplican a un perfil relacionado con restricciones de calendario, programación y restricción.

**Acción de marketing por correo electrónico**: Acción de marketing que utiliza datos en campañas de segmentación de correo electrónico.

**Código incrustado**: En el contexto de las etiquetas, el código incrustado es una etiqueta de script ubicada dentro del HTML en un sitio o entorno. El código incrustado indica al explorador dónde recuperar la compilación.

**Enumeración**: Una enumeración (enumeración) es un campo XDM limitado a un conjunto de valores predefinidos.

**Entorno**: En el contexto de las etiquetas , un entorno es un conjunto de instrucciones de implementación que especifica el envío de host y el formato de archivo de una compilación. Una biblioteca debe estar emparejada con un entorno para poder crearse.

**Diagnóstico de errores**: Los diagnósticos de error permiten la generación de mensajes de error detallados para lotes ingeridos. El umbral de error permite configurar el porcentaje de errores aceptables antes de que falle un lote.

**Evento**: En el contexto de las etiquetas, un evento es un tipo específico de componente de regla, que es un déclencheur que se produce en un dispositivo cliente para comenzar la ejecución de una regla.

**Entidades de eventos**: En el contexto del modelado de datos, las entidades de eventos representan conceptos relacionados con las acciones que puede realizar un cliente, los eventos del sistema o cualquier otro concepto en el que desee rastrear los cambios a lo largo del tiempo. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la variable [!DNL XDM ExperienceEvent] Clase .

**Eventos**: Los eventos son los datos de comportamiento asociados a un perfil.

**Modelo de datos de experiencia (XDM)** [!DNL Experience Data Model] (XDM) es un marco de código abierto que utiliza esquemas estándar para unificar los datos para usarlos con aplicaciones de Experience Platform y Adobe Experience Cloud. XDM estandariza cómo se estructuran los datos y acelera y simplifica el proceso de obtener perspectivas a partir de cantidades masivas de datos.

**Experimento**: Un experimento es el proceso de crear un modelo entrenado formando la instancia con una porción de muestra de datos de producción en vivo. Esto es diferente de un modelo entrenado que se prueba con un conjunto de datos de prueba de retención. Esto también es diferente del concepto de un experimento en algunos marcos de aprendizaje automático donde en realidad significa un proyecto de modelado de muestra.

**Evento de experiencia**: Un evento de experiencia representa una instantánea del sistema cuando se produce una interacción o un evento relacionado con una experiencia de cliente. Los eventos de experiencia son registros de hechos inmutables de lo que ha sucedido y representan lo que ha sucedido sin agregación ni interpretación. En el Modelo de datos de experiencia (XDM), este concepto se captura mediante la función [!DNL XDM ExperienceEvent] Clase .

**Exportar archivo completo**: Archivo de exportación que contiene una instantánea completa de todas las cualificaciones de perfil del segmento seleccionado.

**Exportar archivos incrementales**: Una serie de archivos exportados en los que el primer archivo es una instantánea completa de todas las cualificaciones de perfil del segmento seleccionado y los archivos posteriores son cualificaciones de perfil incrementales desde la exportación anterior.

**Extensión**: En el contexto de las etiquetas , una extensión es un paquete de funcionalidad añadido a una propiedad de etiqueta . Una extensión suele centrarse en una solución de marketing o análisis concreta y proporciona las herramientas necesarias para implementar esa tecnología en un entorno de cliente.

**Paquete de extensión**: En el contexto de las etiquetas , un paquete de extensión es un archivo ZIP creado y cargado por un desarrollador de extensiones que proporciona todo lo necesario para que los usuarios de etiquetas instalen la extensión dentro de su propiedad. Un paquete de extensión contiene un manifiesto que especifica información sobre la extensión, el HTML/JavaScript necesario para que los usuarios finales configuren el comportamiento de la extensión de etiqueta y el JavaScript ejecutable entregado al entorno del cliente (si es necesario).

## F

**Ofertas de reserva**: Una oferta de reserva es la oferta predeterminada que se muestra cuando un usuario final no es apto para ninguna de las ofertas de la colección utilizada.

**Asignación de funciones**: La asignación de funciones se refiere al proceso de asignación de características de los datos a las funciones de entrada y destino que requiere un modelo de aprendizaje automático.

**Campo**: Un campo es el elemento de nivel más bajo de un conjunto de datos, tal como se define en el esquema XDM del conjunto de datos. Cada campo tiene un nombre para hacer referencia y un tipo para indicar el tipo de datos que contiene. Los tipos de campo pueden incluir (entre otros) números enteros, números, cadenas, booleanos y objetos.

**Grupo de campos**: Consulte &quot;Grupo de campos de esquema&quot;.

**Etiquetas de campos**: Las etiquetas de campo son etiquetas de control de datos que se heredan de un conjunto de datos o se aplican directamente a un campo.

**Nombre del campo**: Se utiliza un nombre de campo para hacer referencia al valor de un campo en las consultas y los servicios descendentes.

**Frecuencia**: En [!DNL Query Service], la frecuencia determina con qué frecuencia se ejecutará una consulta programada recurrente.

## G

**Geofence**: Una geovalla es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software almacenar en déclencheur una respuesta cuando un dispositivo móvil entra o sale de un área en particular.

**RGPD (Reglamento general de protección de datos)**: El Reglamento General de Protección de Datos (RGPD) es un marco jurídico que establece directrices para la recopilación y el tratamiento de información personal de personas que se encuentren en la Unión Europea (UE). El RGPD establece los principios para la gestión de datos y los derechos de las personas y abarca todas las empresas que se ocupan de los datos de los ciudadanos de la UE.

**Seguridad**: Las protecciones son umbrales que proporcionan directrices para el uso de los datos y del sistema, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform. Las protecciones pueden referirse a su uso o consumo de datos y procesamiento en relación con sus derechos de licencia.

## H

**HIPAA**: La variable [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) es una ley federal de los Estados Unidos creada para mejorar la eficiencia de la atención de la salud, mejorar la portabilidad del seguro de salud y proteger la privacidad de los pacientes y los miembros del plan de salud. Con arreglo a la Iniciativa, las personas tienen derecho a acceder a su información y a modificarla, y a obtener copias de su historial médico o información sanitaria. Las entidades abarcadas y los asociados comerciales de las entidades abarcadas deben cumplir las normas de la Iniciativa.

**Host**: En el contexto de las etiquetas, un host especifica la ubicación, el dominio y las credenciales de usuario necesarios para que el sistema envíe una compilación.

**Por hora**: En el contexto de las exportaciones de archivos programadas, programa las exportaciones de archivos incrementales cada 3, 6, 8 ó 12 horas.

## I

**Identidad**: Una identidad es un identificador que representa de forma exclusiva a un cliente individual, como un ID de cookie, un ID de dispositivo o un ID de correo electrónico.

**Campos de identidad**: Los campos de identidad son campos XDM que se utilizan para unir información sobre clientes individuales que provienen de múltiples fuentes de datos. Se debe definir una sola identidad principal para que el esquema esté habilitado para utilizarse en el perfil del cliente en tiempo real.

**Etiquetas de identidad (&quot;I&quot;)**: Las etiquetas de uso de datos de identidad (&quot;I&quot;) se utilizan para categorizar los datos que pueden identificar a una persona específica o ponerse en contacto con ella.

**Gráfico de identidad**: Un gráfico de identidad es un mapa de relaciones entre identidades vinculadas y vinculadas que existen para un cliente individual. Cada gráfico de identidad se actualiza casi en tiempo real con la actividad del cliente. La estructura común de las relaciones de identidad en los datos se representa mediante la variable [!UICONTROL Gráfico privado], que sirve como modelo estructural para cada gráfico de identidad individual.

**Área de nombres de identidad**: Un área de nombres de identidad define el contexto de un identificador, como una dirección de correo electrónico o un ID de CRM.

**Servicio de identidad**: [!DNL Experience Platform Identity Service] permite la creación y administración de tipos de identidad, lo que permite vincular las identidades de los clientes entre dispositivos y canales. La capacidad del servicio para vincular identidades permite que el perfil del cliente en tiempo real proporcione una representación completa de cada cliente individual.

**Vinculación de identidad**: La vinculación de identidad es el proceso de identificación de fragmentos de datos y de vinculación para formar un registro de perfil completo.

**Símbolo de identidad**: Un símbolo de identidad es una abreviatura de un área de nombres de identidad que puede utilizarse como referencia en las API.

**Valor de identidad**: Un valor de identidad, combinado con un área de nombres de identidad, es un identificador que representa un individuo, organización o recurso únicos. Al hacer coincidir los datos de registro en los fragmentos de perfil, el área de nombres y el valor de identidad deben coincidir.

**Etiqueta de uso de datos I1**: La variable `I1` la etiqueta de uso de datos se utiliza para clasificar los datos que pueden identificar directamente a una persona específica o ponerse en contacto con ella en lugar de con un dispositivo.

**Etiqueta de uso de datos I2**: La variable `I2` la etiqueta de uso de datos se utiliza para clasificar los datos que se pueden utilizar en combinación con otros datos para identificar indirectamente a una persona específica o ponerse en contacto con ella.

**Organización IMS**: Una organización de IMS (a veces denominada organización de IMS) es el nombre que se utiliza para identificar una empresa o un grupo específico dentro de una empresa en todos los productos de Adobe. Los administradores pueden configurar y administrar el acceso y los permisos de las funciones para los usuarios de una organización.

**Ingesta**: Consulte ingesta de datos.

**Programación de ingesta**: Una programación de ingesta proporciona opciones basadas en el tiempo al ingerir de un origen a un Experience Platform.

**Función de entrada**: Se especifica una función de entrada en la asignación de funciones y la utiliza un modelo de aprendizaje automático para hacer predicciones.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] como [!DNL Attribution AI] y [!DNL Customer AI] son modelos de aprendizaje automático basados en inteligencia artificial que requieren que el Experience Platform (o las aplicaciones creadas sobre Platform como Adobe Real-time Customer Data Platform) se ejecute y funcione.

**Segmentación o personalización basada en intereses**: La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes:

1. Los datos recopilados en el sitio se utilizan para hacer inferencias sobre el interés del usuario.
1. Los datos se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio).
1. Los datos se utilizan para seleccionar qué contenido o anuncios se ofrecen en función de esas inferencias.

## J

**[!DNL JupyterLab]**: Una interfaz de código abierto y basada en web para Project [!DNL Jupyter] que se integra en la interfaz de usuario de Platform.

**[!DNL Jupyter Notebook]**: Los Jupyter Notebooks, integrados con JupyterLab, le permiten realizar tareas de limpieza y transformación de datos, simulación numérica, modelado estadístico, visualización de datos, aprendizaje automático y mucho más en los datos de su Experience Platform en diversos idiomas, como Python, Scala y PySpark.

## K

## L

**LGPD**: La variable [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) tiene por objeto regular el tratamiento de los datos personales de todas las personas físicas o jurídicas en el Brasil. La LGPD otorga a los ciudadanos brasileños el derecho a acceder y eliminar sus datos personales, a saber si sus datos personales se venden o revelan (y a quién), y el derecho a renunciar a que sus datos se vendan a terceros.

**Biblioteca**: En el contexto de las etiquetas, una biblioteca es un conjunto de lógica empresarial que contiene instrucciones sobre cómo debe comportarse la biblioteca de etiquetas en el dispositivo cliente.

**Entidades de búsqueda**: En el contexto del modelado de datos, las entidades de búsqueda representan conceptos que pueden relacionarse con una persona individual, pero que no pueden utilizarse directamente para identificar a la persona. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en clases personalizadas del Modelo de datos de experiencia (XDM) y vinculadas a una entidad de perfil a través de una [relación de esquema](../xdm/tutorials/relationship-ui.md).

## M

**Aprendizaje automático (ML)**: El aprendizaje automático es el campo de estudio que permite a los ordenadores aprender sin ser programados explícitamente.

**Modelo de aprendizaje automático**: Un modelo de aprendizaje automático es un ejemplo de una fórmula de aprendizaje automático que se enseña mediante datos y configuraciones históricos para resolver un caso de uso empresarial. En Adobe Experience Platform Data Science Workspace, los modelos de aprendizaje automático se denominan fórmulas.

**Atributo obligatorio**: Casilla habilitada por el usuario que garantiza que todos los registros de perfil contengan el atributo seleccionado. Por ejemplo: todos los perfiles exportados contienen una dirección de correo electrónico.

**Asignación**: La asignación de datos es el proceso de asignación de campos de datos de origen a campos de destino relacionados en un destino.

**Acción de marketing**: En el marco de control de datos, una acción de marketing (también conocida como caso de uso de marketing) es una acción que realiza un consumidor de datos de Experience Platform, para la cual es necesario comprobar si hay infracciones de las políticas de uso de datos.

**Método Merge**: Al definir una directiva de combinación mediante la interfaz de usuario de Platform, el método de combinación especifica cómo se debe priorizar los fragmentos de datos cuando se produce un conflicto. Al utilizar la API de perfil de cliente en tiempo real para definir una directiva de combinación, el método de combinación se determina utilizando la variable `attributeMerge` objeto.

**Combinar directiva**: Las políticas de combinación son reglas que el Experience Platform utiliza para determinar cómo se combinarán los fragmentos de datos de clientes de varias fuentes para crear un perfil individual. Cuando se produce un conflicto de datos, la política de combinación determina qué datos deben priorizarse para su inclusión en el perfil.

**Mixin**: Consulte &quot;Grupo de campos de esquema&quot;.

**Módulo**: En el contexto de las etiquetas, un módulo es un fragmento de JavaScript ejecutable proporcionado por una extensión, que realiza acciones en un entorno de cliente sin necesidad de crear una regla.

## N

**[!DNL New Zealand Privacy Act]**: La variable [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) controla la forma en que las agencias pueden recopilar, utilizar, revelar, almacenar y dar acceso a la información personal de los ciudadanos y organizaciones de Nueva Zelandia. En 2020, la última versión de la ley introdujo importantes actualizaciones a estas leyes de privacidad, incluyendo nuevos delitos, aumento de multas, notificaciones obligatorias por infracciones de datos y aumento de las facultades del Comisionado de privacidad.

**Simulador para pruebas que no son de producción**: Los entornos limitados que no son de producción son entornos limitados que generalmente se utilizan para experimentos de desarrollo, pruebas o pruebas. A diferencia de los entornos limitados de producción, los entornos limitados que no sean de producción se pueden restablecer y eliminar.

**[!DNL Notebooks]**: [!DNL Notebooks] se crean mediante [!DNL Jupyter Notebook] y se pueden ejecutar para realizar análisis de datos.

## O

**Oferta**: Una oferta es un mensaje de marketing que contiene una propuesta comercial o de ventas a un cliente (potencial). Las ofertas suelen tener reglas específicas que determinan quién puede verlas o recibirlas.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] permite a los especialistas en marketing administrar reglas y modelos formados de propuestas de ofertas al interactuar con usuarios finales en función de los datos recopilados en canales y aplicaciones.

**Biblioteca de ofertas**: La biblioteca de ofertas es una biblioteca central que se utiliza para administrar ofertas, reglas de decisión y actividades personalizadas y de reserva.

**Acción de marketing de personalización en el sitio**: Acción de marketing que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer inferencias sobre los intereses de los usuarios y se utiliza para seleccionar qué contenido o anuncios se proporcionan en función de esas inferencias.

**Acción de marketing de segmentación en el sitio**: Acción de marketing que usa datos para los anuncios en el sitio, incluida la selección y entrega de anuncios en los sitios web o aplicaciones de su organización, o para medir el envío y la eficacia de dichos anuncios.

**Una vez**: En el contexto de las exportaciones de archivos programadas, programa una exportación de archivos completa, única y a petición.

**Sobrescribir estrategia de guardar**: La estrategia de guardado &quot;Sobrescribir&quot; es una opción para introducir datos de terceros a través de una conexión, donde puede especificar si los datos introducidos se sobrescribirán en una programación especificada.

## P

**Ingesta parcial**: La ingesta parcial permite la ingesta de registros válidos de datos de lote dentro de un umbral de error especificado. Se pueden descargar o acceder a los diagnósticos de errores para registros con errores en [!UICONTROL Monitorización] o [!UICONTROL Fuentes] información general de ejecución de flujo de datos.

**Archivos de parqué**: Un archivo de parquet es un formato de archivo de almacenamiento en columnas con estructuras de datos anidadas complejas. Se necesitan archivos de parqué para agregar datos para rellenar un conjunto de datos de esquema.

**PDPA**: La variable [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) se introdujo para proteger a los propietarios tailandeses de la recopilación, el uso o la revelación ilegales de sus datos personales. Inspirada en el RGPD de la Unión Europea, la normativa concede a los ciudadanos tailandeses el derecho de solicitar el acceso o la eliminación de sus datos personales almacenados.

**Ofertas personalizadas**: Una oferta personalizada es un mensaje de marketing personalizable basado en reglas y restricciones de idoneidad.

**Ubicaciones**: una ubicación es la ubicación o el contexto en el que aparece una oferta para un usuario final.

**Espacio de trabajo de directivas**: Espacio de trabajo en la interfaz de usuario de Platform que permite a los administradores de datos ver y administrar las etiquetas y políticas de uso de datos de su organización.

**Política**: Una directiva de uso de datos es una regla que especifica las acciones de marketing que están restringidas en función de la aplicación de etiquetas de uso aplicadas a los datos de Platform.

**Aplicación de políticas**: Permite aplicar políticas de uso de datos con acciones de marketing aplicadas para evitar operaciones de datos que constituyan violaciones de políticas dentro de una organización.

**Clave principal**: Una clave principal es una designación en un esquema para identificar de forma exclusiva todos los registros.

**Prioridad**: En [!DNL Offer Decisioning], la prioridad se utiliza para clasificar las ofertas que cumplen todas las restricciones, como la idoneidad, el calendario y el límite.

**Gráfico de identidad privada**: El gráfico de identidad privada (a veces denominado gráfico privado) es un mapa privado de las relaciones entre identidades vinculadas y vinculadas que se basa en los datos de origen y que solo su organización puede ver. Solo existe un gráfico privado para cada organización y sirve como modelo estructural para los gráficos de identidad individuales generados para cada cliente que interactúa con su marca.

**Perfil del producto**: Los perfiles de producto permiten a los administradores conceder acceso a los usuarios a todos o a un subconjunto de servicios asociados con el Experience Platform.

**Espacio aislado de producción**: Un simulador para pruebas de producción es un simulador para pruebas que se utiliza en el entorno de producción. A diferencia de los entornos limitados que no son de producción, los entornos limitados de producción no se pueden restablecer ni eliminar.

**Perfil**: No debe confundirse con Perfil del cliente en tiempo real como servicio. Un perfil es una representación completa de un cliente individual, creada a partir de registros combinados y datos de series temporales de múltiples fuentes.

**Acceso a perfiles**: La variable `/entities` en la API de perfil de cliente en tiempo real le permite acceder a datos de registro y eventos de serie temporal en el almacén de datos de perfil. Consulte también: Entidades de perfil

**Datos de perfil**: Los datos de perfil hacen referencia a cualquier dato ubicado dentro del almacén de datos de perfil.

**Almacenamiento de datos de perfil**: El almacén de datos de perfil (a veces denominado almacén de perfiles) es un sistema de almacenamiento de datos independiente del lago de datos que utiliza el perfil del cliente en tiempo real para crear y almacenar perfiles.

**Entidades de perfil**: Las entidades de perfil representan atributos relacionados con una persona individual, normalmente un cliente. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la variable [!DNL XDM Individual Profile] Clase . Consulte también: Acceso a perfiles

**Exportación de perfiles**: [!DNL Profile] export es uno de los dos tipos de destinos en Experience Platform. [!DNL Profile] export genera un archivo que contiene perfiles y atributos, y utiliza datos PII sin procesar con el correo electrónico para integrarlos con las plataformas de automatización de correo electrónico y marketing.

**Fragmento de perfil**: Un fragmento de perfil es la información de perfil de una sola identidad de la lista de identidades que existe para un cliente en particular.

**ID de perfil**: Un ID de perfil es un identificador generado automáticamente asociado a un tipo de identidad y representa un perfil.

**Propiedad**: En el contexto de las etiquetas , una propiedad es un contenedor de todo lo necesario para implementar un conjunto de etiquetas.

## Q

**Consulta**: Las consultas son solicitudes de datos de tablas de base de datos.

**Editor de consultas**: El Editor de consultas es una herramienta para escribir, validar y enviar instrucciones SQL en [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) aúna datos conocidos y desconocidos de los clientes para crear perfiles de clientes fiables con una integración simplificada, segmentación inteligente y activación en tiempo real en todo el recorrido digital de clientes.

**Perfil del cliente en tiempo real**: El perfil del cliente en tiempo real (a veces denominado Perfil) proporciona una vista holística de cada cliente al combinar datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. Profile le permite consolidar sus datos de clientes en perfiles individuales que ofrecen cuentas procesables con marca de hora de cada interacción con clientes.

**Fórmula**: Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa los procesos de aprendizaje automático específicos, los algoritmos de IA, la lógica de procesamiento y los parámetros de configuración necesarios para crear y ejecutar un modelo entrenado y, por lo tanto, ayudan a resolver problemas empresariales específicos.

**Registro**: Un registro son datos que se mantienen como filas en un conjunto de datos.

**Registrar datos**: Proporciona información sobre los atributos de un asunto. Un tema podría ser una organización o un individuo.

**Periodicidad**: En [!DNL Query Service], una periodicidad define si una consulta está programada para ejecutarse solo una vez o de forma recurrente.

**Representación**: En [!DNL Offer Decisioning], una representación es información que un canal utiliza para mostrar una oferta, como ubicación o idioma.

**Recurso**: En el contexto de las etiquetas, un recurso es un término genérico que hace referencia a las opciones que el usuario de etiquetas puede configurar dentro del entorno del cliente, incluidas las extensiones, los elementos de datos y las reglas.

**Control de acceso basado en roles**: El control de acceso basado en roles permite a los administradores asignar acceso y permisos a los usuarios del Experience Platform. Los permisos incluyen la capacidad de ver o utilizar funciones de Experience Platform, como la creación de entornos limitados, la definición de esquemas y la administración de conjuntos de datos.

**Regla**: En el contexto de las etiquetas, una regla es una colección de componentes que definen un conjunto específico de eventos, condiciones y acciones que deben agruparse lógicamente.

**Componente de regla**: En el contexto de las etiquetas, los componentes de regla son los eventos, las condiciones y las acciones que constituyen una regla.

**Tiempo de ejecución**: Tiempo de ejecución especifica un entorno de tiempo de ejecución para una fórmula de aprendizaje automático. [!DNL Python], R, [!DNL Spark], PySpark y Tensorflow runtimes permiten introducir una URL a una imagen Docker para un origen de fórmula.

## S

**Datos de muestra**: Los datos de ejemplo son una previsualización de un archivo de datos, normalmente las primeras 100 filas, que proporciona a un científico de datos o a un ingeniero una idea de qué esquema o datos se encuentran en el archivo de datos.

**Sandbox**: Un entorno limitado es una construcción virtual que divide una sola instancia de Platform en un entorno virtual independiente para ayudar a desarrollar y desarrollar aplicaciones de experiencia digital.

**Restablecimiento de Sandbox**: Un restablecimiento de entorno limitado elimina todos los datos, incluidos los datos, perfiles y segmentos de un entorno limitado. Los restablecimientos del Simulador para pruebas pueden afectar a los datos conectados a destinos internos o externos.

**Conmutador de espacio aislado**: El control del conmutador de simulador de pruebas en el Experience Platform permite a los usuarios navegar entre los entornos limitados a los que tienen acceso. Si se cambia un simulador para pruebas, todo el contenido cambiará y puede alterar el acceso a las funciones en función de los permisos.

**Programación**: Una programación es una especificación definida por el usuario sobre la frecuencia o cadencia de la ingesta de datos desde una fuente de datos de terceros a Adobe Experience Platform.

**Puntuación**: La puntuación es el proceso de generación de perspectivas a partir de datos mediante un modelo entrenado.

**Esquema**: Un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. Un esquema consta de una clase y un grupo de campos opcionales y se utiliza para crear conjuntos de datos y conjuntos de datos. Un esquema puede incluir atributos de comportamiento, marcas de tiempo, identidades, definiciones de atributos, relaciones, etc.

**Grupo de campos de esquema**: En Experience Data Model (XDM), un grupo de campos de esquema permite a los usuarios ampliar los campos reutilizables para definir uno o más atributos que se pretenden incluir en un esquema.

**Biblioteca de esquemas**: La biblioteca de esquemas contiene recursos XDM estándar del sector disponibles por Adobe, así como recursos personalizados definidos por su organización.

**Registro de esquemas**: El Registro de esquemas proporciona una interfaz de usuario y una API RESTful que se utilizan para ver y administrar todos los recursos relacionados con esquemas en la Biblioteca de esquemas.

**Clave de acceso secreta**: Una clave de acceso secreta es una [!DNL Amazon] Clave S3 que se utiliza junto con el ID de clave de acceso para firmar solicitudes de AWS.

**Segmento**: Un segmento es un conjunto de reglas que incluyen atributos y datos de evento que califican varios perfiles para convertirse en audiencia.

**Generador de segmentos**: La variable [!DNL Segment Builder] es un entorno de desarrollo visual que se utiliza para crear definiciones de segmentos. Sirve como componente común de todas las aplicaciones que utilizan el servicio de segmentación de Experience Platform.

**Definición del segmento**: Una definición de segmento es el conjunto de reglas que se utiliza para describir las características o el comportamiento clave de una audiencia de destino. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia cualificados para un segmento.

**Método de evaluación de segmentos**: Existen dos métodos de evaluación de segmentos: programada y bajo demanda. La evaluación programada permite un programa recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que la evaluación bajo demanda implica la creación de un trabajo de segmento para crear la audiencia inmediatamente.

**Exportación de segmentos**: La exportación de segmentos es uno de los dos tipos de destinos en Experience Platform. Con la exportación de segmentos, puede enviar los perfiles que califican y se han asignado al destino. Utiliza ID de usuario y segmento y datos seudónimos, y normalmente se integra con las redes sociales y otras plataformas de destino de medios digitales.

**ID de segmento**: Un ID de segmento es un identificador autogenerado asociado a un segmento.

**Pertenencia a segmentos**: La pertenencia a segmentos muestra los segmentos de los que forma parte un perfil.

**Reglas de segmento**: Las reglas de segmentos definen las condiciones que determinan si un perfil cumple los requisitos para un segmento.

**Segmentación**: La segmentación es el proceso de dividir un grupo grande de clientes, clientes potenciales o consumidores en grupos más pequeños que comparten atributos similares y que responderán de manera similar a estrategias de marketing específicas.

**Sensei ML Framework**: Sensei ML Framework es un marco unificado de aprendizaje automático (ML) que aprovecha los datos Experience Platform para empoderar a los científicos de datos en el desarrollo de servicios de inteligencia basados en ML de una manera más rápida, escalable y reutilizable.

**Etiquetas confidenciales (&quot;S&quot;)**: Las etiquetas confidenciales (&quot;S&quot;) se utilizan para categorizar los datos considerados confidenciales, como diferentes tipos de datos de comportamiento o geográficos que desea marcar como confidenciales.

**Servicios**: Un potente marco para la operacionalización de los servicios AI y ML mediante el uso de los servicios inteligentes de Adobe. Los servicios ofrecen experiencias de cliente personalizadas en tiempo real u operacionalizan servicios inteligentes personalizados.

**Acción de marketing de personalización de identidad única**: Acción de marketing que utiliza datos para la personalización de contenido en el sitio. La personalización del sitio es cualquier dato que se utiliza para hacer inferencias sobre los intereses de los usuarios y se utiliza para seleccionar qué contenido o anuncios se proporcionan en función de esas inferencias.

**Etiqueta de uso de datos S1**: Un `S1` la etiqueta de uso de datos se utiliza para clasificar los datos que especifican la latitud y la longitud que se pueden usar para determinar la ubicación precisa de un dispositivo.

**Etiqueta de uso de datos S2**: Un `S2` la etiqueta de uso de datos se utiliza para clasificar los datos que se pueden utilizar para determinar un área de geovalla definida a grandes rasgos.

**Fuente**: Un origen es un término general para cualquier conector de entrada en Platform. Consulte también: Conector de origen

**Atributo de origen**: Un atributo de origen es un campo del conjunto de datos de origen. Los atributos de origen se asignan a los campos de esquema de destino.

**Catálogo de origen**: El catálogo de origen es la lista de conectores de origen disponibles en Experience Platform.

**Categoría de origen**: Una categoría de origen es una agrupación de fuentes que tienen características similares.

**Conector de origen**: Los conectores de origen (también conocidos como fuentes) ayudan a los usuarios a ingerir fácilmente datos de múltiples fuentes, lo que permite estructurarlos, etiquetarlos y mejorarlos utilizando los servicios de Experience Platform. Los datos se pueden ingerir desde una variedad de fuentes, como almacenamiento basado en la nube, software de terceros y sistemas CRM.

**Conexión de flujo continuo**: Una conexión de flujo continuo es un punto final único que proporciona el Adobe y que está vinculado a su organización para transmitir datos a Experience Platform.

**Área de nombres de identidad estándar**: Las áreas de nombres de identidad estándar son áreas de nombres de identidad predefinidas proporcionadas por Adobe, que representan soluciones estándar del sector que normalmente se emplean para identificar clientes.

**ingesta por transmisión**: La introducción por transmisión le permite enviar datos desde dispositivos del lado del cliente y del servidor al Experience Platform en tiempo real.

**Segmentación por transmisión**: La segmentación por transmisión es un proceso continuo de selección de datos que actualiza los segmentos en respuesta a la actividad del usuario. Una vez que se ha creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes a [!DNL Real-Time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan con regularidad, lo que garantiza que la audiencia de destino siga siendo relevante.

**Vista del sistema**: La vista del sistema es una representación visual de los conjuntos de datos de origen que fluyen a través de [!DNL Real-Time Customer Profile] a destinos.

## T

**Etiquetas**: En Adobe Experience Platform, las etiquetas proporcionan herramientas para implementar, unificar y administrar integraciones de análisis, marketing y publicidad que son necesarias para potenciar las experiencias relevantes del cliente en todos los dispositivos cliente.

**Funciones de Target**: En la asignación de funciones, una función de destino es la función que predice un modelo.

**Datos de series temporales**: Los datos de series temporales proporcionan una instantánea del sistema en el momento en que el sujeto de un registro realizó una acción directa o indirecta.

**Modelo capacitado**: Un modelo capacitado representa el resultado ejecutable de un proceso de capacitación de modelo, en el que se aplicó un conjunto de datos de capacitación a la instancia del modelo. Un modelo entrenado mantendrá una referencia a cualquier servicio Web inteligente que se cree a partir de él. Un modelo entrenado es adecuado para la puntuación y la creación de un servicio web inteligente.

**Token**: Un token es un tipo de seguridad de autenticación de dos factores que se puede utilizar para autorizar el uso de servicios de equipo con [!DNL Query Service].

## U

**Esquema de unión**: Un esquema de unión es una consolidación de esquemas que comparten la misma clase y que se han habilitado para [!DNL Real-Time Customer Profile]. Pueden existir varios esquemas de unión para una organización, pero solo puede haber un esquema de unión por clase.

## V

**VCDPA**: La variable [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) proporciona nuevos derechos de privacidad de datos a los residentes de Virginia (&quot;Consumidores&quot;), incluido el derecho a acceder, eliminar y corregir datos personales. Los consumidores también tienen derecho a excluirse de la venta de datos personales, a excluirse de la creación de perfiles basados en datos personales y a procesar fines publicitarios personales.

## W

## X

**XDM**: Consulte Modelo de datos de experiencia (XDM).

**Evento de decisión XDM**: El Evento de Decisión XDM es una clase basada en series temporales que se utiliza para capturar observaciones sobre el resultado y el contexto de una actividad de decisión. Esto incluye información sobre cómo se tomó la decisión, cuándo se tomó, qué opciones se propusieron (y se escogieron) y qué estado contextual existió que influyó en la decisión o pudo observarse durante el proceso de decisión.

**XDM ExperienceEvent**: XDM ExperienceEvent es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produjo un evento (o conjunto de eventos), incluyendo el punto en el tiempo y la identidad del sujeto involucrado. Consulte también: Evento de experiencia

**Perfil individual XDM**: XDM [!DNL Individual Profile] es una clase basada en registros que forma una representación singular de los atributos de sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o participaciones específicas, y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

**Sistema XDM**: El sistema XDM representa el marco que operacionaliza los esquemas XDM para su uso en servicios de Experience Platform descendente.

## Y

## Z
