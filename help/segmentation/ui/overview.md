---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía de la interfaz de usuario del Generador de segmentos
topic: ui guide
translation-type: tm+mt
source-git-commit: 822f43b139b68b96b02f9a5fe0549736b2524ab7
workflow-type: tm+mt
source-wordcount: '2562'
ht-degree: 0%

---


# [!UICONTROL Guía del usuario del Generador] de segmentos

[!DNL Adobe Experience Platform Segmentation Service] proporciona una API RESTful y una interfaz de usuario para crear definiciones de segmentos a partir de [!DNL Real-time Customer Profile] datos.

## Primeros pasos

Trabajar con definiciones de segmentos requiere comprender los distintos [!DNL Experience Platform] servicios relacionados con la segmentación. Antes de leer esta guía del usuario, consulte la documentación de los siguientes servicios:

- [!DNL Segmentation Service](../home.md):: El servicio de segmentación permite dividir los datos almacenados en [!DNL Experience Platform] que se relacionan con personas (como clientes, clientes potenciales, usuarios u organizaciones) en grupos más pequeños que comparten características similares y responderán de manera similar a las estrategias de mercadotecnia.
- [!DNL Real-time Customer Profile](../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.
- [!DNL Identity Service](../../identity-service/home.md):: Permite [!DNL Real-time Customer Profile] el puente de identidades de orígenes de datos dispares que se están ingeriendo en Platform.
- [!DNL Experience Data Model (XDM)](../../xdm/home.md):: El marco normalizado por el cual [!DNL Platform] organiza los datos de experiencia del cliente.

También es importante conocer dos términos clave que se utilizan a través de este documento y comprender la diferencia entre ellos:
- **Definición** del segmento: Conjunto de reglas utilizado para describir las características o los comportamientos clave de una audiencia de destinatario.
- **Audiencia**: Conjunto resultante de perfiles que cumplen los criterios de una definición de segmento.

## Acceso a las definiciones de segmentos

Para empezar a trabajar con definiciones de segmentos en [!DNL Adobe Experience Platform], haga clic en **[!UICONTROL Segmentos]** en el panel de navegación izquierdo. Para ver todas las definiciones de segmentos de su organización, haga clic en la ficha *[!UICONTROL Examinar]* . Esta vista lista información sobre la definición del segmento, incluido el método de evaluación, la fecha de creación y la fecha de la última modificación.

El método de evaluación puede ser de flujo continuo o por lotes. Los segmentos de flujo se evalúan constantemente a medida que los datos entran en el sistema. Los segmentos por lotes se evalúan según una programación establecida.

Los segmentos de lote tienen información adicional que muestra tanto la fecha de la última evaluación como la siguiente fecha de evaluación del lote.

Al hacer clic en **[!UICONTROL Crear segmento]** en la esquina superior derecha se abre el espacio de trabajo del Generador de segmentos, donde puede empezar a crear una definición de segmento.

![](../images/segment-builder/segment-browse.png)

## [!UICONTROL Espacio de trabajo Generador] de segmentos

[!UICONTROL El Generador] de segmentos proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos [!DNL Profile] de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.

![](../images/segment-builder/segment-builder.png)

## Componentes básicos de definición de segmentos

Los componentes básicos de las definiciones de segmentos son **[!UICONTROL Atributos]** y **[!UICONTROL Eventos]**. Además, los atributos y eventos contenidos en **[!UICONTROL Audiencias]** existentes también pueden utilizarse como componentes para nuevas definiciones.

Puede ver estos bloques de creación en la sección *Campos* de la izquierda del espacio de trabajo del Generador [!UICONTROL de] segmentos. *[!UICONTROL Campos]* contiene una ficha para cada uno de los componentes principales: **[!UICONTROL Atributos]**, **[!UICONTROL Eventos]** y **[!UICONTROL Audiencias]**.

![](../images/segment-builder/segment-fields.png)

### Atributos

La ficha **[!UICONTROL Atributos]** permite examinar [!DNL Profile] los atributos que pertenecen a la [!DNL XDM Individual Profile] clase. Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al lienzo del generador de reglas en el centro del espacio de trabajo. El lienzo [del generador de](#rule-builder-canvas) reglas se describe con más detalle más adelante en esta guía.

![](../images/segment-builder/attributes.png)

### Eventos

La ficha **[!UICONTROL Eventos]** le permite crear una audiencia basada en eventos o acciones que se hayan realizado con elementos de datos XDM ExperienceEvent. También puede encontrar Tipos de evento en la ficha **[!UICONTROL Eventos]** , que son una colección de eventos de uso común que le permiten crear sus segmentos más rápidamente.

Además de poder buscar [!DNL ExperienceEvent] elementos, también puede buscar Tipos de evento. Los Tipos de evento utilizan la misma lógica de codificación que [!DNL ExperienceEvents], sin necesidad de buscar en la [!DNL XDM ExperienceEvent] clase el evento correcto. Por ejemplo: si se utiliza la barra de búsqueda para buscar &quot;carro&quot;, se devuelven los Tipos de evento &quot;[!UICONTROL AddCart]&quot; y &quot;[!UICONTROL RemoveCart]&quot;, que son dos acciones de carro de compras que se utilizan con mucha frecuencia al generar definiciones de segmentos.

Se puede buscar cualquier tipo de componente escribiendo su nombre en la barra de búsqueda, que utiliza la sintaxis [de búsqueda de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Los resultados de búsqueda comienzan a llenarse a medida que se ingresan palabras completas. Por ejemplo, para generar una regla basada en el campo XDM `ExperienceEvent.commerce.productViews`, escriba &quot;vistas de producto&quot; en el inicio de búsqueda. Una vez escrita la palabra &quot;producto&quot;, comienzan a aparecer los resultados de la búsqueda. Cada resultado incluye la jerarquía de objetos a la que pertenece.

>[!NOTE] Los campos de esquema personalizados definidos por su organización pueden tardar hasta 24 horas en aparecer y estar disponibles para su uso en la creación de reglas.

A continuación, puede arrastrar y soltar fácilmente [!DNL ExperienceEvents] y [!UICONTROL Tipos de evento] en la definición del segmento.

![](../images/segment-builder/events-eventTypes.png)

De forma predeterminada, solo se muestran los campos de esquema rellenados del almacén de datos. Esto incluye [!UICONTROL Tipos de evento]. Si la lista de [!UICONTROL Tipos de evento] no está visible o sólo puede seleccionar &quot;[!UICONTROL Cualquiera]&quot; como [!UICONTROL Tipo de evento], haga clic en el icono de engranaje situado junto a *[!UICONTROL Campos]* y, a continuación, seleccione **[!UICONTROL Mostrar esquema]** ** XDM completo en Campos disponibles. Vuelva a hacer clic en el icono de engranaje para volver a la ficha *[!UICONTROL Campos]* y debería poder realizar la vista de varios campos de [!UICONTROL Tipos de evento] y esquemas, independientemente de si contienen datos o no.

![](../images/segment-builder/show-populated.png)

### Audiencias

La ficha **[!UICONTROL Audiencias]** lista todas las audiencias importadas desde fuentes externas, como Adobe Audience Manager, así como las audiencias creadas dentro de [!DNL Experience Platform].

En la ficha [!UICONTROL Audiencias] , puede ver todos los orígenes disponibles como un grupo de carpetas. Al hacer clic en estas carpetas, se pueden ver las subcarpetas y audiencias disponibles. Además, puede hacer clic en el icono de la carpeta (como se muestra en la imagen de la parte extrema derecha) para vista de la estructura de la carpeta (una marca de verificación indica la carpeta en la que se encuentra actualmente) y volver a las carpetas fácilmente haciendo clic en el nombre de la carpeta en el árbol.

Puede pasar el ratón por encima del ⓘ junto a una audiencia para obtener información de vista sobre la audiencia, incluido su ID, descripción y la jerarquía de carpetas, para localizar la audiencia.

![](../images/segment-builder/audience-folder-structure.png)

También puede buscar [!UICONTROL Audiencias] mediante la barra de búsqueda, que utiliza la sintaxis [de búsqueda de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. En la ficha *[!UICONTROL Audiencias]* , al seleccionar una carpeta de nivel superior, aparece la barra de búsqueda, lo que le permite buscar dentro de esa carpeta. Los resultados de la búsqueda sólo comienzan a completarse una vez ingresadas las palabras completas. Por ejemplo, para buscar una [!UICONTROL Audiencia] con el nombre `Online Shoppers`, escriba &quot;En línea&quot; en el inicio de búsqueda. Una vez que la palabra &quot;En línea&quot; se ha escrito en su totalidad, aparecen los resultados de búsqueda que contienen la palabra &quot;en línea&quot;.

## Lienzo del generador de reglas {#rule-builder-canvas}

Una definición de segmento es un conjunto de reglas que se utilizan para describir las características clave o el comportamiento de una audiencia de destinatario. Estas reglas se crean con el lienzo *[!UICONTROL del]* generador de reglas, ubicado en el centro del Generador [!UICONTROL de]segmentos.

Para agregar una nueva regla a la definición del segmento, arrastre un mosaico desde la ficha *[!UICONTROL Campos]* y suéltelo en el lienzo del generador de reglas. A continuación, se le presentarán opciones específicas del contexto según el tipo de datos que se agrega. Los tipos de datos disponibles incluyen: cadenas, fechas, [!DNL ExperienceEvents], [!UICONTROL Tipos de evento]y [!UICONTROL Audiencias].

![](../images/segment-builder/rule-builder-canvas.png)

### Añadir audiencias

Puede arrastrar y soltar una audiencia de la ficha *[!UICONTROL Audiencia]* en el lienzo del generador de reglas para hacer referencia a la pertenencia a la audiencia en la nueva definición del segmento. Esto le permite incluir o excluir la pertenencia a una audiencia como un atributo en la nueva regla de segmento.

Para [!DNL Platform] audiencias creadas con el Generador de segmentos, se le ofrece la opción de convertir la audiencia en el conjunto de reglas que se utilizaron en la definición de segmento para esa audiencia. Esta conversión hace una copia de la lógica de regla, que se puede modificar sin afectar a la definición del segmento original.

>[!NOTE] Al agregar una audiencia desde un origen externo, solo se hace referencia a la pertenencia a la audiencia. No puede convertir la audiencia en reglas y, por lo tanto, las reglas utilizadas para crear la audiencia original no se pueden modificar en la nueva definición de segmento.

![](../images/segment-builder/add-audience-to-segment.png)

## Contenedores

Las reglas de segmentos se evalúan en el orden en que aparecen en la lista. Los Contenedores permiten controlar el orden de ejecución mediante el uso de consultas anidadas.

Una vez que haya agregado al menos un mosaico al lienzo del generador de reglas, puede empezar a agregar contenedores. Para crear un nuevo contenedor, haga clic en las elipses (...) en la esquina superior derecha del mosaico y, a continuación, haga clic en **[!UICONTROL Añadir contenedor]**.

![](../images/segment-builder/add-container.png)

Un nuevo contenedor aparece como el secundario del primer contenedor, pero puede ajustar la jerarquía arrastrando y moviendo los contenedores. El comportamiento predeterminado de un contenedor es &quot;[!UICONTROL Incluir]&quot; el atributo, el evento o la audiencia proporcionados. Puede establecer la regla en perfiles &quot;[!UICONTROL Excluir]&quot; que coincidan con los criterios de contenedor haciendo clic en **[!UICONTROL Incluir]** en la esquina superior izquierda del mosaico y seleccionando &quot;[!UICONTROL Excluir]&quot;.

Un contenedor secundario también se puede extraer y agregar en línea al contenedor principal haciendo clic en &quot;Desajustar contenedor&quot; en el contenedor secundario. Haga clic en las elipses (...) en la esquina superior derecha del contenedor secundario para acceder a esta opción.

![](../images/segment-builder/include-exclude.png)

Una vez que haga clic en **[!UICONTROL Desajustar contenedor]** , se eliminará el contenedor secundario y los criterios aparecerán en línea.

>[!NOTE] Al desajustar contenedores, tenga cuidado de que la lógica siga cumpliendo con la definición de segmento deseada.

![](../images/segment-builder/unwrapped-container-inline.png)

## Combinar directivas

[!DNL Experience Platform] le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear un perfil.

Puede seleccionar una directiva de combinación que coincida con el propósito de marketing de esta audiencia o utilizar la directiva de combinación predeterminada proporcionada por [!DNL Platform]. Puede crear varias directivas de combinación exclusivas para su organización, incluida la creación de su propia directiva de combinación predeterminada. Para obtener instrucciones paso a paso sobre la creación de políticas de combinación para su organización, consulte el tutorial sobre el [trabajo con políticas de combinación mediante la interfaz de usuario](../../profile/ui/merge-policies.md).

Para seleccionar una directiva de combinación para la definición del segmento, haga clic en el icono de engranaje de la ficha *[!UICONTROL Campos]* y, a continuación, utilice el menú *[!UICONTROL desplegable]Combinar directiva *para seleccionar la directiva de combinación que desee utilizar.

![](../images/segment-builder/merge-policy-selector.png)

## Propiedades del segmento

Al crear una definición de segmento, la sección Propiedades *[!UICONTROL del]* segmento en el lado derecho del espacio de trabajo muestra una estimación del tamaño del segmento resultante, lo que le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia.

En la sección Propiedades ** del segmento también puede especificar información importante sobre la definición del segmento, incluidos su *[!UICONTROL nombre]* y *[!UICONTROL descripción]*. Los nombres de definiciones de segmentos se utilizan para identificar el segmento entre los definidos por su organización y, por lo tanto, deben ser descriptivos, concisos y únicos.

A medida que siga generando la definición del segmento, puede realizar la vista de una previsualización paginada de la audiencia seleccionando Perfiles **[!UICONTROL de]** Vista.

![](../images/segment-builder/segment-properties.png)

>[!NOTE] Las estimaciones de Audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de un millón de entidades en el almacén de perfiles, se utiliza el conjunto completo de datos; para entre 1 y 20 millones de entidades se utilizan 1 millón de entidades; y para más de 20 millones de entidades se utiliza el 5% del total. Encontrará más información sobre la generación de estimaciones de segmentos en la sección [de generación de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) estimaciones del tutorial de creación de segmentos.

## Habilitar la segmentación programada {#enable-scheduled-segmentation}

Una vez creadas las definiciones de segmentos, puede evaluarlas mediante una evaluación a pedido o programada (continua). La evaluación significa mover [!DNL Real-time Customer Profile] los datos a través de definiciones de segmentos para producir las audiencias correspondientes. Una vez creadas, las audiencias se guardan y almacenan para que se puedan exportar mediante [!DNL Experience Platform] API.

La evaluación a petición implica el uso de la API para realizar evaluaciones y generar audiencias según sea necesario, mientras que la evaluación programada (también conocida como &#39;segmentación programada&#39;) permite crear una programación recurrente para evaluar definiciones de segmentos a una hora específica (como máximo, una vez al día).

La activación de las definiciones de segmentos para la evaluación programada se puede realizar mediante la interfaz de usuario o la API. En la interfaz de usuario, vuelva a la ficha *[!UICONTROL Examinar]* dentro de **[!UICONTROL Segmentos]** y seleccione **[!UICONTROL Evaluar todos los segmentos]**. Esto hará que todos los segmentos se evalúen según la programación establecida por su organización.

>[!NOTE] La evaluación programada puede habilitarse para entornos limitados con un máximo de cinco (5) directivas de combinación para [!DNL XDM Individual Profile]. Si su organización tiene más de cinco directivas de combinación para [!DNL XDM Individual Profile] dentro de un solo entorno de simulación de pruebas, no podrá usar la evaluación programada.

Actualmente, las programaciones solo se pueden crear mediante la API. Para ver los pasos detallados sobre cómo crear, editar y trabajar con programaciones mediante la API, siga el tutorial para evaluar y acceder a los resultados del segmento, específicamente la sección sobre evaluación [programada mediante la API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/segment-builder/scheduled-segmentation.png)

## Segmentación por flujo continuo

>[!NOTE] Para que la segmentación por flujo continuo funcione, el cliente deberá habilitar la segmentación programada para la organización. Para obtener más información sobre cómo habilitar la segmentación programada, consulte [la sección anterior de esta guía](#enable-scheduled-segmentation)del usuario.

Una consulta se evaluará automáticamente con segmentación de flujo continuo si cumple cualquiera de los siguientes criterios:

| Tipo de Consulta | Detalles | Ejemplo |
| ---------- | ------- | ------- |
| Visita entrante | Cualquier definición de segmento que haga referencia a un solo evento entrante sin restricciones de tiempo. | ![](../images/segment-builder/incoming-hit.png) |
| Visita entrante dentro de un período de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante **en los últimos siete días**. | ![](../images/segment-builder/relative-hit-success.png) |
| Visita entrante que hace referencia a un perfil | Cualquier definición de segmento que haga referencia a un solo evento entrante, sin restricción de tiempo, y uno o más atributos de perfil. | ![](../images/segment-builder/profile-hit.png) |
| Visita entrante que hace referencia a un perfil dentro de un intervalo de tiempo relativo | Cualquier definición de segmento que haga referencia a un solo evento entrante y a uno o varios atributos de perfil, **en los últimos siete días**. | ![](../images/segment-builder/profile-relative-success.png) |
| Varios eventos que hacen referencia a un perfil | Cualquier definición de segmento que haga referencia a varios eventos **en las últimas 24 horas** y (opcionalmente) tiene uno o varios atributos de perfil. | ![](../images/segment-builder/event-history-success.png) |

La siguiente sección lista ejemplos de definición de segmentos que **no se habilitarán** para la segmentación de flujo continuo.

| Tipo de Consulta | Detalles |
| ---------- | ------- | 
| Visita entrante dentro de un período de tiempo relativo | Si la definición del segmento se refiere a un evento entrante **no** dentro del período **de siete días**&#x200B;últimos. Por ejemplo, en las **últimas dos semanas**. | ![](../images/segment-builder/relative-hit-failure.png) |
| Visita entrante que hace referencia a un perfil dentro de una ventana relativa | Las siguientes opciones **no admitirán** la segmentación de flujo continuo:<ul><li>Un evento entrante **no** dentro del **último período** de siete días.</li><li>Definición de segmento que incluye [!DNL Adobe Audience Manager (AAM)] segmentos o características.</li></ul> | ![](../images/segment-builder/profile-relative-failure.png) |
| Varios eventos que hacen referencia a un perfil | Las siguientes opciones **no admitirán** la segmentación de flujo continuo:<ul><li>Un evento que **no** se produce en **las últimas 24 horas**.</li><li>Definición de segmento que incluye segmentos o características de Adobe Audience Manager (AAM).</li></ul> | ![](../images/segment-builder/event-history-failure.png) |
| consultas de varias entidades | Las consultas de varias entidades **no son** compatibles con la segmentación por flujo. |  |

Además, se aplican algunas directrices al realizar la segmentación de flujo:

| Tipo de Consulta | Directrices |
| ---------- | -------- |
| consulta de evento único | La ventana retroactiva está limitada a **siete días**. |
| Consulta con historial de eventos | <ul><li>La ventana retroactiva está limitada a **un día**.</li><li>Entre los eventos **debe** existir una condición estricta de ordenación de tiempo.</li><li>Solo se permiten pedidos de tiempo simples (antes y después) entre los eventos.</li><li>Los eventos individuales **no se pueden** negar. Sin embargo, toda la consulta **puede** ser anulada.</li></ul> |

### Monitoreo de la segmentación de flujo continuo

Después de crear un segmento con transmisión habilitada, puede supervisar los detalles de ese segmento.

![](../images/segment-builder/monitoring-streaming-segment.png)

En concreto, se muestran detalles sobre el tamaño ** total de audiencia cualificada. Si un trabajo se ha ejecutado en las últimas 24 horas, se muestra el Tamaño **** total de Audiencia del trabajo, además de un gráfico de líneas para la audiencia agregada. De lo contrario, se muestra el Tamaño **[!UICONTROL de Audiencia]** estimado, además de una línea de tendencia de visualización.

![](../images/segment-builder/monitoring-streaming-segment-graph.png)

Para obtener información adicional sobre la última evaluación de segmentos, haga clic en la burbuja de información.

![](../images/segment-builder/info-bubble.png)

## Violaciones de políticas DULE

>[!NOTE] Las infracciones de directiva DULE solo se aplican si está creando un segmento que se ha asignado a un destino.

Una vez que haya terminado de crear el segmento, éste se analizará [!DNL Data Governance] para asegurarse de que no haya violaciones de política dentro del segmento. Para obtener más información sobre las infracciones DULE y de políticas, consulte la descripción general [de la etiqueta de uso de](../../data-governance/labels/overview.md)datos.

![](../images/segment-builder/segment-dule-policy-violations.png)

## Pasos siguientes

El Generador de segmentos proporciona un flujo de trabajo enriquecido que le permite aislar audiencias comercializables de [!DNL Real-time Customer Profile] los datos. Después de leer esta guía, debería poder:

- Cree definiciones de segmentos mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Estimaciones de Vista de su audiencia potencial, permitiéndole ajustar las definiciones de segmentos según sea necesario.
- Habilite todas las definiciones de segmentos para la segmentación programada.
- Active las definiciones de segmentos especificadas para la segmentación de flujo continuo.

Para obtener instrucciones paso a paso sobre cómo trabajar con [!DNL Segmentation Service] el uso de la [!DNL Segmentation Service] API, consulte el tutorial [Creación de segmentos de audiencia mediante APIs](../tutorials/create-a-segment.md) .