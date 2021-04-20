---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;servicio de segmentación;guía del usuario;guía de interfaz de usuario;guía de interfaz de usuario de segmentación;generador de segmentos;Generador de segmentos;
solution: Experience Platform
title: Guía de la interfaz de usuario del Generador de segmentos
topic: ui guide
description: El Generador de segmentos en la interfaz de usuario de Adobe Experience Platform proporciona un espacio de trabajo enriquecido que le permite interactuar con los elementos de datos del perfil. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.
exl-id: b27516ea-8749-4b44-99d0-98d3dc2f4c65
translation-type: tm+mt
source-git-commit: bad293cf25b955496897d895169ec494416e9787
workflow-type: tm+mt
source-wordcount: '1942'
ht-degree: 0%

---

# [!DNL Segment Builder] Guía de la interfaz de usuario

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de  [!DNL Profile] datos. El espacio de trabajo proporciona controles intuitivos para la creación y edición de reglas, como los mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.

![](../images/ui/segment-builder/segment-builder.png)

## Componentes básicos de definición de segmentos

Los componentes básicos de las definiciones de segmentos son atributos y eventos. Además, los atributos y eventos contenidos en audiencias existentes también pueden utilizarse como componentes para nuevas definiciones.

Puede ver estos componentes básicos en la sección **[!UICONTROL Fields]** del lado izquierdo del espacio de trabajo [!DNL Segment Builder]. **[!UICONTROL Fields]** contiene una pestaña para cada uno de los componentes principales: &quot;[!UICONTROL Attributes]&quot;, &quot;[!UICONTROL Events]&quot; y &quot;[!UICONTROL Audiences]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Atributos

La pestaña **[!UICONTROL Attributes]** permite examinar los atributos [!DNL Profile] pertenecientes a la clase [!DNL XDM Individual Profile]. Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al lienzo del generador de reglas en el centro del espacio de trabajo. El [lienzo del generador de reglas](#rule-builder-canvas) se explica con más detalle más adelante en esta guía.

![](../images/ui/segment-builder/attributes.png)

### Eventos

La pestaña **[!UICONTROL Events]** le permite crear una audiencia en función de eventos o acciones que se hayan producido utilizando elementos de datos [!DNL XDM ExperienceEvent]. También puede encontrar Tipos de eventos en la pestaña **[!UICONTROL Events]**, que son una colección de eventos usados comúnmente para permitirle crear sus segmentos más rápidamente.

Además de poder buscar elementos [!DNL ExperienceEvent] , también puede buscar tipos de eventos. Los tipos de eventos utilizan la misma lógica de codificación que [!DNL ExperienceEvents], sin que sea necesario buscar en la clase [!DNL XDM ExperienceEvent] buscando el evento correcto. Por ejemplo, el uso de la barra de búsqueda para buscar &quot;carro&quot; devuelve los Tipos de eventos &quot;[!UICONTROL AddCart]&quot; y &quot;[!UICONTROL RemoveCart]&quot;, que son dos acciones del carro de compras que se usan con mucha frecuencia al crear definiciones de segmentos.

Se puede buscar cualquier tipo de componente escribiendo su nombre en la barra de búsqueda, que utiliza la sintaxis de búsqueda [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Los resultados de la búsqueda comienzan a rellenarse a medida que se introducen palabras completas. Por ejemplo, para generar una regla basada en el campo XDM `ExperienceEvent.commerce.productViews`, empiece a escribir &quot;vistas del producto&quot; en el campo de búsqueda. Una vez que se ha escrito la palabra &quot;producto&quot;, empiezan a aparecer los resultados de la búsqueda. Cada resultado incluye la jerarquía de objetos a la que pertenece.

>[!NOTE]
>
>Los campos de esquema personalizados definidos por su organización pueden tardar hasta 24 horas en aparecer y estar disponibles para su uso en la creación de reglas.

A continuación, puede arrastrar y soltar fácilmente [!DNL ExperienceEvents] y &quot;[!UICONTROL Event Types]&quot; en la definición del segmento.

![](../images/ui/segment-builder/events-eventTypes.png)

De forma predeterminada, solo se muestran los campos de esquema rellenados del almacén de datos. Esto incluye &quot;[!UICONTROL Event Types]&quot;. Si la lista &quot;[!UICONTROL Event Types]&quot; no está visible o solo puede seleccionar &quot;[!UICONTROL Any]&quot; como &quot;[!UICONTROL Event Type]&quot;, seleccione el **icono del engranaje** situado junto a **[!UICONTROL Fields]** y, a continuación, seleccione **[!UICONTROL Show full XDM schema]** en **[!UICONTROL Available Fields]**. Seleccione de nuevo el **icono de engranaje** para volver a la pestaña **[!UICONTROL Fields]** y ahora debería poder ver varios campos &quot;[!UICONTROL Event Types]&quot; y de esquema, independientemente de si contienen datos o no.

![](../images/ui/segment-builder/show-populated.png)

### Audiencias

La pestaña **[!UICONTROL Audiences]** enumera todas las audiencias importadas desde fuentes externas, como Adobe Audience Manager, así como las audiencias creadas dentro de [!DNL Experience Platform].

En la pestaña **[!UICONTROL Audiences]**, puede ver todos los orígenes disponibles como un grupo de carpetas. Al seleccionar las carpetas, se pueden ver las subcarpetas y audiencias disponibles. Además, puede seleccionar el icono de la carpeta (como se muestra en la imagen de la derecha) para ver la estructura de la carpeta (una marca de verificación indica la carpeta en la que se encuentra) y desplazarse fácilmente por las carpetas seleccionando el nombre de una carpeta en el árbol.

Puede pasar el ratón sobre la ⓘ junto a una audiencia para ver información sobre la audiencia, como su ID, descripción y la jerarquía de carpetas, para localizar la audiencia.

![](../images/ui/segment-builder/audience-folder-structure.png)

También puede buscar audiencias usando la barra de búsqueda, que utiliza la sintaxis de búsqueda de [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). En la pestaña **[!UICONTROL Audiences]**, seleccionar una carpeta de nivel superior hace que aparezca la barra de búsqueda, lo que le permite buscar dentro de esa carpeta. Los resultados de búsqueda solo comienzan a rellenarse una vez que se introducen palabras completas. Por ejemplo, para encontrar una audiencia denominada `Online Shoppers`, empiece a escribir &quot;En línea&quot; en la barra de búsqueda. Una vez que la palabra &quot;Online&quot; se ha escrito en su totalidad, aparecen los resultados de búsqueda que contienen la palabra &quot;Online&quot;.

## Lienzo del generador de reglas {#rule-builder-canvas}

Una definición de segmento es un conjunto de reglas que se utilizan para describir características clave o el comportamiento de una audiencia de destino. Estas reglas se crean utilizando el lienzo del generador de reglas, ubicado en el centro de [!DNL Segment Builder].

Para agregar una regla nueva a la definición del segmento, arrastre un mosaico desde la pestaña **[!UICONTROL Fields]** y suéltelo en el lienzo del generador de reglas. A continuación, se le presentarán opciones específicas del contexto según el tipo de datos que se agreguen. Los tipos de datos disponibles incluyen: cadenas, fechas, [!DNL ExperienceEvents], &quot;[!UICONTROL Event Types]&quot; y audiencias.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Los cambios más recientes en Adobe Experience Platform han actualizado el uso de los operadores lógicos `OR` y `AND` entre eventos. Estas actualizaciones no afectarán a los segmentos existentes. Sin embargo, estos cambios afectarán a todas las actualizaciones subsiguientes de segmentos existentes y nuevas creaciones de segmentos. Lea las [constantes de tiempo actualizadas](./segment-refactoring.md) para obtener más información.

### Adición de audiencias

Puede arrastrar y soltar una audiencia de la pestaña **[!UICONTROL Audience]** en el lienzo del generador de reglas para hacer referencia a la pertenencia a la audiencia en la nueva definición del segmento. Esto le permite incluir o excluir la pertenencia a una audiencia como atributo en la nueva regla de segmento.

Para [!DNL Platform] audiencias creadas con [!DNL Segment Builder], se le da la opción de convertir la audiencia en el conjunto de reglas que se usaron en la definición del segmento para esa audiencia. Esta conversión hace una copia de la lógica de regla, que se puede modificar sin afectar a la definición original del segmento. Asegúrese de haber guardado los cambios recientes en la definición del segmento antes de convertirla a la lógica de regla.

>[!NOTE]
>
>Al añadir una audiencia desde una fuente externa, solo se hace referencia a la pertenencia a la audiencia. No puede convertir la audiencia en reglas y, por lo tanto, las reglas utilizadas para crear la audiencia original no se pueden modificar en la nueva definición del segmento.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Si surgen conflictos al convertir audiencias en reglas, [!DNL Segment Builder] intentará conservar las opciones existentes lo mejor que pueda.

### Vista de código

También puede ver una versión basada en código de una regla creada en [!DNL Segment Builder]. Una vez creada la regla dentro del lienzo del generador de reglas, puede seleccionar **[!UICONTROL Code view]** para ver el segmento como PQL.

![](../images/ui/segment-builder/code-view.png)

La vista de código proporciona un botón que le permite copiar el valor del segmento para utilizarlo en llamadas API. Para obtener la última versión del segmento, asegúrese de haber guardado los cambios más recientes en el segmento.

![](../images/ui/segment-builder/copy-code.png)

### Funciones de agregación

Una agregación en [!DNL Segment Builder] es un cálculo de un grupo de atributos XDM cuyo tipo de datos es un número (un doble o un número entero). Las cuatro funciones de agregación admitidas en el Generador de segmentos son SUMA, PROMEDIO, MIN y MAX.

Para crear una función de agregación, seleccione un evento del carril izquierdo e insértelo en el contenedor [!UICONTROL Events].

![](../images/ui/segment-builder/select-event.png)

Después de colocar el evento dentro del contenedor de eventos, seleccione el icono de puntos suspensivos (...) seguido de **[!UICONTROL Aggregate]**.

![](../images/ui/segment-builder/add-aggregation.png)

Ahora se agrega la agregación. Ahora puede seleccionar la función de agregación, elegir qué atributo agregar, la función de igualdad y el valor. Por el ejemplo siguiente, este segmento calificaría cualquier perfil que tenga una suma de valores comprados buena a 100 $, aunque cada compra individual sea inferior a 100 $.

![](../images/ui/segment-builder/filled-aggregation.png)

### Contar funciones

Las funciones de recuento del Generador de segmentos se utilizan para buscar eventos especificados y contar la cantidad de veces que se han completado. Las funciones de recuento compatibles con el Generador de segmentos son &quot;Al menos&quot;, &quot;Como máximo&quot;, &quot;Exactamente&quot;, &quot;Entre&quot; y &quot;Todo&quot;.

Para crear una función de recuento, seleccione un evento en el carril izquierdo e insértelo en el contenedor [!UICONTROL Events] .

![](../images/ui/segment-builder/add-event.png)

Después de colocar el evento dentro del contenedor de eventos, seleccione el botón [!UICONTROL At least 1] .

![](../images/ui/segment-builder/add-count.png)

Ahora se agrega la función de recuento. Ahora puede seleccionar la función de recuento y el valor de la función . El ejemplo siguiente sería incluir cualquier evento que tenga al menos un clic.

![](../images/ui/segment-builder/select-count.png)

## Contenedores

Las reglas de segmentos se evalúan en el orden en que aparecen en la lista. Los contenedores permiten controlar el orden de ejecución mediante el uso de consultas anidadas.

Una vez que haya agregado al menos un mosaico al lienzo del generador de reglas, puede empezar a agregar contenedores. Para crear un contenedor nuevo, seleccione los puntos suspensivos (...) en la esquina superior derecha del mosaico y, a continuación, seleccione **[!UICONTROL Add container]**.

![](../images/ui/segment-builder/add-container.png)

Un nuevo contenedor aparece como secundario del primer contenedor, pero puede ajustar la jerarquía arrastrando y moviendo los contenedores. El comportamiento predeterminado de un contenedor es &quot;[!UICONTROL Include]&quot; el atributo, evento o audiencia proporcionados. Puede establecer la regla en perfiles &quot;[!UICONTROL Exclude]&quot; que coincidan con los criterios del contenedor seleccionando **[!UICONTROL Include]** en la esquina superior izquierda del mosaico y seleccionando &quot;[!UICONTROL Exclude]&quot;.

Un contenedor secundario también se puede extraer y agregar en línea al contenedor principal seleccionando &quot;desajustar contenedor&quot; en el contenedor secundario. Seleccione los puntos suspensivos (...) en la esquina superior derecha del contenedor secundario para acceder a esta opción.

![](../images/ui/segment-builder/include-exclude.png)

Una vez seleccionado **[!UICONTROL Unwrap container]**, el contenedor secundario se elimina y los criterios aparecen en línea.

>[!NOTE]
>
>Al desajustar contenedores, tenga cuidado de que la lógica siga cumpliendo con la definición de segmento deseada.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Combinar directivas

[!DNL Experience Platform] permite reunir datos de varias fuentes y combinarlos para ver una vista completa de cada uno de sus clientes. Al unir estos datos, las políticas de combinación son las reglas que [!DNL Platform] usa para determinar cómo se priorizarán los datos y qué datos se combinarán para crear un perfil.

Puede seleccionar una directiva de combinación que coincida con su propósito de marketing para esta audiencia o utilizar la directiva de combinación predeterminada proporcionada por [!DNL Platform]. Puede crear varias directivas de combinación exclusivas de su organización, incluida la creación de su propia directiva de combinación predeterminada. Para obtener instrucciones paso a paso sobre la creación de directivas de combinación para su organización, consulte el tutorial sobre [cómo trabajar con directivas de combinación mediante la IU](../../profile/ui/merge-policies.md).

Para seleccionar una política de combinación para su definición de segmento, seleccione el icono de engranaje en la ficha **[!UICONTROL Fields]** y, a continuación, utilice el menú desplegable **[!UICONTROL Merge Policy]** para seleccionar la política de combinación que desea utilizar.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Propiedades del segmento

Al crear una definición de segmento, la sección **[!UICONTROL Segment Properties]** del lado derecho del espacio de trabajo muestra una estimación del tamaño del segmento resultante, lo que le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia.

En la sección **[!UICONTROL Segment Properties]** también puede especificar información importante sobre la definición del segmento, incluido su nombre y descripción. Los nombres de definiciones de segmentos se utilizan para identificar el segmento entre los definidos por su organización y, por lo tanto, deben ser descriptivos, concisos y únicos.

A medida que siga creando su definición de segmento, puede ver una vista previa paginada de la audiencia seleccionando **[!UICONTROL View Profiles]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Las estimaciones de audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de 1 millón de entidades en el almacén de perfiles, se utiliza el conjunto completo de datos; para entre 1 y 20 millones de entidades, se utilizan 1 millón de entidades; y para más de 20 millones de entidades, se utiliza el 5% del total de entidades. Puede encontrar más información sobre la generación de estimaciones de segmentos en la [sección de generación de estimaciones](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) del tutorial de creación de segmentos.

## Pasos siguientes {#next-steps}

El Generador de segmentos proporciona un flujo de trabajo enriquecido que le permite aislar las audiencias comercializables de los datos [!DNL Real-time Customer Profile]. Después de leer esta guía, debería poder:

- Cree definiciones de segmento mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Consulte las estimaciones de su audiencia potencial, lo que le permite ajustar las definiciones de segmentos según sea necesario.
- Habilite todas las definiciones de segmentos para la segmentación programada.
- Habilite definiciones de segmento especificadas para la segmentación de flujo continuo.

Para obtener más información sobre [!DNL Segmentation Service], siga leyendo la documentación y complete su aprendizaje viendo los vídeos relacionados. Para obtener más información sobre las otras partes de la interfaz de usuario de [!DNL Segmentation Service], consulte la [[!DNL Segmentation Service] guía del usuario](./overview.md)
