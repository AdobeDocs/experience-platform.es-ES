---
keywords: Experience Platform;inicio;temas populares;ui;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquema;registro de esquema;esquema;esquema;esquemas;esquemas;crear;tipo de datos;tipos de datos;
solution: Experience Platform
title: Crear y editar tipos de datos mediante la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear y editar tipos de datos en la interfaz de usuario del Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 0%

---

# Crear y editar tipos de datos mediante la interfaz de usuario

En Experience Data Model (XDM), los tipos de datos son campos reutilizables que contienen varios subcampos. Aunque son similares a los grupos de campos de esquema en que permiten el uso coherente de una estructura de varios campos, los tipos de datos son más flexibles porque se pueden incluir en cualquier parte de la estructura de esquema, mientras que los grupos de campos solo se pueden agregar en el nivel raíz.

Adobe Experience Platform proporciona muchos tipos de datos estándar que se pueden usar para cubrir una amplia variedad de casos de uso comunes de administración de experiencias. Sin embargo, también puede definir sus propios tipos de datos personalizados para satisfacer sus necesidades comerciales únicas.

Este tutorial trata los pasos para crear y editar tipos de datos personalizados en la interfaz de usuario de Platform.

## Requisitos previos

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [Información general de XDM](../../home.md) para una introducción al papel de XDM dentro del ecosistema del Experience Platform, y [conceptos básicos de la composición del esquema](../../schema/composition.md) para saber cómo contribuyen los tipos de datos a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir también el tutorial de [composición de un esquema en la interfaz de usuario](../../tutorials/create-schema-ui.md) para familiarizarse con las diversas capacidades de la [!DNL Schema Editor].

## Abra el [!DNL Schema Editor] para un tipo de datos

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo para abrir [!UICONTROL Esquemas] espacio de trabajo y, a continuación, seleccione **[!UICONTROL Tipos de datos]** pestaña . Se muestra una lista de los tipos de datos disponibles, incluidos los definidos por el Adobe y los creados por su organización.

![](../../images/ui/resources/data-types/data-types-tab.png)

Desde aquí tiene dos opciones:

- [Crear un nuevo tipo de datos](#create)
- [Seleccionar un tipo de datos existente para editar](#edit)

### Crear un nuevo tipo de datos {#create}

En el **[!UICONTROL Tipos de datos]** , seleccione **[!UICONTROL Crear tipo de datos]**.

![](../../images/ui/resources/data-types/create.png)

La variable [!DNL Schema Editor] , mostrando la estructura actual del nuevo tipo de datos en el lienzo. A la derecha del editor, puede proporcionar un nombre para mostrar y una descripción opcional para el tipo de datos. Asegúrese de proporcionar un nombre único y conciso para su tipo de datos, ya que así es como se identificará al agregarlo a un esquema.

Este tutorial crea un tipo de datos que describe una propiedad de restaurante, por lo que al tipo de datos se le asigna el nombre para mostrar &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Desde aquí, puede avanzar hasta el [sección siguiente](#add-fields) para empezar a añadir campos al nuevo tipo de datos.

### Editar un tipo de datos existente

>[!NOTE]
>
>Una vez que se utiliza un tipo de datos existente en un esquema que se ha habilitado para su uso en el perfil del cliente en tiempo real, solo se pueden realizar cambios no destructivos en ese tipo de datos a partir de entonces. Consulte la [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Solo se pueden editar los tipos de datos personalizados definidos por su organización. Para reducir la lista mostrada, seleccione el icono de filtro (![Icono de filtro](../../images/ui/resources/data-types/filter.png)) para mostrar los controles del filtrado en función de [!UICONTROL Propietario]. Select **[!UICONTROL Cliente]** para mostrar solo los tipos de datos personalizados que pertenecen a su organización.

Seleccione el tipo de datos que desea editar en la lista para abrir el carril derecho, mostrando los detalles del tipo de datos. Seleccione el nombre del tipo de datos en el carril derecho para abrir su estructura en la [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## Añadir campos al tipo de datos {#add-fields}

Para empezar a añadir campos al tipo de datos, seleccione la opción **plus (+)** junto al campo de nivel raíz en el lienzo. A continuación aparece un nuevo campo y el carril derecho se actualiza para mostrar los controles del nuevo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilice los controles del carril derecho para configurar los detalles del nuevo campo. Consulte la guía de [definición de campos en la interfaz de usuario](../fields/overview.md#define) para ver pasos específicos sobre cómo configurar y añadir el campo al tipo de datos.

El tipo de datos Restaurant requiere un campo de cadena para representar el nombre del restaurante. Como tal, la variable [!UICONTROL Nombre del campo] se establece como &quot;nombre&quot; y [!UICONTROL Tipo] se configura como &quot;[!UICONTROL Cadena]&quot;. Select **[!UICONTROL Aplicar]** para aplicar los cambios al campo .

![](../../images/ui/resources/data-types/name-field.png)

Siga agregando más campos al tipo de datos según sea necesario. El tipo de datos de ejemplo Restaurante ahora tiene campos adicionales para marca, capacidad de asiento y espacio en el suelo.

![](../../images/ui/resources/data-types/more-fields.png)

Además de los campos básicos, también puede anidar tipos de datos adicionales dentro del tipo de datos personalizado. Por ejemplo, el tipo de datos Restaurante requiere un campo que represente la dirección física de la propiedad. En esta situación, puede agregar un nuevo campo &quot;dirección&quot; al que se asigna el tipo de datos estándar &quot;[!UICONTROL Dirección postal]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Esto demuestra la flexibilidad de los tipos de datos en la descripción de los datos: los tipos de datos pueden emplear campos que también son tipos de datos, que pueden contener otros tipos de datos, etc. Esto le permite abstraer y reutilizar patrones de datos comunes en todos los esquemas XDM, lo que facilita la representación de estructuras de datos complejas.

Una vez que haya terminado de agregar campos al tipo de datos, seleccione **[!UICONTROL Guardar]** para guardar los cambios y agregar el tipo de datos al [!DNL Schema Library].

## Añadir el tipo de datos a un esquema

Una vez creado un tipo de datos, puede empezar a utilizarlo en sus esquemas. Dado que los esquemas XDM están compuestos por una clase y cero o más grupos de campos, los campos proporcionados por un tipo de datos no se pueden agregar directamente a un esquema. En su lugar, deben incluirse en una clase o un grupo de campos.

Comience por seguir los pasos involucrados con [adición de un campo a una clase](./classes.md#add-fields) o [adición de un campo a un grupo de campos](./field-groups.md#add-fields). También puede empezar [adición de un campo directamente a un esquema](./schemas.md#add-individual-fields) y elija la clase principal o el grupo de campos desde allí. Al elegir el **[!UICONTROL Tipo]** para el nuevo campo, seleccione el nombre del tipo de datos en el menú desplegable.

## Conversión de un objeto de varios campos en un tipo de datos {#convert}

Cuando se crea un campo de tipo de objeto con varios subcampos en la variable [!DNL Schema Editor], puede convertir ese campo en un tipo de datos para que pueda utilizar la misma estructura de campos en una clase o grupo de campos diferente.

Para convertir un campo de tipo objeto en un tipo de datos, seleccione el campo en el lienzo. Antes de convertir el campo, asegúrese de que la variable **[!UICONTROL Nombre para mostrar]** es descriptivo de los datos que contendrá el objeto, ya que se convertirá en el nombre del tipo de datos. Cuando esté listo para convertir el campo, seleccione **[!UICONTROL Convertir en nuevo tipo de datos]** en el carril derecho.

![](../../images/ui/resources/data-types/convert-object.png)

El lienzo actualiza el tipo de datos del campo de &quot;[!UICONTROL Objeto]&quot; al nuevo tipo de datos. Esta estructura ahora se puede reutilizar en otras clases y grupos de campos seleccionando este tipo de datos de la variable **[!UICONTROL Tipo]** al definir un nuevo campo.

![](../../images/ui/resources/data-types/converted.png)

## Pasos siguientes

Esta guía explica cómo crear y editar tipos de datos mediante la interfaz de usuario de Platform. Para obtener más información sobre las capacidades de la variable [!UICONTROL Esquemas] espacio de trabajo, consulte [[!UICONTROL Esquemas] información general del espacio de trabajo](../overview.md).

Para aprender a administrar los tipos de datos mediante el [!DNL Schema Registry] API, consulte la [guía de extremo de tipos de datos](../../api/data-types.md).
