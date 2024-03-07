---
keywords: Experience Platform;inicio;temas populares;ui;XDM;sistema XDM;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos de experiencia;modelo de datos;modelo de datos;registro de esquemas;registro de esquemas;esquema;esquemas;esquemas;crear;tipo de datos;tipos de datos;
solution: Experience Platform
title: Crear y editar tipos de datos mediante la interfaz de usuario
type: Tutorial
description: Obtenga información sobre cómo crear y editar tipos de datos en la interfaz de usuario de Experience Platform.
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: c04e5a49f2a4e90345ca20ecd0547d02b5004fcf
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 6%

---

# Creación y edición de tipos de datos mediante la interfaz de usuario {#ui-create-and-edit}

>[!CONTEXTUALHELP]
>id="platform_schemas_datatype_filter"
>title="Filtro de tipo de datos estándar o personalizado"
>abstract="La lista de tipos de datos disponibles se filtra previamente en función de cómo se crearon. Seleccione el botón de opción para elegir entre las opciones Estándar y Personalizado. La opción Estándar muestra las entidades creadas por Adobe y la opción Personalizada muestra las entidades creadas dentro de su organización. Consulte la documentación para obtener más información sobre la creación y edición de tipos de datos."

En el modelo de datos de experiencia (XDM), los tipos de datos son campos reutilizables que contienen varios subcampos. Aunque son similares a los grupos de campos de esquema en el sentido de que permiten el uso coherente de una estructura de varios campos, los tipos de datos son más flexibles porque se pueden incluir en cualquier parte de la estructura de esquema, mientras que los grupos de campos solo se pueden añadir en el nivel raíz.

Adobe Experience Platform proporciona muchos tipos de datos estándar que se pueden utilizar para cubrir una amplia variedad de casos de uso comunes de administración de experiencias. Sin embargo, también puede definir sus propios tipos de datos personalizados para satisfacer sus necesidades comerciales únicas.

>[!NOTE]
>
>Si un campo está definido como un tipo de datos específico, no se puede crear el mismo campo con un tipo de datos diferente en otro esquema. Esta restricción se aplica a todo el inquilino de la organización.

Este tutorial trata los pasos para crear y editar tipos de datos personalizados en la interfaz de usuario de Platform.

## Requisitos previos {#prerequisites}

Esta guía requiere una comprensión práctica del sistema XDM. Consulte la [Información general de XDM](../../home.md) para obtener una introducción a la función de XDM dentro del ecosistema de Experience Platform, y la [conceptos básicos de composición de esquemas](../../schema/composition.md) para saber cómo los tipos de datos contribuyen a los esquemas XDM.

Aunque no es necesario para esta guía, se recomienda seguir el tutorial en [composición de un esquema en la IU](../../tutorials/create-schema-ui.md) para familiarizarse con las diversas capacidades de la [!DNL Schema Editor].

## Abra el [!DNL Schema Editor] para un tipo de datos {#data-type}

En la IU de Platform, seleccione **[!UICONTROL Esquemas]** en la navegación izquierda para abrir [!UICONTROL Esquemas] espacio de trabajo y seleccione **[!UICONTROL Tipos de datos]** pestaña. Se muestra una lista de los tipos de datos disponibles. La lista de tipos de datos se filtra automáticamente en función de cómo se crearon. La configuración predeterminada muestra los tipos de datos definidos por el Adobe. También puede filtrar la lista para mostrar los que ha creado su organización.

![El [!UICONTROL Esquemas] workspace con [!UICONTROL Esquemas] en el panel de navegación izquierdo y [!UICONTROL Tipos de datos] resaltado.](../../images/ui/resources/data-types/data-types-tab.png)

A partir de aquí, tiene las siguientes opciones:

- [Crear un nuevo tipo de datos](#create)
- [Filtrar tipos de datos](#filter)
- [Seleccione un tipo de datos existente para editarlo](#edit)

### Crear un nuevo tipo de datos {#create}

Desde el **[!UICONTROL Tipos de datos]** pestaña, seleccione **[!UICONTROL Crear tipo de datos]**.

![El [!UICONTROL Esquemas] workspace [!UICONTROL Tipos de datos] pestaña con [!UICONTROL Crear tipo de datos] resaltado.](../../images/ui/resources/data-types/create.png)

El [!DNL Schema Editor] aparece, mostrando la estructura actual del nuevo tipo de datos en el lienzo. En el lado derecho del editor, puede proporcionar un nombre para mostrar y una descripción opcional para el tipo de datos. Asegúrese de proporcionar un nombre único y conciso para el tipo de datos, ya que así es como se identificará al agregarlo a un esquema.

Este tutorial crea un tipo de datos que describe una propiedad de restaurante, de modo que al tipo de datos se le asigna el nombre para mostrar &quot;Restaurante&quot;.

![](../../images/ui/resources/data-types/data-type-properties.png)

Desde aquí puede ir directamente a la [sección siguiente](#add-fields) para empezar a agregar campos al nuevo tipo de datos.

### Filtrar tipos de datos {#filter}

La lista de tipos de datos disponibles se filtra previamente en función de cómo se crearon. Seleccione el botón de opción para elegir entre las [!UICONTROL Standard] y [!UICONTROL Personalizado] opciones. El [!UICONTROL Standard] muestra las entidades creadas por Adobe y la opción [!UICONTROL Personalizado] Esta opción muestra las entidades creadas dentro de su organización.

![El [!UICONTROL Tipos de datos] de la pestaña [!UICONTROL Esquemas] workspace con [!UICONTROL Standard] y [!UICONTROL Personalizado] resaltado.](../../images/ui/resources/data-types/standard-and-custom-data-types.png)

### Editar un tipo de datos existente {#edit}

>[!NOTE]
>
>Una vez que se utiliza un tipo de datos existente en un esquema que se ha habilitado para su uso en el Perfil del cliente en tiempo real, solo se pueden realizar cambios no destructivos en ese tipo de datos a partir de entonces. Consulte la [reglas de evolución de esquema](../../schema/composition.md#evolution) para obtener más información.

Solo se pueden editar los tipos de datos personalizados definidos por su organización. Seleccionar **[!UICONTROL Personalizado]** para mostrar solo los tipos de datos personalizados que son propiedad de su organización.

Seleccione el tipo de datos que desea editar de la lista para abrir el carril derecho, mostrando los detalles del tipo de datos. Desde el panel de detalles también puede descargar un archivo de muestra, copiar la estructura JSON o añadir el tipo de datos a un paquete.

Seleccione el nombre del tipo de datos en el carril derecho para abrir su estructura en la [!DNL Schema Editor].

![El [!UICONTROL Tipos de datos] de la pestaña [!UICONTROL Esquemas] workspace, con un tipo de datos, [!UICONTROL Personalizado] y el tipo de datos [!UICONTROL Nombre] resaltado.](../../images/ui/resources/data-types/edit.png)

## Añadir campos al tipo de datos {#add-fields}

Para empezar a añadir campos al tipo de datos, seleccione la **más (+)** junto al campo de nivel raíz en el lienzo. A continuación aparece un nuevo campo y el carril derecho se actualiza para mostrar los controles del nuevo campo.

![](../../images/ui/resources/data-types/new-field.png)

Utilice los controles del carril derecho para configurar los detalles del nuevo campo. Consulte la guía de [definición de campos en la IU](../fields/overview.md#define) para obtener pasos específicos sobre cómo configurar y agregar el campo al tipo de datos.

El tipo de datos Restaurant requiere un campo de cadena que represente el nombre del restaurante. Como tal, la variable [!UICONTROL Nombre de campo] se establece como &quot;nombre&quot; y la variable [!UICONTROL Tipo] se establece como &quot;[!UICONTROL Cadena]&quot;. Seleccionar **[!UICONTROL Aplicar]** para aplicar los cambios al campo.

![](../../images/ui/resources/data-types/name-field.png)

Siga agregando más campos al tipo de datos según sea necesario. El tipo de datos de ejemplo Restaurante ahora tiene campos adicionales para la marca, la capacidad de los asientos y la superficie.

![](../../images/ui/resources/data-types/more-fields.png)

Además de los campos básicos, también puede anidar tipos de datos adicionales dentro del tipo de datos personalizado. Por ejemplo, el tipo de datos Restaurante requiere un campo que represente la dirección física de la propiedad. En esta situación, puede agregar un nuevo campo &quot;dirección&quot; al que se le asigna el tipo de datos estándar &quot;[!UICONTROL Dirección postal]&quot;.

![](../../images/ui/resources/data-types/address-field.png)

Esto demuestra lo flexibles que pueden ser los tipos de datos a la hora de describir sus datos: los tipos de datos pueden emplear campos que también son tipos de datos, que a su vez pueden contener más tipos de datos, etc. Esto le permite abstraer y reutilizar patrones de datos comunes a través de los esquemas XDM, lo que facilita la representación de estructuras de datos complejas.

Cuando haya terminado de agregar campos al tipo de datos, seleccione **[!UICONTROL Guardar]** para guardar los cambios y agregar el tipo de datos a [!DNL Schema Library].

## Añadir el tipo de datos a un esquema {#add-data-type}

Una vez creado un tipo de datos, puede empezar a utilizarlo en los esquemas. Dado que los esquemas XDM están compuestos por una clase y cero o más grupos de campos, los campos proporcionados por un tipo de datos no se pueden añadir directamente a un esquema. En su lugar, deben incluirse en una clase o un grupo de campos.

Comience por seguir los pasos involucrados con [adición de un campo a una clase](./classes.md#add-fields) o [adición de un campo a un grupo de campos](./field-groups.md#add-fields). Como alternativa, puede iniciar [adición de un campo directamente a un esquema](./schemas.md#add-individual-fields) y elija la clase principal o el grupo de campos desde allí. Al elegir la variable **[!UICONTROL Tipo]** para el nuevo campo, seleccione el nombre del tipo de datos en el menú desplegable.

## Conversión de un objeto de varios campos en un tipo de datos {#convert}

Cuando se crea un campo de tipo de objeto con varios subcampos en la variable [!DNL Schema Editor]Además, puede convertir ese campo en un tipo de datos para poder utilizar la misma estructura de campo en una clase o grupo de campos diferente.

Para convertir un campo de tipo de objeto en un tipo de datos, seleccione el campo en el lienzo. Antes de convertir el campo, asegúrese de que la variable **[!UICONTROL Nombre para mostrar]** es descriptivo de los datos que contendrá el objeto, ya que se convertirá en el nombre del tipo de datos. Cuando esté listo para convertir el campo, seleccione **[!UICONTROL Convertir a nuevo tipo de datos]** en el carril derecho.

![](../../images/ui/resources/data-types/convert-object.png)

El lienzo actualiza el tipo de datos del campo de &quot;[!UICONTROL Objeto]&quot; al nuevo tipo de datos. Esta estructura ahora se puede reutilizar en otras clases y grupos de campos seleccionando este tipo de datos en la **[!UICONTROL Tipo]** cuando se define un nuevo campo.

![](../../images/ui/resources/data-types/converted.png)

## Pasos siguientes {#next-steps}

En esta guía se explica cómo crear y editar tipos de datos mediante la interfaz de usuario de Platform. Para obtener más información sobre las capacidades de [!UICONTROL Esquemas] Workspace, consulte la [[!UICONTROL Esquemas] información general de workspace](../overview.md).

Para obtener información sobre cómo administrar los tipos de datos mediante [!DNL Schema Registry] API, consulte la [guía de extremo de tipos de datos](../../api/data-types.md).
