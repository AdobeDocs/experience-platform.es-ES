---
keywords: Experience Platform;inicio;Área de trabajo de ciencia de datos;temas populares;área de trabajo de ciencia de datos;ciencia de datos
solution: Experience Platform
title: Información general del área de trabajo de ciencias de datos
topic: overview
description: Esta guía proporciona información general sobre los conceptos clave relacionados con el espacio de trabajo de ciencia de datos en Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 0%

---


# Información general sobre el área de trabajo de ciencias de datos

Adobe Experience Platform [!DNL Data Science Workspace] utiliza el aprendizaje automático y la inteligencia artificial para generar perspectivas a partir de los datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a realizar predicciones mediante el uso de sus recursos de contenido y datos en las soluciones de Adobe.

Los científicos de datos de todos los niveles encontrarán herramientas sofisticadas y fáciles de usar que apoyen el rápido desarrollo, la capacitación y el ajuste de las recetas de aprendizaje automático -todos los beneficios de la tecnología de IA, sin la complejidad.

Con [!DNL Data Science Workspace], los científicos de datos pueden crear fácilmente API de servicios inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otros servicios de Adobe, incluidos Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar las experiencias digitales personalizadas y dirigidas en aplicaciones web, de escritorio y móviles.

Esta guía proporciona una visión general de los conceptos clave relacionados con [!DNL Data Science Workspace].

## Introducción

La empresa de hoy da una alta prioridad a la extracción de grandes datos para predicciones y perspectivas que los ayudarán a personalizar las experiencias de los clientes y a ofrecer más valor a los clientes y al negocio.
Por importante que sea, pasar de los datos a las perspectivas puede tener un alto costo. Generalmente requiere de científicos de datos capacitados que realicen investigaciones intensivas y que requieran mucho tiempo para desarrollar modelos o fórmulas de aprendizaje automático que impulsen los servicios inteligentes. El proceso es largo, la tecnología es compleja y los científicos de datos calificados pueden ser difíciles de encontrar.

Con [!DNL Data Science Workspace], Adobe Experience Platform le permite brindar IA centrada en la experiencia en toda la empresa, lo que optimiza y acelera la conversión de datos a perspectivas en código con:
- Un entorno de aprendizaje automático y tiempo de ejecución
- Acceso integrado a los datos almacenados en Adobe Experience Platform
- Un esquema de datos unificado creado en [!DNL Experience Data Model] (XDM)
- La potencia informática esencial para el aprendizaje automático/IA y la administración de grandes conjuntos de datos
- Fórmulas de aprendizaje automático prediseñadas para acelerar el salto a experiencias impulsadas por AI
- Creación, reutilización y modificación simplificadas de recetas para científicos de datos de diferentes niveles de aptitud
- Publicación y uso compartido de servicios inteligentes con sólo unos pocos clics (sin programador) y supervisión y readiestramiento para la optimización continua de las experiencias personalizadas de los clientes

Los científicos de datos de todos los niveles de habilidades obtendrán perspectivas digitales más rápidas y efectivas antes.

## Primeros pasos

Antes de profundizar en los detalles de [!DNL Data Science Workspace], aquí hay un breve resumen de los términos clave:

| Término | Definición |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] dentro de  [!DNL Experience Platform] permite a los clientes crear modelos de aprendizaje automático utilizando datos en las soluciones de Adobe  [!DNL Experience Platform] y en todas partes para generar perspectivas y predicciones inteligentes y crear experiencias digitales de usuario final deliciosas. |
| Inteligencia artificial | La inteligencia artificial es una teoría y un desarrollo de sistemas informáticos capaces de realizar tareas que normalmente requieren inteligencia humana, como la percepción visual, el reconocimiento del habla, la toma de decisiones y la traducción entre idiomas. |
| Aprendizaje automático | El aprendizaje automático es el campo de estudio que permite a las computadoras aprender sin programarse explícitamente. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework es un sistema de aprendizaje automático unificado en todo el Adobe que aprovecha los datos  [!DNL Experience Platform] para empoderar a los científicos de datos en el desarrollo de servicios de inteligencia impulsados por el aprendizaje automático de manera más rápida, escalable y reutilizable. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) es el esfuerzo de estandarización liderado por el Adobe para definir esquemas estándar como  [!DNL Profile] y  [!DNL ExperienceEvent], para la administración de la experiencia del cliente. |
| [!DNL JupyterLab] | [!DNL JupyterLab] es una interfaz web de código abierto para Project Jupyter y está estrechamente integrada en  [!DNL Experience Platform]. |
| Fórmulas | Una fórmula es el término de Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo AI o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarias para crear y ejecutar un modelo capacitado y, por tanto, ayuda a resolver problemas comerciales específicos. |
| Modelo | Un modelo es una instancia de una fórmula de aprendizaje automático que se capacita mediante datos históricos y configuraciones para resolver un caso de uso comercial. |
| Capacitación | La formación es el proceso de aprendizaje de patrones y perspectivas a partir de datos etiquetados. |
| Modelo capacitado | Un modelo formado representa el resultado ejecutable de un proceso de formación de modelo, en el que se aplicó un conjunto de datos de formación a la instancia de modelo. Un modelo capacitado mantendrá una referencia a cualquier servicio Web inteligente que se cree a partir de él. El modelo entrenado es adecuado para la puntuación y la creación de un servicio Web inteligente. Las modificaciones de un modelo capacitado se pueden rastrear como una nueva versión. |
| Puntuación | La puntuación es el proceso de generación de perspectivas a partir de datos mediante un modelo capacitado. |
| Service | Un servicio implementado expone la funcionalidad de una inteligencia artificial, un modelo de aprendizaje automático o un algoritmo avanzado a través de una API para que otros servicios o aplicaciones puedan utilizarla para crear aplicaciones inteligentes. |

El siguiente gráfico describe la relación jerárquica entre Fórmulas, Modelos, Ejecuciones de formación y Ejecuciones de puntuación.

![](./images/home/recipe_hiearchy_ui.png)

## Explicación [!DNL Data Science Workspace]

Con [!DNL Data Science Workspace], los científicos de datos pueden optimizar el proceso engorroso de descubrir perspectivas en grandes conjuntos de datos. Basado en un entorno de aprendizaje automático y un tiempo de ejecución comunes, [!DNL Data Science Workspace] ofrece administración avanzada de flujos de trabajo, administración de modelos y escalabilidad. Los servicios inteligentes admiten la reutilización de las fórmulas de aprendizaje automático para potenciar diversas aplicaciones creadas con productos y soluciones de Adobe.

### Acceso a datos de un solo nivel

Los datos son la piedra angular de la IA y el aprendizaje automático.

[!DNL Data Science Workspace] está completamente integrado con Adobe Experience Platform, incluyendo Data Lake,  [!DNL Real-time Customer Profile]y  [!DNL Unified Edge]. Explore todos los datos de su organización almacenados en Adobe Experience Platform a la vez, junto con grandes datos comunes y bibliotecas de aprendizaje profundo, como [!DNL Spark] ML y [!DNL TensorFlow]. Si no encuentra lo que necesita, ingrese sus propios conjuntos de datos utilizando el esquema estandarizado XDM.

### Fórmulas de aprendizaje automático precompiladas

[!DNL Data Science Workspace] incluye fórmulas de aprendizaje automático prediseñadas para necesidades comerciales comunes, como la predicción de ventas minoristas y la detección de anomalías, de modo que los científicos y desarrolladores de datos no tienen que tener que realizar inicios desde cero. Actualmente se ofrecen tres fórmulas: [predicción de compra de productos](./pre-built-recipes/product-purchase-prediction.md), [recomendaciones de productos](./pre-built-recipes/product-recommendations.md) y [ventas minoristas](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si lo prefiere, puede adaptar una fórmula prediseñada a sus necesidades, importar una fórmula o un inicio desde cero para crear una fórmula personalizada. Sin embargo, una vez que se enseña y se pone a punto una fórmula, la creación de un servicio inteligente personalizado no requiere de un desarrollador, sólo unos clics y está listo para crear una experiencia digital personalizada y dirigida.

### Flujo de trabajo centrado en el científico de datos

Cualquiera que sea su nivel de experiencia en ciencia de datos, [!DNL Data Science Workspace] ayuda a simplificar y acelerar el proceso de encontrar perspectivas en los datos y aplicarlas a las experiencias digitales.

### Exploración de datos

Encontrar los datos adecuados y prepararlos es la parte más trabajadora para crear una fórmula efectiva. [!DNL Data Science Workspace] y Adobe Experience Platform le ayudará a pasar de los datos a las perspectivas más rápidamente.

En Adobe Experience Platform, los datos de canales cruzados están centralizados y almacenados en el esquema estandarizado XDM, por lo que los datos son más fáciles de encontrar, comprender y limpiar. Un único almacén de datos basado en un esquema común puede ahorrarle innumerables horas de exploración y preparación de datos.

A medida que navega, utilice R, [!DNL Python] o Scala con el [!DNL Jupyter Notebook] host integrado para explorar el catálogo de datos en [!DNL Platform]. Con uno de estos idiomas, también puede aprovechar [!DNL Spark] ML y TensorFlow. Inicio desde cero o utilice una de las plantillas de portátiles proporcionadas para problemas empresariales específicos.

Como parte del flujo de trabajo de exploración de datos, también puede ingestar datos nuevos o utilizar funciones existentes para ayudar en la preparación de datos.

### Creación

Con [!DNL Data Science Workspace], usted decide cómo desea crear las fórmulas.

- Ahorre tiempo buscando una fórmula prediseñada que satisfaga sus necesidades comerciales, que puede utilizar tal cual o configurar para satisfacer sus necesidades específicas.
- Cree una fórmula desde cero, utilizando el tiempo de ejecución de creación en Jupyter Notebook para desarrollar y registrar la fórmula.
- Cargue una fórmula creada fuera de Adobe Experience Platform en [!DNL Data Science Workspace] o importe el código de fórmula desde un repositorio, como [!DNL Git], mediante la autenticación y la integración disponibles entre [!DNL Git] y [!DNL Data Science Workspace].

### Experimentación

El espacio de trabajo de ciencia de datos aporta una gran flexibilidad al proceso de experimentación. Inicio con tu receta. A continuación, cree una instancia independiente, utilizando el mismo algoritmo principal emparejado con características únicas, como parámetros de ajuste híper. Puede crear tantas instancias como necesite, formando y anotando cada instancia tantas veces como desee. A medida que los capacita, [!DNL Data Science Workspace] rastrea fórmulas, instancias de fórmula e instancias formadas, junto con métricas de evaluación, para que no tenga que hacerlo.

### Operacionalización

Cuando estás satisfecho con tu fórmula, son sólo unos clics para crear un servicio inteligente. No se requiere codificación: puede hacerlo usted mismo, sin tener que contratar a un desarrollador o ingeniero. Por último, publique el servicio inteligente en E/S de Adobe y estará listo para que su equipo de experiencia digital lo consuma.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Mejora continua

[!DNL Data Science Workspace] rastrea dónde se invocan los servicios inteligentes y cómo funcionan. A medida que los datos entran en funcionamiento, puede evaluar la precisión inteligente del servicio para cerrar el bucle y volver a preparar las fórmulas según sea necesario para mejorar el rendimiento. El resultado es un refinamiento continuo en la precisión de la personalización del cliente.

### Acceso a nuevas funciones y conjuntos de datos

Los científicos de datos pueden aprovechar las nuevas tecnologías y conjuntos de datos en cuanto estén disponibles a través de los servicios de Adobe. A través de actualizaciones frecuentes, hacemos el trabajo de integrar datasets y tecnologías en la plataforma, para que no tenga que hacerlo.

### Seguridad y paz mental

La seguridad de los datos es una de las principales prioridades del Adobe. Adobe protege sus datos con los procesos y controles de seguridad desarrollados para ayudarle a cumplir con las normas, regulaciones y certificaciones aceptadas por el sector.

La seguridad está integrada en el software y los servicios como parte del ciclo de vida seguro del producto de Adobe.
Para obtener más información sobre la seguridad de los datos de Adobe y software, el cumplimiento de normas y más, visite la página de seguridad en https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] en acción

Las predicciones y perspectivas proporcionan la información necesaria para ofrecer una experiencia altamente personalizada a cada cliente que visite su sitio web, se ponga en contacto con su centro de llamadas o participe en otras experiencias digitales. Así es como su trabajo diario sucede con [!DNL Data Science Workspace].

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
Todos los datos de Adobe Experience Platform cumplen con un esquema XDM estandarizado, lo que elimina la necesidad de crear un modelo complejo para unir datos u obtener ayuda de un ingeniero de datos.

Si no encuentra inmediatamente los datos que necesita, pero existen fuera de Adobe Experience Platform, es una tarea relativamente simple para ingerir conjuntos de datos adicionales, que también se transformarán en el esquema XDM estandarizado.\
Puede utilizar [!DNL Jupyter Notebook] para simplificar el procesamiento previo de los datos, posiblemente comenzando con una plantilla de portátil o un bloc de notas que haya utilizado anteriormente para comprar.

![](./images/home/notebook_templates.png)

### Crear la fórmula

Si ya has encontrado una fórmula que satisfaga todas tus necesidades, puedes pasar a la experimentación. O bien, puede modificar un poco la fórmula o crear una desde cero, aprovechando el tiempo de ejecución de creación [!DNL Data Science Workspace] en [!DNL Jupyter Notebook]. El uso del tiempo de ejecución de creación garantiza que puede utilizar el flujo de trabajo de puntuación y formación [!DNL Data Science Workspace] y convertir la fórmula más adelante para que otras personas de su organización puedan almacenarla y reutilizarla.

También puede importar una fórmula en [!DNL Data Science Workspace] y aprovechar los flujos de trabajo de experimentación a medida que crea su servicio inteligente.

### Experimente con la fórmula

Con una fórmula que incorpora los algoritmos principales de aprendizaje automático, se pueden crear muchas instancias de fórmula con una sola fórmula. Estas instancias de fórmula se denominan modelos. Un modelo requiere capacitación y evaluación para optimizar su eficacia y eficiencia operativa, un proceso que normalmente consiste en pruebas y errores.

![](./images/home/recipe_hiearchy_ui.png)

A medida que imparte formación a sus modelos, se generan ejecuciones de formación y evaluaciones. [!DNL Data Science Workspace] realiza un seguimiento de las métricas de evaluación de cada modelo único y de sus ejecuciones de formación. Las métricas de evaluación generadas a través de la experimentación le permitirán determinar la ejecución de la capacitación que tenga el mejor rendimiento.

![](./images/home/evaluation_metrics.png)

Visite el tutorial [API](./models-recipes/train-evaluate-model-api.md) o [UI](./models-recipes/train-evaluate-model-ui.md) sobre cómo entrenar y evaluar modelos en [!DNL Data Science Workspace].

### Operacionalizar el modelo

Cuando haya seleccionado la fórmula mejor capacitada para satisfacer sus necesidades comerciales, puede crear un servicio inteligente en [!DNL Data Science Workspace] sin asistencia para desarrolladores. Son sólo un par de clics - no se requiere codificación. Otros miembros de la organización pueden acceder a un servicio inteligente publicado sin necesidad de volver a crear el modelo.

Un servicio inteligente publicado se puede configurar para formarse automáticamente de vez en cuando utilizando nuevos datos a medida que estén disponibles. Esto garantiza que su servicio mantenga su eficiencia y eficacia a medida que el tiempo continúa.

## Pasos siguientes

[!DNL Data Science Workspace] ayuda a optimizar y simplificar el flujo de trabajo de la ciencia de datos, desde la recopilación de datos hasta los algoritmos hasta los servicios inteligentes para los científicos de datos de todos los niveles de habilidades. Con las herramientas sofisticadas que ofrece [!DNL Data Science Workspace], puede reducir considerablemente el tiempo desde los datos hasta las perspectivas.

Lo que es más importante, [!DNL Data Science Workspace] pone las capacidades de optimización algorítmica y ciencia de datos de la plataforma de mercadotecnia líder del Adobe en manos de los científicos de datos empresariales. Por primera vez, las empresas pueden incorporar algoritmos propios a la plataforma, aprovechando las potentes capacidades de aprendizaje automático y de IA del Adobe para ofrecer experiencias de cliente altamente personalizadas a gran escala.

Con la combinación de conocimientos de marca y el aprendizaje automático y la destreza en IA de los Adobes, las empresas tienen el poder de impulsar más valor comercial y lealtad de marca dando a los clientes lo que desean, antes de pedirlo.

Para obtener información adicional, como un flujo de trabajo diario completo, lea la [documentación de paso de Área de trabajo de ciencias de datos](./walkthrough.md).

## Recursos adicionales

El siguiente vídeo está diseñado para admitir su comprensión de [!DNL Data Science Workspace].

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

