---
keywords: Experience Platform;inicio;Data Science Workspace;temas populares;espacio de trabajo de ciencia de datos;ciencia de datos
solution: Experience Platform
title: Información general de Data Science Workspace
description: Esta guía proporciona información general sobre los conceptos clave relacionados con Data Science Workspace en Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---

# Información general de Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para extraer perspectivas de sus datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a realizar predicciones utilizando los recursos de contenido y datos en las soluciones de Adobe.

Los científicos de datos de todos los niveles encontrarán herramientas sofisticadas y fáciles de usar que apoyen el rápido desarrollo, capacitación y ajuste de recetas de aprendizaje automático -todos los beneficios de la tecnología de IA, sin la complejidad.

con [!DNL Data Science Workspace], los científicos de datos pueden crear fácilmente API de servicios inteligentes, con tecnología de aprendizaje automático. Estos servicios trabajan con otros servicios de Adobe, incluidos Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y segmentadas en aplicaciones web, de escritorio y móviles.

Esta guía proporciona información general sobre los conceptos clave relacionados con [!DNL Data Science Workspace].

## Introducción

La empresa de hoy otorga gran prioridad a la extracción de grandes datos para predicciones y perspectivas que les ayudarán a personalizar las experiencias de los clientes y a ofrecer más valor a los clientes, así como al negocio.
Por más importante que sea, pasar de los datos a las perspectivas puede tener un alto coste. Generalmente, requiere científicos de datos calificados que lleven a cabo una investigación de datos intensiva y que consume mucho tiempo para desarrollar modelos o recetas de aprendizaje automático, que impulsen los servicios inteligentes. El proceso es largo, la tecnología es compleja y los científicos de datos calificados pueden ser difíciles de encontrar.

con [!DNL Data Science Workspace], Adobe Experience Platform le permite ofrecer una IA centrada en la experiencia en toda la empresa, lo que optimiza y acelera la relación entre datos y perspectivas para codificarlos con:
- Un marco de aprendizaje automático y tiempo de ejecución
- Acceso integrado a los datos almacenados en Adobe Experience Platform
- Un esquema de datos unificado creado en [!DNL Experience Data Model] (XDM)
- La potencia informática esencial para el aprendizaje automático/IA y la administración de grandes conjuntos de datos
- Fórmulas de aprendizaje automático prediseñadas para acelerar el salto a experiencias controladas por IA
- Creación, reutilización y modificación simplificadas de recetas para científicos de datos de diferentes niveles de habilidades
- Publicación y uso compartido inteligente de servicios en tan solo unos pocos clics (sin desarrollador) y monitorización y formación para optimizar continuamente las experiencias personalizadas del cliente

Los científicos de datos de todos los niveles de habilidades lograrán perspectivas digitales más rápidas y efectivas antes.

## Primeros pasos

Antes de sumergirse en los detalles de [!DNL Data Science Workspace], aquí tiene un breve resumen de los términos clave:

| Término | Definición |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] en [!DNL Experience Platform] permite a los clientes crear modelos de aprendizaje automático utilizando datos de [!DNL Experience Platform] y soluciones de Adobe para generar perspectivas y predicciones inteligentes con el fin de tejer experiencias digitales de usuario final encantadoras. |
| Inteligencia artificial | La inteligencia artificial es una teoría y el desarrollo de sistemas informáticos que son capaces de realizar tareas que normalmente requieren inteligencia humana, como la percepción visual, el reconocimiento del habla, la toma de decisiones y la traducción entre idiomas. |
| Aprendizaje automático | El aprendizaje automático es el campo de estudio que permite a los ordenadores aprender sin ser programados explícitamente. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework es un marco de aprendizaje automático unificado en todo el Adobe que aprovecha los datos [!DNL Experience Platform] facultar a los científicos de datos para que desarrollen servicios de inteligencia impulsados por el aprendizaje automático de una manera más rápida, escalable y reutilizable. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) es el esfuerzo de estandarización liderado por el Adobe para definir esquemas estándar como [!DNL Profile] y [!DNL ExperienceEvent], para Customer Experience Management. |
| [!DNL JupyterLab] | [!DNL JupyterLab] es una interfaz basada en web de código abierto para Project Jupyter y está estrechamente integrada en [!DNL Experience Platform]. |
| Fórmulas | Una fórmula es el término del Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo AI o un conjunto de algoritmos, lógica de procesamiento y configuración necesarios para crear y ejecutar un modelo entrenado y, por lo tanto, ayuda a resolver problemas empresariales específicos. |
| Modelo | Un modelo es una instancia de una fórmula de aprendizaje automático que se enseña mediante datos y configuraciones históricos para resolver un caso de uso empresarial. |
| Formación | La formación es el proceso de aprendizaje de patrones y perspectivas a partir de datos etiquetados. |
| Modelo capacitado | Un modelo formado representa el resultado ejecutable de un proceso de capacitación modelo, en el que se aplicó un conjunto de datos de capacitación a la instancia del modelo. Un modelo entrenado mantendrá una referencia a cualquier servicio web inteligente que se cree a partir de él. El modelo entrenado es adecuado para la puntuación y la creación de un servicio web inteligente. Las modificaciones realizadas en un modelo entrenado se pueden rastrear como una nueva versión. |
| Puntuación | La puntuación es el proceso de generación de perspectivas a partir de datos mediante un modelo entrenado. |
| Service | Un servicio implementado expone la funcionalidad de una inteligencia artificial, un modelo de aprendizaje automático o un algoritmo avanzado a través de una API para que otros servicios o aplicaciones puedan utilizarla para crear aplicaciones inteligentes. |

El siguiente gráfico describe la relación jerárquica entre Fórmulas, Modelos, Ejecuciones de capacitación y Ejecuciones de puntuación.

![](./images/home/recipe_hiearchy_ui.png)

## Explicación [!DNL Data Science Workspace]

con [!DNL Data Science Workspace], sus científicos de datos pueden optimizar el engorroso proceso de descubrir perspectivas en grandes conjuntos de datos. Basado en un marco común de aprendizaje automático y en tiempo de ejecución, [!DNL Data Science Workspace] ofrece administración avanzada del flujo de trabajo, administración de modelos y escalabilidad. Los servicios inteligentes admiten la reutilización de recetas de aprendizaje automático para impulsar una variedad de aplicaciones creadas con productos y soluciones de Adobe.

### Acceso de datos único

Los datos son la piedra angular de la IA y el aprendizaje automático.

[!DNL Data Science Workspace] está totalmente integrado con Adobe Experience Platform, incluido el lago de datos, [!DNL Real-Time Customer Profile]y [!DNL Unified Edge]. Explore todos los datos de su organización almacenados en Adobe Experience Platform a la vez, junto con grandes datos comunes y bibliotecas de aprendizaje profundo, como [!DNL Spark] ML y [!DNL TensorFlow]. Si no encuentra lo que necesita, ingrese sus propios conjuntos de datos con el esquema estandarizado XDM.

### Fórmulas de aprendizaje automático prediseñadas

[!DNL Data Science Workspace] incluye fórmulas de aprendizaje automático prediseñadas para necesidades empresariales comunes, como la predicción de ventas minoristas y la detección de anomalías, de modo que los científicos y desarrolladores de datos no tienen que empezar desde cero. Actualmente se ofrecen tres recetas, [predicción de compra de productos](./pre-built-recipes/product-purchase-prediction.md), [recomendaciones de productos](./pre-built-recipes/product-recommendations.md)y [ventas minoristas](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si lo prefiere, puede adaptar una fórmula prediseñada a sus necesidades, importar una receta o empezar desde cero para crear una fórmula personalizada. Sin embargo, una vez que se prepara y se ajusta una fórmula de forma hiperprecisa, la creación de un servicio inteligente personalizado no requiere desarrollador, solo unos clics y está listo para crear una experiencia digital personalizada y con objetivo.

### Flujo de trabajo centrado en el científico de datos

Cualquiera que sea su nivel de experiencia en ciencia de datos, [!DNL Data Science Workspace] ayuda a simplificar y acelerar el proceso de encontrar perspectivas en los datos y aplicarlas a las experiencias digitales.

### Exploración de datos

Encontrar los datos adecuados y prepararlos es la parte más intensiva en mano de obra para crear una receta eficaz. [!DNL Data Science Workspace] y Adobe Experience Platform le ayudará a pasar de los datos a las perspectivas con mayor rapidez.

En Adobe Experience Platform, los datos de canales cruzados están centralizados y almacenados en el esquema estandarizado XDM, por lo que es más fácil encontrar, comprender y limpiar los datos. Un único almacén de datos basado en un esquema común puede ahorrarle innumerables horas de exploración y preparación de datos.

Mientras navega, utilice R, [!DNL Python], o Scala con el [!DNL Jupyter Notebook] examinar el catálogo de datos en [!DNL Platform]. Con uno de estos idiomas, también puede aprovechar [!DNL Spark] ML y TensorFlow. Comience desde cero o utilice una de las plantillas de portátiles proporcionadas para problemas empresariales específicos.

Como parte del flujo de trabajo de exploración de datos, también puede introducir datos nuevos o utilizar funciones existentes para ayudar en la preparación de los datos.

### Creación

con [!DNL Data Science Workspace], decide cómo desea crear fórmulas.

- Ahorre tiempo buscando una fórmula prediseñada que satisfaga sus necesidades comerciales, que puede utilizar tal cual o configurar para satisfacer sus necesidades específicas.
- Cree una fórmula desde cero, utilizando el tiempo de ejecución de creación en Jupyter Notebook para desarrollar y registrar la fórmula.
- Cargar una fórmula creada fuera de Adobe Experience Platform a [!DNL Data Science Workspace] o importar código de fórmula de un repositorio, como [!DNL Git], utilizando la autenticación y la integración disponibles entre [!DNL Git] y [!DNL Data Science Workspace].

### Experimento

Data Science Workspace aporta una gran flexibilidad al proceso de experimentación. Comience con su fórmula. A continuación, cree una instancia independiente, utilizando el mismo algoritmo central emparejado con características únicas, como los parámetros de ajuste híper. Puede crear tantas instancias como necesite, entrenando y puntuando cada instancia tantas veces como desee. Mientras los entrenas, [!DNL Data Science Workspace] realiza el seguimiento de fórmulas, instancias de fórmula e instancias formadas, junto con métricas de evaluación, para que no tenga que hacerlo.

### Operacionalización

Cuando estás contento con tu receta, son solo unos pocos clics para crear un servicio inteligente. No se requiere código - puede hacerlo usted mismo, sin incluir a un desarrollador o ingeniero. Por último, publique el servicio inteligente en Adobe IO y estará listo para que lo consuma su equipo de experiencia digital.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Mejora continua

[!DNL Data Science Workspace] rastrea dónde se invocan los servicios inteligentes y cómo funcionan. A medida que los datos se incorporan, puede evaluar la precisión del servicio inteligente para cerrar el bucle y volver a preparar las fórmulas según sea necesario para mejorar el rendimiento. El resultado es un refinamiento continuo en la precisión de la personalización del cliente.

### Acceso a nuevas funciones y conjuntos de datos

Los científicos de datos pueden aprovechar las nuevas tecnologías y conjuntos de datos en cuanto estén disponibles a través de los servicios de Adobe. A través de actualizaciones frecuentes, hacemos el trabajo de integrar conjuntos de datos y tecnologías en la plataforma, por lo que no tiene que tener que hacerlo.

### Seguridad y paz mental

La seguridad de los datos es una prioridad máxima para el Adobe. Adobe protege sus datos con procesos y controles de seguridad desarrollados para ayudarle a cumplir con las normas, regulaciones y certificaciones aceptadas por el sector.

La seguridad está integrada en el software y los servicios como parte del ciclo de vida seguro del producto de Adobe.
Para obtener más información sobre la seguridad de los datos de Adobe y software, el cumplimiento de normas y más, visite la página de seguridad en https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] en acción

Las predicciones y perspectivas proporcionan la información necesaria para ofrecer una experiencia altamente personalizada a cada cliente que visite su sitio web, contacte con su centro de llamadas o se involucre en otras experiencias digitales. Así es como ocurre su trabajo diario con [!DNL Data Science Workspace].

### Definir el problema

Todo comienza con un problema de negocios. Por ejemplo, un centro de llamadas en línea necesita contexto para ayudarles a convertir una opinión negativa en positiva para los clientes.

Hay muchos datos sobre el cliente. Han explorado el sitio, puesto artículos en el carro de compras e incluso hecho pedidos. Es posible que hayan recibido correos electrónicos, utilizado cupones o que se hayan puesto en contacto con el centro de llamadas anteriormente. Por lo tanto, la fórmula necesita utilizar los datos disponibles sobre el cliente y sus actividades para determinar la propensión a comprar y recomendar una oferta que el cliente probablemente aprecie y utilice.

![](./images/home/example_problem.png)

En el momento del contacto del centro de llamadas, el cliente todavía tiene dos pares de zapatos en el carro, pero quitó una camisa. Con esta información, el servicio inteligente puede recomendar que el agente del centro de llamadas ofrezca un cupón de 20% de descuento en zapatos durante la llamada. Si el cliente utiliza el cupón, esa información se agrega al conjunto de datos y las predicciones mejoran aún más la próxima vez que el cliente invoque .

### Explorar y preparar los datos

En función del problema comercial definido, sabe que la fórmula debería analizar todas las transacciones web del cliente, incluidas las visitas al sitio, las búsquedas, las vistas de página, los vínculos en los que se hizo clic, las acciones del carro de compras, las ofertas recibidas, los correos electrónicos recibidos, las interacciones del centro de llamadas, etc.

Un científico de datos suele pasar hasta el 75% del tiempo necesario para crear una fórmula que explore y transforme los datos. Los datos suelen proceder de varios repositorios y se guardan en distintos esquemas; deben combinarse y asignarse antes de poder utilizarse para crear una fórmula.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Si comienza desde cero o configura una fórmula existente, comience la búsqueda de datos en un catálogo de datos centralizado y estandarizado para su organización, lo que simplifica considerablemente la búsqueda. Incluso podría descubrir que otro científico de datos de su organización ya ha identificado un conjunto de datos similar y elegir ajustar ese conjunto de datos en lugar de comenzar desde cero.
Todos los datos de Adobe Experience Platform cumplen con un esquema XDM estandarizado, lo que elimina la necesidad de crear un modelo complejo para unir datos u obtener ayuda de un ingeniero de datos.

Si no encuentra inmediatamente los datos que necesita, pero existen fuera de Adobe Experience Platform, es una tarea relativamente sencilla ingerir conjuntos de datos adicionales, que también se transformarán en el esquema XDM estandarizado.\
Puede usar [!DNL Jupyter Notebook] para simplificar el procesamiento previo de los datos, es posible que comience con una plantilla de bloc de notas o un bloc de notas que haya utilizado anteriormente para comprar propensión.

![](./images/home/notebook_templates-new.png)

### Crear la fórmula

Si ya ha encontrado una fórmula que satisfaga todas sus necesidades, puede pasar a la experimentación. O bien, puede modificar un poco la fórmula o crear una desde cero, aprovechando el [!DNL Data Science Workspace] tiempo de ejecución de creación en [!DNL Jupyter Notebook]. El uso del tiempo de ejecución de la creación garantiza que ambos pueden utilizar la variable [!DNL Data Science Workspace] flujo de trabajo de formación y puntuación y convierta la fórmula más tarde para que otras personas de su organización puedan almacenarla y reutilizarla.

También puede importar una fórmula en [!DNL Data Science Workspace] y aproveche los flujos de trabajo de experimentación a medida que crea su servicio inteligente.

### Experimente con la fórmula

Con una fórmula que incorpora los algoritmos principales de aprendizaje automático, se pueden crear muchas instancias de fórmula con una sola fórmula. Estas instancias de fórmula se denominan modelos. Un modelo requiere capacitación y evaluación para optimizar su eficacia y eficiencia operativa, un proceso que normalmente consiste en pruebas y errores.

![](./images/home/recipe_hiearchy_ui.png)

A medida que imparte formación a los modelos, se generan ejecuciones de formación y evaluaciones. [!DNL Data Science Workspace] realiza un seguimiento de las métricas de evaluación para cada modelo único y sus ejecuciones de formación. Las métricas de evaluación generadas a través de la experimentación le permitirán determinar la ejecución de capacitación que mejor rendimiento tiene.

![](./images/home/evaluation_metrics.png)

Visite o bien [API](./models-recipes/train-evaluate-model-api.md) o [IU](./models-recipes/train-evaluate-model-ui.md) tutorial sobre cómo entrenar y evaluar modelos en [!DNL Data Science Workspace].

### Operacionalizar el modelo

Cuando haya seleccionado la fórmula mejor capacitada para satisfacer sus necesidades empresariales, puede crear un servicio inteligente en [!DNL Data Science Workspace] sin asistencia para desarrolladores. Son solo un par de clics - no se requiere código. Otros miembros de su organización pueden acceder a un servicio inteligente publicado sin necesidad de volver a crear el modelo.

Un servicio inteligente publicado se puede configurar para que se entrene automáticamente de vez en cuando con nuevos datos a medida que estén disponibles. Esto garantiza que su servicio mantenga su eficiencia y eficacia a medida que el tiempo continúa.

## Pasos siguientes

[!DNL Data Science Workspace] ayuda a optimizar y simplificar el flujo de trabajo de la ciencia de datos, desde la recopilación de datos a los algoritmos hasta los servicios inteligentes para los científicos de datos de todos los niveles de cualificación. Con las herramientas sofisticadas [!DNL Data Science Workspace] proporciona, puede acortar en gran medida el tiempo desde los datos hasta las perspectivas.

Más importante aún, [!DNL Data Science Workspace] pone las capacidades de optimización algorítmica y de ciencia de datos de la plataforma de marketing líder de Adobe en manos de científicos de datos empresariales. Por primera vez, las empresas pueden aportar algoritmos propios a la plataforma, aprovechando las potentes capacidades de aprendizaje automático y de IA de Adobe para ofrecer experiencias de cliente altamente personalizadas a escala masiva.

Con la combinación de experiencia de marca y el aprendizaje automático de los Adobes y la habilidad IA, las empresas tienen el poder de impulsar más valor comercial y lealtad de marca dando a los clientes lo que desean, antes de pedirlo.

Para obtener información adicional, como un flujo de trabajo diario completo, comience por leer la [Introducción a Data Science Workspace](./walkthrough.md) documentación.

## Recursos adicionales

El siguiente vídeo está diseñado para admitir su comprensión de [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)