---
keywords: Experience Platform;interfaz de usuario;IU;tableros;tablero;perfiles;segmentos;destinos;uso de licencias
title: Editar esquema para crear widgets de panel personalizados
description: Esta guía proporciona instrucciones paso a paso para seleccionar atributos y configurar el esquema de su organización con el fin de crear widgets personalizados para paneles de Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Editar esquema para crear widgets personalizados

Para crear widgets personalizados para paneles de Adobe Experience Platform, primero debe identificar los atributos de perfil del cliente en tiempo real en los que se basarán los widgets.

Esta guía proporciona instrucciones paso a paso para editar el esquema de su organización seleccionando atributos para crear widgets de panel personalizados.

Una vez seleccionados los atributos y configurado el esquema, puede continuar con los pasos para [creación de widgets personalizados para los paneles](custom-widgets.md).

>[!NOTE]
>
>A los usuarios se les debe otorgar el permiso de &quot;Administrar paneles estándar&quot; para poder editar el esquema. Para ver los pasos sobre la concesión de permisos de acceso para los paneles, consulte la [guía de permisos del panel](../permissions.md).

## Biblioteca de widgets {#widget-library}

Esta guía requiere acceso a [!UICONTROL Biblioteca de widgets] en el Experience Platform. Para obtener más información sobre la biblioteca de widgets y cómo acceder a ella dentro de la interfaz de usuario, comience por leer el [introducción a la biblioteca de widgets](widget-library.md).

## Editar esquema

En la biblioteca de widgets, la variable **[!UICONTROL Personalizado]** Esta pestaña permite crear widgets y compartirlos con otros usuarios de su organización para personalizar el aspecto de los paneles.

Antes de poder crear widgets personalizados, se deben seleccionar atributos de perfil del cliente en tiempo real para garantizar que los datos se incluyan como parte de la instantánea diaria.

>[!IMPORTANT]
>
>Su organización puede seleccionar un máximo de 20 atributos.

Si su organización no ha seleccionado ningún atributo de perfil, comience por seleccionar **[!UICONTROL Configurar]** en el centro de la pantalla.

![La pestaña Personalizado del espacio de trabajo de la biblioteca de widgets con Configurar resaltado.](../images/customization/configure-schema.png)

Cuando se haya creado al menos un atributo personalizado, seleccione **[!UICONTROL Editar esquema]** para ver los atributos seleccionados y agregar más.

![La pestaña Personalizado del espacio de trabajo de la biblioteca de widgets con Editar esquema resaltado.](../images/customization/edit-schema.png)

## Seleccionar un atributo

Para seleccionar un atributo en la **[!UICONTROL Seleccionar campo de esquema de unión]** , vaya al atributo en el esquema de unión (o utilice la búsqueda) y seleccione la casilla de verificación situada junto al atributo. Al seleccionar la casilla de verificación, también se agrega el atributo a **[!UICONTROL Atributos seleccionados]** en el lado derecho del cuadro de diálogo.

>[!NOTE]
>
>Para que un atributo sea visible para la selección, debe ser uno de los siguientes: Cadena, Fecha, Fecha-hora, Booleano, Corto, Largo, Entero o Byte. Los tipos de datos Map y Double no son compatibles y aparecen atenuados para que no se puedan seleccionar.

Después de elegir los atributos que desea agregar, seleccione **[!UICONTROL Guardar]** para guardar los atributos y volver a la pestaña widgets personalizados.

>[!WARNING]
>Los atributos recién seleccionados estarán disponibles después de la siguiente captura de pantalla diaria cuando se actualicen los datos.

![El cuadro de diálogo para seleccionar atributos de esquema con atributos y Guardar resaltados.](../images/customization/select-attribute.png)

## Pasos siguientes

Después de leer esta guía, puede navegar a la biblioteca de widgets y seleccionar los atributos del perfil del cliente en tiempo real para configurar el esquema. Con los atributos de perfil seleccionados, puede empezar [creación de widgets personalizados para los paneles](custom-widgets.md).
