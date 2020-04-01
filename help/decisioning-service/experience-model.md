---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: modelo de dominio de decisiones de experiencia
topic: overview
translation-type: tm+mt
source-git-commit: 0f13ea667eecf936c69bcd98b0035a4355d73631

---


# modelo de dominio de decisiones de experiencia

En esta sección se explican los componentes del servicio de toma de decisiones y se detallan las formas en que interactúan esos componentes. Los conceptos y sus relaciones forman el *Dominio* del problema de toma de decisiones. Estos componentes fundamentales entran en juego independientemente de cómo utilice el servicio de toma de decisiones.

## Opciones de decisión

Una opción *de* decisión de experiencia es una experiencia potencial que se puede presentar a un cliente específico. Una opción también se denomina opción o alternativa. Al decidir la siguiente mejor opción para un cliente, el servicio de decisiones considera las opciones ***d<sub>1</sub>***a***<sub>dN</sub>*** entre un conjunto finito de opciones **`D`**.

Las decisiones se toman identificando la mejor opción entre un conjunto de opciones disponibles. Un enfoque es eliminar sucesivamente las opciones *de* decisión ***<sub>di</sub>***desde el conjunto de*** D ***hasta que solo quede uno y luego elija un &quot;ganador&quot; al azar del conjunto restante. Otra forma de toma de decisiones es clasificar las opciones de decisión restantes (elegibles) según el resultado esperado.

### Conjunto finito de opciones de decisión

En el dominio de decisiones de experiencias, las opciones desde las que se seleccionan una o varias existen a priori y, al calcular una decisión, no se crean nuevas opciones sobre la marcha. Decimos que el dominio de las opciones es finito en el momento en que se toman las decisiones. Esto puede parecer una limitación, pero un conjunto finito de opciones da lugar a la posibilidad de utilizar algoritmos de aprendizaje automático y técnicas similares para decidir cuál de las opciones es &quot;la mejor&quot;. Muchos algoritmos de aprendizaje no podrían producir una mejor opción entre un conjunto de alternativas infinitas que no se pueden comparar entre sí y para las que no existen datos de muestra.

## Resultados de las decisiones

Es importante diferenciar entre el resultado de la decisión `d` y el resultado `o`, es decir, los resultados previstos que se estipulan en la decisión. Una decisión a menudo no puede producir un resultado directamente. La decisión es sólo seleccionar (o proponer) la opción con el mejor resultado esperado. Entre propuestas y resultados se producen muchos eventos e interacciones, que a menudo se retrasan días o semanas. En términos más formales, el resultado es una función de la decisión `o = f(d)`.

Para encontrar la decisión óptima, a cada resultado se le asigna un valor ***de*** utilidad `U(o) = U(f(d))`.
En el caso de uso de la decisión de Oferta, esa función calcularía el coste para cumplir la oferta y el valor obtenido por la empresa cuando la oferta es aceptada por el cliente. El resultado se utilizaría para encontrar la decisión óptima (oferta) maximizando el valor de la utilidad sobre todas las opciones (ofertas).

Por lo general, no es posible predecir con certeza cuál será el resultado de una decisión determinada y, por tanto, es necesario un enfoque probabilístico. El valor ***de*** utilidad `U(o)` se convierte en el valor de utilidad ***esperado de una opción*** de decisión `EU(d)`

## Propuestas de decisión

Una propuesta *de* decisión es una selección de opciones de decisión que se hizo en respuesta a una solicitud de decisión real. Como se ha indicado anteriormente, los resultados de una decisión pueden producirse mucho más tarde y los resultados tampoco pueden lograrse en un solo paso. Por lo tanto, es importante seguir las propuestas mediante diversos eventos *de* experiencia para que se puedan atribuir a las opciones de decisión. Este bucle de retroalimentación se utiliza para mejorar la precisión de predicción de `EU(d)`.

Una propuesta se mantiene como una entidad y, por lo tanto, tiene un identificador. La entidad contiene referencias a las opciones seleccionadas y puede registrar los datos de contexto que se utilizaron para tomar la decisión. Tener un identificador también permite que otras entidades hagan referencia a él. Una de esas entidades es el evento *de* decisión. Tiene la marca de fecha y hora, marcando cuando se tomó su decisión (propuesta). Un evento de decisión es un hecho registrado de la acción de ejecución de la decisión. Otros eventos que hacen referencia a la entidad de propuesta son los eventos de experiencia. Todos los eventos de experiencia pueden ampliarse para hacer referencia a una propuesta de decisión. La interpretación de hacerlo es que el evento de la experiencia puede atribuirse total o parcialmente a la propuesta de la decisión.

## Estrategia de decisión - Algoritmo

Con un conjunto finito de alternativas para elegir, cada estrategia *de* decisión es esencialmente un algoritmo - o una función - que toma **`N`** opciones de decisión *{d<sub>1</sub>, d<sub>2</sub>, ...<sub>dN</sub>* *<sub></sub><sub></sub><sub></sub>* }como entrada y produce una lista clasificada de opciones de decisión (dr1, dr2taquígrafo.... )según la cual la opción de la primera decisión de la lista se considera óptima según una utilidad prevista, la segunda opción de la lista resultante se considera entonces la segunda mejor opción y así sucesivamente. Generalmente, el conjunto tendrá una cardinalidad mayor que la lista clasificada resultante, ya que el algoritmo de decisión elimina las opciones que no son elegibles y un algoritmo puede configurarse para que solo devuelva las opciones principales, deteniéndose después de encontrar suficientes opciones. **`K`** 
El marco general de decisión se muestra en el diagrama siguiente.

![Fig. 1](./images/decisioning-optimization.png)

## Actividades de decisión

*Las actividades* de decisión configuran el algoritmo y proporcionan parámetros para una estrategia de decisión específica. Los parámetros de estrategia incluyen las restricciones aplicadas a las opciones y a la función de clasificación. Todas las decisiones se adoptan en el contexto de una actividad. El servicio de toma de decisiones aloja muchas actividades y las actividades se pueden reutilizar en todos los canales. En cualquier momento dado, la mejor opción se evalúa en función del conjunto más reciente de restricciones, reglas y modelos.

Una actividad de decisión define la recopilación de las opciones de decisión que se han de considerar. filtros el subconjunto de todas las opciones que son de interés para esta actividad. Esto permite que el servicio de toma de decisiones administre categorías de temas dentro del catálogo de todas las opciones.

Una actividad de decisión especifica una opción *de* reserva en caso de que las restricciones combinadas descalifiquen todas las demás opciones. Esto significa que siempre hay una respuesta a la pregunta: ¿Cuál es actualmente la opción &quot;mejor&quot;?

Las actividades de decisión pueden especificar el lugar en el que se entrega la experiencia. Esto reduce aún más el número de opciones de decisión que pueden considerarse y es otra limitación impuesta por la actividad de decisión. Esto se denomina restricción *de* colocación. Solo se tendrán en cuenta las opciones de decisión que tengan contenido que cumpla esta restricción de colocación. Esto se evalúa en las primeras etapas de la estrategia de decisión. Cuando las definiciones cambian las restricciones de colocación de cada actividad de decisión se vuelven a evaluar y la opción de decisión puede entrar o quedar fuera de consideración para una o más actividades de decisión.

## Contexto de la decisión

Hasta ahora, sólo se describió la *lógica* empresarial que afecta la decisión. Pero aún más impactante para el resultado son los *datos* de entrada de la decisión. Estos datos se denominan contexto *de* decisión y son diferentes para cada usuario y cada vez que se toma una decisión, a diferencia de las restricciones, reglas y modelos que son iguales para los distintos usuarios de la misma actividad. Las reglas, restricciones y modelos también cambian con menos frecuencia. Para la toma de decisiones en tiempo real, el contexto de las decisiones también deberá determinarse en tiempo real.

Los datos de contexto de decisión pueden dividirse en datos relacionados con el perfil del usuario, datos comerciales y datos recopilados internamente.

- *Las entidades* de Perfil se utilizan para representar los datos del usuario final, pero no todas las entidades de perfil representan a un individuo. Podría ser un hogar, un grupo social o cualquier otro tema. Los eventos de experiencias son registros de datos de serie temporal adjuntos a un perfil. Si hay una experiencia, estos datos son el *tema* de esta experiencia.
- Por otro lado, están las entidades *comerciales*. Se pueden considerar como los *objetos* de las interacciones. A menudo se hace referencia a esas entidades en los eventos de experiencia de las entidades de perfil. Ejemplos de entidades comerciales son sitios web y páginas, tiendas, detalles de productos, contenido digital, datos de inventario de productos, etc.
- La última categoría de datos en el contexto de la decisión son los datos que se crearon durante el funcionamiento del servicio de decisiones. Todos los eventos de decisión entran en esa categoría, junto con las respuestas de los clientes, los datos de propuesta forman un conjunto de datos internos denominado el historial *de* proposición-respuesta.

Existen tres rutas que los datos pueden tomar para convertirse en parte del contexto de decisión. Los datos de registros y series temporales se pueden cargar mediante archivos de conjuntos de datos. Esta ruta es principalmente para la sincronización masiva con sistemas externos. Los datos de registros y series temporales también se pueden transmitir a la plataforma donde los datos se indizan y se unen a las entidades de formulario. A través de la tercera ruta, los datos de contexto se pueden pasar como parámetros a la solicitud de decisión. Esta forma de datos es efímera y sólo es pertinente para la decisión solicitada. No se mantiene como entidad y no está disponible para otras solicitudes.
