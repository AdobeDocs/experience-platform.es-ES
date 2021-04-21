---
keywords: Experience Platform;inicio;temas populares;ui;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;esquema;esquema;esquemas;esquemas;crear;tipo de datos;tipos de datos;
solution: Experience Platform
title: Crear y editar tipos de datos mediante la interfaz de usuario
topic-legacy: tutorial
type: Tutorial
description: Obtenga información sobre cómo crear y editar tipos de datos en la interfaz de usuario del Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1106'
ht-degree: 0%

---

# Crear y editar tipos de datos mediante la interfaz de usuario

En el Modelo de datos de experiencia (XDM), los tipos de datos se utilizan como campos de referencia en clases o mezclas del mismo modo que los campos literales básicos; la diferencia clave es que los tipos de datos pueden definir varios subcampos. Aunque son similares a las mezclas en el sentido de que permiten el uso coherente de una estructura de varios campos, los tipos de datos son más flexibles porque pueden incluirse en cualquier lugar de la estructura del esquema, mientras que las mezclas sólo pueden agregarse en el nivel raíz.

Adobe Experience Platform proporciona muchos tipos de datos estándar que se pueden usar para cubrir una amplia variedad de casos de uso comunes de administración de experiencias. Sin embargo, también puede definir sus propios tipos de datos personalizados para satisfacer sus necesidades comerciales únicas.

Este tutorial trata los pasos para crear y editar tipos de datos personalizados en la interfaz de usuario de Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema del Experience Platform y los [conceptos básicos de la composición del esquema](../../schema/composition.md) para saber cómo los tipos de datos contribuyen a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir también el tutorial sobre [composición de un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las distintas capacidades de [!DNL Schema Editor].

## Abra [!DNL Schema Editor] para un tipo de datos

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Schemas]** en el panel de navegación izquierdo para abrir el espacio de trabajo [!UICONTROL Schemas] y, a continuación, seleccione la pestaña **[!UICONTROL Data types]** . Se muestra una lista de los tipos de datos disponibles, incluidos los definidos por el Adobe, así como los creados por su organización.

![](../../images/ui/resources/data-types/data-types-tab.png)

Desde aquí tiene dos opciones:

- [Crear un nuevo tipo de datos](#create)
- [Seleccionar un tipo de datos existente para editar](#edit)

### Crear un nuevo tipo de datos {#create}

En la pestaña **[!UICONTROL Data types]**, seleccione **[!UICONTROL Create data type]**.

![](../../images/ui/resources/data-types/create.png)

Aparece el [!DNL Schema Editor], que muestra la estructura actual del nuevo tipo de datos en el lienzo. A la derecha del editor, puede proporcionar un nombre para mostrar y una descripción opcional para el tipo de datos. Asegúrese de proporcionar un nombre único y conciso para su tipo de datos, ya que así es como se identificará al agregarlo a un esquema.

Este tutorial crea un tipo de datos que describe una propiedad de restaurante, por lo que al tipo de datos se le asigna el nombre para mostrar &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

A partir de aquí, puede avanzar a la [siguiente sección](#add-fields) para empezar a añadir campos al nuevo tipo de datos.

### Editar un tipo de datos existente

Solo se pueden editar los tipos de datos personalizados definidos por su organización. Para reducir la lista mostrada, seleccione el icono de filtro (![Icono de filtro](../../images/ui/resources/data-types/filter.png)) para mostrar los controles de filtrado basados en [!UICONTROL Owner]. Seleccione **[!UICONTROL Customer]** para mostrar solo los tipos de datos personalizados que pertenecen a su organización.

Seleccione el tipo de datos que desea editar en la lista para abrir el carril derecho, mostrando los detalles del tipo de datos. Seleccione el nombre del tipo de datos en el carril derecho para abrir su estructura en [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Agregar campos al tipo de datos {#add-fields}

Para empezar a añadir campos al tipo de datos, seleccione el icono **plus (+)** situado junto al campo de nivel raíz en el lienzo. A continuación aparece un nuevo campo y el carril derecho se actualiza para mostrar los controles del nuevo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilice los controles del carril derecho para configurar los detalles del nuevo campo. Consulte la guía sobre la [definición de campos en la interfaz de usuario](../fields/overview.md#define) para ver los pasos específicos sobre cómo configurar y agregar el campo al tipo de datos.

El tipo de datos Restaurant requiere un campo de cadena para representar el nombre del restaurante. Como tal, el [!UICONTROL Field name] se establece como &quot;nombre&quot; y el [!UICONTROL Type] se establece como &quot;[!UICONTROL String]&quot;. Seleccione **[!UICONTROL Apply]** para aplicar los cambios al campo.

![](../../images/ui/resources/data-types/name-field.png)

Siga agregando más campos al tipo de datos según sea necesario. El tipo de datos de ejemplo Restaurante ahora tiene campos adicionales para marca, capacidad de asiento y espacio en el suelo.

![](../../images/ui/resources/data-types/more-fields.png)

Además de los campos básicos, también puede anidar tipos de datos adicionales dentro del tipo de datos personalizado. Por ejemplo, el tipo de datos Restaurante requiere un campo que represente la dirección física de la propiedad. En esta situación, puede agregar un nuevo campo &quot;dirección&quot; al que se asigna el tipo de datos estándar &quot;[!UICONTROL Postal address]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Esto demuestra la flexibilidad de los tipos de datos en la descripción de los datos: los tipos de datos pueden emplear campos que también son tipos de datos, que pueden contener otros tipos de datos, etc. Esto le permite abstraer y reutilizar patrones de datos comunes en todos los esquemas XDM, lo que facilita la representación de estructuras de datos complejas.

Una vez que haya terminado de agregar campos al tipo de datos, seleccione **[!UICONTROL Save]** para guardar los cambios y agregar el tipo de datos al [!DNL Schema Library].

## Añadir el tipo de datos a una clase o mezcla

Una vez creado un tipo de datos, puede empezar a utilizarlo en sus esquemas. Dado que los esquemas XDM están compuestos por una clase y cero o más mezclas, los campos proporcionados por un tipo de datos no se pueden agregar directamente a un esquema. En su lugar, deben incluirse en una clase o mezcla.

Comience por seguir los pasos relacionados con la [adición de un campo a una clase](./classes.md#add-fields) o [adición de un campo a una mezcla](./mixins.md#add-fields). Cuando elija **[!UICONTROL Type]** para el nuevo campo, seleccione el nombre del tipo de datos en el menú desplegable.

## Conversión de un objeto de varios campos en un tipo de datos {#convert}

Cuando se crea un campo de tipo de objeto con varios subcampos en el [!DNL Schema Editor], se puede convertir ese campo en un tipo de datos para poder utilizar la misma estructura de campo en una clase o mezcla diferente.

Para convertir un campo de tipo objeto en un tipo de datos, seleccione el campo en el lienzo. Antes de convertir el campo, asegúrese de que **[!UICONTROL Display name]** sea descriptivo de los datos que contendrá el objeto, ya que este será el nombre del tipo de datos. Cuando esté listo para convertir el campo , seleccione **[!UICONTROL Convert to new data type]** en el carril derecho.

![](../../images/ui/resources/data-types/convert-object.png)

El lienzo actualiza el tipo de datos del campo de &quot;[!UICONTROL Object]&quot; al nuevo tipo de datos. Los subcampos también tienen iconos de bloqueo pequeños junto a ellos, lo que indica que ya no son campos individuales sino parte de un tipo de datos de varios campos. Esta estructura ahora se puede reutilizar en otras clases y mezclas seleccionando este tipo de datos en la lista desplegable **[!UICONTROL Type]** al definir un nuevo campo.

![](../../images/ui/resources/data-types/converted.png)

## Pasos siguientes

Esta guía explica cómo crear y editar tipos de datos mediante la interfaz de usuario de Platform. Para obtener más información sobre las capacidades del espacio de trabajo [!UICONTROL Schemas], consulte la [[!UICONTROL Schemas] descripción general del espacio de trabajo](../overview.md).

Para aprender a administrar los tipos de datos mediante la API [!DNL Schema Registry], consulte la [guía de extremo de los tipos de datos](../../api/data-types.md).
