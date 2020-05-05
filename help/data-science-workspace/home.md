---
keywords: Experience Platform;home;Data Science Workspace;popular topics
solution: Experience Platform
title: Información general sobre el área de trabajo de ciencias de datos
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34

---


# Información general sobre el área de trabajo de ciencias de datos

Adobe Experience Platform Data Science Workspace utiliza el aprendizaje automático y la inteligencia artificial para generar perspectivas a partir de los datos. Integrado en la plataforma Adobe Experience, el espacio de trabajo de ciencia de datos le ayuda a realizar predicciones con su contenido y recursos de datos en todas las soluciones de Adobe.

Los científicos de datos de todos los niveles encontrarán herramientas sofisticadas y fáciles de usar que apoyen el rápido desarrollo, la capacitación y el ajuste de las recetas de aprendizaje automático -todos los beneficios de la tecnología de IA, sin la complejidad.

Con Data Science Workspace, los científicos de datos pueden crear fácilmente API de servicios inteligentes, basadas en el aprendizaje automático. Estos servicios funcionan con otros servicios de Adobe, incluidos Adobe Destinatario y Adobe Analytics Cloud, para ayudarle a automatizar las experiencias digitales personalizadas y con objetivos en aplicaciones web, de escritorio y móviles.

Esta guía proporciona información general sobre los conceptos clave relacionados con el espacio de trabajo de ciencias de datos.

## Introducción

La empresa de hoy da una alta prioridad a la extracción de grandes datos para predicciones y perspectivas que los ayudarán a personalizar las experiencias de los clientes y a ofrecer más valor a los clientes y al negocio.
Por importante que sea, pasar de los datos a las perspectivas puede tener un alto costo. Generalmente requiere de científicos de datos capacitados que realicen investigaciones intensivas y que requieran mucho tiempo para desarrollar modelos o fórmulas de aprendizaje automático que impulsen los servicios inteligentes. El proceso es largo, la tecnología es compleja y los científicos de datos calificados pueden ser difíciles de encontrar.

Con Data Science Workspace, Adobe Experience Platform le permite ofrecer a toda la empresa un contenido de IA centrado en la experiencia, lo que optimiza y acelera la conversión de datos a perspectivas en código con:
- Un entorno de aprendizaje automático y tiempo de ejecución
- Acceso integrado a los datos almacenados en Adobe Experience Platform
- Un esquema de datos unificado creado en el modelo de datos de experiencia (XDM)
- La potencia informática esencial para el aprendizaje automático/IA y la administración de grandes conjuntos de datos
- Fórmulas de aprendizaje automático prediseñadas para acelerar el salto a experiencias impulsadas por AI
- Creación, reutilización y modificación simplificadas de recetas para científicos de datos con diferentes niveles de aptitud
- Publicación y uso compartido de servicios inteligentes con sólo unos pocos clics (sin programador) y supervisión y readiestramiento para la optimización continua de las experiencias personalizadas de los clientes

Los científicos de datos de todos los niveles de habilidades obtendrán perspectivas digitales más rápidas y efectivas antes.

## Primeros pasos

Antes de profundizar en los detalles de Data Science Workspace, a continuación se presenta un breve resumen de los términos clave:

| Término | Definición |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Área de trabajo de ciencia de datos | El espacio de trabajo de ciencias de datos de la plataforma de experiencia permite a los clientes crear modelos de aprendizaje automático que utilizan datos en la plataforma de experiencia y en las soluciones de Adobe para generar perspectivas y predicciones inteligentes que permiten crear experiencias digitales de usuario final deliciosas. |
| Inteligencia artificial | La inteligencia artificial es una teoría y un desarrollo de sistemas informáticos capaces de realizar tareas que normalmente requieren inteligencia humana, como la percepción visual, el reconocimiento del habla, la toma de decisiones y la traducción entre idiomas. |
| Aprendizaje automático | El aprendizaje automático es el campo de estudio que permite a las computadoras aprender sin programarse explícitamente. |
| Marco para el transporte marítimo de Sensei ML | Sensei ML Framework es un marco de aprendizaje automático unificado en Adobe que aprovecha los datos de la plataforma Experience para potenciar a los científicos de datos en el desarrollo de servicios de inteligencia basados en el aprendizaje automático de una manera más rápida, escalable y reutilizable. |
| Modelo de datos de experiencia | El modelo de datos de experiencia (XDM) es el esfuerzo de estandarización que lleva a cabo Adobe para definir esquemas estándar como Perfil y ExperienceEvent para la administración de la experiencia del cliente. |
| JupyterLab | JupyterLab es una interfaz basada en web de código abierto para Project Jupyter y está estrechamente integrada en la plataforma de experiencias. |
| Fórmulas | Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo AI o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarios para crear y ejecutar un modelo capacitado y, por tanto, ayuda a resolver problemas empresariales específicos. |
| Modelo | Un modelo es una instancia de una fórmula de aprendizaje automático que se capacita mediante datos históricos y configuraciones para resolver un caso de uso comercial. |
| Formación | La formación es el proceso de aprendizaje de patrones y perspectivas a partir de datos etiquetados. |
| Modelo capacitado | Un modelo formado representa el resultado ejecutable de un proceso de formación de modelo, en el que se aplicó un conjunto de datos de formación a la instancia de modelo. Un modelo capacitado mantendrá una referencia a cualquier servicio Web inteligente que se cree a partir de él. El modelo entrenado es adecuado para la puntuación y la creación de un servicio Web inteligente. Las modificaciones de un modelo capacitado se pueden rastrear como una nueva versión. |
| Puntuación | La puntuación es el proceso de generación de perspectivas a partir de datos mediante un modelo capacitado. |
| Service | Un servicio implementado expone la funcionalidad de una inteligencia artificial, un modelo de aprendizaje automático o un algoritmo avanzado a través de una API para que otros servicios o aplicaciones puedan utilizarla para crear aplicaciones inteligentes. |

El siguiente gráfico describe la relación jerárquica entre Fórmulas, Modelos, Ejecuciones de formación y Ejecuciones de puntuación.

![](./images/home/recipe_hiearchy_ui.png)

## Explicación del área de trabajo de ciencias de la información

Con Data Science Workspace, sus científicos de datos pueden optimizar el proceso engorroso de descubrir perspectivas en grandes conjuntos de datos. Basado en un entorno de aprendizaje automático y un tiempo de ejecución comunes, Data Science Workspace ofrece administración avanzada de flujos de trabajo, administración de modelos y escalabilidad. Los servicios inteligentes admiten la reutilización de las fórmulas de aprendizaje automático para potenciar una variedad de aplicaciones creadas con productos y soluciones de Adobe.

### Acceso a datos de un solo nivel

Los datos son la piedra angular de la IA y el aprendizaje automático.

El espacio de trabajo de Data Science está totalmente integrado con la plataforma Adobe Experience, incluidos Data Lake, Real-time Customer Perfil y Unified Edge. Explore todos los datos de su organización almacenados en Adobe Experience Platform a la vez, junto con grandes datos comunes y bibliotecas de aprendizaje profundo, como Spark ML y TensorFlow. Si no encuentra lo que necesita, ingrese sus propios conjuntos de datos utilizando el esquema estandarizado XDM.

### Fórmulas de aprendizaje automático precompiladas

Data Science Workspace incluye fórmulas de aprendizaje automático prediseñadas para necesidades comerciales comunes, como la predicción de ventas minoristas y la detección de anomalías, de modo que los científicos de datos y los desarrolladores no tienen que tener que realizar inicios desde cero. Actualmente se ofrecen tres fórmulas: predicción [de compra de](./pre-built-recipes/product-purchase-prediction.md)productos, recomendaciones [de](./pre-built-recipes/product-recommendations.md)productos y ventas [](./pre-built-recipes/retail-sales.md)minoristas.

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si lo prefiere, puede adaptar una fórmula prediseñada a sus necesidades, importar una fórmula o un inicio desde cero para crear una fórmula personalizada. Sin embargo, una vez que se enseña y se pone a punto una fórmula, la creación de un servicio inteligente personalizado no requiere de un desarrollador, sólo unos clics y está listo para crear una experiencia digital personalizada y dirigida.

### Flujo de trabajo centrado en el científico de datos

Independientemente del nivel de experiencia en ciencia de datos, el espacio de trabajo de ciencia de datos ayuda a simplificar y acelerar el proceso de encontrar perspectivas en los datos y aplicarlas a las experiencias digitales.

### Exploración de datos

Encontrar los datos adecuados y prepararlos es la parte más trabajadora para crear una fórmula efectiva. El espacio de trabajo de ciencia de datos y la plataforma de Adobe Experience le ayudarán a pasar de los datos a las perspectivas con mayor rapidez.

En Adobe Experience Platform, los datos de canales cruzados están centralizados y almacenados en el esquema estandarizado XDM, por lo que los datos son más fáciles de encontrar, comprender y limpiar. Un único almacén de datos basado en un esquema común puede ahorrarle innumerables horas de exploración y preparación de datos.

A medida que navega, utilice R, Python o Scala con el bloc de notas Jupyter integrado y alojado para explorar el catálogo de datos en la plataforma. Con uno de estos idiomas, también puede aprovechar Spark ML y TensorFlow. Inicio desde cero o utilice una de las plantillas de portátiles proporcionadas para problemas empresariales específicos.

Como parte del flujo de trabajo de exploración de datos, también puede ingestar datos nuevos o utilizar funciones existentes para ayudar en la preparación de datos.

### Creación  

Con Área de trabajo de ciencias de datos, usted decide cómo desea crear las fórmulas.

- Ahorre tiempo buscando una fórmula prediseñada que satisfaga sus necesidades comerciales, que puede utilizar tal cual o configurar para satisfacer sus necesidades específicas.
- Cree una fórmula desde cero, utilizando el tiempo de ejecución de creación en Jupyter Notebook para desarrollar y registrar la fórmula.
- Cargue una fórmula creada fuera de la plataforma de Adobe Experience en el espacio de trabajo de ciencia de datos o importe el código de fórmula desde un repositorio, como Git, mediante la autenticación y la integración disponibles entre Git y el espacio de trabajo de ciencia de datos.

### Experimentación

El espacio de trabajo de ciencia de datos aporta una gran flexibilidad al proceso de experimentación. Inicio con tu receta. A continuación, cree una instancia independiente, utilizando el mismo algoritmo principal emparejado con características únicas, como parámetros de ajuste híper. Puede crear tantas instancias como necesite, formando y anotando cada instancia tantas veces como desee. A medida que los capacita, Área de trabajo de ciencia de datos rastrea fórmulas, instancias de fórmula e instancias formadas, junto con métricas de evaluación, para que no tenga que hacerlo.

### Operacionalización

Cuando estás satisfecho con tu fórmula, son sólo unos clics para crear un servicio inteligente. No se requiere codificación: puede hacerlo usted mismo, sin tener que contratar a un desarrollador o ingeniero. Por último, publique el servicio inteligente en Adobe IO y estará listo para que lo consuma su equipo de experiencia digital.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Mejora continua

Área de trabajo de ciencia de datos rastrea dónde se invocan los servicios inteligentes y su rendimiento. A medida que los datos entran en funcionamiento, puede evaluar la precisión inteligente del servicio para cerrar el bucle y volver a preparar las fórmulas según sea necesario para mejorar el rendimiento. El resultado es un refinamiento continuo en la precisión de la personalización del cliente.

### Acceso a nuevas funciones y conjuntos de datos

Los científicos de datos pueden aprovechar las nuevas tecnologías y conjuntos de datos en cuanto estén disponibles a través de los servicios de Adobe. A través de actualizaciones frecuentes, hacemos el trabajo de integrar datasets y tecnologías en la plataforma, para que no tenga que hacerlo.

### Control de acceso en Área de trabajo de ciencias de datos

Control de acceso para la plataforma de experiencias se administra a través de la Consola de administración de [Adobe](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la descripción general [del](../access-control/home.md) control de acceso para obtener más información.

>[!IMPORTANT] Para utilizar el área de trabajo de ciencias de datos, debe habilitarse el permiso &quot;Administrar área de trabajo de ciencias de datos&quot;.

La siguiente tabla describe los efectos de habilitar o deshabilitar este permiso:

| Permiso | Habilitado | Desactivado |
|---|---|---|
| Administrar área de trabajo de ciencias de datos | Proporciona acceso a todos los servicios de Data Science Workspace. | El acceso a la API y a la interfaz de usuario de todos los servicios dentro de Área de trabajo de ciencias de datos está deshabilitado. Aunque está deshabilitado, se evita el enrutamiento a las páginas *Modelos* y *servicios* de Data Science Workspace. |

### Seguridad y paz mental

La seguridad de los datos es una prioridad máxima para Adobe. Adobe protege sus datos con los procesos y controles de seguridad desarrollados para ayudarle a cumplir con las normas, regulaciones y certificaciones aceptadas por el sector.

La seguridad está integrada en el software y los servicios como parte del ciclo de vida seguro del producto de Adobe.
Para obtener más información sobre la seguridad de los datos y el software de Adobe, el cumplimiento de normas y mucho más, visite la página de seguridad en https://www.adobe.com/security.html.

### Compatibilidad con Simulador para pruebas

Los entornos limitados son particiones virtuales dentro de una sola instancia de la plataforma de experiencia. Cada instancia de Plataforma admite un entorno limitado de producción y varios entornos limitados que no sean de producción, cada uno de los cuales mantiene su propia biblioteca de recursos de la Plataforma. Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. Para obtener más información sobre los entornos limitados, consulte la descripción general [de los](../sandboxes/home.md)entornos limitados.

Actualmente, el área de trabajo de ciencias de datos tiene un par de limitaciones de entorno limitado:

- Los recursos de cómputo se comparten en el entorno limitado de producción y en los entornos limitados que no son de producción. El aislamiento de los entornos limitados de producción se establecerá en el futuro.
- Actualmente, las cargas de trabajo de Scala/Spark y PySpark para portátiles y fórmulas solo se admiten en el entorno limitado de producción. La compatibilidad con los entornos limitados que no sean de producción se establecerá en el futuro.

## Área de trabajo de ciencia de datos en acción

Las predicciones y perspectivas proporcionan la información necesaria para ofrecer una experiencia altamente personalizada a cada cliente que visite su sitio web, se ponga en contacto con su centro de llamadas o participe en otras experiencias digitales. Así es como su trabajo diario se lleva a cabo con Área de trabajo de ciencias de datos.

### Definir el problema

Todo inicio con un problema de negocios. Por ejemplo, un centro de llamadas en línea necesita contexto para ayudarles a convertir una opinión negativa del cliente en positiva.

Hay muchos datos sobre el cliente. Han explorado el sitio, han colocado artículos en el carro de compras e incluso han realizado pedidos. Es posible que hayan recibido correos electrónicos, utilizado cupones o se hayan puesto en contacto con el centro de llamadas anteriormente. La fórmula, entonces, necesita utilizar los datos disponibles sobre el cliente y sus actividades para determinar la propensión a comprar y recomendar una oferta que el cliente probablemente apreciará y usará.

![](./images/home/example_problem.png)

En el momento del contacto con el centro de llamadas, el cliente aún tiene dos pares de zapatos en el carro, pero se quitó una camisa. Con esta información, el servicio inteligente puede recomendar que el agente del centro de llamadas oferta un cupón de 20% de descuento en zapatos durante la llamada. Si el cliente utiliza el cupón, esa información se agrega al conjunto de datos y las predicciones mejoran aún más la próxima vez que llama el cliente.

### Explorar y preparar los datos

En función del problema comercial definido, sabe que la fórmula debe analizar todas las transacciones Web del cliente, incluidas las visitas al sitio, las búsquedas, las vistas de página, los vínculos en los que se hizo clic, las acciones del carro de compras, las ofertas recibidas, los correos electrónicos recibidos, las interacciones con el centro de llamadas, etc.

Por lo general, un científico de datos emplea hasta el 75% del tiempo necesario para crear una fórmula que explora y transforma los datos. Los datos suelen proceder de varios repositorios y se guardan en diferentes esquemas; se deben combinar y asignar antes de poder utilizarlos para crear una fórmula.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Si está empezando desde cero o configurando una fórmula existente, comience la búsqueda de datos en un catálogo de datos centralizado y estandarizado para su organización, lo que simplifica la búsqueda considerablemente. Incluso puede que otro científico de datos de su organización ya haya identificado un conjunto de datos similar y elija afinar ese conjunto de datos en lugar de hacerlo desde cero.
Todos los datos de Adobe Experience Platform cumplen con un esquema XDM estandarizado, lo que elimina la necesidad de crear un modelo complejo para unirse a los datos o obtener ayuda de un ingeniero de datos.

Si no encuentra inmediatamente los datos que necesita, pero existen fuera de Adobe Experience Platform, es una tarea relativamente sencilla de ingerir conjuntos de datos adicionales, que también se transformarán en el esquema XDM estandarizado.\
Puede utilizar el bloc de notas Jupyter para simplificar el procesamiento previo de los datos, posiblemente a partir de una plantilla de portátil o un bloc de notas que haya utilizado anteriormente para comprar.

![](./images/home/notebook_templates.png)

### Crear la fórmula

Si ya has encontrado una fórmula que satisfaga todas tus necesidades, puedes pasar a la experimentación. O bien, puede modificar un poco la fórmula o crear una desde cero, aprovechando el tiempo de ejecución de creación de Data Science Workspace en Jupyter Notebook. El uso del tiempo de ejecución de creación garantiza que puede utilizar el flujo de trabajo de formación y puntuación de Área de trabajo de ciencia de datos y convertir la fórmula más adelante para que otras personas de su organización puedan almacenarla y reutilizarla.

También puede importar una fórmula en el área de trabajo de ciencias de datos y aprovechar los flujos de trabajo de experimentación a medida que crea el servicio inteligente.

### Experimente con la fórmula

Con una fórmula que incorpora los algoritmos principales de aprendizaje automático, se pueden crear muchas instancias de fórmula con una sola fórmula. Estas instancias de fórmula se denominan modelos. Un modelo requiere capacitación y evaluación para optimizar su eficacia y eficiencia operativa, un proceso que normalmente consiste en pruebas y errores.

![](./images/home/recipe_hiearchy_ui.png)

A medida que imparte formación a sus modelos, se generan ejecuciones de formación y evaluaciones. Área de trabajo de ciencia de datos realiza un seguimiento de las métricas de evaluación de cada modelo único y de sus ejecuciones de formación. Las métricas de evaluación generadas a través de la experimentación le permitirán determinar la ejecución de la capacitación que tenga el mejor rendimiento.

![](./images/home/evaluation_metrics.png)

Visite [esta sección](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) para ver tutoriales sobre cómo entrenar y evaluar modelos en Área de trabajo de ciencia de datos.

### Operacionalizar el modelo

Cuando haya seleccionado la fórmula mejor capacitada para responder a sus necesidades comerciales, puede crear un servicio inteligente en Área de trabajo de ciencias de datos sin necesidad de asistencia para desarrolladores. Son sólo un par de clics - no se requiere codificación. Otros miembros de la organización pueden acceder a un servicio inteligente publicado sin necesidad de volver a crear el modelo.

Un servicio inteligente publicado se puede configurar para formarse automáticamente de vez en cuando utilizando nuevos datos a medida que estén disponibles. Esto garantiza que su servicio mantenga su eficiencia y eficacia a medida que el tiempo continúa.

## Pasos siguientes

Área de trabajo de ciencias de datos ayuda a optimizar y simplificar el flujo de trabajo de la ciencia de datos, desde la recopilación de datos a los algoritmos a los servicios inteligentes, para científicos de datos de todos los niveles de habilidades. Con las herramientas sofisticadas que proporciona el área de trabajo de ciencias de la información, puede acortar considerablemente el tiempo de los datos a las perspectivas.

Lo que es más importante, el espacio de trabajo de ciencia de datos pone las funciones de optimización algorítmica y ciencia de datos de la plataforma de marketing líder de Adobe en manos de los científicos de datos empresariales. Por primera vez, las empresas pueden incorporar algoritmos propios a la plataforma, aprovechando las potentes funciones de aprendizaje automático y de IA de Adobe para ofrecer experiencias de cliente altamente personalizadas a gran escala.

Con la combinación de experiencia en la marca y el aprendizaje automático y la destreza en IA de Adobe, las empresas tienen el poder de generar más valor empresarial y lealtad a la marca dando a los clientes lo que desean, antes de pedirlo.

Para obtener información adicional, como un flujo de trabajo diario completo, lea la documentación de introducción [a](./walkthrough.md) Data Science Workspace.

## Recursos adicionales

El siguiente vídeo está diseñado para admitir su comprensión del espacio de trabajo de ciencia de datos.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

