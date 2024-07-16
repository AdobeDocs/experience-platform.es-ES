---
title: Definición de campos de mapa en la IU
description: Obtenga información sobre cómo definir un campo de asignación en la interfaz de usuario del Experience Platform.
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: ee27fc42a1ee23ef650d320df64e5970a84d0d38
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Definición de campos de asignación en la IU

Adobe Experience Platform permite personalizar completamente la estructura de las clases personalizadas del modelo de datos de experiencia (XDM), los grupos de campos de esquema y los tipos de datos.

También puede definir campos de asignación en el Editor de esquemas para modelar estructuras de datos flexibles y dinámicas o almacenar una colección de pares clave-valor.

Al definir un nuevo campo en la interfaz de usuario (IU) de Platform, use la lista desplegable **[!UICONTROL Tipo]** y seleccione &quot;**[!UICONTROL Mapa]**&quot; de la lista.

![Editor de esquemas con la lista desplegable Tipo y el valor de Mapa resaltados.](../../images/ui/fields/special/map.png)

Aparece una propiedad [!UICONTROL Map value type]. Este valor es necesario para los tipos de datos [!UICONTROL Map]. Los valores disponibles para el mapa son [!UICONTROL String] y [!UICONTROL Integer]. Seleccione un valor de la lista desplegable de opciones disponibles.

![Se ha resaltado el editor de esquemas con la lista desplegable [!UICONTROL Asignar tipo de valor].](../../images/ui/fields/special/map-value-type.png)

Una vez configurado el subcampo, debe asignarlo a un grupo de campos. Utilice el menú desplegable **[!UICONTROL Grupo de campos]** o el campo de búsqueda y seleccione **[!UICONTROL Aplicar]**. Puede seguir agregando campos al objeto mediante el mismo proceso o seleccionar **[!UICONTROL Guardar]** para confirmar la configuración.

![Registro de la selección y configuración del grupo de campos que se está aplicando.](../../images/ui/fields/special/assign-to-field-group.gif)

## Restricciones de uso {#restrictions}

XDM impone las siguientes restricciones al uso de este tipo de datos:

* Los tipos de mapa DEBEN ser del tipo `object`.
* Los tipos de mapa NO DEBEN tener propiedades definidas (es decir, definen objetos &quot;vacíos&quot;).
* Los tipos de mapa DEBEN incluir un campo `additionalProperties.type` que describa los valores que se pueden colocar en el mapa, ya sea `string` o `integer`.
* La segmentación de varias entidades solo se puede definir en función de las claves de asignación y no de los valores.
* Las audiencias de la cuenta no admiten mapas.

Asegúrese de utilizar únicamente campos de tipo mapa cuando sea absolutamente necesario, ya que presentan los siguientes inconvenientes de rendimiento:

* El tiempo de respuesta de [Adobe Experience Platform Query Service](../../../query-service/home.md) se degrada de tres a diez segundos para 100 millones de registros.
* Los mapas deben tener menos de 16 claves o se arriesgarán a una mayor degradación.

>[!NOTE]
>
>La interfaz de usuario de Platform tiene limitaciones en la forma de extraer las claves de los campos de tipo mapa. Mientras que los campos de tipo objeto se pueden expandir, los mapas se muestran como un único campo. Los campos de asignación creados mediante la API de Registro de esquemas que no son tipos de datos de cadena o enteros se muestran como tipos de datos &quot;[!UICONTROL Complejos]&quot;.

## Pasos siguientes

Después de leer este documento, ahora puede definir los campos de asignación en la interfaz de usuario de Platform. Recuerde que solo puede utilizar clases y grupos de campos para agregar campos a esquemas. Para obtener más información sobre cómo administrar estos recursos en la interfaz de usuario, consulte las guías sobre la creación y edición de [clases](../resources/classes.md) y [grupos de campos](../resources/field-groups.md).

Para obtener más información sobre las capacidades del área de trabajo [!UICONTROL Esquemas], consulte la descripción general del área de trabajo [[!UICONTROL Esquemas]](../overview.md).
