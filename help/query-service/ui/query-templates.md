---
title: Plantillas de consulta
description: Las plantillas de consulta son consultas SQL guardadas reutilizables que otros usuarios pueden reutilizar para ahorrar tiempo y esfuerzo. Se pueden crear mediante el Editor de consultas o la API del servicio de consultas y están disponibles para su uso en todos los conjuntos de datos de Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Plantillas de consulta

El servicio de consultas de Adobe Experience Platform permite guardar y reutilizar código SQL en forma de plantillas de consulta. Las plantillas ahorran esfuerzo al evitar la repetición de tareas que se realizan con más frecuencia. Puede compartir plantillas dentro de su organización y cambiar fácilmente los valores de la consulta sin necesidad de acceder o comprender el SQL subyacente.

Este documento proporciona la información necesaria para crear plantillas de consulta en el servicio de consultas.

## Requisitos previos

Debe tener el permiso [!UICONTROL Administrar consultas] habilitado para acceder al Editor de consultas y ver el panel de consultas en la interfaz de usuario de Experience Platform. El permiso se habilita a través de Adobe [Admin Console](https://adminconsole.adobe.com/). Póngase en contacto con el administrador de su organización si no tiene privilegios de administrador para habilitar este permiso. Consulte la documentación de control de acceso para obtener [instrucciones completas sobre cómo agregar permisos a través de Admin Console](../../access-control/home.md).

## Creación de una plantilla de consulta

Puede crear plantillas de consulta mediante dos métodos, ya sea realizando una petición POST al extremo `query-templates` de la API del servicio de consultas o escribiendo, nombrando y guardando una consulta a través del Editor de consultas.

### Utilice el Editor de consultas para crear y guardar una consulta como plantilla

Consulte la documentación para obtener instrucciones sobre cómo usar el Editor de consultas para [escribir](./user-guide.md#query-authoring) y [guardar consultas](./user-guide.md#saving-queries). Una vez que haya asignado un nombre a la consulta y la haya guardado, podrá volver a utilizarla como plantilla de consulta en la ficha [!UICONTROL Plantillas].

>[!TIP]
>
>Al guardar una consulta en el Editor de consultas, aparece un mensaje de confirmación para notificarle que la acción se ha realizado correctamente. Este mensaje emergente contiene un vínculo que proporciona una forma cómoda de desplazarse al espacio de trabajo de programación de consultas. Consulte la [documentación de consultas de programación](./query-schedules.md) para obtener información sobre cómo ejecutar consultas en una cadencia personalizada.

## Examinar plantillas de consulta {#browse}

En el área de trabajo Consultas de la IU de Experience Platform, seleccione **[!UICONTROL Plantillas]** para mostrar la lista de consultas guardadas disponibles.

![Espacio de trabajo de consultas con la ficha Plantillas resaltada.](../images/ui/query-templates/query-templates.png)

Para buscar información de plantilla relevante, seleccione cualquier plantilla de consulta de la lista disponible para abrir el panel de detalles.

![Panel de detalles del área de trabajo de consultas con el identificador de consulta resaltado.](../images/ui/query-templates/details-panel.png)

Desde el panel de detalles puede ejecutar las siguientes acciones:

* Seleccione **[!UICONTROL Ejecutar como CTAS]** para crear una tabla nueva seleccionando datos de una tabla o tablas existentes. Esta opción sólo está disponible si tiene una consulta SELECT.
* Seleccione **[!UICONTROL Agregar programación]** para comenzar a editar la programación de la plantilla de consulta.
* Seleccione **[!UICONTROL Ver programación]** para ir a la ficha [!UICONTROL Programaciones] del Editor de consultas. Esta vista contiene toda la información de programación asociada a la consulta.
* Seleccione **[!UICONTROL Eliminar consulta]** para eliminar la plantilla.
* Seleccione el nombre de la plantilla para navegar hasta el Editor de consultas, donde el SQL se rellena previamente para su edición.

### Utilice la API del servicio de consultas para crear una plantilla

Consulte la documentación para obtener instrucciones sobre [cómo crear una plantilla de consulta](../api/query-templates.md#create-a-query-template) mediante la API del servicio de consultas. Los detalles de una plantilla de consulta recién creada se encuentran en el cuerpo de la respuesta.

>[!NOTE]
>
>Las plantillas creadas mediante la API también están visibles en la pestaña Plantillas del servicio de consulta de la interfaz de usuario de Experience Platform.

## Pasos siguientes

Al leer este documento, ahora comprende mejor cómo crear plantillas de consulta en el servicio de consultas. Consulte la [descripción general de la interfaz de usuario](./overview.md) o la [guía de la API del servicio de consultas](../api/getting-started.md) para obtener más información acerca de las funcionalidades del servicio de consultas.

Consulte la [guía de extremo de consultas programadas](../api/scheduled-queries.md) para obtener información sobre cómo programar consultas mediante la API o la [guía del editor de consultas](./user-guide.md#scheduled-queries) para la interfaz de usuario.
