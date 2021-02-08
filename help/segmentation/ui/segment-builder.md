---
keywords: Experience Platform;inicio;temas populares;Servicio de segmentación;segmentación;servicio de segmentación;guía del usuario;guía de ui;guía de ui de segmentación;generador de segmentos;Generador de segmentos;
solution: Experience Platform
title: Guía de la interfaz de usuario del Generador de segmentos
topic: ui guide
description: 'El Generador de segmentos en la interfaz de usuario de Adobe Experience Platform proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos de datos de Perfil. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar propiedades de datos. '
translation-type: tm+mt
source-git-commit: 8fc1c5414f38e84ed1700ee95b1c382007ff2c27
workflow-type: tm+mt
source-wordcount: '1928'
ht-degree: 0%

---


# [!DNL Segment Builder] Guía de la interfaz de usuario

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos  [!DNL Profile] de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.

![](../images/ui/segment-builder/segment-builder.png)

## Componentes básicos de definición de segmentos

Los componentes básicos de las definiciones de segmentos son atributos y eventos. Además, los atributos y eventos contenidos en las audiencias existentes también pueden utilizarse como componentes para nuevas definiciones.

Puede ver estos bloques de creación en la sección **[!UICONTROL Campos]** a la izquierda del área de trabajo [!DNL Segment Builder]. **** Los campos contienen una ficha para cada uno de los componentes principales: &quot;[!UICONTROL Atributos]&quot;, &quot;[!UICONTROL Eventos]&quot; y &quot;[!UICONTROL Audiencias]&quot;.

![](../images/ui/segment-builder/segment-fields.png)

### Atributos

La ficha **[!UICONTROL Atributos]** permite examinar [!DNL Profile] atributos pertenecientes a la clase [!DNL XDM Individual Profile]. Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al lienzo del generador de reglas en el centro del espacio de trabajo. El [lienzo del generador de reglas](#rule-builder-canvas) se analiza más detalladamente más adelante en esta guía.

![](../images/ui/segment-builder/attributes.png)

### Eventos

La ficha **[!UICONTROL Eventos]** le permite crear una audiencia basada en eventos o acciones que se llevaron a cabo mediante [!DNL XDM ExperienceEvent] elementos de datos. También puede encontrar Tipos de evento en la ficha **[!UICONTROL Eventos]**, que son una colección de eventos de uso común que le permiten crear sus segmentos más rápidamente.

Además de poder buscar [!DNL ExperienceEvent] elementos, también puede buscar Tipos de evento. Los tipos de evento utilizan la misma lógica de codificación que [!DNL ExperienceEvents], sin que sea necesario buscar en la clase [!DNL XDM ExperienceEvent] el evento correcto. Por ejemplo: si se utiliza la barra de búsqueda para buscar &quot;carro&quot;, se devuelven los Tipos de evento &quot;[!UICONTROL AddCart]&quot; y &quot;[!UICONTROL RemoveCart]&quot;, que son dos acciones de carro de compras que se utilizan con mucha frecuencia al generar definiciones de segmentos.

Se puede buscar cualquier tipo de componente escribiendo su nombre en la barra de búsqueda, que utiliza la sintaxis de búsqueda [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). Los resultados de búsqueda comienzan a llenarse a medida que se ingresan palabras completas. Por ejemplo, para generar una regla basada en el campo XDM `ExperienceEvent.commerce.productViews`, escriba &quot;vistas de producto&quot; en el campo de búsqueda. Una vez escrita la palabra &quot;producto&quot;, comienzan a aparecer los resultados de la búsqueda. Cada resultado incluye la jerarquía de objetos a la que pertenece.

>[!NOTE]
>
>Los campos de esquema personalizados definidos por su organización pueden tardar hasta 24 horas en aparecer y estar disponibles para su uso en la creación de reglas.

Luego puede arrastrar y soltar [!DNL ExperienceEvents] y &quot;[!UICONTROL Tipos de evento]&quot; en la definición del segmento.

![](../images/ui/segment-builder/events-eventTypes.png)

De forma predeterminada, solo se muestran los campos de esquema rellenados del almacén de datos. Esto incluye &quot;[!UICONTROL Tipos de evento]&quot;. Si la lista &quot;[!UICONTROL Tipos de evento]&quot; no está visible o sólo puede seleccionar &quot;[!UICONTROL Cualquiera]&quot; como &quot;[!UICONTROL Tipo de evento]&quot;, seleccione el **icono de engranaje** junto a **[!UICONTROL Campos]**, luego seleccione &lt;a 10/>Mostrar Xfull. DM esquema ]**en**[!UICONTROL  Campos disponibles ]**.**[!UICONTROL  Vuelva a seleccionar el **icono de engranaje** para volver a la ficha **[!UICONTROL Campos]** y debería poder vista de varios campos &quot;[!UICONTROL Tipos de evento]&quot; y de esquema, independientemente de si contienen datos o no.

![](../images/ui/segment-builder/show-populated.png)

### Audiencias

La ficha **[!UICONTROL Audiencias]** lista todas las audiencias importadas desde fuentes externas, como Adobe Audience Manager, así como audiencias creadas dentro de [!DNL Experience Platform].

En la ficha **[!UICONTROL Audiencias]**, puede ver todos los orígenes disponibles como un grupo de carpetas. Al seleccionar las carpetas, se pueden ver las subcarpetas y audiencias disponibles. Además, puede seleccionar el icono de la carpeta (como se muestra en la imagen de la parte extrema derecha) para realizar la vista de la estructura de la carpeta (una marca de verificación indica la carpeta en la que se encuentra actualmente) y desplazarse fácilmente por las carpetas seleccionando el nombre de la carpeta en el árbol.

Puede pasar el ratón por encima del ⓘ junto a una audiencia para obtener información de vista sobre la audiencia, incluido su ID, descripción y la jerarquía de carpetas, para localizar la audiencia.

![](../images/ui/segment-builder/audience-folder-structure.png)

También puede buscar audiencias mediante la barra de búsqueda, que utiliza la sintaxis de búsqueda [Lucene](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax). En la ficha **[!UICONTROL Audiencias]**, al seleccionar una carpeta de nivel superior, aparece la barra de búsqueda, lo que le permite buscar dentro de esa carpeta. Los resultados de la búsqueda sólo comienzan a completarse una vez ingresadas las palabras completas. Por ejemplo, para encontrar una audiencia con el nombre `Online Shoppers`, escriba &quot;En línea&quot; en el inicio de búsqueda. Una vez que la palabra &quot;En línea&quot; se ha escrito en su totalidad, aparecen los resultados de búsqueda que contienen la palabra &quot;en línea&quot;.

## Lienzo del generador de reglas {#rule-builder-canvas}

Una definición de segmento es un conjunto de reglas que se utilizan para describir las características clave o el comportamiento de una audiencia de destinatario. Estas reglas se crean utilizando el lienzo del generador de reglas, ubicado en el centro de [!DNL Segment Builder].

Para agregar una nueva regla a la definición del segmento, arrastre un mosaico de la ficha **[!UICONTROL Campos]** y suéltelo en el lienzo del generador de reglas. A continuación, se le presentarán opciones específicas del contexto según el tipo de datos que se agrega. Los tipos de datos disponibles incluyen: cadenas, fechas, [!DNL ExperienceEvents], &quot;[!UICONTROL Tipos de evento]&quot; y audiencias.

![](../images/ui/segment-builder/rule-builder-canvas.png)

>[!IMPORTANT]
>
>Los últimos cambios en Adobe Experience Platform han actualizado el uso de los operadores lógicos `OR` y `AND` entre eventos. Estas actualizaciones no afectarán a los segmentos existentes. Sin embargo, todos los cambios afectarán a todas las actualizaciones subsiguientes de segmentos existentes y nuevas creaciones de segmentos. Lea las [constantes de tiempo actualizadas](./segment-refactoring.md) para obtener más información.

### Añadir audiencias

Puede arrastrar y soltar una audiencia de la ficha **[!UICONTROL Audiencia]** en el lienzo del generador de reglas para hacer referencia a la pertenencia a la audiencia en la nueva definición del segmento. Esto le permite incluir o excluir la pertenencia a una audiencia como un atributo en la nueva regla de segmento.

Para las audiencias [!DNL Platform] creadas con [!DNL Segment Builder], se le ofrece la opción de convertir la audiencia en el conjunto de reglas que se usaron en la definición del segmento para esa audiencia. Esta conversión hace una copia de la lógica de regla, que se puede modificar sin afectar a la definición del segmento original. Asegúrese de que ha guardado los cambios recientes en la definición del segmento antes de convertirlo a lógica de regla.

>[!NOTE]
>
>Al agregar una audiencia desde un origen externo, solo se hace referencia a la pertenencia a la audiencia. No puede convertir la audiencia en reglas y, por lo tanto, las reglas utilizadas para crear la audiencia original no se pueden modificar en la nueva definición de segmento.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Si surgen conflictos al convertir audiencias en reglas, [!DNL Segment Builder] intentará preservar las opciones existentes de la mejor manera posible.

### Vista de código

Otra opción es la vista de una versión basada en código de una regla creada en [!DNL Segment Builder]. Una vez que haya creado la regla dentro del lienzo del generador de reglas, puede seleccionar **[!UICONTROL vista de código]** para ver el segmento como PQL.

![](../images/ui/segment-builder/code-view.png)

La vista de código proporciona un botón que le permite copiar el valor del segmento que se va a utilizar en las llamadas de API. Para obtener la versión más reciente del segmento, asegúrese de haber guardado los cambios más recientes en el segmento.

![](../images/ui/segment-builder/copy-code.png)

### Funciones de agregación

Una agregación en [!DNL Segment Builder] es un cálculo en un grupo de atributos XDM cuyo tipo de datos es un número (un doble o un entero). Las cuatro funciones de agregación admitidas en el Generador de segmentos son SUM, PROMEDIO, MIN y MAX.

Para crear una función de agregación, seleccione un evento del carril izquierdo e insértelo en el contenedor [!UICONTROL Eventos].

![](../images/ui/segment-builder/select-event.png)

Después de colocar el evento dentro del contenedor de Eventos, seleccione el icono de elipses (...), seguido de **[!UICONTROL Acumulada]**.

![](../images/ui/segment-builder/add-aggregation.png)

Ahora se agrega la agregación. Ahora puede seleccionar la función de agregación, elegir qué atributo se va a acumulado, la función de igualdad y el valor. Para el ejemplo siguiente, este segmento calificaría cualquier perfil que tenga una suma de valores comprados buena a más de $100, incluso si cada compra individual es menor a $100.

![](../images/ui/segment-builder/filled-aggregation.png)

## Contenedores

Las reglas de segmentos se evalúan en el orden en que aparecen en la lista. Los contenedores permiten controlar el orden de ejecución mediante el uso de consultas anidadas.

Una vez que haya agregado al menos un mosaico al lienzo del generador de reglas, puede empezar a agregar contenedores. Para crear un nuevo contenedor, seleccione las elipses (...) en la esquina superior derecha del mosaico y, a continuación, seleccione **[!UICONTROL Añadir contenedor]**.

![](../images/ui/segment-builder/add-container.png)

Un nuevo contenedor aparece como el secundario del primer contenedor, pero puede ajustar la jerarquía arrastrando y moviendo los contenedores. El comportamiento predeterminado de un contenedor es &quot;[!UICONTROL Incluir]&quot; el atributo, el evento o la audiencia proporcionados. Puede establecer la regla en perfiles &quot;[!UICONTROL Excluir]&quot; que coincidan con los criterios de contenedor seleccionando **[!UICONTROL Incluir]** en la esquina superior izquierda del mosaico y seleccionando &quot;[!UICONTROL Excluir]&quot;.

Un contenedor secundario también se puede extraer y agregar en línea al contenedor principal seleccionando &quot;Desajustar contenedor&quot; en el contenedor secundario. Seleccione las elipses (...) en la esquina superior derecha del contenedor secundario para acceder a esta opción.

![](../images/ui/segment-builder/include-exclude.png)

Una vez seleccionado **[!UICONTROL Desajustar contenedor]**, se elimina el contenedor secundario y los criterios aparecen en línea.

>[!NOTE]
>
>Al desajustar contenedores, tenga cuidado de que la lógica siga cumpliendo con la definición de segmento deseada.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Combinar directivas

[!DNL Experience Platform] le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] utiliza para determinar cómo se priorizarán los datos y qué datos se combinarán para crear un perfil.

Puede seleccionar una directiva de combinación que coincida con su propósito de marketing para esta audiencia o utilizar la directiva de combinación predeterminada proporcionada por [!DNL Platform]. Puede crear varias directivas de combinación exclusivas para su organización, incluida la creación de su propia directiva de combinación predeterminada. Para obtener instrucciones paso a paso sobre cómo crear políticas de combinación para su organización, consulte el tutorial sobre [cómo trabajar con políticas de combinación mediante la IU](../../profile/ui/merge-policies.md).

Para seleccionar una directiva de combinación para la definición del segmento, seleccione el icono de engranaje en la ficha **[!UICONTROL Campos]** y, a continuación, utilice el menú desplegable **[!UICONTROL Política de combinación]** para seleccionar la directiva de combinación que desee utilizar.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Propiedades del segmento

Al crear una definición de segmento, la sección **[!UICONTROL Propiedades del segmento]** a la derecha del área de trabajo muestra una estimación del tamaño del segmento resultante, lo que le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia.

En la sección **[!UICONTROL Propiedades del segmento]** también puede especificar información importante sobre la definición del segmento, incluido su nombre y descripción. Los nombres de definiciones de segmentos se utilizan para identificar el segmento entre los definidos por su organización y, por lo tanto, deben ser descriptivos, concisos y únicos.

A medida que siga generando la definición del segmento, puede realizar la vista de una previsualización paginada de la audiencia seleccionando **[!UICONTROL Perfiles de Vista]**.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Las estimaciones de audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de un millón de entidades en el almacén de perfiles, se utiliza el conjunto completo de datos; para entre 1 y 20 millones de entidades se utilizan 1 millón de entidades; y para más de 20 millones de entidades se utiliza el 5% del total. Encontrará más información sobre la generación de estimaciones de segmentos en la [sección de generación de estimaciones](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) del tutorial de creación de segmentos.

## Próximos pasos y recursos adicionales {#next-steps}

El Generador de segmentos proporciona un flujo de trabajo enriquecido que le permite aislar audiencias comercializables de datos [!DNL Real-time Customer Profile]. Después de leer esta guía, debería poder:

- Cree definiciones de segmentos mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Estimaciones de vista de su audiencia potencial, permitiéndole ajustar las definiciones de segmentos según sea necesario.
- Habilite todas las definiciones de segmentos para la segmentación programada.
- Active las definiciones de segmentos especificadas para la segmentación de flujo continuo.

Para obtener más información acerca de [!DNL Segmentation Service], siga leyendo la documentación y complementando su aprendizaje, vea los videos a continuación. Para obtener más información sobre las otras partes de la [!DNL Segmentation Service] interfaz de usuario, lea la [[!DNL Segmentation Service] guía del usuario](./overview.md)

>[!WARNING]
>
> La [!DNL Platform] IU que se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

**Crear un segmento:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Crear un segmento dinámico:**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)