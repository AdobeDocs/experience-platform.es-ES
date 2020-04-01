---
keywords: Experience Platform;user guide;customer ai;popular topics
solution: Experience Platform
title: Guía del usuario de AI del cliente
topic: User guide
translation-type: tm+mt
source-git-commit: 7987cec12c22e9b48ddc9fdc263d7cd28bd172f2

---


# Guía del usuario de AI del cliente

La API del cliente, como parte de Servicios inteligentes, le permite generar puntuaciones de tendencia personalizadas sin tener que preocuparse por el aprendizaje automático.

En esta guía se explican los pasos para trabajar con la API del cliente. Se proporcionan pasos para los siguientes temas:

* [Configurar una instancia](#configure-an-instance)
* [Crear segmentos de clientes con puntuaciones predichas](#create-customer-segments-with-predicted-scores)

Además, el apéndice de este tutorial proporciona información sobre la [salida de la API](#customer-ai-output-data)del cliente.

## Configurar una instancia

Los servicios inteligentes ofrecen a los clientes un servicio de inteligencia artificial como un servicio de Adobe Sensei sencillo de usar que se puede configurar para diferentes casos de uso. Las siguientes secciones proporcionan los pasos para configurar una instancia de AI del cliente.

### Configurar la instancia

En la interfaz de usuario de la plataforma, haga clic en **Servicios** en el panel de navegación izquierdo. Aparece el navegador de **servicios** y muestra todos los servicios disponibles. En el contenedor de AI del cliente, haga clic en **Abrir**.

![](./images/user-guide/navigate-to-service.png)

La pantalla *de AI* del cliente muestra todas las instancias de AI del cliente existentes. Haga clic en **Crear instancia**.

![](./images/user-guide/dashboard.png)

Aparece el flujo de trabajo de creación de instancias, comenzando en el paso *Configuración* .

A continuación encontrará información importante sobre los valores con los que debe proporcionar la instancia:

* El nombre de la instancia se utiliza en todos los lugares donde se muestra la puntuación de AI del cliente. Por lo tanto, los nombres deben describir lo que las puntuaciones de predicción representan, por ejemplo, &quot;Probabilidad de cancelar la suscripción de la revista&quot;.

* El tipo de tendencia determina la intención de la puntuación y la polaridad de la métrica. Puede elegir entre **Corn** o **Conversión**. Consulte la nota en [resumen](./discover-insights.md#scoring-summary) de puntuación en el documento de perspectivas de descubrimiento para obtener más información sobre cómo afecta el tipo de tendencia a la instancia.

* La fuente de datos es la ubicación de los datos. Dataset es el conjunto de datos de entrada que se utiliza para predecir puntuaciones. Según el diseño, la API del cliente utiliza los datos del Evento de experiencias de consumo para calcular las puntuaciones de tendencia. Al seleccionar un conjunto de datos en el selector desplegable, solo se muestran los que son compatibles con la API del cliente.

* De forma predeterminada, se generan puntuaciones de tendencia para todos los perfiles, a menos que se especifique una población elegible. Puede especificar una población elegible definiendo condiciones para incluir o excluir perfiles en función de eventos.

Proporcione los valores necesarios y haga clic en **Siguiente**.

![](./images/user-guide/setup.png)

### Definir un objetivo

Aparece el paso *Definir objetivo* y proporciona un entorno interactivo para que usted pueda definir visualmente un objetivo. Un objetivo se compone de uno o más eventos, donde la incidencia de cada evento se basa en la condición que contiene. El objetivo de una instancia de AI de cliente es determinar la probabilidad de lograr su objetivo dentro de un intervalo de tiempo determinado.

Haga clic en **Especificar nombre** de campo y seleccione un campo en la lista desplegable. Haga clic en la segunda entrada y seleccione una cláusula para la condición del evento, luego proporcione un valor de destinatario para completar el evento. Para configurar eventos adicionales, haga clic en **Añadir evento**. Por último, complete el objetivo aplicando un intervalo de tiempo de predicción en número de días y, a continuación, haga clic en **Siguiente**.

![](./images/user-guide/goal.png)

### Configurar una programación *(opcional)*

Aparece el paso *avanzado* . Este paso opcional le permite configurar una programación para automatizar las ejecuciones de predicciones, definir exclusiones de predicciones para filtrar determinados eventos o hacer clic en **Finalizar** si no se necesita nada.

Configure un programa de puntuación configurando la frecuencia *de* puntuación. Las ejecuciones de predicciones automatizadas se pueden programar para que se ejecuten de forma semanal o mensual.

![](./images/user-guide/schedule.png)

Debajo de la configuración de programación, puede definir exclusiones de predicción para evitar que se evalúen eventos que cumplan determinadas condiciones al generar puntuaciones. Esta función se puede utilizar para filtrar las entradas de datos irrelevantes.

Para excluir determinados eventos, haga clic en **Añadir exclusión** y defina el evento de la misma manera que se define el objetivo. Para eliminar una exclusión, haga clic en las elipses (**...**) en la parte superior derecha del contenedor de evento y, a continuación, haga clic en **Eliminar Contenedor**.

![](./images/user-guide/exclusion.png)

Excluya eventos según sea necesario y haga clic en **Finalizar** para crear la instancia.

![](./images/user-guide/advanced.png)

Si la instancia se crea correctamente, se activa inmediatamente una ejecución de predicción y las ejecuciones posteriores se ejecutan según la programación definida.

>[!NOTE] Según el tamaño de los datos de entrada, las ejecuciones de predicciones pueden tardar hasta 24 horas en completarse.

Al seguir esta sección, ha configurado una instancia de AI del cliente y se ha ejecutado una ejecución de predicción. Una vez finalizada correctamente la ejecución, las perspectivas puntuadas rellenan automáticamente los perfiles con puntuaciones predichas. Espere hasta 24 horas antes de continuar con la siguiente sección de este tutorial.

## Crear segmentos de clientes con puntuaciones predichas

Cuando se completa una ejecución de predicción, los Perfiles consumen automáticamente las puntuaciones de propensión predichas. El enriquecimiento de Perfiles con puntuaciones de AI de cliente permite crear segmentos de clientes para encontrar audiencias en función de sus puntuaciones de tendencia. Esta sección proporciona los pasos para crear segmentos mediante el Generador de segmentos. Para ver un tutorial más sólido sobre la creación de segmentos, consulte la guía [de usuario del Generador](../../segmentation/tutorials/create-a-segment.md)de segmentos.

>[!IMPORTANT] Para utilizar este método, es necesario habilitar el Perfil del cliente en tiempo real para el conjunto de datos.

En la interfaz de usuario de la plataforma, haga clic en **Segmentos** en el panel de navegación izquierdo y, a continuación, haga clic en **Crear segmento**.

![](./images/user-guide/segments.png)

Aparece el Generador *de segmentos* . En la columna *Campos* de la izquierda y en la ficha *Atributos* , haga clic en la carpeta denominada Perfil **individual** XDM y, a continuación, haga clic en la carpeta con la Área de nombres de su organización. La carpeta denominada **Customer AI** contiene los resultados de las ejecuciones de predicciones y recibe el nombre de la instancia a la que pertenecen las puntuaciones. Haga clic en una carpeta de instancia para acceder a los resultados de la instancia deseada.

![](./images/user-guide/results.png)

Situado en el centro del Generador de segmentos, arrastre y suelte el atributo **Puntuación** en el lienzo *del creador de* reglas para definir una regla.

En la columna de propiedades *del* segmento de la derecha, proporcione un nombre para el segmento.

![](./images/user-guide/properties.png)

Por encima de la columna *Campos* de la izquierda, haga clic en el icono de **engranaje** y seleccione una política **de** combinación. Click **Save** to create the segment.

![](./images/user-guide/merge_policy.png)

## Pasos siguientes

Siguiendo este tutorial, ha configurado correctamente una instancia de AI del cliente, ha generado puntuaciones de tendencia y ha encontrado audiencias basadas en sus puntuaciones de tendencia mediante el Generador de segmentos. Ahora puede realizar el destinatario de sus audiencias activándolas en los destinos. Consulte la descripción general [de](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) destinos para obtener más información.

## Apéndice

En la siguiente sección se proporciona información adicional sobre la salida de la API del cliente.

### Datos de salida de AI del cliente

La IA del cliente genera varios atributos para perfiles individuales que se consideran elegibles. Estos valores son consumidos por el Perfil del cliente en tiempo real, que puede utilizarse para crear y definir segmentos. En la tabla siguiente se describen los distintos atributos encontrados en la salida de la API del cliente:

| Atributo | Descripción |
| ----- | ----------- |
| Puntuación | La probabilidad relativa de que un cliente alcance el objetivo previsto dentro del intervalo de tiempo definido. Este valor no debe tratarse como un porcentaje de probabilidad, sino como la probabilidad de un individuo en comparación con la población total. Esta puntuación va de 0 a 100. |
| Probabilidad | Este atributo es la verdadera probabilidad de un perfil para alcanzar el objetivo previsto dentro del intervalo de tiempo definido. Al comparar resultados entre objetivos diferentes, se recomienda considerar la probabilidad por encima del percentil o la puntuación. La probabilidad siempre debe utilizarse para determinar la probabilidad media entre la población elegible, ya que la probabilidad tiende a estar en el lado inferior en el caso de eventos que no ocurren con frecuencia. Los valores para el intervalo de probabilidad entre 0 y 1. |
| Percentil | Este valor proporciona información sobre el rendimiento de un perfil en relación con otros perfiles con una puntuación similar. Por ejemplo, un perfil con una clasificación de percentil de 99 para la reproducción indica que tiene un mayor riesgo de producir, en comparación con el 99% de todos los demás perfiles que fueron puntuados. Los percentiles oscilan entre 1 y 100. |
| Tipo de tendencia | El tipo de tendencia seleccionado. |
| Fecha de puntuación | Fecha en la que se produjo la puntuación. |
| Factores influyentes | Razones predichas por las que es probable que un perfil se convierta o se produzca. Los factores están compuestos por los atributos siguientes:<ul><li>Código: El perfil o atributo del comportamiento que influye positivamente en la puntuación predicha de un perfil. </li><li>Valor: Valor del perfil o atributo de comportamiento.</li><li>Importancia: Indica el peso del perfil o el atributo de comportamiento que tiene en la puntuación prevista (bajo, medio, alto)</li></ul> |