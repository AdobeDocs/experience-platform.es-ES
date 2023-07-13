---
solution: Experience Platform
title: Guía de IU del Generador de segmentos
description: El Generador de segmentos en la interfaz de usuario de Adobe Experience Platform proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de datos de perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: 6d33c1bd3921a754edfab227fad236caf60ac960
workflow-type: tm+mt
source-wordcount: '3308'
ht-degree: 4%

---

# [!DNL Segment Builder] Guía de IU

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos.

![Se muestra la interfaz de usuario del Generador de segmentos.](../images/ui/segment-builder/segment-builder.png)

## Bloques de creación de definición de segmento {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="Campos"
>abstract="Los tres tipos de campo que componen una definición de segmento son atributos, eventos y audiencias. Los atributos permiten utilizar atributos de perfil que pertenecen a la clase de perfil individual XDM, los eventos permiten crear una audiencia basada en acciones o eventos que se producen mediante elementos de datos XDM ExperienceEvent y las audiencias permiten utilizar audiencias importadas de fuentes externas."

Los componentes básicos de las definiciones de segmentos son los atributos y los eventos. Además, los atributos y eventos contenidos en las audiencias existentes pueden utilizarse como componentes para nuevas definiciones.

Puede ver estos componentes básicos en la **[!UICONTROL Campos]** en el lado izquierdo de la sección [!DNL Segment Builder] workspace. **[!UICONTROL Campos]** contiene una pestaña para cada uno de los componentes principales:[!UICONTROL Atributos]&quot;, &quot;[!UICONTROL Eventos]&quot;, y &quot;[!UICONTROL Audiencias]&quot;.

![Se resalta la sección de campos del Generador de segmentos.](../images/ui/segment-builder/segment-fields.png)

### Atributos

El **[!UICONTROL Atributos]** le permite examinar [!DNL Profile] atributos que pertenecen a [!DNL XDM Individual Profile] clase. Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al lienzo del generador de reglas en el centro del espacio de trabajo. El [lienzo del generador de reglas](#rule-builder-canvas) se analiza con más detalle más adelante en esta guía.

![Se resalta la sección de atributos de los campos del Generador de segmentos.](../images/ui/segment-builder/attributes.png)

### Eventos

El **[!UICONTROL Eventos]** permite crear una audiencia basada en eventos o acciones que se produjeron mediante [!DNL XDM ExperienceEvent] elementos de datos. También puede encontrar Tipos de eventos en la **[!UICONTROL Eventos]** , que son una colección de eventos utilizados con frecuencia para permitirle crear sus definiciones de segmento más rápidamente.

Además de poder buscar [!DNL ExperienceEvent] , también puede buscar Tipos de eventos. Los tipos de eventos utilizan la misma lógica de codificación que [!DNL ExperienceEvents], sin que sea necesario buscar en el [!DNL XDM ExperienceEvent] clase que busca el evento correcto. Por ejemplo, si utiliza la barra de búsqueda para buscar &quot;carrito&quot;, devuelve &quot;Tipos de eventos&quot;[!UICONTROL AddCart]&quot; y &quot;[!UICONTROL RemoveCart]&quot;, que son dos acciones de carro muy utilizadas al crear definiciones de segmento.

Es posible buscar cualquier tipo de componente escribiendo su nombre en la barra de búsqueda, que utiliza [Sintaxis de búsqueda de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Los resultados de la búsqueda comienzan a rellenarse a medida que se introducen palabras completas. Por ejemplo, para generar una regla basada en el campo XDM `ExperienceEvent.commerce.productViews`, empiece a escribir &quot;vistas de producto&quot; en el campo de búsqueda. Una vez escrita la palabra &quot;product&quot;, los resultados de la búsqueda empiezan a aparecer. Cada resultado incluye la jerarquía de objetos a la que pertenece.

>[!NOTE]
>
>Los campos de esquema personalizados definidos por su organización pueden tardar hasta 24 horas en aparecer y estar disponibles para su uso en la creación de reglas.

A continuación, puede arrastrar y soltar fácilmente [!DNL ExperienceEvents] y &quot;[!UICONTROL Tipos de eventos]&quot; en su definición de segmento.

![Se resalta la sección de eventos de la interfaz de usuario del Generador de segmentos.](../images/ui/segment-builder/events.png)

De forma predeterminada, solo se muestran los campos de esquema rellenados del almacén de datos. Esto incluye &quot;[!UICONTROL Tipos de eventos]&quot;. Si la variable &quot;[!UICONTROL Tipos de eventos]&quot; la lista no está visible o solo puede seleccionar &quot;[!UICONTROL Cualquiera]&quot; as a &quot;[!UICONTROL Tipo de evento]&quot;, seleccione la **icono de engranaje** junto a **[!UICONTROL Campos]**, luego seleccione **[!UICONTROL Mostrar esquema XDM completo]** bajo **[!UICONTROL Campos disponibles]**. Seleccione el **icono de engranaje** de nuevo para volver a la **[!UICONTROL Campos]** y ahora debería poder ver varias &quot;[!UICONTROL Tipos de eventos]&quot; y campos de esquema, independientemente de si contienen datos o no.

![Se resaltan los botones de opción que permiten elegir entre mostrar solo los campos con datos o mostrar todos los campos XDM.](../images/ui/segment-builder/show-populated.png)

#### Conjuntos de datos de grupos de informes Adobe Analytics

Puede utilizar datos de uno o varios grupos de informes de Adobe Analytics como eventos dentro de la segmentación.

Cuando se utilizan datos de un único grupo de informes de Analytics, Platform añade automáticamente descriptores y nombres descriptivos a las eVars, lo que facilita la búsqueda de esos campos dentro de [!DNL Segment Builder].

![Imagen que muestra cómo se asignan las variables genéricas (eVars) a un nombre descriptivo.](../images/ui/segment-builder/single-report-suite.png)

Cuando se utilizan datos de varios grupos de informes de Analytics, Platform **no puede** agregue automáticamente descriptores o nombres descriptivos a las eVars. Como resultado, antes de utilizar los datos de los grupos de informes de Analytics, debe asignar a campos XDM. Encontrará más información sobre la asignación de variables de Analytics a XDM en la [guía de conexión de origen de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping).

Por ejemplo, considere una situación en la que tenía dos grupos de informes con las siguientes variables:

| Campo | Esquema A del grupo de informes | Esquema B del grupo de informes |
| ----- | --------------------- | --------------------- |
| eVar1 | Dominio de referencia | Sesión iniciada en S/N |
| eVar2 | Nombre de página | ID de fidelización de miembro |
| eVar3 | URL | Nombre de página |
| eVar4 | Términos de búsqueda | Nombre del producto |
| evento 1 | Clics | Page Views |
| evento 2 | Page Views | Adiciones al carro de compras |
| event3 | Adiciones al carro de compras | Cierres de compra |
| event4 | Compras | Compras |

En este caso, puede asignar los dos grupos de informes con el esquema siguiente:

![Imagen que muestra cómo se pueden asignar dos grupos de informes a un esquema de unión.](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>Mientras que los valores genéricos de eVar siguen rellenándose, debería **no** utilícelos en sus definiciones de segmentos (si es posible), ya que los valores pueden significar cosas diferentes a las que tenían originalmente en sus informes.

Una vez asignados los grupos de informes, puede utilizar estos campos recién asignados dentro de la segmentación y los flujos de trabajo relacionados con el perfil.

| Escenario | Experiencia del esquema de unión | Variable genérica de segmentación | Variable asignada de segmentación |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| Grupo de informes único | El descriptor de nombre descriptivo se incluye con variables genéricas. <br><br>**Ejemplo:** Nombre de página (eVar 2) | <ul><li>Descriptor de nombre descriptivo incluido con variables genéricas</li><li>Las consultas utilizan datos del conjunto de datos específico, ya que es el único</li></ul> | Las consultas pueden utilizar datos de Adobe Analytics y potencialmente otras fuentes. |
| Múltiples grupos de informes | No se incluyen descriptores de nombres descriptivos con las variables genéricas. <br><br>**Ejemplo:** EVAR 2 | <ul><li>Cualquier campo con varios descriptores aparece como genérico. Esto significa que no aparecen nombres descriptivos en la interfaz de usuario.</li><li>Las consultas pueden utilizar datos de cualquier conjunto de datos que contenga el eVar, lo que puede dar como resultado resultados mixtos o incorrectos.</li></ul> | Las consultas utilizan resultados correctamente combinados de varios conjuntos de datos. |

### Audiencias

El **[!UICONTROL Audiencias]** La pestaña enumera todas las audiencias importadas desde fuentes externas, como Adobe Audience Manager, así como audiencias creadas dentro de [!DNL Experience Platform].

En el **[!UICONTROL Audiencias]** , puede ver todas las fuentes disponibles como un grupo de carpetas. A medida que selecciona las carpetas, se pueden ver las subcarpetas y audiencias disponibles. Además, puede seleccionar el icono de carpeta (como se muestra en la imagen de la derecha) para ver la estructura de carpetas (una marca de verificación indica la carpeta en la que se encuentra actualmente) y volver a navegar fácilmente por las carpetas seleccionando el nombre de una carpeta en el árbol.

Puede situarse sobre el ⓘ situado junto a una audiencia para ver información sobre la audiencia, incluido su ID, descripción y la jerarquía de carpetas para localizar la audiencia.

![Imagen que muestra cómo funciona la jerarquía de carpetas para las audiencias.](../images/ui/segment-builder/audience-folder-structure.png)

También puede buscar audiencias mediante la barra de búsqueda, que utiliza [Sintaxis de búsqueda de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). En el **[!UICONTROL Audiencias]** , al seleccionar una carpeta de nivel superior, aparece la barra de búsqueda, lo que le permite buscar dentro de esa carpeta. Los resultados de la búsqueda solo comienzan a rellenarse una vez que se introducen palabras completas. Por ejemplo, para buscar una audiencia denominada `Online Shoppers`, empiece a escribir &quot;En línea&quot; en la barra de búsqueda. Una vez escrita la palabra &quot;Online&quot;, aparecen los resultados de búsqueda que contienen la palabra &quot;Online&quot;.

## Lienzo del generador de reglas {#rule-builder-canvas}

Una definición de segmento es un conjunto de reglas que se utilizan para describir las características clave o el comportamiento de una audiencia objetivo. Estas reglas se crean mediante el lienzo del generador de reglas, ubicado en el centro de [!DNL Segment Builder].

Para agregar una nueva regla a la definición del segmento, arrastre un mosaico desde el **[!UICONTROL Campos]** y suéltelo en el lienzo del generador de reglas. A continuación, se le presentarán opciones específicas del contexto según el tipo de datos que se agregue. Los tipos de datos disponibles incluyen: cadenas, fechas, [!DNL ExperienceEvents], &quot;[!UICONTROL Tipos de eventos]&quot;, y audiencias.

![El lienzo del generador de reglas en blanco.](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Los cambios más recientes en Adobe Experience Platform han actualizado el uso del `OR` y `AND` operadores lógicos entre eventos. Estas actualizaciones no afectarán a las definiciones de segmentos existentes. Sin embargo, estas modificaciones afectarán a todas las actualizaciones posteriores de las definiciones de segmentos existentes y de las definiciones de segmentos recién creadas. Lea el [actualización de constantes de tiempo](./segment-refactoring.md) para obtener más información.

Al seleccionar un valor para el atributo, verá una lista de valores de enumeración que pueden ser.

![Imagen que muestra la lista de valores de enumeración que puede tener un atributo.](../images/ui/segment-builder/enum-list.png)

Si se selecciona un valor de esta lista de enumeraciones, el valor se delineará con un borde sólido. Sin embargo, para campos que utilizan `meta:enum` enumeraciones (suaves), también puede seleccionar un valor que sea **no** de la lista de enumeraciones. Si crea su propio valor, se delineará con un borde de puntos, junto con una advertencia de que este valor no está en la lista de enumeración.

![Advertencia que se muestra si va a insertar un valor que no forma parte de la lista de enumeración.](../images/ui/segment-builder/enum-warning.png)

Si está creando varios valores, puede añadirlos todos a la vez mediante la carga masiva. Seleccione el ![icono de signo más](../images/ui/segment-builder/plus-icon.png) para mostrar el **[!UICONTROL Agregar valores de forma masiva]** popover.

![El icono &quot;+&quot; aparece resaltado y muestra el botón que puede seleccionar para acceder a la ventana emergente de carga masiva.](../images/ui/segment-builder/add-bulk-values.png)

En el **[!UICONTROL Agregar valores de forma masiva]** Al principio, puede cargar un archivo CSV o TSV.

![Se muestra la ventana emergente Agregar valores en lote. El cuadro de diálogo que puede seleccionar para cargar un archivo CSV o TSV está resaltado.](../images/ui/segment-builder/bulk-values-popover.png)

Como alternativa, puede agregar manualmente valores separados por comas.

![Se muestra la ventana emergente Agregar valores en lote. Tanto el cuadro de diálogo que se puede utilizar para insertar valores como los valores añadidos se resaltan.](../images/ui/segment-builder/bulk-values-comma-separated.png)

Tenga en cuenta que se permite un máximo de 250 valores. Si supera esta cantidad, deberá eliminar algunos valores antes de agregar más.

![Se muestra una advertencia que indica que se ha alcanzado el número máximo de valores.](../images/ui/segment-builder/maximum-values.png)

### Adición de audiencias

Puede arrastrar y soltar una audiencia desde el **[!UICONTROL Audiencia]** en el lienzo del generador de reglas para hacer referencia a la pertenencia a audiencias en la nueva definición de segmento. Esto le permite incluir o excluir la pertenencia a audiencias como atributo en las nuevas reglas de definición de segmentos.

Para [!DNL Platform] audiencias creadas con [!DNL Segment Builder], tiene la opción de convertir la audiencia en el conjunto de reglas que se utilizaron en la definición del segmento para esa audiencia. Esta conversión realiza una copia de la lógica de la regla, que se puede modificar sin afectar a la definición del segmento original. Asegúrese de haber guardado los cambios recientes en la definición del segmento antes de convertirla en lógica de regla.

>[!NOTE]
>
>Al añadir una audiencia desde una fuente externa, solo se hace referencia a la pertenencia a la audiencia. No puede convertir la audiencia en reglas y, por lo tanto, las reglas utilizadas para crear la audiencia original no se pueden modificar en la nueva definición de segmento.

![Esta imagen muestra cómo convertir un atributo de audiencia en reglas.](../images/ui/segment-builder/add-audience-to-segment.png)

Si surge algún conflicto al convertir audiencias en reglas, [!DNL Segment Builder] intentará conservar las opciones existentes lo mejor que pueda.

### Vista de código

También puede ver una versión basada en código de una regla creada en la variable [!DNL Segment Builder]. Una vez creada la regla en el lienzo del generador de reglas, puede seleccionar **[!UICONTROL Vista de código]** para ver su definición de segmento como PQL.

![El botón de vista de código está resaltado, lo que le permite ver la definición del segmento como PQL.](../images/ui/segment-builder/code-view.png)

La vista de código proporciona un botón que le permite copiar el valor de la definición del segmento para utilizarlo en las llamadas de API. Para obtener la última versión de la definición del segmento, asegúrese de haber guardado los cambios más recientes en la definición del segmento.

![El botón Copiar código aparece resaltado, lo que le permite ](../images/ui/segment-builder/copy-code.png)

### Funciones de agregación

Una agregación en [!DNL Segment Builder] es un cálculo en un grupo de atributos XDM cuyo tipo de datos es un número (doble o entero). Las cuatro funciones de agregación compatibles con el Generador de segmentos son SUMA, PROMEDIO, MÍN y MAX.

Para crear una función de agregación, seleccione un evento del carril izquierdo e insértelo en la [!UICONTROL Eventos] contenedor.

![Se resalta la sección de eventos.](../images/ui/segment-builder/events.png)

Después de colocar el evento dentro del contenedor de eventos, seleccione el icono de puntos suspensivos (...), seguido de **[!UICONTROL Agregado]**.

![El texto agregado se resalta. Al seleccionar esta opción, puede seleccionar las funciones de agregación.](../images/ui/segment-builder/add-aggregation.png)

Ahora se agrega la agregación. Ahora puede seleccionar la función de agregación, elegir qué atributo agregar, la función de igualdad y el valor. Para el ejemplo siguiente, esta definición de segmento clasificaría cualquier perfil que tenga una suma de valores comprados buena a 100 $, incluso si cada compra individual es inferior a 100 $.

![Las reglas de evento, que muestran una función de agregación.](../images/ui/segment-builder/filled-aggregation.png)

### Contar funciones {#count-functions}

Las funciones de recuento en el Generador de segmentos se utilizan para buscar eventos especificados y contar el número de veces que se realizan. Las funciones de recuento admitidas en el Generador de segmentos son &quot;Al menos&quot;, &quot;Como máximo&quot;, &quot;Exactamente&quot;, &quot;Entre&quot; y &quot;Todo&quot;.

Para crear una función de recuento, seleccione un evento del carril izquierdo e insértelo en la [!UICONTROL Eventos] contenedor.

![Los campos de eventos se resaltan.](../images/ui/segment-builder/events.png)

Después de colocar el evento dentro del contenedor de eventos, seleccione la opción [!UICONTROL Al menos 1] botón.

![Al menos se resalta, mostrando el área que se debe seleccionar para ver una lista completa de funciones de recuento.](../images/ui/segment-builder/add-count.png)

Ahora se agrega la función de recuento. Ahora puede seleccionar la función de recuento y el valor de la función. El ejemplo siguiente sería incluir cualquier evento que tenga al menos un clic.

![Se muestra y resalta una lista de las funciones de recuento.](../images/ui/segment-builder/select-count.png)

## Contenedores

Las reglas de segmentos se evalúan en el orden en que aparecen en la lista. Los contenedores permiten controlar el orden de ejecución mediante el uso de consultas anidadas.

Una vez que haya agregado al menos un mosaico al lienzo del generador de reglas, puede empezar a agregar contenedores. Para crear un nuevo contenedor, seleccione los puntos suspensivos (...) en la esquina superior derecha del mosaico y, a continuación, seleccione **[!UICONTROL Agregar contenedor]**.

![El botón Agregar contenedor aparece resaltado, lo que permite agregar un contenedor como elemento secundario del primer contenedor.](../images/ui/segment-builder/add-container.png)

Aparece un nuevo contenedor como secundario del primer contenedor, pero puede ajustar la jerarquía arrastrando y moviendo los contenedores. El comportamiento predeterminado de un contenedor es &quot;[!UICONTROL Incluir]&quot; el atributo, evento o audiencia proporcionados. Puede establecer la regla en &quot;[!UICONTROL Excluir]&quot; perfiles que coinciden con los criterios del contenedor seleccionando **[!UICONTROL Incluir]** en la esquina superior izquierda del mosaico y seleccione &quot;[!UICONTROL Excluir]&quot;.

Un contenedor secundario también se puede extraer y agregar en línea al contenedor principal seleccionando &quot;Desenvolver contenedor&quot; en el contenedor secundario. Seleccione los puntos suspensivos (...) en la esquina superior derecha del contenedor secundario para acceder a esta opción.

![Se resaltan las opciones que permiten desenvolver o eliminar el contenedor.](../images/ui/segment-builder/include-exclude.png)

Una vez que seleccione **[!UICONTROL Desenvolver contenedor]** el contenedor secundario se elimina y los criterios aparecen en línea.

>[!NOTE]
>
>Al desajustar contenedores, tenga cuidado de que la lógica siga cumpliendo con la definición de segmento deseada.

![El contenedor se muestra después de desenvolverlo.](../images/ui/segment-builder/unwrapped-container.png)

## Políticas de combinación

>[!CONTEXTUALHELP]
>id="platform_segmentation_createSegment_segmentBuilder_mergePolicies"
>title="Políticas de combinación"
>abstract="Las políticas de combinación permiten la combinación de diferentes conjuntos de datos para formar su perfil. Platform proporciona una política de combinación predeterminada, o puede crear una nueva política de combinación predeterminada en Perfiles. Elija una política de combinación que coincida con su propósito de marketing para esta audiencia."

[!DNL Experience Platform] le permite reunir datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear un perfil.

Puede seleccionar una política de combinación que coincida con su propósito de marketing para esta audiencia o utilizar la política de combinación predeterminada proporcionada por [!DNL Platform]. Puede crear varias políticas de combinación exclusivas de su organización, incluida la creación de su propia política de combinación predeterminada. Para obtener instrucciones paso a paso sobre la creación de directivas de combinación para su organización, comience por leer el [resumen de políticas de combinación](../../profile/merge-policies/overview.md).

Para seleccionar una política de combinación para su definición de segmento, seleccione el icono de engranaje en la **[!UICONTROL Campos]** y, a continuación, utilice la pestaña **[!UICONTROL Política de combinación]** menú desplegable para seleccionar la política de combinación que desee utilizar.

![Se resaltará el selector de la política de combinación. Esto le permite elegir qué política de combinación seleccionar para la definición del segmento.](../images/ui/segment-builder/merge-policy-selector.png)

## Propiedades de definición del segmento {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="Propiedades de definición del segmento"
>abstract="La sección de propiedades de la definición del segmento muestra una estimación del tamaño de la definición del segmento resultante, con el número de perfiles cualificados en comparación con el número total de perfiles. Esto permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia."

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="Actualizar estimaciones"
>abstract="Puede actualizar las estimaciones de la definición del segmento para ver inmediatamente una previsualización de cuántos perfiles cumplen los requisitos para la definición de segmento propuesta. Las estimaciones de audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=es#estimate-and-preview-an-audience" text="Calcular y previsualizar una audiencia"

Al crear una definición de segmento, la variable **[!UICONTROL Propiedades del segmento]** en la parte derecha del espacio de trabajo se muestra una estimación del tamaño de la definición del segmento resultante, que le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia.

El **[!UICONTROL Propiedades del segmento]** también es donde puede especificar información importante sobre la definición del segmento, incluido su nombre, descripción y tipo de evaluación. Los nombres de las definiciones de segmentos se utilizan para identificar la definición de segmentos entre las definidas por su organización y, por lo tanto, deben ser descriptivos, concisos y únicos.

A medida que vaya creando la definición del segmento, podrá ver una vista previa paginada de la audiencia seleccionando **[!UICONTROL Ver perfiles]**.

![Se resalta la sección de propiedades de la definición del segmento. Las propiedades de la definición del segmento incluyen, entre otras, el nombre de la definición del segmento, la descripción y el método de evaluación.](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Las estimaciones de audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de 1 millón de entidades en su almacén de perfiles, se utiliza el conjunto de datos completo; para entre 1 y 20 millones de entidades, se utiliza 1 millón de entidades; y para más de 20 millones de entidades, se utiliza el 5% del total de entidades. Encontrará más información sobre la generación de estimaciones para las definiciones de segmentos en la [sección de generación de estimaciones](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) del tutorial de creación de definiciones de segmentos.

También puede seleccionar el método de evaluación. Si sabe qué método de evaluación desea utilizar, puede seleccionarlo mediante la lista desplegable. Si desea saber para qué tipos de evaluación se adapta esta definición de segmento, puede seleccionar el icono Examinar ![icono de carpeta con lupa](../images/ui/segment-builder/segment-evaluation-select-icon.png) para ver una lista de los métodos de evaluación de definición de segmento disponibles.

El [!UICONTROL Idoneidad del método de evaluación] aparece la ventana emergente. Esta ventana emergente muestra los métodos de evaluación disponibles, que son por lotes, flujo continuo y Edge. La ventana emergente muestra qué métodos de evaluación son elegibles e inelegibles. Según los parámetros que haya utilizado en la definición del segmento, es posible que no cumpla los requisitos para determinados métodos de evaluación. Para obtener más información sobre los requisitos de cada método de evaluación, lea la [segmentación por streaming](./streaming-segmentation.md#query-types) o el [segmentación de borde](./edge-segmentation.md#query-types) información general.

![Aparecerá la ventana emergente de idoneidad del método de evaluación. Esto muestra qué métodos de evaluación son aptos e no aptos para la definición del segmento.](../images/ui/segment-builder/select-evaluation-method.png)

Si selecciona un método de evaluación no válido, se le pedirá que cambie las reglas de definición del segmento o que cambie el método de evaluación.

![El método de evaluación aparece. Si se selecciona un método de evaluación no apto, la ventana emergente explica por qué no es apto.](../images/ui/segment-builder/ineligible-evaluation-method.png)

Puede encontrar más información sobre los distintos métodos de evaluación de definiciones de segmentos en la [resumen de segmentación](../home.md#evaluate-segments).

## Pasos siguientes {#next-steps}

El Generador de segmentos proporciona un flujo de trabajo enriquecido que le permite aislar las audiencias comercializables de [!DNL Real-Time Customer Profile] datos. Después de leer esta guía, debería poder:

- Cree definiciones de segmentos utilizando una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Vea estimaciones de su audiencia potencial, lo que le permite ajustar sus definiciones de segmento según sea necesario.
- Habilite todas las definiciones de segmentos para la segmentación programada.
- Habilite las definiciones de segmento especificadas para la segmentación de flujo continuo.

Para obtener más información acerca de [!DNL Segmentation Service], siga leyendo la documentación y complemente su aprendizaje viendo los vídeos relacionados. Para obtener más información acerca de las otras partes de [!DNL Segmentation Service] Interfaz de usuario, lea la [[!DNL Segmentation Service] guía del usuario](./overview.md)
