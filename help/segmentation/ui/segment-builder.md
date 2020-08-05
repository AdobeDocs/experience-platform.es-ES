---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guía del usuario del Generador de segmentos del servicio de segmentación
topic: ui guide
translation-type: tm+mt
source-git-commit: ab43c677ab45c7aa047a50049c0dd8613b003403
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 0%

---


# [!DNL Segment Builder] guía del usuario

[!DNL Segment Builder] proporciona un espacio de trabajo enriquecido que le permite interactuar con elementos [!DNL Profile] de datos. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar propiedades de datos.

![](../images/ui/segment-builder/segment-builder.png)

## Componentes básicos de definición de segmentos

Los componentes básicos de las definiciones de segmentos son **[!UICONTROL Atributos]** y **[!UICONTROL Eventos]**. Además, los atributos y eventos contenidos en **[!UICONTROL Audiencias]** existentes también pueden utilizarse como componentes para nuevas definiciones.

Puede ver estos bloques de creación en la sección **[!UICONTROL Campos]** del lado izquierdo del [!DNL Segment Builder] espacio de trabajo. **[!UICONTROL Campos]** contiene una ficha para cada uno de los componentes principales: **[!UICONTROL Atributos]**, **[!UICONTROL Eventos]** y **[!UICONTROL Audiencias]**.

![](../images/ui/segment-builder/segment-fields.png)

### Atributos

La ficha **[!UICONTROL Atributos]** permite examinar [!DNL Profile] los atributos que pertenecen a la [!DNL XDM Individual Profile] clase. Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al lienzo del generador de reglas en el centro del espacio de trabajo. El lienzo [del generador de](#rule-builder-canvas) reglas se describe con más detalle más adelante en esta guía.

![](../images/ui/segment-builder/attributes.png)

### Eventos

La ficha **[!UICONTROL Eventos]** permite crear una audiencia basada en eventos o acciones que se hayan realizado con elementos [!DNL XDM ExperienceEvent] de datos. También puede encontrar Tipos de evento en la ficha **[!UICONTROL Eventos]** , que son una colección de eventos de uso común que le permiten crear sus segmentos más rápidamente.

Además de poder buscar [!DNL ExperienceEvent] elementos, también puede buscar Tipos de evento. Los Tipos de evento utilizan la misma lógica de codificación que [!DNL ExperienceEvents], sin necesidad de buscar en la [!DNL XDM ExperienceEvent] clase el evento correcto. Por ejemplo: si se utiliza la barra de búsqueda para buscar &quot;carro&quot;, se devuelven los Tipos de evento &quot;[!UICONTROL AddCart]&quot; y &quot;[!UICONTROL RemoveCart]&quot;, que son dos acciones de carro de compras que se utilizan con mucha frecuencia al generar definiciones de segmentos.

Se puede buscar cualquier tipo de componente escribiendo su nombre en la barra de búsqueda, que utiliza la sintaxis [de búsqueda de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. Los resultados de búsqueda comienzan a llenarse a medida que se ingresan palabras completas. Por ejemplo, para generar una regla basada en el campo XDM `ExperienceEvent.commerce.productViews`, escriba &quot;vistas de producto&quot; en el inicio de búsqueda. Una vez escrita la palabra &quot;producto&quot;, comienzan a aparecer los resultados de la búsqueda. Cada resultado incluye la jerarquía de objetos a la que pertenece.

>[!NOTE]
>
>Los campos de esquema personalizados definidos por su organización pueden tardar hasta 24 horas en aparecer y estar disponibles para su uso en la creación de reglas.

A continuación, puede arrastrar y soltar fácilmente [!DNL ExperienceEvents] y [!UICONTROL Tipos de evento] en la definición del segmento.

![](../images/ui/segment-builder/events-eventTypes.png)

De forma predeterminada, solo se muestran los campos de esquema rellenados del almacén de datos. Esto incluye [!UICONTROL Tipos de evento]. Si la lista de [!UICONTROL Tipos de evento] no está visible o sólo puede seleccionar &quot;[!UICONTROL Cualquiera]&quot; como [!UICONTROL Tipo de evento], seleccione el icono de engranaje situado junto a **[!UICONTROL Campos]** y, a continuación, seleccione **[!UICONTROL Mostrar esquema]** **** XDM completo en Campos disponibles. Seleccione de nuevo el icono de engranaje para volver a la ficha **[!UICONTROL Campos]** y ahora debe poder realizar la vista de varios campos de [!UICONTROL Tipos de evento] y esquemas, independientemente de si contienen datos o no.

![](../images/ui/segment-builder/show-populated.png)

### Audiencias

La ficha **[!UICONTROL Audiencias]** lista todas las audiencias importadas desde fuentes externas, como Adobe Audience Manager, así como las audiencias creadas dentro de [!DNL Experience Platform].

En la ficha **[!UICONTROL Audiencias]** , puede ver todos los orígenes disponibles como un grupo de carpetas. Al seleccionar las carpetas, se pueden ver las subcarpetas y audiencias disponibles. Además, puede seleccionar el icono de la carpeta (como se muestra en la imagen de la parte extrema derecha) para realizar la vista de la estructura de la carpeta (una marca de verificación indica la carpeta en la que se encuentra actualmente) y desplazarse fácilmente por las carpetas seleccionando el nombre de la carpeta en el árbol.

Puede pasar el ratón por encima del ⓘ junto a una audiencia para obtener información de vista sobre la audiencia, incluido su ID, descripción y la jerarquía de carpetas, para localizar la audiencia.

![](../images/ui/segment-builder/audience-folder-structure.png)

También puede buscar [!UICONTROL Audiencias] mediante la barra de búsqueda, que utiliza la sintaxis [de búsqueda de](https://docs.microsoft.com/en-us/azure/search/query-lucene-syntax)Lucene. En la ficha **[!UICONTROL Audiencias]** , al seleccionar una carpeta de nivel superior, aparece la barra de búsqueda, lo que le permite buscar dentro de esa carpeta. Los resultados de la búsqueda sólo comienzan a completarse una vez ingresadas las palabras completas. Por ejemplo, para buscar una [!UICONTROL Audiencia] con el nombre `Online Shoppers`, escriba &quot;En línea&quot; en el inicio de búsqueda. Una vez que la palabra &quot;En línea&quot; se ha escrito en su totalidad, aparecen los resultados de búsqueda que contienen la palabra &quot;en línea&quot;.

## Lienzo del generador de reglas {#rule-builder-canvas}

Una definición de segmento es un conjunto de reglas que se utilizan para describir las características clave o el comportamiento de una audiencia de destinatario. Estas reglas se crean utilizando el lienzo del generador de reglas, ubicado en el centro de [!DNL Segment Builder].

Para agregar una nueva regla a la definición del segmento, arrastre un mosaico desde la ficha **[!UICONTROL Campos]** y suéltelo en el lienzo del generador de reglas. A continuación, se le presentarán opciones específicas del contexto según el tipo de datos que se agrega. Los tipos de datos disponibles incluyen: cadenas, fechas, [!DNL ExperienceEvents], [!UICONTROL Tipos de evento]y [!UICONTROL Audiencias].

![](../images/ui/segment-builder/rule-builder-canvas.png)

### Añadir audiencias

Puede arrastrar y soltar una audiencia de la ficha **[!UICONTROL Audiencia]** en el lienzo del generador de reglas para hacer referencia a la pertenencia a la audiencia en la nueva definición del segmento. Esto le permite incluir o excluir la pertenencia a una audiencia como un atributo en la nueva regla de segmento.

Para [!DNL Platform] audiencias creadas con [!DNL Segment Builder], se le ofrece la opción de convertir la audiencia en el conjunto de reglas que se utilizaron en la definición del segmento para esa audiencia. Esta conversión hace una copia de la lógica de regla, que se puede modificar sin afectar a la definición del segmento original. Asegúrese de que ha guardado los cambios recientes en la definición del segmento antes de convertirlo a lógica de regla.

>[!NOTE]
>
>Al agregar una audiencia desde un origen externo, solo se hace referencia a la pertenencia a la audiencia. No puede convertir la audiencia en reglas y, por lo tanto, las reglas utilizadas para crear la audiencia original no se pueden modificar en la nueva definición de segmento.

![](../images/ui/segment-builder/add-audience-to-segment.png)

Si surgen conflictos al convertir audiencias en reglas, [!DNL Segment Builder] intentará conservar las opciones existentes en la medida de sus posibilidades.

### vista de código

Como alternativa, puede vista una versión basada en código de una regla creada en la [!DNL Segment Builder]. Una vez que haya creado la regla dentro del lienzo del generador de reglas, puede seleccionar vista **[!UICONTROL de]** código para ver el segmento como PQL.

![](../images/ui/segment-builder/code-view.png)

La vista de código proporciona un botón que le permite copiar el valor del segmento que se va a utilizar en las llamadas de API. Para obtener la versión más reciente del segmento, asegúrese de haber guardado los cambios más recientes en el segmento.

![](../images/ui/segment-builder/copy-code.png)

## Contenedores

Las reglas de segmentos se evalúan en el orden en que aparecen en la lista. Los Contenedores permiten controlar el orden de ejecución mediante el uso de consultas anidadas.

Una vez que haya agregado al menos un mosaico al lienzo del generador de reglas, puede empezar a agregar contenedores. Para crear un nuevo contenedor, seleccione las elipses (...) en la esquina superior derecha del mosaico y, a continuación, seleccione **[!UICONTROL Añadir contenedor]**.

![](../images/ui/segment-builder/add-container.png)

Un nuevo contenedor aparece como el secundario del primer contenedor, pero puede ajustar la jerarquía arrastrando y moviendo los contenedores. El comportamiento predeterminado de un contenedor es &quot;[!UICONTROL Incluir]&quot; el atributo, el evento o la audiencia proporcionados. Puede definir la regla en perfiles de &quot;[!UICONTROL exclusión]&quot; que coincidan con los criterios de contenedor seleccionando **[!UICONTROL Incluir]** en la esquina superior izquierda del mosaico y seleccionando &quot;[!UICONTROL Excluir]&quot;.

Un contenedor secundario también se puede extraer y agregar en línea al contenedor principal seleccionando &quot;Desajustar contenedor&quot; en el contenedor secundario. Seleccione las elipses (...) en la esquina superior derecha del contenedor secundario para acceder a esta opción.

![](../images/ui/segment-builder/include-exclude.png)

Una vez seleccionado **[!UICONTROL Desajustar contenedor]** , se elimina el contenedor secundario y los criterios aparecen en línea.

>[!NOTE]
>
>Al desajustar contenedores, tenga cuidado de que la lógica siga cumpliendo con la definición de segmento deseada.

![](../images/ui/segment-builder/unwrapped-container-inline.png)

## Combinar directivas

[!DNL Experience Platform] le permite reunir datos de múltiples fuentes y combinarlos para ver una vista completa de cada uno de sus clientes individuales. Al reunir estos datos, las políticas de combinación son las reglas que [!DNL Platform] se utilizan para determinar cómo se priorizarán los datos y qué datos se combinarán para crear un perfil.

Puede seleccionar una directiva de combinación que coincida con el propósito de marketing de esta audiencia o utilizar la directiva de combinación predeterminada proporcionada por [!DNL Platform]. Puede crear varias directivas de combinación exclusivas para su organización, incluida la creación de su propia directiva de combinación predeterminada. Para obtener instrucciones paso a paso sobre la creación de políticas de combinación para su organización, consulte el tutorial sobre el [trabajo con políticas de combinación mediante la interfaz de usuario](../../profile/ui/merge-policies.md).

Para seleccionar una directiva de combinación para la definición del segmento, seleccione el icono de engranaje en la ficha **[!UICONTROL Campos]** y, a continuación, utilice el menú desplegable **[!UICONTROL Combinar directiva]** para seleccionar la directiva de combinación que desee utilizar.

![](../images/ui/segment-builder/merge-policy-selector.png)

## Propiedades del segmento

Al crear una definición de segmento, la sección Propiedades *[!UICONTROL del]* segmento en el lado derecho del espacio de trabajo muestra una estimación del tamaño del segmento resultante, lo que le permite ajustar la definición del segmento según sea necesario antes de crear la propia audiencia.

En la sección Propiedades **** del segmento también puede especificar información importante sobre la definición del segmento, incluidos su **[!UICONTROL nombre]** y **[!UICONTROL descripción]**. Los nombres de definiciones de segmentos se utilizan para identificar el segmento entre los definidos por su organización y, por lo tanto, deben ser descriptivos, concisos y únicos.

A medida que siga generando la definición del segmento, puede realizar la vista de una previsualización paginada de la audiencia seleccionando Perfiles **[!UICONTROL de]** Vista.

![](../images/ui/segment-builder/segment-properties.png)

>[!NOTE]
>
>Las estimaciones de Audiencia se generan utilizando un tamaño de muestra de los datos de muestra de ese día. Si hay menos de un millón de entidades en el almacén de perfiles, se utiliza el conjunto completo de datos; para entre 1 y 20 millones de entidades se utilizan 1 millón de entidades; y para más de 20 millones de entidades se utiliza el 5% del total. Encontrará más información sobre la generación de estimaciones de segmentos en la sección [de generación de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) estimaciones del tutorial de creación de segmentos.

## Próximos pasos y recursos adicionales {#next-steps}

El Generador de segmentos proporciona un flujo de trabajo enriquecido que le permite aislar audiencias comercializables de [!DNL Real-time Customer Profile] los datos. Después de leer esta guía, debería poder:

- Cree definiciones de segmentos mediante una combinación de atributos, eventos y audiencias existentes como componentes básicos.
- Utilice el lienzo y los contenedores del generador de reglas para controlar el orden en que se ejecutan las reglas de segmentos.
- Estimaciones de Vista de su audiencia potencial, permitiéndole ajustar las definiciones de segmentos según sea necesario.
- Habilite todas las definiciones de segmentos para la segmentación programada.
- Habilite definiciones de segmentos especificadas para la segmentación de flujo continuo.

Para obtener más información sobre [!DNL Segmentation Service], siga leyendo la documentación y complementando su aprendizaje, vea los vídeos siguientes. Para obtener más información sobre las otras partes de la [!DNL Segmentation Service] interfaz de usuario, lea la guía del [[!DNL Segmentation Service] usuario](./overview.md)

>[!WARNING]
>
> La [!DNL Platform] interfaz de usuario que se muestra en los siguientes vídeos no está actualizada. Consulte la documentación anterior para obtener las capturas de pantalla y la funcionalidad más recientes de la interfaz de usuario.

**Crear un segmento:**

>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)

**Crear un segmento dinámico:**

>[!VIDEO](https://video.tv.adobe.com/v/27428?quality=12&learn=on)