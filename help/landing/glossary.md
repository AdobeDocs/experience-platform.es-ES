---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Glosario de Adobe Experience Platform
description: Un glosario de terminología importante en Experience Platform.
exl-id: 00eae5f5-7dfa-45ac-aff9-9e1769a3a53a
source-git-commit: b16eae9698de6c20022fdf1a3ff659df35e440f6
workflow-type: tm+mt
source-wordcount: '7996'
ht-degree: 0%

---

# Glosario de Adobe Experience Platform {#adobe-experience-platform-glossary}

## A

**Control de acceso**: El control de acceso basado en funciones permite a los administradores asignar acceso y permisos a los usuarios de Experience Platform. Los permisos incluyen la capacidad de ver o utilizar funciones de Experience Platform, como crear entornos limitados, definir esquemas y administrar conjuntos de datos.

**ID de clave de acceso**: un ID de clave de acceso es un identificador único asociado a un [!DNL Amazon] Clave de acceso secreta S3. El ID de clave de acceso y la clave de acceso secreta se utilizan juntos para firmar [!DNL Amazon Web Services] Solicitudes de (AWS).

**Acción**: en el contexto de las etiquetas, una acción es un tipo específico de componente de regla que define lo que debe suceder después de que se produzca un evento y de que se evalúen y aprueben las condiciones.

**Activar**: Activar es la acción realizada por un usuario para asignar un segmento o perfiles a un destino como [!DNL Oracle Eloqua], [!DNL Google], o [!DNL Salesforce Marketing Cloud].

**Actividad**: en [!DNL Offer Decisioning], una actividad de contiene la lógica que indica la selección de una oferta.

**Administrador**: una o más personas de su organización que pueden configurar y personalizar permisos de Experience Platform en Adobe Admin Console.

**Adobe Admin Console**: Adobe Admin Console proporciona una ubicación central para administrar los derechos de productos de Adobe y el acceso para su organización. A través de la consola, los administradores pueden conceder a grupos de usuarios permisos de acceso para varias funciones de Platform, como &quot;Administrar conjuntos de datos&quot;, &quot;Ver conjuntos de datos&quot; o &quot;Administrar perfiles&quot;.

**Adobe Experience Platform**: Adobe Experience Platform estandariza los datos y el contenido en toda la empresa, lo que potencia los perfiles de los consumidores en tiempo real, permite la ciencia de datos y acelera la velocidad de contenido para impulsar la personalización de la experiencia en todo el recorrido del cliente.

**Adobe Experience Platform Query Service**: permite a los analistas de datos consultar eventos y perfiles para utilizarlos en análisis y aprendizaje automático. Con Query Service, los analistas y científicos de datos pueden extraer todos sus conjuntos de datos almacenados en Experience Platform (incluidos los datos de comportamiento, así como los puntos de venta, la administración de la relación con los clientes, etc.) y consultar dichos conjuntos de datos para responder a preguntas específicas acerca de los datos.

**Servicio de segmentación de Adobe Experience Platform**: permite crear segmentos y audiencias a partir de los datos del perfil del cliente en tiempo real. Estas audiencias se pueden exportar a sus propios conjuntos de datos dentro del lago de datos.

**Adobe Servicios inteligentes**: los servicios inteligentes como Attribution AI y la inteligencia artificial aplicada al cliente son modelos de aprendizaje automático basados en inteligencia artificial creados específicamente y que requieren que el Experience Platform los ejecute y los utilice.

**Adobe I/O**: Adobe I/O forma parte de Experience Platform y proporciona acceso a todo lo que los desarrolladores necesitan para integrar, ampliar y personalizar Platform, incluidas las API, los eventos, la consola de desarrollador y las herramientas útiles.

**Adobe Sensei**: Adobe Sensei es la plataforma de inteligencia que alimenta al Experience Platform. También proporciona un conjunto de servicios de IA que permite a las marcas mejorar su capacidad para ofrecer experiencias del cliente personalizadas en tiempo real.

**Amazon S3 bucket**: [!DNL Amazon S3] contenedores son los contenedores fundamentales para los datos almacenados en [!DNL Amazon] ecosistema. Los contenedores contienen objetos, cada objeto se almacena y recupera mediante una clave única asignada al desarrollador.

**Conector de Amazon S3**: La [!DNL Amazon] El conector S3 permite a los clientes de Experience Platform conectarse y acceder de forma segura a sus [!DNL Amazon] Datos de S3.

**APA**: La [[!DNL Australia Privacy Act (Privacy Act)]](https://www.oaic.gov.au/privacy/the-privacy-act) promueve y protege la privacidad de las personas y regula cómo las agencias y organizaciones gubernamentales australianas manejan la información personal. El [!DNL Privacy Act] incluye principios que se aplican a las organizaciones del sector privado. Por ejemplo, se otorga a las personas el derecho a comprender por qué se recopila la información personal y cómo se utilizará, la capacidad de acceder, borrar sus datos y corregir la información personal.

**Anexar estrategia de guardado**: la estrategia de guardado &quot;anexar&quot; es una opción utilizada al especificar datos de terceros para su ingesta mediante una conexión y anexar cualquier dato o fila nuevos al final del conjunto de datos. Las filas introducidas anteriormente permanecen inalteradas y solo las filas creadas desde la última ejecución programada se incorporan a Experience Platform. Las filas modificadas en el sistema de origen permanecen inalteradas en el Experience Platform.

**Matriz**: las matrices se utilizan para elementos ordenados con el mismo tipo de datos.

**Inteligencia artificial**: la inteligencia artificial es una teoría y un desarrollo de sistemas informáticos capaces de realizar tareas que normalmente requieren inteligencia humana, como la percepción visual, el reconocimiento de voz, la toma de decisiones y la traducción entre idiomas.

**Atributos**: los atributos son características especificadas que representan un perfil.

**Combinación de atributos**: Al definir una política de combinación mediante la API de Perfil del cliente en tiempo real, la variable `attributeMerge` indica la forma en que la política de combinación priorizará los atributos de perfil en caso de conflictos de datos. Equivale a seleccionar una [!UICONTROL Método de combinación] al definir una política de combinación en la IU de Platform.

**Attribution AI**: [!DNL Attribution AI] es un servicio inteligente con tecnología de Adobe Sensei que ofrece funciones de atribución multicanal algorítmicas en todo el ciclo de vida del cliente.

**Audiencia**: una audiencia es el conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

**Tamaño de audiencia**: Un tamaño de audiencia es el número total de perfiles que cumplen los criterios de una definición de segmento y cumplen los requisitos para ser miembros de la audiencia.

**Instantánea de audiencia**: una instantánea de audiencia captura todos los perfiles aptos para los criterios del segmento en el momento de la segmentación.

## B

**Relleno**: Para los orígenes programados, la opción de relleno permite la ingesta de datos históricos.

**Período de relleno**: el periodo de relleno es una opción para establecer el periodo de tiempo para la ingesta de datos históricos de terceros a través de una conexión de origen. Si se selecciona un período de relleno de &quot;para siempre&quot;, se ingestará todo el historial de los datos de origen en Experience Platform.

**Lote**: un lote es un conjunto de datos recopilados durante un período de tiempo y procesados juntos como una sola unidad. Los conjuntos de datos están compuestos por varios lotes.

**ID de lote**: un ID de lote es un identificador generado por el Adobe para un lote de datos.

**Ingesta por lotes**: la introducción por lotes le permite introducir datos en Experience Platform como archivos por lotes. Los lotes son unidades de datos compuestas por uno o más archivos que se van a introducir como una sola unidad.

**Segmentación por lotes**: la segmentación por lotes es una alternativa a un proceso de selección de datos en curso y mueve todos los datos de perfil a la vez a través de definiciones de segmentos para producir audiencias correspondientes. Una vez creado, este segmento se guarda y almacena para que se pueda exportar para su uso.

**Generar**: En el contexto de las etiquetas, una compilación es un archivo o conjunto de archivos que contienen todas las configuraciones y el código necesarios para ejecutar la lógica empresarial contenida dentro de una biblioteca, lo que le permite implementar esa biblioteca en el sitio web o la aplicación móvil.

**Herramientas de inteligencia empresarial**: Las herramientas de inteligencia empresarial (BI) están integradas principalmente con [!DNL Experience Platform Query Service]. Las herramientas de BI son tipos de software de aplicación que recopilan y procesan grandes cantidades de datos no estructurados de sistemas internos y externos.

## C

**Límite**: en [!DNL Offer Decisioning], el límite (también conocido como límite de frecuencia) se utiliza en las reglas de toma de decisiones para definir cuántas veces se presenta una oferta. Existen dos tipos de límite: la cantidad de veces que se puede proponer una oferta en la audiencia de destinatario combinada (denominada &quot;Límite global&quot;) y la cantidad de veces que se puede proponer una oferta al mismo usuario final (denominada &quot;Límite de perfil&quot;).

**Catálogo**: En el contexto de las fuentes y los destinos, un catálogo es una galería con conexiones disponibles a aplicaciones de Adobe y tecnologías de terceros. No debe confundirse con [!DNL Catalog Service].

**[!DNL Catalog Service]**: [!DNL Catalog Service] (a veces se llama [!DNL Catalog]) es el sistema de registro para la ubicación y el linaje de datos dentro de Adobe Experience Platform. Mientras que todos los datos que se incorporan a Experience Platform se almacenan en el lago de datos como archivos y directorios, [!DNL Catalog] contiene los metadatos y la descripción de esos archivos y directorios para fines de búsqueda, supervisión y control de datos.

**CCPA**: La [[!DNL California Consumer Privacy Act (CCPA)]](https://oag.ca.gov/privacy/ccpa) mejora los derechos de privacidad y la protección del consumidor para los residentes de California, Estados Unidos. La CCPA otorga nuevos derechos de privacidad de datos a los residentes de California, como el derecho a acceder a sus datos personales y eliminarlos, a saber si sus datos personales se venden o revelan (y a quién) y el derecho a optar por que sus datos no se vendan a terceros.

**Clase**: en el modelo de datos de experiencia (XDM), una clase define el conjunto más pequeño de campos utilizados para crear un esquema y define el comportamiento base del objeto comercial que representa el esquema.

**Cliente**: un cliente es una herramienta o aplicación externa que se conecta a [!DNL Query Service] mediante [!DNL PostgreSQL] protocolo o API HTTP.

**Colección**: en [!DNL Offer Decisioning], las colecciones son subconjuntos de ofertas basados en condiciones predefinidas definidas definidas por un experto en marketing, como la categoría de la oferta.

**Combinar con acción de marketing PII**: una acción de marketing que combina cualquier información de identificación personal (PII) con datos anónimos. Los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de dichos datos con datos directamente identificables.

**Interfaz de línea de comandos**: una interfaz de línea de comandos es una herramienta basada en texto que se puede utilizar para conectarse a [!DNL Query Service] para la ejecución de consultas sin procesar.

**Composición**: una composición es una agrupación de componentes que se forman juntos para formar el esquema.

**Condición**: en el contexto de las etiquetas, una condición es un componente de regla que evalúa una sentencia lógica que debe devolver `true` o `false`. Todas las condiciones deben evaluarse como `true` y todas las condiciones de excepción deben evaluarse como `false` antes de ejecutar cualquier acción en la regla.

**Consola**: en [!DNL Query Service], la consola proporciona información sobre el estado y el funcionamiento de una consulta. La consola muestra el estado de la conexión a [!DNL Query Service], las operaciones de consulta que se están ejecutando y los mensajes de error resultantes de esas consultas.

**Etiquetas de contrato (&quot;C&quot;)**: Las etiquetas de uso de datos del contrato (&quot;C&quot;) se utilizan para categorizar los datos que tienen obligaciones contractuales o están relacionados con las políticas de gobernanza de datos de su organización.

**CPRA**: La [[!DNL California Consumer Privacy Rights Act (CPRA)]](https://cppa.ca.gov/regulations/consumer_privacy_act.html) amplía y corrige partes del [!DNL California Consumer Privacy Act (CCPA)]. El [!DNL CPRA] establece una nueva línea de base para la privacidad de datos de consumo en California al aumentar los derechos de los consumidores y ampliar el tipo de datos cubiertos a través de una definición más amplia de información personal confidencial. Además, la variable [!DNL CPRA] estableció la Agencia de Protección de Privacidad de California, una nueva agencia dedicada a implementar y hacer cumplir las reglas de privacidad de datos.

**Etiqueta de contrato C1**: A `C1` la etiqueta de uso de datos del contrato especifica que los datos solo se pueden exportar desde Adobe Experience Cloud de forma acumulada sin incluir identificadores individuales o de dispositivo. Por ejemplo, los datos que se originaron en las redes sociales.

**Etiqueta de contrato C2**: A `C2` la etiqueta de uso de datos del contrato especifica datos que no se pueden exportar a terceros. Algunos proveedores de datos tienen condiciones en sus contratos que prohíben la exportación de datos desde el lugar donde se recopilaron originalmente. Por ejemplo, los contratos de redes sociales suelen restringir la transferencia de datos que se reciben de ellas. C2 es más restrictivo que C1, que solo requiere agregación y datos anónimos.

**Etiqueta de contrato C3**: A `C3` la etiqueta de uso de datos del contrato especifica datos que no se pueden combinar o utilizar de otro modo con información directamente identificable. Algunos proveedores de datos tienen términos en sus contratos que prohíben la combinación o el uso de esos datos con información directamente identificable. Por ejemplo, los contratos para datos procedentes de redes de publicidad, servidores de publicidad y proveedores de datos de terceros suelen incluir prohibiciones contractuales específicas sobre el uso de datos directamente identificables.

**Etiqueta de contrato C4**: A `C4` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para segmentar anuncios o contenido, ya sea en el sitio o entre sitios. C4 es la etiqueta más restrictiva, ya que incluye las etiquetas C5, C6 y C7.

**Etiqueta de contrato C5**: A `C5` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para la segmentación entre sitios de contenido o anuncios basados en intereses. La segmentación basada en intereses, o personalización, se produce si se cumplen las tres condiciones siguientes: Los datos recopilados en el sitio se utilizan para hacer deducciones sobre el interés de un usuario; se utilizan en otro contexto como en otro sitio o aplicación; y se utilizan para seleccionar qué contenido o anuncios se muestran en función de esas deducciones.

**Etiqueta de contrato C6**: A `C6` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para la segmentación de anuncios en el sitio. La segmentación de anuncios en el sitio incluye la selección y el envío de anuncios en los sitios web o las aplicaciones de la organización, o para medir el envío y la eficacia de dichos anuncios. Esto incluye el uso de datos en el sitio recopilados anteriormente sobre el interés de los usuarios por seleccionar anuncios, procesar datos sobre qué anuncios se mostraron, cuándo y dónde se mostraron y si los usuarios realizaron alguna acción relacionada con el anuncio, como seleccionar un anuncio o realizar una compra.

**Etiqueta de contrato C7**: A `C7` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para la segmentación de contenido en el sitio. La segmentación de contenido en el sitio incluye la selección y entrega de contenido en los sitios web o las aplicaciones de la organización, o para medir la entrega y la eficacia de dicho contenido. Esto incluye información recopilada anteriormente sobre el interés de los usuarios por seleccionar contenido, el procesamiento de datos sobre qué contenido se mostró, con qué frecuencia o durante cuánto tiempo, cuándo y dónde se mostró y si los usuarios realizaron alguna acción relacionada con el contenido, incluida la selección de contenido, por ejemplo.

**Etiqueta de contrato C8**: A `C8` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para medir los sitios web o las aplicaciones de la organización. Esto no incluye la segmentación basada en intereses, que es la recopilación de información sobre el uso que usted hace de este servicio para posteriormente personalizar contenido y/o publicidad en otros contextos.

**Etiqueta de contrato C9**: A `C9` la etiqueta de uso de datos del contrato especifica que los datos no se pueden utilizar en flujos de trabajo de ciencia de datos. Algunos contratos incluyen prohibiciones explícitas sobre los datos utilizados para la ciencia de datos. A veces se formulan en términos que prohíben el uso de datos para inteligencia artificial (IA), aprendizaje automático (ML) o modelado.

**Etiqueta de contrato C10**: A `C10` la etiqueta de uso de datos del contrato especifica que los datos no se pueden usar para la activación de identidad vinculada. Algunas políticas de uso de datos restringen el uso de datos de identidad vinculados para la personalización. El `C10` La etiqueta de se aplica automáticamente a los segmentos si sus políticas de combinación utilizan la opción &quot;gráfico privado&quot;.

**Columna Fecha de creación**: La selección de una columna Fecha de creación es una opción al especificar datos de terceros a través de una conexión de origen. Cuando se selecciona la estrategia de guardado de datos anexados y el esquema del conjunto de datos contiene varios campos de fecha, debe elegir entre el esquema disponible para especificar una columna de clave Fecha de creación. La opción Fecha de creación no está disponible cuando se selecciona la estrategia de sobrescritura y guardado.

**Crear tabla como selección**: Crear tabla como selección (CTAS) es un comando SQL que, cuando se ejecuta como parte de una consulta SQL completa y válida, ordena [!DNL Query Service] para mantener los resultados de la consulta en un conjunto de datos. Puede crear un nuevo conjunto de resultados, sobrescribir resultados anteriores o anexar a resultados anteriores.

**Datos entre sitios**: los datos entre sitios son la combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas.

**Acción de marketing de segmentación entre sitios**: una acción de marketing que utiliza datos para la segmentación de anuncios entre sitios. La combinación de datos de varios sitios, incluida una combinación de datos in situ y datos externos o una combinación de datos de varias fuentes externas, se denomina datos entre sitios. Los datos entre sitios generalmente se recopilan y procesan para hacer deducciones sobre los intereses de los clientes.

**Área de nombres de identidad personalizada**: su organización puede crear áreas de nombres de identidad personalizadas para representar identidades de una organización o caso empresarial específico.

**Etiquetas personalizadas**: las etiquetas de uso de datos personalizadas le permiten crear y aplicar etiquetas específicas a campos de datos que satisfacen necesidades comerciales específicas.

**Inteligencia artificial aplicada al cliente**: la inteligencia artificial aplicada al cliente es un servicio inteligente impulsado por Adobe Sensei que enriquece los perfiles de los clientes con las tendencias basadas en IA y potencia la segmentación de clientes y los esfuerzos de segmentación.

## D

**Diario**: en el contexto de las exportaciones de archivos programadas, programa las exportaciones de archivos completas o incrementales una vez al día, todos los días, desde la fecha de inicio hasta la fecha de finalización a la hora especificada por el usuario.

**Diccionario de datos**: en el contexto de las etiquetas, un diccionario de datos (también conocido como mapa de datos) es un conjunto de elementos de datos definidos dentro de una propiedad.

**Elemento de datos**: en el contexto de las etiquetas, un elemento de datos es un puntero utilizado dentro de reglas y extensiones para señalar a un fragmento de datos específico que existe en el dispositivo cliente.

**Ingesta de datos**: la ingesta de datos es el proceso de añadir datos de un origen a un Experience Platform. Los datos se pueden ingerir en Platform de varias formas, incluido el streaming, los lotes o la adición a través de conectores de origen.

**Capa de datos**: en el contexto de las etiquetas, una capa de datos es una estructura de datos que existe en el dispositivo cliente y que contiene metadatos sobre el contexto en el que se visualiza una página o pantalla.

**Gobernanza de datos**: la gobernanza de datos abarca las estrategias y tecnologías utilizadas para garantizar que los datos cumplan con las regulaciones y las políticas organizativas con respecto al uso de datos.

**Socios de integración de datos**: los socios de integración de datos simplifican y automatizan la carga y transformación de volúmenes masivos de datos de más de 200 fuentes a Experience Platform sin necesidad de escribir código.

**Etiquetas de conjuntos de datos**: Se pueden añadir etiquetas de uso de datos a los conjuntos de datos. Todos los campos de ese conjunto de datos heredarán las etiquetas del conjunto de datos.

**Data Science Workspace**: [!DNL Data Science Workspace] Experience Platform permite a los clientes crear modelos de aprendizaje automático utilizando datos en aplicaciones de Platform y de Adobe para crear segmentos inteligentes, generar perspectivas y proporcionar predicciones, lo que le permite mejorar en gran medida las experiencias digitales del usuario final.

**Fuente de datos**: una fuente de datos es un origen de datos designado por el usuario. Algunos ejemplos de fuente de datos son una aplicación móvil, eventos de perfil o experiencia, eventos de perfil de sitio web o un CRM.

**Administrador de datos**: un administrador de datos es la persona responsable de la administración, la supervisión y la aplicación de los recursos de datos de una organización. Un administrador de datos también garantiza que las políticas de gobernanza de datos se salvaguarden y mantengan para cumplir con las regulaciones gubernamentales y las políticas organizativas.

**Flujo de datos**: un flujo de datos es un conjunto o una colección de mensajes que comparten el mismo esquema y que se envían desde la misma fuente.

**Tipo de datos**: un tipo de datos es un recurso XDM reutilizable que define un campo de tipo de objeto que contiene varias propiedades en una representación jerárquica.

**Etiquetas de uso de datos**: las etiquetas de uso de datos le permiten categorizar los datos que reflejan consideraciones relacionadas con la privacidad y condiciones contractuales para cumplir con las regulaciones y políticas corporativas. Las etiquetas de uso de datos agregadas a un conjunto de datos se heredan o se aplican a todos los campos dentro de ese conjunto de datos. Las etiquetas de uso de datos también se pueden aplicar directamente a los campos.

**Flujo de datos**: un flujo de datos es una canalización virtual de datos que fluye a Platform desde un origen a otros destinos.

**Ejecución de flujo de datos**: una ejecución de flujo de datos es un flujo de datos que aterriza en Experience Platform en función de una programación especificada por el usuario.

**Conjunto de datos**: un conjunto de datos es una construcción de almacenamiento y administración para una colección de datos, normalmente una tabla, que contiene un esquema (columnas) y campos (filas).

**ID de conjunto de datos**: Identificador generado por el Adobe para un conjunto de datos ingerido.

**Salida de conjunto de datos**: la salida del conjunto de datos proporciona un mecanismo para determinar qué opción &quot;Crear tabla como selección&quot; se utilizará para una tabla en particular [!DNL Query Service] correr.

**Clave de deduplicación**: clave principal definida por el usuario que determina la identidad con la que los usuarios desean que se dedupliquen sus perfiles&#x200B;

**Columna Delta**: una columna delta permite seleccionar un campo de datos de origen para representar una marca de tiempo para la ingesta incremental.

**Estrategia de guardado delta**: la estrategia de guardado delta es una opción para la ingesta de datos de terceros a través de una conexión de origen. La opción permite al usuario especificar que se incorporen filas nuevas o modificadas de datos de origen al Experience Platform. Las filas nuevas se agregan al final del conjunto de datos y las filas cambiadas se actualizan en el conjunto de datos en el Experience Platform.

**Descriptor**: en el Modelo de datos de experiencia (XDM), un descriptor es un conjunto adicional de metadatos relacionados con esquemas que describe un comportamiento específico para un campo. El Experience Platform puede utilizar los descriptores para comprender el comportamiento de esquema deseado, como la relación entre dos esquemas.

**Destino**: un destino es un término general para cualquier punto de conexión, como una aplicación de Adobe, una plataforma de publicidad, un servicio de almacenamiento en la nube o un servicio de marketing, en el que se activa y se entrega una audiencia.

**Categoría de destino**: una categoría de destino es una agrupación de destinos que tienen características similares.

**Catálogo de destino**: un catálogo de destino es una lista de destinos disponibles en Experience Platform.

**Reglas de llamada directa**: en el contexto de las etiquetas, una regla de llamada directa es una regla que se ejecuta cuando se la llama directamente desde la página, omitiendo la detección de eventos y los sistemas de búsqueda.

**Nombre para mostrar**: en el modelo de datos de experiencia (XDM), un nombre para mostrar es un nombre fácil de usar para un campo que se muestra en la interfaz de usuario.

## E

**Oferta elegible**: una oferta elegible se puede ofrecer de forma coherente a un perfil, ya que cumple con las restricciones definidas por adelantado.

**Reglas de elegibilidad**: en [!DNL Offer Decisioning]Sin embargo, las reglas de elegibilidad se aplican a un perfil relacionado con las restricciones de calendario, programación y límite.

**Acción de marketing de direccionamiento de correo electrónico**: una acción de marketing que utiliza datos en campañas de direccionamiento de correo electrónico.

**Código incrustado**: en el contexto de las etiquetas, el código incrustado es una etiqueta de script colocada dentro del HTML en un sitio o entorno. El código incrustado indica al explorador dónde recuperar la compilación.

**Enumeración**: una enumeración (enum) es un campo XDM restringido a un conjunto de valores predefinidos.

**Entorno**: en el contexto de las etiquetas, un entorno es un conjunto de instrucciones de implementación que especifica el envío del host y el formato de archivo de una compilación. Una biblioteca debe estar emparejada con un entorno para poder crearla.

**Diagnósticos de error**: Los diagnósticos de error permiten la generación de mensajes de error detallados para los lotes ingeridos. El umbral de error permite configurar el porcentaje de errores aceptables antes de que falle un lote.

**Evento**: en el contexto de las etiquetas, un evento es un tipo específico de componente de regla, que es un déclencheur que se produce en un dispositivo cliente para comenzar la ejecución de una regla.

**Entidades de evento**: en el contexto del modelado de datos, las entidades de evento representan conceptos relacionados con las acciones que un cliente puede realizar, los eventos del sistema o cualquier otro concepto en el que puede que desee rastrear los cambios a lo largo del tiempo. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la variable [!DNL XDM ExperienceEvent] clase.

**Eventos**: los eventos son los datos de comportamiento asociados a un perfil.

**Modelo de datos de experiencia (XDM)** [!DNL Experience Data Model] (XDM) es un marco de trabajo de código abierto que utiliza esquemas estándar para unificar datos para utilizarlos con aplicaciones de Experience Platform y Adobe Experience Cloud. XDM estandariza cómo se estructuran los datos, acelera y simplifica el proceso de obtener perspectivas a partir de cantidades masivas de datos.

**Experimento**: un experimento es el proceso de creación de un modelo entrenado mediante la formación de la instancia con una porción de muestra de datos de producción en directo. Esto es diferente a un modelo entrenado que se prueba con un conjunto de datos de prueba de exclusión. Esto también es diferente del concepto de un experimento en algunos marcos de aprendizaje automático en los que en realidad significa un proyecto de modelado de muestra.

**Evento de experiencia**: un evento de experiencia representa una instantánea del sistema cuando se produce una interacción o evento relacionado con una experiencia del cliente. Los eventos de experiencia son registros de hechos inmutables de lo que ha ocurrido y representan lo que ha sucedido sin agregación ni interpretación. En el Modelo de datos de experiencia (XDM), este concepto se captura mediante [!DNL XDM ExperienceEvent] clase.

**Exportar archivo completo**: Un archivo de exportación que contiene una instantánea completa de todas las cualificaciones de perfil del segmento seleccionado.

**Exportar archivos incrementales**: serie de archivos exportados en los que el primer archivo es una instantánea completa de todas las cualificaciones de perfil del segmento seleccionado y los archivos siguientes son cualificaciones de perfil incrementales desde la exportación anterior.

**Extensión**: en el contexto de las etiquetas, una extensión es un paquete de funcionalidades añadido a una propiedad de etiqueta. Una extensión suele centrarse en una solución de análisis o marketing determinada y proporciona las herramientas necesarias para implementar esa tecnología en un entorno de cliente.

**Paquete de extensión**: En el contexto de las etiquetas, un paquete de extensiones es un archivo ZIP creado y cargado por un desarrollador de extensiones que proporciona todo lo necesario para que los usuarios de etiquetas instalen la extensión dentro de su propiedad. Un paquete de extensión contiene un manifiesto que especifica información sobre la extensión, el HTML/JavaScript necesario para que los usuarios finales configuren el funcionamiento de la extensión de etiqueta y el JavaScript ejecutable entregado al entorno del cliente (si es necesario).

## F

**Ofertas de reserva**: Una oferta de reserva es la oferta predeterminada que se muestra cuando un usuario final no cumple los requisitos para ninguna de las ofertas de la colección utilizada.

**Asignación de funciones**: la asignación de funciones hace referencia al proceso de asignación de funciones de datos a funciones de entrada y destino que requiere un modelo de aprendizaje automático.

**Campo**: un campo es el elemento de nivel inferior de un conjunto de datos, tal como se define en el esquema XDM del conjunto de datos. Cada campo tiene un nombre para fines de referencia y un tipo para indicar el tipo de datos que contiene. Los tipos de campo pueden incluir (entre otros) números enteros, números, cadenas, booleanos y objetos.

**Grupo de campos**: Consulte &quot;Grupo de campos de esquema&quot;.

**Etiquetas de campo**: las etiquetas de campo son etiquetas de control de datos que se heredan de un conjunto de datos o se aplican directamente a un campo.

**Nombre de campo**: Se utiliza un nombre de campo para hacer referencia al valor de un campo en las consultas y los servicios descendentes.

**Frecuencia**: en [!DNL Query Service], la frecuencia determina con qué frecuencia se ejecutará una consulta programada recurrente.

## G

**Geoperímetro**: una geovalla es un límite geográfico virtual, definido por la tecnología GPS o RFID, que permite al software almacenar en déclencheur una respuesta cuando un dispositivo móvil entra o sale de una zona en particular.

**RGPD (Reglamento General de Protección de Datos)**: el Reglamento General de Protección de Datos (RGPD) es un marco jurídico que establece directrices para la recopilación y el procesamiento de información personal de personas dentro de la Unión Europea (UE). El RGPD establece los principios para la gestión de datos y los derechos de las personas y abarca a todas las empresas que se ocupan de los datos de los ciudadanos de la UE.

**Protecciones**: las protecciones son umbrales que proporcionan directrices para el uso de datos y del sistema, la optimización del rendimiento y la prevención de errores o resultados inesperados en Adobe Experience Platform. Las protecciones pueden hacer referencia al uso o consumo de datos y al procesamiento en relación con los derechos de licencia.

## H

**HIPAA**: La [[!DNL Health Insurance Portability and Accountability Act (HIPAA)]](https://www.hhs.gov/hipaa/index.html) es una ley federal de Estados Unidos creada para mejorar la eficiencia de la atención médica, mejorar la portabilidad del seguro de salud y proteger la privacidad de los pacientes y los miembros del plan de salud. En virtud de la ley HIPAA, las personas tienen derecho a acceder a su información y modificarla, así como a obtener copias de sus registros médicos o de la información sobre su salud. Las entidades cubiertas y los socios comerciales de las entidades cubiertas deben seguir las regulaciones de la HIPAA.

**Host**: en el contexto de las etiquetas, un host especifica la ubicación, el dominio y las credenciales de usuario necesarios para que el sistema envíe una compilación.

**Por hora**: En el contexto de las exportaciones de archivos programadas, programa las exportaciones de archivos incrementales cada 3, 6, 8 o 12 horas.

## I

**Identidad**: una identidad es un identificador que representa de forma exclusiva a un cliente individual, como un ID de cookie, un ID de dispositivo o un ID de correo electrónico.

**Campos de identidad**: los campos de identidad son campos XDM que se utilizan para unir información sobre clientes individuales procedentes de varias fuentes de datos. Se debe definir una sola identidad principal para que el esquema se habilite para su uso en el perfil del cliente en tiempo real.

**Etiquetas de identidad (&quot;I&quot;)**: las etiquetas de uso de datos de identidad (&quot;I&quot;) se utilizan para categorizar los datos que pueden identificar o ponerse en contacto con una persona específica.

**Gráfico de identidad**: un gráfico de identidad es un mapa de relaciones entre identidades vinculadas que existen para un cliente individual. Cada gráfico de identidad se actualiza en tiempo casi real con la actividad del cliente. La estructura común de las relaciones de identidad en sus datos se representa mediante la variable [!UICONTROL Gráfico privado], que sirve como modelo estructural para cada gráfico de identidad individual.

**Área de nombres de identidad**: un área de nombres de identidad define el contexto de un identificador, como una dirección de correo electrónico o un ID de CRM.

**Servicio de identidad**: [!DNL Experience Platform Identity Service] permite la creación y administración de tipos de identidad, lo que permite vincular identidades de clientes entre dispositivos y canales. La capacidad del servicio para vincular identidades permite que el Perfil del cliente en tiempo real proporcione una representación completa de cada cliente individual.

**Vinculación de identidad**: la vinculación de identidad es el proceso de identificar fragmentos de datos y unirlos para formar un registro de perfil completo.

**Símbolo de identidad**: un símbolo de identidad es una abreviatura de un área de nombres de identidad que se puede utilizar como referencia en las API.

**Valor de identidad**: un valor de identidad, combinado con un área de nombres de identidad, es un identificador que representa a un individuo, organización o recurso único. Al hacer coincidir los datos de los registros en los fragmentos del perfil, el área de nombres y el valor de identidad deben coincidir.

**Etiqueta de uso de datos I1**: La `I1` la etiqueta de uso de datos se utiliza para clasificar los datos que pueden identificar o contactar directamente a una persona específica en lugar de un dispositivo.

**Etiqueta de uso de datos I2**: La `I2` la etiqueta de uso de datos se utiliza para clasificar los datos que se pueden utilizar en combinación con otros datos para identificar o ponerse en contacto indirectamente con una persona específica.

**Organización IMS**: una organización de IMS (a veces denominada como organización de IMS) es el nombre que se utiliza para identificar una empresa o un grupo específico dentro de una empresa a través de productos de Adobe. Los administradores pueden configurar y administrar el acceso y los permisos de las funciones a los usuarios de una organización.

**Ingesta**: Consulte ingesta de datos.

**Programación de ingesta**: una programación de ingesta proporciona opciones basadas en el tiempo al ingerir desde un origen a un Experience Platform.

**Función de entrada**: una función de entrada se especifica en la asignación de funciones y la utiliza un modelo de aprendizaje automático para realizar predicciones.

**[!DNL Intelligent Services]**: [!DNL Intelligent Services] como [!DNL Attribution AI] y [!DNL Customer AI] son modelos de aprendizaje automático basados en inteligencia artificial que requieren Experience Platform (o aplicaciones creadas sobre Platform, como Adobe Real-time Customer Data Platform) para ejecutarse y funcionar.

**Personalización o segmentación basada en intereses**: La segmentación basada en intereses, también conocida como personalización, se produce si se cumplen las tres condiciones siguientes:

1. Los datos recopilados en el sitio se utilizan para hacer deducciones sobre los intereses de un usuario.
1. Los datos se utilizan en otro contexto, como en otro sitio o aplicación (fuera del sitio).
1. Los datos se utilizan para seleccionar qué contenido o anuncios se muestran en función de esas deducciones.

## J

**[!DNL JupyterLab]**: Una interfaz de código abierto basada en web para Project [!DNL Jupyter] que está integrado en la interfaz de usuario de Platform.

**[!DNL Jupyter Notebook]**: integrado con JupyterLab, Jupyter Notebooks le permite realizar tareas de limpieza y transformación de datos, simulación numérica, modelado estadístico, visualización de datos, aprendizaje automático y mucho más sobre los datos de su Experience Platform en una variedad de idiomas como Python, Scala y PySpark.

## K

## L

**LGPD**: La [[!DNL Lei Geral de Proteção de Dados (LGPD)]](https://gdpr.eu/gdpr-vs-lgpd/) tiene por objeto regular el tratamiento de los datos personales de todas las personas físicas o físicas en Brasil. La LGPD otorga a los ciudadanos de Brasil el derecho de acceder y eliminar sus datos personales, de saber si sus datos personales se venden o revelan (y a quién) y el derecho de optar por que sus datos sean vendidos a terceros.

**Biblioteca**: en el contexto de las etiquetas, una biblioteca es un conjunto de lógica empresarial que contiene instrucciones sobre cómo se debe comportar la biblioteca de etiquetas en el dispositivo cliente.

**Entidades de búsqueda**: en el contexto del modelado de datos, las entidades de búsqueda representan conceptos que pueden relacionarse con una persona individual, pero no se pueden utilizar directamente para identificar a la persona. Las entidades incluidas en esta categoría deben representarse mediante esquemas basados en clases personalizadas del Modelo de datos de experiencia (XDM) y vincularse a una entidad de perfil mediante un [relación de esquema](../xdm/tutorials/relationship-ui.md).

## M

**Aprendizaje automático (ML)**: el aprendizaje automático es el campo de estudio que permite a los ordenadores aprender sin estar explícitamente programados.

**Modelo de aprendizaje automático**: un modelo de aprendizaje automático es una instancia de una fórmula de aprendizaje automático que se entrena con datos históricos y configuraciones para resolver un caso de uso empresarial. En Adobe Experience Platform Data Science Workspace, los modelos de aprendizaje automático se denominan fórmulas.

**Atributo obligatorio**: Casilla de verificación activada por el usuario que garantiza que todos los registros de perfil contengan el atributo seleccionado. Por ejemplo: todos los perfiles exportados contienen una dirección de correo electrónico.

**Asignación**: la asignación de datos es el proceso de asignación de campos de datos de origen a campos de destino relacionados en un destino.

**Acción de marketing**: en el marco de trabajo de gobernanza de datos, una acción de marketing (también conocida como caso de uso de marketing) es una acción que realiza un consumidor de datos Experience Platform, para la cual es necesario comprobar si se han infringido las políticas de uso de datos.

**Método de combinación**: Al definir una política de combinación mediante la interfaz de usuario de Platform, el método de combinación especifica cómo se debe priorizar los fragmentos de datos cuando se produce un conflicto. Al utilizar la API de Perfil del cliente en tiempo real para definir una política de combinación, el método de combinación se determina mediante la variable `attributeMerge` objeto.

**Política de combinación**: Las políticas de combinación son reglas que utiliza Experience Platform para determinar cómo se combinarán los fragmentos de datos de clientes de varias fuentes para crear un perfil individual. Cuando se produce un conflicto de datos, la política de combinación determina qué datos deben tener prioridad para su inclusión en el perfil.

**MHMDAa**: La [[!DNL Washington My Health My Data Act]](https://app.leg.wa.gov/RCW/default.aspx?cite=19.373&amp;full=true) mejora los derechos de privacidad de los consumidores con respecto a sus datos de salud. Exige revelaciones, consentimiento del consumidor y derechos de eliminación para los datos de salud, y prohíbe la venta de datos de salud sin autorización. Además, la ley hace ilegal el uso de geoperimetraje alrededor de las instalaciones de salud.

**Mixin**: Consulte &quot;Grupo de campos de esquema&quot;.

**Módulo**: en el contexto de las etiquetas, un módulo es un fragmento de JavaScript ejecutable proporcionado por una extensión, que realiza acciones en un entorno de cliente sin necesidad de crear una regla.

## N

**[!DNL New Zealand Privacy Act]**: La [[!DNL New Zealand Privacy Act]](https://www.privacy.org.nz/privacy-act-2020/privacy-principles/) controla cómo las agencias pueden recopilar, utilizar, revelar, almacenar y dar acceso a la información personal de los ciudadanos y organizaciones de Nueva Zelanda. En 2020, la última versión de la ley introdujo actualizaciones significativas a estas leyes de privacidad, incluidos nuevos delitos, el aumento de las multas, las notificaciones obligatorias por violaciones de datos y el aumento de los poderes del Comisionado de Privacidad.

**Zona protegida de no producción**: Las zonas protegidas que no son de producción se utilizan normalmente para experimentos, pruebas o ensayos de desarrollo. A diferencia de las zonas protegidas de producción, las que no son de producción se pueden restablecer y eliminar.

**[!DNL Notebooks]**: [!DNL Notebooks] se crean mediante [!DNL Jupyter Notebook] y se pueden ejecutar para realizar análisis de datos.

## O

**Oferta**: una oferta es un mensaje de marketing que contiene una propuesta comercial o de ventas a un cliente (potencial). Las ofertas suelen tener reglas específicas que determinan quién puede verlas o recibirlas.

**[!DNL Offer Decisioning]**: [!DNL Offer Decisioning] permite a los especialistas en marketing administrar reglas y modelos formados de propuestas de ofertas al interactuar con usuarios finales en función de los datos recopilados en canales y aplicaciones.

**Biblioteca de ofertas**: la biblioteca de ofertas es una biblioteca central que se utiliza para administrar ofertas de reserva y personalizadas, reglas de decisión y actividades.

**Acción de marketing de personalización en el sitio**: una acción de marketing que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer deducciones sobre los intereses de los usuarios, y se utiliza para seleccionar qué contenido o anuncios se muestran en función de esas deducciones.

**Acción de marketing de segmentación en el sitio**: una acción de marketing que utiliza datos para anuncios en el sitio, incluida la selección y el envío de anuncios en los sitios web o las aplicaciones de la organización, o para medir el envío y la eficacia de dichos anuncios.

**Una**: en el contexto de las exportaciones de archivos programadas, programa una exportación de archivos completa, única y bajo demanda.

**Sobrescribir estrategia de guardado**: la estrategia de guardado &quot;Sobrescribir&quot; es una opción para la ingesta de datos de terceros a través de una conexión, donde puede especificar si los datos ingeridos se sobrescribirán en una programación especificada.

## P

**Ingesta parcial**: la ingesta parcial permite la ingesta de registros válidos de datos por lotes dentro de un umbral de error especificado. Los diagnósticos de error para registros fallidos se pueden descargar o acceder en [!UICONTROL Monitorización] o [!UICONTROL Fuentes] resumen de ejecución de flujo de datos.

**Archivos de parquet**: un archivo de Parquet es un formato de archivo de almacenamiento en columnas con estructuras de datos anidadas complejas. Los archivos de parquet son necesarios para agregar datos y rellenar un conjunto de datos de esquema.

**PDPA**: La [[!DNL Personal Data Protection Act (PDPA)]](https://www.pdpc.gov.sg/Overview-of-PDPA/The-Legislation/Personal-Data-Protection-Act) fue introducido para proteger a los propietarios de datos tailandeses de la recopilación, uso o divulgación ilegales de sus datos personales. Inspirada en el RGPD de la Unión Europea, la normativa concede a los ciudadanos tailandeses el derecho de solicitar el acceso a sus datos personales almacenados o la eliminación de los mismos.

<!-- Not yet released
**PDPD**: The [[!DNL Personal Data Protection Decree] (PDPD) 
-->

**Ofertas personalizadas**: una oferta personalizada es un mensaje de marketing personalizable basado en reglas de elegibilidad y restricciones.

**Ubicaciones**: una ubicación es la ubicación o el contexto en el que aparece una oferta para un usuario final.

**Área de trabajo Políticas**: espacio de trabajo en la IU de Platform que permite a los administradores de datos ver y administrar las etiquetas y directivas de uso de datos de su organización.

**Política**: una directiva de uso de datos es una regla que especifica acciones de marketing restringidas en función de la aplicación de etiquetas de uso aplicadas a datos de Platform.

**Aplicación de políticas**: permite aplicar políticas de uso de datos con acciones de marketing aplicadas para evitar operaciones de datos que constituyan violaciones de políticas dentro de una organización.

**Clave principal**: una clave principal es una designación en un esquema para identificar de forma exclusiva todos los registros.

**Prioridad**: en [!DNL Offer Decisioning], la prioridad se utiliza para clasificar ofertas que cumplen todas las restricciones, como elegibilidad, calendario y límite.

**Gráfico de identidad privada**: el gráfico de identidad privada (a veces denominado gráfico privado) es un mapa privado de relaciones entre identidades vinculadas que se crea en función de los datos de origen y es visible solo por su organización. Solo existe un gráfico privado para cada organización y sirve como modelo estructural para los gráficos de identidad individuales generados para cada cliente que interactúa con su marca.

**Perfil del producto**: los perfiles de producto permiten a los administradores otorgar acceso de usuario a todos o un subconjunto de servicios asociados con Experience Platform.

**Zona protegida de producción**: una zona protegida de producción es una zona protegida destinada a su uso en el entorno de producción. A diferencia de las zonas protegidas que no son de producción, estas no se pueden restablecer ni eliminar.

**Perfil**: No debe confundirse con el perfil del cliente en tiempo real como servicio, un perfil es una representación completa de un cliente individual, construido a partir de datos de registros combinados y series temporales de varias fuentes.

**Acceso al perfil**: La `/entities` El punto final de la API de Perfil del cliente en tiempo real le permite acceder a los datos de registro y a los eventos de series temporales en el almacén de datos de perfil. Consulte también: Entidades de perfil

**Datos de perfil**: los datos de perfil hacen referencia a cualquier dato que se encuentre dentro del almacén de datos de perfil.

**Almacén de datos de perfil**: el almacén de datos de perfil (a veces denominado almacén de perfiles) es un sistema de almacenamiento de datos independiente del lago de datos y que el perfil del cliente en tiempo real utiliza para crear y almacenar perfiles.

**Entidades de perfil**: Las entidades de perfil representan atributos relacionados con una persona individual, normalmente un cliente. Las entidades incluidas en esta categoría deben estar representadas por esquemas basados en la variable [!DNL XDM Individual Profile] clase. Consulte también: Acceso a perfiles

**Exportación de perfiles**: [!DNL Profile] export es uno de los dos tipos de destinos de Experience Platform. [!DNL Profile] La exportación de genera un archivo que contiene perfiles y atributos, y utiliza datos PII sin procesar con el correo electrónico para integrarlos con las plataformas de marketing y automatización de correo electrónico.

**Fragmento de perfil**: un fragmento de perfil es la información de perfil de una sola identidad de la lista de identidades que existen para un cliente en particular.

**ID de perfil**: un ID de perfil es un identificador generado automáticamente y asociado a un tipo de identidad que representa un perfil.

**Propiedad**: en el contexto de las etiquetas, una propiedad es un contenedor para todo lo necesario para implementar un conjunto de etiquetas.

## Q

**Consulta**: Las consultas son solicitudes de datos de tablas de base de datos.

**Editor de consultas**: el Editor de consultas es una herramienta para escribir, validar y enviar instrucciones SQL en [!DNL Query Service].

## R

**Real-time Customer Data Platform**: Adobe Real-time Customer Data Platform (Real-Time CDP) reúne datos conocidos y desconocidos de los clientes para crear perfiles de clientes fiables con integración simplificada, segmentación inteligente y activación en tiempo real en el recorrido digital del cliente.

**Perfil del cliente en tiempo real**: Perfil del cliente en tiempo real (también denominado Perfil) proporciona una vista integral de cada cliente individual combinando datos de varios canales, incluidos en línea, sin conexión, CRM y de terceros. El perfil le permite consolidar los datos de sus clientes en perfiles individuales que ofrecen cuentas procesables con marca de tiempo de cada interacción con los clientes.

**Fórmula**: una fórmula es el término que utiliza el Adobe para una especificación de modelo y es un contenedor de nivel superior que representa procesos específicos de aprendizaje automático, algoritmos de IA, lógica de procesamiento y parámetros de configuración necesarios para crear y ejecutar un modelo entrenado y, por lo tanto, ayudar a resolver problemas empresariales específicos.

**Registro**: un registro son datos que persisten como filas en un conjunto de datos.

**Registrar datos**: Proporciona información sobre los atributos de un asunto. Un sujeto podría ser una organización o un individuo.

**Periodicidad**: en [!DNL Query Service], una periodicidad define si una consulta está programada para ejecutarse solo una vez o de forma recurrente.

**Representación**: en [!DNL Offer Decisioning], una representación es información utilizada por un canal para mostrar una oferta, como la ubicación o el idioma.

**Recurso**: en el contexto de las etiquetas, un recurso es un término genérico que hace referencia a las opciones que el usuario de etiquetas puede configurar dentro del entorno del cliente, incluidas las extensiones, los elementos de datos y las reglas.

**Control de acceso basado en roles**: El control de acceso basado en funciones permite a los administradores asignar acceso y permisos a los usuarios de Experience Platform. Los permisos incluyen la capacidad de ver o utilizar funciones de Experience Platform, como crear entornos limitados, definir esquemas y administrar conjuntos de datos.

**Regla**: en el contexto de las etiquetas, una regla es una colección de componentes que definen un conjunto específico de eventos, condiciones y acciones que deben agruparse lógicamente.

**Componente de regla**: en el contexto de las etiquetas, los componentes de regla son los eventos, condiciones y acciones que conforman una regla.

**Runtime**: Runtime especifica un entorno de tiempo de ejecución para una fórmula de aprendizaje automático. [!DNL Python], R, [!DNL Spark]Los tiempos de ejecución de, PySpark y Tensorflow permiten introducir una URL en una imagen Docker para un origen de fórmula.

## S

**Datos de muestra**: los datos de muestra son una previsualización de un archivo de datos, normalmente las primeras 100 filas, que proporciona a un científico o ingeniero de datos una idea de qué esquema o datos hay en el archivo de datos.

**Sandbox**: una zona protegida es una construcción virtual que divide una sola instancia de Platform en un entorno virtual independiente para ayudar a desarrollar y evolucionar aplicaciones de experiencia digital.

**Restablecimiento de zona protegida**: Un restablecimiento de zona protegida elimina todos los datos, incluidos los datos, perfiles y segmentos, de una zona protegida. Los reinicios de zona protegida pueden afectar a los datos conectados a destinos internos o externos.

**Conmutador de zona protegida**: el control del conmutador de zona protegida en Experience Platform permite a los usuarios navegar entre zonas protegidas a las que tienen acceso. Cambiar una zona protegida cambiará todo el contenido y puede alterar el acceso a las funciones en función de los permisos.

**Programación**: una programación es una especificación definida por el usuario sobre la frecuencia o la cadencia de la ingesta de datos de una fuente de datos de terceros a Adobe Experience Platform.

**Puntuación**: la puntuación es el proceso de generar perspectivas a partir de datos mediante un modelo entrenado.

**Esquema**: un esquema es un conjunto de reglas que representan y validan la estructura y el formato de los datos. Un esquema consta de una clase y de grupos de campos opcionales y se utiliza para crear conjuntos de datos y flujos de datos. Un esquema puede incluir atributos de comportamiento, marcas de tiempo, identidades, definiciones de atributos, relaciones, etc.

**Grupo de campos de esquema**: en el modelo de datos de experiencia (XDM), un grupo de campos de esquema permite a los usuarios ampliar campos reutilizables para definir uno o más atributos que se van a incluir en un esquema.

**Biblioteca de esquemas**: la biblioteca de esquemas contiene recursos XDM estándar del sector disponibles por Adobe, así como recursos personalizados definidos por su organización.

**Registro de esquemas**: El Registro de esquemas proporciona una interfaz de usuario y una API RESTful que se utilizan para ver y administrar todos los recursos relacionados con esquemas en la Biblioteca de esquemas.

**Clave de acceso secreta**: una clave de acceso secreta es un [!DNL Amazon] Clave S3 que se utiliza junto con el ID de clave de acceso para firmar solicitudes de AWS.

**Segmento**: un segmento es un conjunto de reglas que incluyen atributos y datos de evento que califican a una serie de perfiles para convertirlos en audiencia.

**Generador de segmentos**: La [!DNL Segment Builder] es un entorno de desarrollo visual que se utiliza para generar definiciones de segmentos. Sirve como un componente común de todas las aplicaciones que utilizan el servicio de segmentación de Experience Platform.

**Definición del segmento**: Una definición de segmento es el conjunto de reglas que se utiliza para describir las características clave o el comportamiento de una audiencia objetivo. Una vez conceptualizadas, las reglas descritas en una definición de segmento se utilizan para determinar los miembros de audiencia aptos para un segmento.

**Método de evaluación de segmentos**: Existen dos métodos de evaluación de segmentos: programado y bajo demanda. La evaluación programada permite una programación recurrente para ejecutar un trabajo de exportación en un momento específico, mientras que la evaluación bajo demanda implica la creación de un trabajo de segmento para crear la audiencia inmediatamente.

**Exportación de segmentos**: La exportación de segmentos es uno de los dos tipos de destinos en Experience Platform. Con la exportación de segmentos, puede enviar los perfiles que cumplen los requisitos y que se han asignado al destino. Utiliza ID de segmento y usuario, así como datos seudónimos, y normalmente se integra con las redes sociales y otras plataformas de destino de medios digitales.

**ID del segmento**: Un ID de segmento es un identificador generado automáticamente y asociado a un segmento.

**Abono de segmentos**: El abono a segmentos muestra de qué segmento(s) forma parte actualmente un perfil.

**Reglas de segmento**: Las reglas de segmentos definen las condiciones que determinan si un perfil cumple los requisitos para un segmento.

**Segmentación**: la segmentación es el proceso de dividir un gran grupo de clientes, clientes potenciales o consumidores en grupos más pequeños que comparten atributos similares y que responderán de manera similar a estrategias de marketing específicas.

**Marco ML de Sensei**: el marco de trabajo ML de Sensei es un marco de trabajo de aprendizaje automático unificado (ML) que aprovecha los datos de los Experience Platform para permitir a los científicos de datos desarrollar servicios de inteligencia impulsados por ML de forma más rápida, escalable y reutilizable.

**Etiquetas confidenciales (&quot;S&quot;)**: Las etiquetas confidenciales (&quot;S&quot;) se utilizan para categorizar los datos considerados confidenciales, como diferentes tipos de datos de comportamiento o geográficos que desea marcar como confidenciales.

**Servicios**: un potente marco para poner en funcionamiento los servicios de IA y ML mediante el uso de los servicios inteligentes de Adobe. Los servicios ofrecen experiencias del cliente personalizadas en tiempo real o ponen en funcionamiento servicios inteligentes personalizados.

**Acción de marketing de personalización de identidad única**: una acción de marketing que utiliza datos para la personalización de contenido en el sitio. La personalización en el sitio es cualquier dato que se utiliza para hacer deducciones sobre los intereses de los usuarios, y se utiliza para seleccionar qué contenido o anuncios se muestran en función de esas deducciones.

**Etiqueta de uso de datos S1**: Un `S1` la etiqueta de uso de datos se utiliza para clasificar los datos que especifican la latitud y la longitud que se pueden utilizar para determinar la ubicación exacta de un dispositivo.

**Etiqueta de uso de datos S2**: Un `S2` la etiqueta de uso de datos se usa para clasificar los datos que se pueden usar para determinar un área de geovalla definida en sentido amplio.

**Origen**: una fuente es un término general para cualquier conector de entrada en Platform. Consulte también: Conector de origen

**Atributo de origen**: un atributo de origen es un campo del conjunto de datos de origen. Los atributos de origen se asignan a campos de esquema de destino.

**Catálogo de origen**: el catálogo de origen es la lista de conectores de origen disponibles en Experience Platform.

**Categoría de origen**: una categoría de origen es una agrupación de orígenes que tienen características similares.

**Conector de origen**: los conectores de origen (también conocidos como fuentes) ayudan a los usuarios a ingerir fácilmente datos de varias fuentes, lo que permite estructurar, etiquetar y mejorar los datos mediante servicios de Experience Platform. Los datos se pueden ingerir desde una variedad de fuentes, como almacenamiento basado en la nube, software de terceros y sistemas CRM.

**Conexión de streaming**: una conexión de flujo continuo es un punto final único proporcionado por el Adobe y vinculado a su organización para transmitir datos a Experience Platform.

**Área de nombres de identidad estándar**: las áreas de nombres de identidad estándar son áreas de nombres de identidad predefinidas proporcionadas por Adobe, que representan soluciones estándar del sector que normalmente se emplean para identificar clientes.

**Ingesta por streaming**: la introducción por transmisión le permite enviar datos desde dispositivos del cliente y del lado del servidor al Experience Platform en tiempo real.

**Segmentación de streaming**: la segmentación de streaming es un proceso de selección de datos continuo que actualiza los segmentos en respuesta a la actividad del usuario. Una vez que se ha creado y guardado un segmento, la definición del segmento se aplica a los datos entrantes a [!DNL Real-Time Customer Profile]. Las adiciones y eliminaciones de segmentos se procesan regularmente, lo que garantiza que la audiencia de destino siga siendo relevante.

**Vista del sistema**: la vista de sistema es una representación visual de los conjuntos de datos de origen que fluyen por [!DNL Real-Time Customer Profile] a destinos.

## T

**Etiquetas**: en Adobe Experience Platform, las etiquetas proporcionan herramientas para implementar, unificar y administrar las integraciones de análisis, marketing y publicidad necesarias para potenciar las importantes experiencias del cliente en todos los dispositivos cliente.

**Funciones de destino**: en la asignación de funciones, una función de destino es la función predicha por un modelo.

**Datos de series temporales**: los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto del registro realiza una acción, ya sea directa o indirectamente.

**Modelo entrenado**: un modelo entrenado representa la salida ejecutable de un proceso de formación de modelos, en el que se aplicó un conjunto de datos de formación a la instancia del modelo. Un modelo entrenado mantendrá una referencia a cualquier servicio web inteligente que se cree a partir de él. Un modelo entrenado es adecuado para puntuar y crear un servicio web inteligente.

**Token**: un token es un tipo de seguridad de autenticación de doble factor que se puede utilizar para autorizar el uso de servicios de equipo con [!DNL Query Service].

## U

**UCPA**: La [[!DNL Utah Consumer Privacy Act]](https://le.utah.gov/~2022/bills/static/SB0227.html) crea el derecho de un consumidor a saber qué datos personales recopila una empresa, cómo utiliza la empresa sus datos personales y si la empresa vende sus datos personales. Los consumidores pueden exigir a la empresa que elimine o deje de vender sus datos personales.

**Esquema de unión**: un esquema de unión es una consolidación de esquemas que comparten la misma clase y que se han habilitado para [!DNL Real-Time Customer Profile]. Puede haber varios esquemas de unión para una organización, pero solo puede haber un esquema de unión por clase.

## V

**VCDPA**: La [[!DNL Virginia Consumer Data Protection Act (VCDPA)]](https://lis.virginia.gov/cgi-bin/legp604.exe?212+sum+HB2307) proporciona nuevos derechos de privacidad de datos a los residentes de Virginia (&quot;Consumidores&quot;), incluido el derecho a acceder, eliminar y corregir datos personales. Los consumidores también tienen derecho a excluirse de la venta de datos personales, de la creación de perfiles basados en datos personales y del procesamiento de fines publicitarios personales.

## W

## X

**XDM**: Consulte Experience Data Model (XDM).

**Evento de decisión de XDM**: el evento de decisión XDM es una clase basada en series temporales que se utiliza para capturar observaciones sobre el resultado y el contexto de una actividad de decisión. Esto incluye información sobre cómo se tomó la decisión, cuándo se produjo, qué opciones se propusieron (y eligieron) y qué estado contextual existió que influyó en la decisión o que se pudo observar durante el proceso de decisión.

**ExperienceEvent de XDM**: ExperienceEvent de XDM es una clase basada en series temporales que se utiliza para capturar el estado del sistema cuando se produjo un evento (o conjunto de eventos), incluido el momento y la identidad del sujeto involucrado. Consulte también: Evento de experiencia

**Perfil individual de XDM**: XDM [!DNL Individual Profile] es una clase basada en registros que forma una representación singular de los atributos de los sujetos identificados y parcialmente identificados. Los perfiles altamente identificados pueden utilizarse para comunicaciones personales o compromisos específicos y pueden contener información personal detallada como nombre, sexo, fecha de nacimiento, ubicación e información de contacto, incluidos números de teléfono y direcciones de correo electrónico.

**Sistema XDM**: el sistema XDM representa el marco de trabajo que pone en funcionamiento los esquemas XDM para su uso en servicios de Experience Platform descendentes.

## Y

## Z
