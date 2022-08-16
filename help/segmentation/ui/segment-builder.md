---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;servicio de segmentación;guía del usuario;guía de interfaz de usuario;guía de interfaz de usuario de segmentación;generador de segmentos;Generador de segmentos;
solution: Experience Platform
title: Guía de la interfaz de usuario del Generador de segmentos
topic-legacy: ui guide
description: El Generador de segmentos en la interfaz de usuario de Adobe Experience Platform proporciona un espacio de trabajo enriquecido que le permite interactuar con los elementos de datos del perfil. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
source-git-commit: dd87f9e5787961442ca7d7b4c761d2e7ca724994
workflow-type: tm+mt
source-wordcount: '3081'
ht-degree: 1%

---

# [!DNL Segment Builder] Guía de la interfaz de usuario

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con [!DNL Profile] elementos de datos. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.

![Se muestra la interfaz de usuario del generador de segmentos.](../images/ui/segment-builder/segment-builder.png)

## Componentes básicos de definición de segmentos {#building-blocks}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_fields"
>title="Campos"
>abstract="Los tres tipos de campo que componen un segmento son atributos, eventos y audiencias. Los atributos permiten utilizar atributos de perfil que pertenecen a la clase de perfil individual XDM, los eventos permiten crear una audiencia basada en acciones o eventos que se producen mediante elementos de datos XDM ExperienceEvent y las audiencias permiten utilizar audiencias importadas de fuentes externas."

Los componentes básicos de las definiciones de segmentos son atributos y eventos. Además, los atributos y eventos contenidos en audiencias existentes pueden utilizarse como componentes para nuevas definiciones.

Puede ver estos componentes básicos en el **[!UICONTROL Campos]** a la izquierda del [!DNL Segment Builder] espacio de trabajo. **[!UICONTROL Campos]** contiene una pestaña para cada uno de los componentes principales: &quot;[!UICONTROL Atributos]&quot;, &quot;[!UICONTROL Eventos]&quot;, y &quot;[!UICONTROL Audiencias]&quot;.

![Se resalta la sección de campos del Generador de segmentos.](../images/ui/segment-builder/segment-fields.png)

### Atributos

La variable **[!UICONTROL Atributos]** le permite explorar [!DNL Profile] atributos que pertenecen a la variable [!DNL XDM Individual Profile] Clase . Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al lienzo del generador de reglas en el centro del espacio de trabajo. La variable [lienzo del generador de reglas](#rule-builder-canvas) más adelante en esta guía.

![Se resalta la sección Atributos de los campos del Generador de segmentos.](../images/ui/segment-builder/attributes.png)

### Eventos

La variable **[!UICONTROL Eventos]** le permite crear una audiencia en función de eventos o acciones que se hayan realizado con [!DNL XDM ExperienceEvent] elementos de datos. También puede encontrar Tipos de eventos en la **[!UICONTROL Eventos]** , que son una colección de eventos que se utilizan con frecuencia para permitirle crear sus segmentos más rápidamente.

Además de poder buscar [!DNL ExperienceEvent] también puede buscar tipos de eventos. Los tipos de eventos utilizan la misma lógica de codificación que [!DNL ExperienceEvents], sin que sea necesario que busque en la [!DNL XDM ExperienceEvent] buscando el evento correcto. Por ejemplo, si se utiliza la barra de búsqueda para buscar &quot;carro&quot;, se devuelven los Tipos de eventos .[!UICONTROL AddCart]&quot; y &quot;[!UICONTROL RemoveCart]&quot;, que son dos acciones del carro de compras que se usan con mucha frecuencia al crear definiciones de segmentos.

Se puede buscar cualquier tipo de componente escribiendo su nombre en la barra de búsqueda, que utiliza [Sintaxis de búsqueda de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Los resultados de la búsqueda comienzan a rellenarse a medida que se introducen palabras completas. Por ejemplo, para generar una regla basada en el campo XDM `ExperienceEvent.commerce.productViews`, empiece a escribir &quot;vistas del producto&quot; en el campo de búsqueda. Una vez que se ha escrito la palabra &quot;producto&quot;, empiezan a aparecer los resultados de la búsqueda. Cada resultado incluye la jerarquía de objetos a la que pertenece.

>[!NOTE]
>
>Los campos de esquema personalizados definidos por su organización pueden tardar hasta 24 horas en aparecer y estar disponibles para su uso en la creación de reglas.

A continuación, puede arrastrar y soltar fácilmente [!DNL ExperienceEvents] y &quot;[!UICONTROL Tipos de eventos]&quot; en su definición de segmento.

![Se resalta la sección de eventos de la interfaz de usuario del Generador de segmentos.](../images/ui/segment-builder/events.png)

De forma predeterminada, solo se muestran los campos de esquema rellenados del almacén de datos. Esto incluye &quot;[!UICONTROL Tipos de eventos]&quot;. Si la variable[!UICONTROL Tipos de eventos]&quot; no está visible, o solo puede seleccionar &quot;[!UICONTROL Cualquiera]&quot; como &quot;[!UICONTROL Tipo de evento]&quot;, seleccione **icono de engranaje** junto a **[!UICONTROL Campos]** y, a continuación, seleccione **[!UICONTROL Mostrar esquema XDM completo]** under **[!UICONTROL Campos disponibles]**. Seleccione el **icono de engranaje** para volver a la **[!UICONTROL Campos]** y ahora debería poder ver varias[!UICONTROL Tipos de eventos]&quot; y campos de esquema, independientemente de si contienen datos o no.

![](../images/ui/segment-builder/show-populated.png)

#### Conjuntos de datos de grupos de informes de Adobe Analytics

Los datos de uno o varios grupos de informes de Adobe Analytics se pueden usar como eventos dentro de la segmentación.

Al utilizar datos de un único grupo de informes de Analytics, Platform agregará automáticamente descriptores y nombres descriptivos a las eVars, lo que facilita la búsqueda de dichos campos en [!DNL Segment Builder].

![Imagen que muestra cómo se asignan las variables genéricas (eVars) a un nombre descriptivo.](../images/ui/segment-builder/single-report-suite.png)

Cuando se utilizan datos de varios grupos de informes de Analytics, Platform **cannot** agregue automáticamente descriptores o nombres descriptivos a las eVars. Como resultado, antes de usar los datos de los grupos de informes de Analytics, debe asignarlos a campos XDM. Puede encontrar más información sobre la asignación de variables de Analytics a XDM en la [Guía de conexión de origen de Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md#mapping).

Por ejemplo, imaginemos una situación en la que tenía dos grupos de informes con las siguientes variables:

| Campo | Esquema A del grupo de informes | Esquema B del grupo de informes |
| ----- | --------------------- | --------------------- |
| eVar1 | Dominio de referencia | Inicio de sesión Y/N |
| eVar2 | Nombre de página | ID de fidelidad de miembro |
| eVar3 | URL | Nombre de página |
| eVar4 | Términos de búsqueda | Nombre del producto |
| evento 1 | Clics | Page Views |
| evento 2 | Vistas de páginas | Adiciones al carro de compras |
| event3 | Adiciones al carro de compras | Cierres de compra |
| event4 | Compras | Compras |

En este caso, puede asignar los dos grupos de informes con el esquema siguiente:

![Una imagen que muestra cómo se pueden asignar dos grupos de informes a un esquema de unión.](../images/ui/segment-builder/union-schema.png)

>[!NOTE]
>
>Aunque los valores de eVar genéricos se sigan llenando, debe **not** utilícelos en las definiciones de segmentos (si es posible), ya que los valores podrían tener un significado distinto al original en sus informes.

Una vez asignados los grupos de informes, puede utilizar estos campos recién asignados dentro de los flujos de trabajo y la segmentación relacionados con el perfil.

| Escenario | Experiencia del esquema de unión | Variable genérica de segmentación | Variable asignada de segmentación |
| -------- | ----------------------- | ----------------------------- | ---------------------------- |
| Grupo de informes único | El descriptor de nombre descriptivo se incluye con variables genéricas. <br><br>**Ejemplo:** Nombre de página (eVar2) | <ul><li>Descriptor de nombres descriptivos incluido con variables genéricas</li><li>Las consultas utilizan datos del conjunto de datos específico, ya que es la única</li></ul> | Las consultas pueden utilizar datos de Adobe Analytics y otras fuentes potenciales. |
| Múltiples grupos de informes | No se incluyen descriptores de nombres descriptivos con las variables genéricas. <br><br>**Ejemplo:** eVar2 | <ul><li>Cualquier campo con varios descriptores aparece como genérico. Esto significa que no aparecen nombres descriptivos en la interfaz de usuario.</li><li>Las consultas pueden utilizar datos de cualquier conjunto de datos que contenga el eVar, lo que puede dar como resultado resultados mixtos o incorrectos.</li></ul> | Las consultas utilizan resultados combinados correctamente de varios conjuntos de datos. |

### Audiencias

La variable **[!UICONTROL Audiencias]** ficha enumera todas las audiencias importadas desde fuentes externas, como Adobe Audience Manager, así como las audiencias creadas en [!DNL Experience Platform].

En el **[!UICONTROL Audiencias]** , puede ver todos los orígenes disponibles como un grupo de carpetas. Al seleccionar las carpetas, se pueden ver las subcarpetas y audiencias disponibles. Además, puede seleccionar el icono de la carpeta (como se muestra en la imagen de la derecha) para ver la estructura de la carpeta (una marca de verificación indica la carpeta en la que se encuentra) y desplazarse fácilmente por las carpetas seleccionando el nombre de una carpeta en el árbol.

Puede pasar el ratón sobre la ⓘ junto a una audiencia para ver información sobre la audiencia, como su ID, descripción y la jerarquía de carpetas, para localizar la audiencia.

![Imagen que muestra cómo funciona la jerarquía de carpetas para las audiencias.](../images/ui/segment-builder/audience-folder-structure.png)

También puede buscar audiencias usando la barra de búsqueda, que utiliza [Sintaxis de búsqueda de Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). En el **[!UICONTROL Audiencias]** , seleccionar una carpeta de nivel superior hace que aparezca la barra de búsqueda, lo que le permite buscar dentro de esa carpeta. Los resultados de búsqueda solo comienzan a rellenarse una vez que se introducen palabras completas. Por ejemplo, para buscar una audiencia denominada `Online Shoppers`, empiece a escribir &quot;En línea&quot; en la barra de búsqueda. Una vez que la palabra &quot;Online&quot; se ha escrito en su totalidad, aparecen los resultados de búsqueda que contienen la palabra &quot;Online&quot;.

## Lienzo del generador de reglas {#rule-builder-canvas}

Una definición de segmento es un conjunto de reglas que se utilizan para describir características clave o el comportamiento de una audiencia de destino. Estas reglas se crean utilizando el lienzo del generador de reglas, ubicado en el centro de [!DNL Segment Builder].

Para agregar una regla nueva a la definición del segmento, arrastre un mosaico desde el **[!UICONTROL Campos]** y suéltela en el lienzo del generador de reglas. A continuación, se le presentarán opciones específicas del contexto según el tipo de datos que se agreguen. Los tipos de datos disponibles incluyen: cadenas, fechas, [!DNL ExperienceEvents], &quot;[!UICONTROL Tipos de eventos]&quot; y audiencias.

![El lienzo vacío del generador de reglas.](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Los últimos cambios realizados en Adobe Experience Platform han actualizado el uso de la variable `OR` y `AND` operadores lógicos entre eventos. Estas actualizaciones no afectarán a los segmentos existentes. Sin embargo, estos cambios afectarán a todas las actualizaciones posteriores de segmentos existentes y nuevas creaciones de segmentos. Lea el [actualización de constantes temporales](./segment-refactoring.md) para obtener más información.

Al seleccionar un valor para el atributo, verá una lista de valores de enumeración que puede ser el atributo.

![Imagen que muestra la lista de valores de enumeración que puede ser un atributo.](../images/ui/segment-builder/enum-list.png)

Si selecciona un valor de esta lista de enumeraciones, el valor se delineará con un borde sólido. Sin embargo, para los campos que utilizan `meta:enum` (suave) enumeraciones, también puede seleccionar un valor que sea **not** de la lista de enumeraciones. Si crea su propio valor, se delineará con un borde de puntos, junto con una advertencia de que este valor no está en la lista de enumeración.

![Advertencia que se muestra si se inserta un valor que no forma parte de la lista de enumeración.](../images/ui/segment-builder/enum-warning.png)

### Adición de audiencias

Puede arrastrar y soltar una audiencia desde la **[!UICONTROL Audiencia]** en el lienzo del generador de reglas para hacer referencia a la pertenencia a la audiencia en la nueva definición de segmento. Esto le permite incluir o excluir la pertenencia a una audiencia como atributo en la nueva regla de segmento.

Para [!DNL Platform] audiencias creadas con [!DNL Segment Builder], tiene la opción de convertir la audiencia en el conjunto de reglas que se usaron en la definición del segmento para esa audiencia. Esta conversión hace una copia de la lógica de regla, que se puede modificar sin afectar a la definición original del segmento. Asegúrese de haber guardado los cambios recientes en la definición del segmento antes de convertirla a la lógica de regla.

>[!NOTE]
>
>Al añadir una audiencia desde una fuente externa, solo se hace referencia a la pertenencia a la audiencia. No puede convertir la audiencia en reglas y, por lo tanto, las reglas utilizadas para crear la audiencia original no se pueden modificar en la nueva definición del segmento.

![Esta imagen muestra cómo convertir un atributo de audiencia en reglas.](../images/ui/segment-builder/add-audience-to-segment.png)

Si surgen conflictos al convertir audiencias en reglas, [!DNL Segment Builder] intentará conservar las opciones existentes en la medida de sus posibilidades.

### Vista de código

También puede ver una versión basada en código de una regla creada en la variable [!DNL Segment Builder]. Una vez creada la regla dentro del lienzo del generador de reglas, puede seleccionar **[!UICONTROL Vista de código]** para ver su segmento como PQL.

![El botón de vista de código está resaltado, lo que le permite ver el segmento como PQL.](../images/ui/segment-builder/code-view.png)

La vista de código proporciona un botón que le permite copiar el valor del segmento para utilizarlo en llamadas API. Para obtener la última versión del segmento, asegúrese de haber guardado los cambios más recientes en el segmento.

![Se resalta el botón Copiar código, que le permite ](../images/ui/segment-builder/copy-code.png)

### Funciones de agregación

Una agregación en [!DNL Segment Builder] es un cálculo de un grupo de atributos XDM cuyo tipo de datos es un número (doble o entero). Las cuatro funciones de agregación admitidas en el Generador de segmentos son SUMA, PROMEDIO, MIN y MAX.

Para crear una función de agregación, seleccione un evento del carril izquierdo e insértelo en el [!UICONTROL Eventos] contenedor.

![Se resalta la sección de eventos.](../images/ui/segment-builder/events.png)

Después de colocar el evento dentro del contenedor de eventos, seleccione el icono de puntos suspensivos (...), seguido de **[!UICONTROL Agregar]**.

![El texto agregado se resalta. Si selecciona esta opción, puede seleccionar funciones de agregación.](../images/ui/segment-builder/add-aggregation.png)

Ahora se agrega la agregación. Ahora puede seleccionar la función de agregación, elegir qué atributo agregar, la función de igualdad y el valor. Por el ejemplo siguiente, este segmento calificaría cualquier perfil que tenga una suma de valores comprados buena a 100 $, aunque cada compra individual sea inferior a 100 $.

![Las reglas de evento, que muestran una función de agregación.](../images/ui/segment-builder/filled-aggregation.png)

### Contar funciones {#count-functions}

Las funciones de recuento del Generador de segmentos se utilizan para buscar eventos especificados y contar la cantidad de veces que se han completado. Las funciones de recuento compatibles con el Generador de segmentos son &quot;Al menos&quot;, &quot;Como máximo&quot;, &quot;Exactamente&quot;, &quot;Entre&quot; y &quot;Todo&quot;.

Para crear una función de recuento, seleccione un evento en el carril izquierdo e insértelo en el [!UICONTROL Eventos] contenedor.

![Los campos de eventos se resaltan.](../images/ui/segment-builder/events.png)

Después de colocar el evento dentro del contenedor de eventos, seleccione la opción [!UICONTROL Al menos 1] botón.

![Al menos está resaltado, mostrando el área que desea seleccionar para ver una lista completa de funciones de recuento.](../images/ui/segment-builder/add-count.png)

Ahora se agrega la función de recuento. Ahora puede seleccionar la función de recuento y el valor de la función . El ejemplo siguiente sería incluir cualquier evento que tenga al menos un clic.

![Se muestra y se resalta una lista de las funciones de recuento.](../images/ui/segment-builder/select-count.png)

## Contenedores

Las reglas de segmentos se evalúan en el orden en que aparecen en la lista. Los contenedores permiten controlar el orden de ejecución mediante el uso de consultas anidadas.

Una vez que haya agregado al menos un mosaico al lienzo del generador de reglas, puede empezar a agregar contenedores. Para crear un contenedor nuevo, seleccione los puntos suspensivos (...) en la esquina superior derecha del mosaico y, a continuación, seleccione **[!UICONTROL Agregar contenedor]**.

![El botón Agregar contenedor se resalta, lo que permite agregar un contenedor como secundario del primer contenedor.](../images/ui/segment-builder/add-container.png)

Un nuevo contenedor aparece como secundario del primer contenedor, pero puede ajustar la jerarquía arrastrando y moviendo los contenedores. El comportamiento predeterminado de un contenedor es &quot;[!UICONTROL Incluir]&quot; el atributo, evento o audiencia proporcionados. Puede establecer la regla en &quot;[!UICONTROL Excluir]&quot; perfiles que coinciden con los criterios del contenedor seleccionando **[!UICONTROL Incluir]** en la esquina superior izquierda del mosaico y seleccione &quot;[!UICONTROL Excluir]&quot;.

Un contenedor secundario también se puede extraer y agregar en línea al contenedor principal seleccionando &quot;desajustar contenedor&quot; en el contenedor secundario. Seleccione los puntos suspensivos (...) en la esquina superior derecha del contenedor secundario para acceder a esta opción.

![Las opciones que permiten desajustar o eliminar el contenedor se resaltan.](../images/ui/segment-builder/include-exclude.png)

Una vez seleccionada **[!UICONTROL Desajustar contenedor]** el contenedor secundario se elimina y los criterios aparecen en línea.

>[!NOTE]
>
>Al desajustar contenedores, tenga cuidado de que la lógica siga cumpliendo con la definición de segmento deseada.

![El contenedor se muestra después de estar sin ajustar.](../images/ui/segment-builder/unwrapped-container.png)

## Combinar directivas

[!DNL Experience Platform] permite reunir datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear un perfil.

Puede seleccionar una directiva de combinación que coincida con su propósito de marketing para esta audiencia o utilizar la directiva de combinación predeterminada proporcionada por [!DNL Platform]. Puede crear varias directivas de combinación exclusivas de su organización, incluida la creación de su propia directiva de combinación predeterminada. Para obtener instrucciones paso a paso sobre la creación de directivas de combinación para su organización, comience leyendo el [información general sobre políticas de combinación](../../profile/merge-policies/overview.md).

Para seleccionar una política de combinación para su definición de segmento, seleccione el icono de engranaje en el **[!UICONTROL Campos]** y, a continuación, utilice la pestaña **[!UICONTROL Política de combinación]** menú desplegable para seleccionar la política de combinación que desee utilizar.

![Se resalta el selector de políticas de combinación. Esto le permite elegir qué política de combinación seleccionar para su definición de segmento.](../images/ui/segment-builder/merge-policy-selector.png)

## Propiedades del segmento {#segment-properties}

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_segmentproperties"
>title="Propiedades del segmento"
>abstract="La sección de propiedades del segmento muestra una estimación del tamaño del segmento resultante, mostrando el número de perfiles cualificados en comparación con el número total de perfiles. Esto le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia."

>[!CONTEXTUALHELP]
>id="platform_segments_createsegment_segmentbuilder_refreshestimate"
>title="Actualizar estimaciones"
>abstract="Puede actualizar las estimaciones de su segmento para ver inmediatamente una vista previa de cuántos perfiles calificarían para el segmento propuesto. Las estimaciones de audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/tutorials/create-a-segment.html?lang=en#estimate-and-preview-an-audience" text="Más información sobre la documentación"

Al crear una definición de segmento, la variable **[!UICONTROL Propiedades del segmento]** a la derecha del espacio de trabajo muestra una estimación del tamaño del segmento resultante, lo que le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia.

La variable **[!UICONTROL Propiedades del segmento]** también es donde puede especificar información importante sobre la definición del segmento, como su nombre, descripción y tipo de evaluación. Los nombres de definiciones de segmentos se utilizan para identificar el segmento entre los definidos por su organización y, por lo tanto, deben ser descriptivos, concisos y únicos.

A medida que siga creando su definición de segmento, puede ver una vista previa paginada de la audiencia seleccionando **[!UICONTROL Ver perfiles]**.

![Se resalta la sección de propiedades de la definición del segmento. Las propiedades del segmento incluyen, entre otras, el nombre del segmento, la descripción y el método de evaluación.](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Las estimaciones de audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de 1 millón de entidades en el almacén de perfiles, se utiliza el conjunto completo de datos; para entre 1 y 20 millones de entidades, se utilizan 1 millón de entidades; y para más de 20 millones de entidades, se utiliza el 5% del total de entidades. Encontrará más información sobre la generación de estimaciones de segmentos en la [sección de generación de estimaciones](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) del tutorial de creación de segmentos.

También puede seleccionar el método de evaluación. Si sabe qué método de evaluación desea utilizar, puede seleccionar el método de evaluación deseado mediante la lista desplegable. Si desea saber para qué tipos de evaluación se califica este segmento, puede seleccionar el icono Examinar ![icono de carpeta con una lupa](../images/ui/segment-builder/segment-evaluation-select-icon.png) para ver una lista de los métodos de evaluación de segmentos disponibles.

La variable [!UICONTROL Requisitos del método de evaluación] se abre. Esta ventana emergente muestra los métodos de evaluación disponibles, que son por lotes, flujo continuo y borde. La ventana emergente muestra qué métodos de evaluación son elegibles e inelegibles. Según los parámetros que haya utilizado en la definición del segmento, es posible que no cumpla los requisitos para ciertos métodos de evaluación. Para obtener más información sobre los requisitos para cada método de evaluación, lea la [segmentación de flujo continuo](./streaming-segmentation.md#query-types) o [segmentación de arista](./edge-segmentation.md#query-types) información general.

![Aparecerá la ventana emergente de idoneidad para el método de evaluación. Esto muestra qué métodos de evaluación de segmentos son elegibles e inelegibles para el segmento.](../images/ui/segment-builder/select-evaluation-method.png)

Si selecciona un método de evaluación no válido, se le pedirá que cambie las reglas de definición del segmento o el método de evaluación.

![Elemento emergente del método de evaluación. Si se selecciona un método de evaluación de segmentos no apto, la ventana emergente explica por qué no es apto.](../images/ui/segment-builder/ineligible-evaluation-method.png)

Encontrará más información sobre los distintos métodos de evaluación de definiciones de segmentos en la [información general sobre segmentación](../home.md#evaluate-segments).

## Pasos siguientes {#next-steps}

El Generador de segmentos proporciona un flujo de trabajo enriquecido que le permite aislar las audiencias comercializables de [!DNL Real-time Customer Profile] datos. Después de leer esta guía, debería poder:

- Cree definiciones de segmento mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Consulte las estimaciones de su audiencia potencial, lo que le permite ajustar las definiciones de segmentos según sea necesario.
- Habilite todas las definiciones de segmentos para la segmentación programada.
- Habilite definiciones de segmento especificadas para la segmentación de flujo continuo.

Para obtener más información sobre [!DNL Segmentation Service], continúe leyendo la documentación y complementando su aprendizaje viendo los vídeos relacionados. Para obtener más información sobre las otras partes de la variable [!DNL Segmentation Service] Interfaz de usuario, lea la [[!DNL Segmentation Service] guía del usuario](./overview.md)
