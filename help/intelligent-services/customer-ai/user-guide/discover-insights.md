---
keywords: Experience Platform;perspectivas;ai del cliente;temas populares;perspectivas de los clientes
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Descubra perspectivas con Customer AI
topic-legacy: Discovering insights
description: Este documento sirve como guía para interactuar con perspectivas de instancias de servicio en la interfaz de usuario de Intelligent Services Customer AI.
exl-id: 8aaae963-4029-471e-be9b-814147a5f160
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '1632'
ht-degree: 1%

---

# Descubra perspectivas con Customer AI

Customer AI, como parte de Servicios inteligentes, proporciona a los especialistas en marketing la capacidad de aprovechar Adobe Sensei para anticipar cuál será la próxima acción de sus clientes. La AI del cliente se utiliza para generar puntuaciones de tendencia personalizadas, como la generación y la conversión de perfiles individuales a escala. Esto se logra sin tener que transformar las necesidades del negocio en un problema de aprendizaje automático, seleccionando un algoritmo, capacitación o implementación.

Este documento sirve como guía para interactuar con perspectivas de instancias de servicio en la interfaz de usuario de Intelligent Services Customer AI.

## Primeros pasos

Para utilizar perspectivas para Customer AI, debe tener disponible una instancia de servicio con un estado de ejecución correcto. Para crear una nueva instancia de servicio, visite [Configuración de una instancia AI del cliente](./configure.md). Si ha creado recientemente una instancia de servicio y sigue siendo de formación y puntuación, espere 24 horas para que termine de ejecutarse.

## Información general de la instancia de servicio

En la interfaz de usuario de [!DNL Adobe Experience Platform], haga clic en **[!UICONTROL Services]** en el panel de navegación izquierdo. Aparece el explorador *Services* y muestra los servicios inteligentes disponibles. En el contenedor de Customer AI, haga clic en **[!UICONTROL Open]**.

![Acceso a la instancia](../images/insights/navigate-to-service.png)

Aparece la página del servicio Customer AI. Esta página enumera las instancias de servicio de Customer AI y muestra información sobre ellas, incluido el nombre de la instancia, el tipo de inclinación, la frecuencia con la que se ejecuta la instancia y el estado de la última actualización.

>[!NOTE]
>
>Solo las instancias de servicio que hayan completado las ejecuciones de puntuación exitosas tienen perspectivas.

![Crear instancia](../images/insights/dashboard.png)

Seleccione un nombre de instancia de servicio para comenzar.

![Crear instancia](../images/insights/click-the-name.png)

A continuación, la página perspectivas de esa instancia de servicio aparece con la opción de seleccionar **[!UICONTROL Últimas puntuaciones]** o **[!UICONTROL Resumen de rendimiento]**. La pestaña predeterminada **[!UICONTROL Últimas puntuaciones]** proporciona visualizaciones de los datos. Las visualizaciones y lo que puede hacer con los datos se explican con más detalle en esta guía.

La pestaña **[!UICONTROL Performance summary]** muestra las tasas reales de pérdida o conversión de cada bloque de propensión. Para obtener más información, consulte la sección sobre [métricas de resumen de rendimiento](#performance-metrics).

![página de configuración](../images/insights/landing_page_insights.png)

### Detalles de instancias de servicio

Existen dos formas de ver los detalles de instancias de servicio: desde el panel o dentro de la instancia de servicio.

Para ver una descripción general de los detalles de la instancia de servicio dentro del panel, seleccione un contenedor de instancia de servicio, evitando el hipervínculo adjunto al nombre. Se abre un carril derecho que proporciona detalles adicionales. Los controles contienen lo siguiente:

- **[!UICONTROL Editar]**: La selección de  **** Editar permite modificar una instancia de servicio existente. Puede editar el nombre, la descripción y la frecuencia de puntuación de la instancia.
- **[!UICONTROL Clonar]**: Al seleccionar  **** Clonecopies, se configura la instancia de servicio seleccionada actualmente. A continuación, puede modificar el flujo de trabajo para realizar ajustes menores y cambiarle el nombre como una nueva instancia.
- **[!UICONTROL Eliminar]**: Puede eliminar una instancia de servicio, incluidas las ejecuciones históricas.
- **[!UICONTROL Fuente]** de datos: Un vínculo al conjunto de datos utilizado por esta instancia.
- **[!UICONTROL Frecuencia]** de ejecución: La frecuencia con la que se produce una puntuación y el momento en que se realiza.
- **[!UICONTROL Definición]** de puntuación: Información general rápida sobre el objetivo que configuró para esta instancia.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>En caso de que falle una ejecución de puntuación, se proporciona un mensaje de error. El mensaje de error aparece en **Últimos detalles de ejecución** en el carril derecho, que solo es visible para las ejecuciones fallidas.

![error al ejecutar el mensaje](../images/insights/failed-run.png)

La segunda manera de ver detalles adicionales para una instancia de servicio se encuentra dentro de la página de perspectivas. Puede hacer clic en **[!UICONTROL Mostrar más]** en la parte superior derecha para rellenar una lista desplegable. Los detalles se enumeran, como la definición de puntuación, cuándo se creó y el tipo de tendencia. Para obtener más información sobre cualquiera de las propiedades enumeradas, visite [Configuración de una instancia AI del cliente](./configure.md).

![mostrar más](../images/insights/landing-show-more.png)

![mostrar más](../images/insights/show-more.png)

### Editar una instancia

Para editar una instancia, haga clic en **[!UICONTROL Editar]** en el panel de navegación superior derecho.

![haga clic en el botón editar](../images/insights/edit-button.png)

Aparece el cuadro de diálogo de edición, que le permite editar el nombre, la descripción, el estado y la frecuencia de puntuación de la instancia. Para confirmar los cambios y cerrar el cuadro de diálogo, seleccione **[!UICONTROL Guardar]** en la esquina inferior derecha.

![editar popover](../images/insights/edit-instance.png)

### Más acciones

El botón **[!UICONTROL Más acciones]** se encuentra en la navegación superior derecha junto a **[!UICONTROL Editar]**. Al hacer clic en **[!UICONTROL Más acciones]** se abre un menú desplegable que le permite seleccionar una de las siguientes operaciones:

- **[!UICONTROL Clonar]**: Al seleccionar  **** Clonecopies, se configura la instancia de servicio. A continuación, puede modificar el flujo de trabajo para realizar ajustes menores y cambiarle el nombre como una nueva instancia.
- **[!UICONTROL Eliminar]**: Elimina la instancia.
- **[!UICONTROL Puntuaciones]** de acceso: Al seleccionar  **[!UICONTROL Puntuaciones de]** acceso , se abre un cuadro de diálogo que contiene un vínculo a las puntuaciones de  [descarga del ](./download-scores.md) tutorial de AI del cliente, mientras que el cuadro de diálogo también proporciona el ID del conjunto de datos necesario para realizar llamadas de API.
- **[!UICONTROL Ver el historial]** de ejecución: Aparecerá un cuadro de diálogo que contiene una lista de todas las ejecuciones de puntuación asociadas a la instancia de servicio.

![más acciones](../images/insights/more-actions.png)

## Resumen de puntuación {#scoring-summary}

Resumen de puntuación muestra el número total de perfiles clasificados y los categoriza en bloques que contienen alta, media y baja tendencia. Los bloques de propensión se determinan en función del rango de puntuación, el bajo es inferior a 24, el medio es de 25 a 74 y el alto es superior a 74. Cada cubo tiene un color correspondiente a la leyenda.

>[!NOTE]
>
>Si se trata de una puntuación de tendencia de conversión, las puntuaciones altas se muestran en verde y las bajas, en rojo. Si predice que la propensión de pérdida es invertida, las puntuaciones altas están en rojo y las bajas son verdes. El espacio medio permanece amarillo independientemente del tipo de inclinación que elija.

![resumen de puntuación](../images/insights/scoring-summary.png)

Puede situarse sobre cualquier color del anillo para ver información adicional, como un porcentaje y el número total de perfiles pertenecientes a un bloque.

![](../images/insights/scoring-ring.png)

## Distribución de puntuaciones

La tarjeta **[!UICONTROL Distribution of Score]** le proporciona un resumen visual de la población en función de la puntuación. Los colores que se ven en la tarjeta [!UICONTROL Distribution of Score] representan el tipo de puntuación de tendencia generada. Al pasar el ratón por encima de cualquiera de las distribuciones de puntuación, se obtiene el recuento exacto que pertenece a esa distribución.

![distribución de puntuaciones](../images/insights/distribution-of-scores.png)

## Factores influyentes

Para cada grupo de puntuación, se genera una tarjeta que muestra los 10 factores influyentes principales para ese grupo. Los factores influyentes le proporcionan detalles adicionales sobre por qué sus clientes pertenecen a varios bloques de puntuaciones.

![Factores influyentes](../images/insights/influential-factors.png)

### Desgloses de factores influyentes

Al pasar el ratón por encima de cualquiera de los factores de mayor influencia, los datos se desglosan aún más. Se le proporciona una descripción general de por qué ciertos perfiles pertenecen a un grupo de propensión. Según el factor, se le pueden dar valores numéricos, categóricos o booleanos. El ejemplo siguiente muestra valores categóricos por región.

![captura de pantalla de desglose](../images/insights/drilldown.png)

Además, con los desgloses, puede comparar un factor de distribución si se produce en dos o más bloques de inclinación y crear segmentos más específicos con estos valores. El siguiente ejemplo ilustra el primer caso de uso:

![](../images/insights/drilldown-compare.png)

Puede ver que los perfiles con baja tendencia a convertir tienen menos probabilidades de haber realizado una visita reciente a las páginas web de adobe.com. El factor &quot;Días transcurridos desde la última visita web&quot; tiene solo un 8 % de cobertura frente al 26 % en los perfiles de propensión media. Con estos números, puede comparar la distribución dentro de cada bloque para el factor. Esta información se puede utilizar para inferir que la actualización en webvisit no es tan influyente en el bloque de baja propensión como en el de propensión media.

### Creación de segmentos

Al seleccionar el botón **[!UICONTROL Crear segmento]** en cualquiera de los contenedores para obtener una propensión baja, media y alta, se le redirige al Generador de segmentos.

>[!NOTE]
>
>El botón **[!UICONTROL Crear segmento]** solo está disponible si el perfil del cliente en tiempo real está habilitado para el conjunto de datos. Para obtener más información sobre cómo habilitar el perfil del cliente en tiempo real, visite [Información general del perfil del cliente en tiempo real](../../../rtcdp/overview.md).

![Haga clic en crear segmento](../images/insights/influential-factors-create-segment.png)

![Creación de segmentos](../images/insights/create-segment.png)

El generador de segmentos se utiliza para definir un segmento. Al seleccionar **[!UICONTROL Crear segmento]** en la página Perspectivas, Customer AI agrega automáticamente la información de bloques seleccionada al segmento. Para terminar de crear el segmento, simplemente rellene los contenedores *Name* y *Description* ubicados en el carril derecho de la interfaz de usuario del generador de segmentos. Una vez que haya dado un nombre y una descripción al segmento, haga clic en **[!UICONTROL Guardar]** en la parte superior derecha.

>[!NOTE]
>
>Dado que las puntuaciones de tendencia se escriben en el perfil individual, están disponibles en el Generador de segmentos como cualquier otro atributo de perfil. Cuando vaya al Generador de segmentos para crear nuevos segmentos, podrá ver todas las distintas puntuaciones de tendencia en el área de nombres Customer AI.

![Relleno de segmentos](../images/insights/segment-saving.png)

Para ver el nuevo segmento en la interfaz de usuario de Platform, haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo. La página **[!UICONTROL Examinar]** aparece y muestra todos los segmentos disponibles.

![Todos sus segmentos](../images/insights/Segments-dashboard.png)

## Métricas de resumen de rendimiento {#performance-metrics}

La pestaña **[!UICONTROL Performance summary]** muestra las tasas de conversión o pérdida reales, separadas en cada uno de los bloques de tendencia marcados por Customer AI.

![Ficha Resumen del rendimiento](../images/insights/summary_tab.png)

Inicialmente solo se muestran las tasas esperadas (líneas de puntos). Las tasas esperadas se muestran cuando no se ha producido una ejecución de puntuación y los datos aún no están disponibles. Sin embargo, una vez que ha pasado una ventana de resultados, la tasa esperada se sustituye por una tasa real (línea sólida).

Al pasar el ratón por encima de las líneas, se muestra la fecha y la tasa real/esperada de ese día en ese bloque.

![Ejemplo de depósito](../images/insights/churn_tab.png)

Puede filtrar el intervalo de tiempo para ver las tasas esperadas y reales que se muestran. Seleccione el **icono de calendario** ![icono](../images/insights/calendar_icon.png)y, a continuación, seleccione un nuevo intervalo de fechas. Los resultados de cada uno de los bloques se actualizan para mostrarse dentro del nuevo intervalo de fechas.

![Selector de fecha](../images/insights/date_selector.png)

### Tasas de ejecución de puntuación individual

La mitad inferior de la pestaña **[!UICONTROL Performance summary]** muestra los resultados de cada ejecución de puntuación individual. Seleccione la fecha desplegable en la parte superior derecha para mostrar los resultados de una ejecución de puntuación diferente.

Dependiendo de si está pronosticando la pérdida o conversión, el gráfico [!UICONTROL Distribution of Score] muestra la distribución de perfiles alterados/convertidos y no producidos/no convertidos en cada incremento.

![puntuación individual](../images/insights/scoring_tab.png)

## Pasos siguientes

Este documento describía las perspectivas proporcionadas por una instancia de servicio de Customer AI. Ahora puede continuar con el tutorial sobre la [descarga de puntuaciones en Customer AI](./download-scores.md) o examinar las otras [guías de servicios inteligentes de Adobe](../../home.md) que se ofrecen.

## Recursos adicionales

En el siguiente vídeo se describe cómo utilizar Customer AI para ver el resultado de los modelos y los factores influyentes.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)
