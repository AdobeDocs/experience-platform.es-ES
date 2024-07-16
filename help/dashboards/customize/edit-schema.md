---
keywords: Experience Platform;interfaz de usuario;IU;tableros;tablero;perfiles;segmentos;destinos;uso de licencias
title: Editar esquema para crear widgets de panel personalizados
description: Esta guía proporciona instrucciones paso a paso para seleccionar atributos y configurar el esquema de su organización con el fin de crear widgets personalizados para paneles de Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Editar esquema para crear widgets personalizados

Para crear widgets personalizados para paneles de Adobe Experience Platform, primero debe identificar los atributos de perfil del cliente en tiempo real en los que se basarán los widgets.

Esta guía proporciona instrucciones paso a paso para editar el esquema de su organización seleccionando atributos para crear widgets de panel personalizados.

Una vez seleccionados los atributos y configurado el esquema, puede continuar con los pasos para [crear widgets personalizados para sus paneles](custom-widgets.md).

>[!NOTE]
>
>A los usuarios se les debe otorgar el permiso de &quot;Administrar paneles estándar&quot; para poder editar el esquema. Para obtener información sobre los pasos necesarios para conceder permisos de acceso a los paneles, consulte la [guía de permisos de paneles](../permissions.md).

## Biblioteca de widgets {#widget-library}

Esta guía requiere acceso a la [!UICONTROL biblioteca de widgets] en el Experience Platform. Para obtener más información sobre la biblioteca de widgets y cómo acceder a ella desde la interfaz de usuario, lea la [descripción general de la biblioteca de widgets](widget-library.md).

## Editar esquema

Dentro de la biblioteca de widgets, la pestaña **[!UICONTROL Custom]** le permite crear widgets y compartirlos con otros usuarios de su organización para personalizar el aspecto de sus paneles.

Antes de poder crear widgets personalizados, se deben seleccionar atributos de perfil del cliente en tiempo real para garantizar que los datos se incluyan como parte de la instantánea diaria.

>[!IMPORTANT]
>
>Su organización puede seleccionar un máximo de 20 atributos.

Si su organización no ha seleccionado ningún atributo de perfil, comience por seleccionar **[!UICONTROL Configurar]** en el centro de la pantalla.

![La ficha Personalizado del área de trabajo de la biblioteca de widgets con la opción Configurar resaltada.](../images/customization/configure-schema.png)

Cuando se haya creado al menos un atributo personalizado, seleccione **[!UICONTROL Editar esquema]** para ver los atributos seleccionados y agregar más.

![La ficha Personalizado del área de trabajo de la biblioteca de widgets con el esquema de edición resaltado.](../images/customization/edit-schema.png)

## Seleccionar un atributo

Para seleccionar un atributo en el cuadro de diálogo **[!UICONTROL Seleccionar campo de esquema de unión]**, vaya al atributo en el esquema de unión (o utilice la búsqueda) y seleccione la casilla que hay junto al atributo. Al seleccionar la casilla de verificación, también se agrega el atributo a la lista **[!UICONTROL Atributos seleccionados]** en el lado derecho del cuadro de diálogo.

>[!NOTE]
>
>Para que un atributo sea visible para la selección, debe ser uno de los siguientes: Cadena, Fecha, Fecha-hora, Booleano, Corto, Largo, Entero o Byte. Los tipos de datos Map y Double no son compatibles y aparecen atenuados para que no se puedan seleccionar.

Después de elegir los atributos que deseas agregar, selecciona **[!UICONTROL Guardar]** para guardar tus atributos y volver a la pestaña de widgets personalizados.

>[!WARNING]
>Los atributos recién seleccionados estarán disponibles después de la siguiente captura de pantalla diaria cuando se actualicen los datos.

![Cuadro de diálogo para seleccionar atributos de esquema con atributos y Guardar resaltados.](../images/customization/select-attribute.png)

## Pasos siguientes

Después de leer esta guía, puede navegar a la biblioteca de widgets y seleccionar los atributos del perfil del cliente en tiempo real para configurar el esquema. Con los atributos de perfil seleccionados, puedes empezar a [crear widgets personalizados para tus paneles](custom-widgets.md).
