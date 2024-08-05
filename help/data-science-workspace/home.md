---
keywords: Experience Platform; hogar; Data Science Espacio de trabajo; temas populares; ciencia de datos espacio de trabajo; Ciencia de datos
solution: Experience Platform
title: Información general de Data Science Espacio de trabajo
description: Este guía proporciona una visión general de los conceptos clave relacionados con la ciencia de datos Espacio de trabajo en Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 0%

---

# Información general del espacio de trabajo de ciencia de datos

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos anteriores a Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] utiliza aprendizaje automático e inteligencia artificial para obtener información de sus datos. Integrado en Adobe Experience Platform, [!DNL Data Science Workspace] le ayuda a hacer predicciones utilizando sus recursos de contenido y datos en las soluciones de Adobe.

Los científicos de datos de todos los niveles de habilidad encontrarán herramientas sofisticadas y fáciles de usar que respaldan el rápido desarrollo, entrenamiento y ajuste de las recetas de aprendizaje automático -todos los beneficios de la tecnología de IA, sin la complejidad.

Con [!DNL Data Science Workspace], los científicos de datos pueden crear fácilmente API de servicios inteligentes con tecnología de aprendizaje automático. Estos servicios funcionan con otros servicios de Adobe, incluidos Adobe Target y Adobe Analytics Cloud, para ayudarle a automatizar experiencias digitales personalizadas y específicas en aplicaciones web, de escritorio y móviles.

Este guía proporciona una visión general de los conceptos clave relacionados con [!DNL Data Science Workspace].

## Introducción

La empresa de hoy otorga una alta prioridad a la minería de big data de predicciones y conocimientos que les ayudarán a personalizar las experiencias de los clientes y ofrecer más valor a los clientes y al negocio.
Tan importante como es, pasar de los datos a la información puede tener un alto costo. Por lo general, requiere científicos de datos calificados que realicen investigaciones de datos intensivas y lentas para desarrollar modelos de aprendizaje automático, o recetas, que impulsen los servicios inteligentes. El proceso es largo, la tecnología es compleja y los científicos de datos calificados pueden ser difíciles de encontrar.

Con [!DNL Data Science Workspace], Adobe Experience Platform le permite llevar la IA centrada en la experiencia a toda la empresa, optimizando y acelerando la conversión de datos en información al código con:
- Un tiempo de ejecución y marco de trabajo de aprendizaje automático
- Acceso integrado a los datos almacenados en Adobe Experience Platform
- Un esquema de datos unificado basado en [!DNL Experience Data Model] (XDM)
- La potencia informática esencial para el aprendizaje automático/IA y la gestión de grandes conjuntos de datos
- Recetas de aprendizaje automático prediseñadas para acelerar el salto a experiencias impulsadas por IA
- Creación, reutilización y modificación simplificadas de recetas para científicos de datos de diversos niveles de habilidad
- Servicio inteligente que publica y comparte con solo unos pocos clics, sin un desarrollador, y monitoreo y reciclaje para la optimización continua de las experiencias personalizadas de los clientes

Los científicos de datos de todos los niveles de habilidad lograrán experiencias digitales más rápidas y efectivas antes.

## Introducción

Antes de sumergirse en los detalles de [!DNL Data Science Workspace], aquí tiene un breve resumen de los términos clave:

| Término | Definición |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] within [!DNL Experience Platform] permite a los clientes crear modelos de aprendizaje automático utilizando soluciones de datos y [!DNL Experience Platform] Adobe Systems para generar información inteligente y predicciones para tejer experiencias digitales de fin de usuario encantadoras. |
| Inteligencia artificial | La inteligencia artificial es una teoría y desarrollo de sistemas informáticos que son capaces de realizar tareas que normalmente requieren inteligencia humanos, como la percepción visual, el reconocimiento de voz, la toma de decisiones y la traducción entre idiomas. |
| Aprendizaje automático | El aprendizaje automático es el campo de estudio que permite a las computadoras la capacidad de aprender sin ser programadas explícitamente. |
| Marco de trabajo de [!DNL Sensei] ML | El módulo de aprendizaje automático de [!DNL Sensei] es un módulo de aprendizaje automático unificado en todo el Adobe que aprovecha los datos de [!DNL Experience Platform] para empoderar a los científicos de datos en el desarrollo de servicios de inteligencia impulsados por el aprendizaje automático de una manera más rápida, escalable y reutilizable. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) es el esfuerzo de estandarización liderado por el Adobe para definir esquemas estándar como [!DNL Profile] y [!DNL ExperienceEvent], para la administración de experiencias del cliente. |
| [!DNL JupyterLab] | [!DNL JupyterLab] es una interfaz basada en web de código abierto para Project Jupyter y está totalmente integrada en [!DNL Experience Platform]. |
| Fórmulas | Una fórmula es el término que utiliza el Adobe para una especificación de modelo y es un contenedor de nivel superior que representa un aprendizaje automático específico, un algoritmo de IA o un conjunto de algoritmos, una lógica de procesamiento y una configuración necesarios para crear y ejecutar un modelo entrenado y, por lo tanto, ayudar a resolver problemas empresariales específicos. |
| Modelo | Un modelo es una instancia de una fórmula de aprendizaje automático que se forma con datos históricos y configuraciones para resolver un caso de uso empresarial. |
| Aprendizaje | La formación es el proceso de aprendizaje de patrones y perspectivas a partir de datos etiquetados. |
| Modelo entrenado | Un modelo entrenado representa la salida ejecutable de un proceso de formación de modelos, en el que se aplicó un conjunto de datos de formación a la instancia del modelo. Un modelo entrenado mantendrá una referencia a cualquier servicio web inteligente que se cree a partir de él. El modelo entrenado es adecuado para puntuar y crear un servicio web inteligente. Las modificaciones realizadas en un modelo entrenado se pueden rastrear como una nueva versión. |
| Puntuación | La puntuación es el proceso de generar información a partir de los datos mediante un modelo entrenado. |
| Servicio | Un servicio implementado expone la funcionalidad de una inteligencia artificial, un modelo de aprendizaje automático o un algoritmo avanzado a través de una API, de modo que otros servicios o aplicaciones puedan consumirlos para crear aplicaciones inteligentes. |

El siguiente gráfico describe la relación jerárquica entre fórmulas, modelos, ejecuciones de formación y ejecuciones de puntuación.

![](./images/home/recipe_hiearchy_ui.png)

## Explicación [!DNL Data Science Workspace]

Con [!DNL Data Science Workspace], los científicos de datos pueden agilizar el engorroso proceso de descubrir información en grandes conjuntos de datos. Compilado en un marco de trabajo de aprendizaje automático y en tiempo de ejecución comunes, [!DNL Data Science Workspace] ofrece administración avanzada de flujos de trabajo, administración de modelos y escalabilidad. Los servicios inteligentes admiten la reutilización de fórmulas de aprendizaje automático para impulsar una variedad de aplicaciones creadas con productos y soluciones de Adobe.

### Acceso a datos en un solo paso

Los datos son la piedra angular de la IA y del aprendizaje automático.

[!DNL Data Science Workspace] está totalmente integrado con Adobe Experience Platform, incluido el lago de datos [!DNL Real-Time Customer Profile] y [!DNL Unified Edge]. Explore todos los datos de su organización almacenados en Adobe Experience Platform a la vez, junto con big data comunes y bibliotecas de aprendizaje profundo, como [!DNL Spark] ML y [!DNL TensorFlow]. Si no encuentra lo que necesita, introduzca sus propios conjuntos de datos mediante el esquema estandarizado XDM.

### Fórmulas de aprendizaje automático prediseñadas

[!DNL Data Science Workspace] incluye fórmulas de aprendizaje automático prediseñadas para necesidades comerciales comunes, como la predicción de ventas minoristas y la detección de anomalías, de modo que los científicos y desarrolladores de datos no tengan que empezar desde cero. Actualmente se ofrecen tres recetas, [predicción de compra de productos](./pre-built-recipes/product-purchase-prediction.md), [recomendaciones de productos](./pre-built-recipes/product-recommendations.md) y [ventas minoristas](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Si lo prefiere, puede adaptar una fórmula prediseñada a sus necesidades, importar una fórmula o inicio desde cero para versión una fórmula personalizada. Independientemente de cómo comience, una vez que entrene e hiperajuste un fórmula, crear un servicio inteligente personalizado no requiere un desarrollador, solo unos pocos clics y estará listo para versión un experiencia digital específico y personalizado.

### Flujo de trabajo centrado en el científico de datos

Sea cual sea su nivel de experiencia en ciencia de datos, [!DNL Data Science Workspace] ayuda a simplificar y acelerar el proceso de encontrar información en datos y aplicarla a experiencias digitales.

### Exploración de datos

Encontrar los datos adecuados y prepararlos es la parte más laboriosa de crear una receta eficaz. [!DNL Data Science Workspace] y Adobe Experience Platform le ayudarán a pasar de los datos a las perspectivas con mayor rapidez.

En Adobe Experience Platform, los datos de canales cruzados están centralizados y almacenados en el esquema estandarizado XDM, por lo que los datos son más fáciles de encontrar, comprender y limpiar. Un único almacén de datos basado en un esquema común puede ahorrarle incontables horas de exploración y preparación de datos.

Mientras explora, use R, [!DNL Python] o Scala con el [!DNL Jupyter Notebook] integrado y alojado para examinar el catálogo de datos de [!DNL Platform]. Con uno de estos lenguajes, también puede aprovechar [!DNL Spark] ML y TensorFlow. Comience desde cero o utilice una de las plantillas de portátiles que se proporcionan para problemas específicos de la empresa.

Como parte del flujo de trabajo de exploración de datos, también puede introducir nuevos datos o utilizar las funciones existentes para ayudar a preparar los datos.

### Creación

Con [!DNL Data Science Workspace], usted decide cómo desea crear las fórmulas.

- Guardar vez buscando una fórmula prediseñada que satisfaga sus necesidades empresariales, que puede usar tal cual o configurar para satisfacer sus requisitos específicos.
- Crear un fórmula desde cero, usando el tiempo de ejecución de creación en Jupyter Notebook para desarrollar y registrar el fórmula.
- Cargue un código de fórmula externo Adobe Experience Platform o [!DNL Data Science Workspace] impórtelo fórmula desde una repositorio, como [!DNL Git], mediante la autenticación y la integración disponibles entre [!DNL Git] y [!DNL Data Science Workspace].

### Experimentación

Data Science Espacio de trabajo aporta una tremenda flexibilidad al proceso de experimentación. Inicio con sus fórmula. A continuación, cree un instancia independiente, utilizando el mismo algoritmo central emparejado con características únicas, como parámetros de hiperajuste. Puede crear tantas instancias como necesite, aprendizaje y puntuando cada instancia tantas veces como desee. A medida que los entrena, [!DNL Data Science Workspace] realiza un seguimiento de las recetas, las instancias de fórmula y las instancias entrenadas, junto con las métricas de evaluación, para que usted no tenga que hacerlo.

### Operacionalización

Cuando esté satisfecho con su fórmula, son solo unos pocos clics para crear un servicio inteligente. No requiere codificación: puede hacerlo usted mismo, sin tener que contratar a un desarrollador o ingeniero. Finalmente, publicar el servicio inteligente a Adobe Systems E/S y estará listo para que su experiencia equipo digital lo consuma.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Mejora continua

[!DNL Data Science Workspace] rastrea dónde se invocan los servicios inteligentes y su rendimiento. A medida que se acumulan los datos, puede evaluar la precisión inteligente del servicio para cerrar el bucle y volver a entrenar las fórmulas según sea necesario para mejorar el rendimiento. El resultado es un refinamiento continuo de la precisión de la personalización del cliente.

### Acceso a nuevas funciones y conjuntos de datos

Los científicos de datos pueden aprovechar las nuevas tecnologías y conjuntos de datos tan pronto como estén disponibles a través de Adobe Systems servicios. A través de actualizaciones frecuentes, hacemos el trabajo de integrar conjuntos de datos y tecnologías en la plataforma, para que usted no tenga que hacerlo.

### Seguridad y tranquilidad

Proteger sus datos es una prioridad para Adobe Systems. Adobe Systems protege sus datos con procesos y controles de seguridad desarrollados para ayudar a cumplir con los estándares, regulaciones y certificaciones aceptados por la industria.

La seguridad está integrada en el software y los servicios como parte del ciclo de vida del producto Adobe Systems Secure.
Para obtener información sobre Adobe Systems seguridad de datos y software, cumplimiento y más, visita el Página de seguridad en https://www.adobe.com/security.html.

## [!DNL Data Science Workspace] en acción

Las predicciones y las perspectivas proporcionan la información que necesita para ofrecer una experiencia altamente personalizada a cada cliente que visita su sitio web, se pone en contacto con su centro de llamadas o participa en otras experiencias digitales. Así es como se realiza el trabajo diario con [!DNL Data Science Workspace].

### Defina el problema

Todo comienza con un problema de negocios. Por ejemplo, un centro de llamadas en línea necesita contexto para ayudarles a convertir en positivo un sentimiento negativo del cliente.

Hay un montón de datos sobre el cliente. Han explorado el sitio, puesto artículos en su carro de compras e incluso realizado pedidos. Es posible que hayan recibido correos electrónicos, utilizado cupones o contactado anteriormente con el centro de llamadas. El fórmula, entonces, necesita usar los datos disponibles sobre el cliente y sus actividades para determinar la propensión a comprar y recomendar un oferta que el cliente probablemente aprecie y use.

![](./images/home/example_problem.png)

En el momento del contacto con el centro de llamadas, el cliente aún tiene dos pares de zapatos en el carro, pero se quitó una camisa. Con esta información, el servicio inteligente podría recomendar que el agente del centro de llamadas ofrezca un cupón de descuento del 20 % en zapatos durante la llamada. Si el cliente utiliza el cupón, esa información se añade al conjunto de datos y las predicciones mejoran aún más la próxima vez que el cliente invoque.

### Exploración y preparación de los datos

En función del problema empresarial definido, sabe que la fórmula debe buscar en todas las transacciones web del cliente, incluidas las visitas al sitio, las búsquedas, las vistas de página, los vínculos en los que se hizo clic, las acciones del carro de compras, las ofertas recibidas, los correos electrónicos recibidos, las interacciones del centro de llamadas, etc.

Un científico de datos generalmente pasa hasta el 75% del tiempo requerido para crear una fórmula explorar y transformar los datos. Los datos a menudo provienen de múltiples repositorios y se guardan en diferentes esquemas: deben combinarse y asignarse antes de que puedan usarse para crear un fórmula.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Si está comenzando desde cero o configurando un fórmula existente, comience su búsqueda de datos en un catálogo de datos centralizado y estandarizado para su organización, lo que simplifica considerablemente la búsqueda. Es posible que igualado descubra que otro científico de datos de su organización ya ha identificado un conjunto de datos similar y elija ajustar ese conjunto de datos en lugar de inicio desde cero.
Todos los datos en Adobe Experience Platform cumplen con un esquema XDM estandarizado, eliminando la necesidad de crear un modelo complejo para unir datos u obtener ayuda de un ingeniero de datos.

Si no encuentra inmediatamente los datos que necesita, pero existen fuera de Adobe Experience Platform, es una tarea relativamente simple de ingerir conjuntos de datos adicionales, que también se transformarán en el esquema XDM estandarizado.\
Puede utilizarlo [!DNL Jupyter Notebook] para simplificar el procesamiento previo de datos, posiblemente comenzando con un plantilla de computadora portátil o una computadora portátil que haya utilizado anteriormente por propensión a comprar.

![](./images/home/notebook_templates-new.png)

### Crear la fórmula

Si ya ha encontrado una fórmula que satisfaga todas sus necesidades, puede pasar a la experimentación. O bien, puede modificar la fórmula un poco o crear una desde cero, aprovechando el tiempo de ejecución de la creación de [!DNL Data Science Workspace] en [!DNL Jupyter Notebook]. El uso del tiempo de ejecución de la creación garantiza que puede usar el flujo de trabajo de formación y puntuación [!DNL Data Science Workspace] y convertir la fórmula más adelante para que otros usuarios de su organización puedan almacenarla y reutilizarla.

También puede importar una fórmula en [!DNL Data Science Workspace] y aprovechar los flujos de trabajo de experimentación al crear su servicio inteligente.

### Experimente con la fórmula

Con una fórmula que incorpora los algoritmos principales de aprendizaje automático, se pueden crear muchas instancias de fórmula con una sola fórmula. Estas instancias de fórmula se denominan modelos. Un modelo requiere entrenamiento y evaluación para optimizar su eficiencia y eficacia operativa, un proceso típicamente consistente en prueba y error.

![](./images/home/recipe_hiearchy_ui.png)

A medida que entrena los modelos, se generan ejecuciones de formación y evaluaciones. [!DNL Data Science Workspace] realiza un seguimiento de las métricas de evaluación de cada modelo único y de sus ejecuciones de formación. Las métricas de evaluación generadas a través de la experimentación le permitirán determinar la ejecución de formación que tenga el mejor rendimiento.

![](./images/home/evaluation_metrics.png)

Visite el tutorial de [API](./models-recipes/train-evaluate-model-api.md) o [IU](./models-recipes/train-evaluate-model-ui.md) sobre cómo entrenar y evaluar modelos en [!DNL Data Science Workspace].

### Poner en funcionamiento el modelo

Una vez que haya seleccionado la fórmula mejor preparada para satisfacer las necesidades de su empresa, puede crear un servicio inteligente en [!DNL Data Science Workspace] sin la ayuda del desarrollador. Son solo un par de clics, no se requiere codificación. Un servicio inteligente publicado es accesible para otros miembros de su organización sin necesidad de volver a crear el modelo.

Un servicio inteligente publicado es configurable para entrenarse automáticamente de vez en cuando utilizando nuevos datos a medida que estén disponibles. Esto garantiza que su servicio mantenga su eficiencia y eficacia a medida que pasa el tiempo.

## Pasos siguientes

[!DNL Data Science Workspace] Ayuda a agilizar y simplificar el flujo de trabajo de ciencia de datos, desde la recopilación de datos hasta los algoritmos y los servicios inteligentes para científicos de datos de todos los niveles de habilidad. Con las sofisticadas herramientas que proporciona [!DNL Data Science Workspace], puede reducir considerablemente el tiempo que transcurre desde los datos hasta las perspectivas.

Lo que es más importante, [!DNL Data Science Workspace] pone las capacidades de optimización algorítmica y de ciencia de datos de la plataforma de marketing líder de Adobe en manos de los científicos de datos empresariales. Por primera vez, las empresas pueden incorporar algoritmos propietarios a la plataforma, aprovechando el potente aprendizaje automático y las capacidades de IA de Adobe para ofrecer experiencias de cliente altamente personalizadas a escala masiva.

Gracias a la combinación de la experiencia de marca y el aprendizaje automático y las habilidades de IA de Adobe, las empresas tienen el poder de impulsar más valor empresarial y lealtad de marca dando a los clientes lo que desean antes de que lo soliciten.

Para obtener información adicional, como un flujo de trabajo diario completo, comience por leer la [documentación de Data Science Workspace](./walkthrough.md).

## Recursos adicionales

El siguiente vídeo está diseñado para ayudarle a comprender [!DNL Data Science Workspace]mejor .

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)