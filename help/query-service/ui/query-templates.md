---
title: Plantillas de consulta
description: Las plantillas de consulta son consultas SQL guardadas reutilizables que otros usuarios pueden reutilizar para ahorrar tiempo y esfuerzo. Se pueden crear mediante el Editor de consultas o la API del servicio de consultas y están disponibles para su uso en todos los conjuntos de datos del Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: d5d69134627b1a162691bda95732d989bd6e3469
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---

# Plantillas de consulta

El servicio de consultas de Adobe Experience Platform permite guardar y reutilizar código SQL en forma de plantillas de consulta. Las plantillas ahorran esfuerzo al evitar la repetición de tareas que se realizan con más frecuencia. Puede compartir plantillas dentro de su organización y cambiar fácilmente los valores de la consulta sin necesidad de acceder o comprender el SQL subyacente.

Este documento proporciona la información necesaria para crear plantillas de consulta en el servicio de consultas.

## Requisitos previos

Debe tener el [!UICONTROL Administración de consultas] permiso habilitado para acceder al Editor de consultas y ver el panel de consultas en la IU de Platform. El permiso se habilita mediante el Adobe [Admin Console](https://adminconsole.adobe.com/). Póngase en contacto con el administrador de su organización si no tiene privilegios de administrador para habilitar este permiso. Consulte la documentación de control de acceso para [instrucciones completas para agregar permisos mediante Admin Console](../../access-control/home.md).

## Creación de una plantilla de consulta

Puede crear plantillas de consulta mediante dos métodos, ya sea realizando una solicitud del POST a la API del servicio de consultas `query-templates` o escribiendo, nombrando y guardando una consulta a través del Editor de consultas.

### Utilice el Editor de consultas para crear y guardar una consulta como plantilla

Consulte la documentación para obtener instrucciones sobre cómo utilizar el Editor de consultas para lo siguiente [escribir](./user-guide.md#query-authoring) y [guardar consultas](./user-guide.md#saving-queries). Una vez que haya asignado un nombre a la consulta y la haya guardado, estará disponible para volver a utilizarse como plantilla de consulta en [!UICONTROL Plantillas] pestaña.

## Examinar plantillas de consulta {#browse}

En el espacio de trabajo Consultas de la IU de Platform, seleccione **[!UICONTROL Plantillas]** para mostrar la lista de consultas guardadas disponibles.

![Espacio de trabajo de consultas con la pestaña Plantillas resaltada.](../images/ui/query-templates/query-templates.png)

Para buscar información de plantilla relevante, seleccione cualquier plantilla de consulta de la lista disponible para abrir el panel de detalles.

![El panel de detalles del espacio de trabajo de consultas con el ID de consulta resaltado.](../images/ui/query-templates/details-panel.png)

Desde el panel de detalles puede ejecutar cuatro acciones independientes:

* Seleccionar **[!UICONTROL Conjunto de datos de salida]** para editar el conjunto de datos de salida de la plantilla seleccionada.
* Seleccionar **[!UICONTROL Ver programación]** para ir al [!UICONTROL Horarios] pestaña. Esta vista contiene toda la información de programación asociada a la consulta.
* Seleccionar **[!UICONTROL Eliminar consulta]** para eliminar la plantilla.
* Seleccione el nombre de la plantilla para navegar hasta el Editor de consultas, donde el SQL ya se ha rellenado para su edición.

### Utilice la API del servicio de consultas para crear una plantilla

Consulte la documentación para obtener instrucciones sobre [cómo crear una plantilla de consulta](../api/query-templates.md#create-a-query-template) mediante la API del servicio de consultas. Los detalles de una plantilla de consulta recién creada se encuentran en el cuerpo de la respuesta.

>[!NOTE]
>
>Las plantillas creadas mediante la API también están visibles en la pestaña Plantillas del servicio de consulta de la IU de Platform.

## Pasos siguientes

Al leer este documento, ahora comprende mejor cómo crear plantillas de consulta en el servicio de consultas. Consulte la [Información general de IU](./overview.md), o el [Guía de API del servicio de consultas](../api/getting-started.md) para obtener más información sobre las funcionalidades del servicio de consultas.

Consulte la [guía de extremo de consultas programadas](../api/scheduled-queries.md) para obtener información sobre cómo programar consultas mediante la API, o la [Guía del editor de consultas](./user-guide.md#scheduled-queries) para la interfaz de usuario.
