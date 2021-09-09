---
keywords: Experience Platform;interfaz de usuario;IU;paneles;tablero;perfiles;segmentos;destinos;uso de licencias
title: Editar esquema para crear widgets de tablero personalizados
description: 'Esta guía proporciona instrucciones paso a paso para seleccionar atributos y configurar el esquema de su organización con el fin de crear utilidades personalizadas para los paneles de Adobe Experience Platform. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Editar esquema para crear widgets personalizados

Para crear utilidades personalizadas para paneles de Adobe Experience Platform, primero debe identificar los atributos de perfil del cliente en tiempo real en los que se basarán las utilidades.

Esta guía proporciona instrucciones paso a paso para editar el esquema de su organización seleccionando atributos para crear widgets de tablero personalizados.

Una vez seleccionados los atributos y configurado el esquema, puede continuar con los pasos para [crear widgets personalizados para sus tableros](custom-widgets.md).

>[!NOTE]
>
>Se debe conceder a los usuarios el permiso &quot;Administrar tableros estándar&quot; para poder editar el esquema. Para ver los pasos sobre la concesión de permisos de acceso para los tableros, consulte la [guía de permisos de tablero](../permissions.md).

## Biblioteca de utilidades {#widget-library}

Esta guía requiere acceso a la [!UICONTROL biblioteca de utilidades] dentro de Experience Platform. Para obtener más información sobre la biblioteca de widgets y cómo acceder a ella dentro de la interfaz de usuario, lea por favor la [descripción general de la biblioteca de utilidades](widget-library.md).

## Edición del esquema

Dentro de la biblioteca de utilidades, la pestaña **[!UICONTROL Personalizado]** le permite crear utilidades y compartirlas con otros usuarios de su organización para personalizar el aspecto de sus tableros.

Para poder crear utilidades personalizadas, se deben seleccionar los atributos de Perfil del cliente en tiempo real para garantizar que los datos se incluyan como parte de la instantánea diaria.

>[!IMPORTANT]
>
>Su organización puede seleccionar un máximo de 20 atributos.

Si su organización no ha seleccionado ningún atributo de perfil, comience por seleccionar **[!UICONTROL Edit schema]** en la esquina superior derecha de la biblioteca de widgets.

Cuando se haya creado al menos un atributo personalizado, seleccione **[!UICONTROL Edit schema]** para ver los atributos seleccionados y añada más.

![](../images/customization/edit-schema.png)

## Seleccionar un atributo

Para seleccionar un atributo en el cuadro de diálogo **[!UICONTROL Select union schema field]**, vaya al atributo en el esquema de unión (o utilice la búsqueda) y seleccione la casilla situada junto al atributo. Al seleccionar la casilla de verificación, también se agrega el atributo a la lista **[!UICONTROL Atributos seleccionados]** en el lado derecho del cuadro de diálogo.

>[!NOTE]
>
>Para que un atributo esté visible para su selección, debe ser uno de los siguientes: Cadena, Fecha, Fecha-Hora, Booleano, Corto, Largo, Entero o Byte. Los tipos de datos Mapa y Doble no son compatibles y aparecen atenuados para que no se puedan seleccionar.

Después de elegir los atributos que desea añadir, seleccione **[!UICONTROL Save]** para guardar los atributos y volver a la pestaña de widgets personalizados.

>[!WARNING]
>Los atributos recién seleccionados estarán disponibles después de la siguiente instantánea diaria cuando se actualicen los datos.

![](../images/customization/select-attribute.png)

## Pasos siguientes

Después de leer esta guía, puede navegar a la biblioteca de utilidades y seleccionar los atributos del perfil del cliente en tiempo real para configurar el esquema. Con los atributos de perfil seleccionados, puede empezar a [crear widgets personalizados para sus tableros](custom-widgets.md).