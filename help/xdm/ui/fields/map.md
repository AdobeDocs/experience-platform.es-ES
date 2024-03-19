---
title: Definición de campos de mapa en la IU
description: Obtenga información sobre cómo definir un campo de asignación en la interfaz de usuario del Experience Platform.
source-git-commit: 8eea73c91d0671b1ddaeb8da0dc18b3e5e306f57
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Definición de campos de asignación en la IU

Adobe Experience Platform permite personalizar completamente la estructura de las clases personalizadas del modelo de datos de experiencia (XDM), los grupos de campos de esquema y los tipos de datos.

También puede definir campos de asignación en el Editor de esquemas para modelar estructuras de datos flexibles y dinámicas o almacenar una colección de pares clave-valor. La estructura de datos de asignación permite búsquedas, inserciones y eliminaciones eficientes y rápidas donde se organiza y accede a la información en función de identificadores únicos.

Al definir un nuevo campo en la interfaz de usuario de Platform, utilice el **[!UICONTROL Tipo]** y seleccione &quot;**[!UICONTROL Mapa]**&quot; de la lista.

![El Editor de esquemas con la lista desplegable Tipo y el valor Mapa resaltado.](../../images/ui/fields/special/map.png)

A [!UICONTROL Asignar tipo de valor] aparece la propiedad. Este valor es necesario para [!UICONTROL Mapa] tipos de datos. Los valores disponibles para el mapa son [!UICONTROL Cadena] y [!UICONTROL Entero]. Seleccione un valor de la lista desplegable de opciones disponibles.

![El Editor de esquemas con [!UICONTROL Asignar tipo de valor] menú desplegable resaltado.](../../images/ui/fields/special/map-value-type.png)

Una vez configurado el subcampo, debe asignarlo a un grupo de campos. Utilice el **[!UICONTROL Grupo de campos]** menú desplegable o campo de búsqueda y seleccione **[!UICONTROL Aplicar]**. Puede seguir añadiendo campos al objeto mediante el mismo proceso o seleccionar **[!UICONTROL Guardar]** para confirmar la configuración.

![Registro de la selección y configuración del grupo de campos que se está aplicando.](../../images/ui/fields/special/assign-to-field-group.gif)

>[!NOTE]
>
>La interfaz de usuario de Platform tiene limitaciones en la forma de extraer las claves de los campos de tipo mapa. Mientras que los campos de tipo objeto se pueden expandir, los mapas se muestran como un único campo. Los campos de asignación creados mediante la API de Registro de esquemas que no son tipos de datos de cadena o enteros se muestran como &quot;[!UICONTROL Complejo]&quot; tipos de datos.

## Pasos siguientes

Después de leer este documento, ahora puede definir los campos de asignación en la interfaz de usuario de Platform. Recuerde que solo puede utilizar clases y grupos de campos para agregar campos a esquemas. Para obtener más información sobre cómo administrar estos recursos en la interfaz de usuario, consulte las guías sobre creación y edición [clases](../resources/classes.md) y [grupos de campos](../resources/field-groups.md).

Para obtener más información sobre las capacidades de [!UICONTROL Esquemas] Workspace, consulte la [[!UICONTROL Esquemas] información general de workspace](../overview.md).
