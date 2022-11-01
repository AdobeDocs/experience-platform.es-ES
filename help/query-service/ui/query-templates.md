---
title: Plantillas de consulta
description: Las plantillas de consulta son consultas SQL guardadas reutilizables y que otros usuarios pueden reutilizar para ahorrar tiempo y esfuerzo. Se pueden crear mediante el Editor de consultas o la API del servicio de consultas y están disponibles para su uso en todos los conjuntos de datos del Experience Platform.
exl-id: e74d058f-bb89-45ed-83cc-2e3a33401270
source-git-commit: a085bac6b4ee825d534710ae91d6690fa076e873
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 1%

---

# Plantillas de consulta

El servicio de consulta de Adobe Experience Platform le permite guardar y reutilizar código SQL en forma de plantillas de consulta. Las plantillas ahorran esfuerzo al evitar la repetición de tareas que se realizan con más frecuencia. Puede compartir plantillas dentro de su organización y cambiar fácilmente los valores de consulta sin necesidad de acceder o comprender el SQL subyacente.

Este documento proporciona la información necesaria para crear plantillas de consulta en el servicio de consulta.

## Requisitos previos

Debe tener la variable [!UICONTROL Administrar consultas] permiso habilitado para acceder al Editor de consultas y ver el panel de consultas dentro de la interfaz de usuario de Platform. El permiso se habilita a través del Adobe [Admin Console](https://adminconsole.adobe.com/). Póngase en contacto con el administrador de su organización si no tiene privilegios de administrador para habilitar este permiso. Consulte la documentación de control de acceso para [instrucciones completas para añadir permisos mediante Admin Console](../../access-control/home.md).

## Creación de una plantilla de consulta

Puede crear plantillas de consulta mediante dos métodos, ya sea realizando una solicitud de POST a la API del servicio de consulta `query-templates` o escribiendo, nombrando y guardando una consulta a través del Editor de consultas.

### Utilice el Editor de consultas para crear y guardar una consulta como plantilla

Consulte la documentación para obtener instrucciones sobre cómo utilizar el Editor de consultas para [write](./user-guide.md#query-authoring) y [guardar consultas](./user-guide.md#saving-queries). Una vez que haya asignado un nombre a la consulta y la haya guardado, podrá reutilizarla como plantilla de consulta desde el [!UICONTROL Plantillas] pestaña .

En el espacio de trabajo Consultas de la interfaz de usuario de Platform, seleccione **[!UICONTROL Plantillas]** para mostrar la lista de consultas guardadas disponibles.

![El espacio de trabajo de consultas con la pestaña Plantillas resaltada.](../images/ui/query-templates/query-templates.png)

Para encontrar información de plantilla relevante, seleccione cualquier plantilla de consulta de la lista disponible para abrir el panel de detalles.

![El panel de detalles del espacio de trabajo de consultas con el ID de consulta resaltado.](../images/ui/query-templates/details-panel.png)

### Utilizar la API del servicio de consulta para crear una plantilla

Consulte la documentación para obtener instrucciones sobre [cómo crear una plantilla de consulta](../api/query-templates.md#create-a-query-template) mediante la API del servicio de consulta. Los detalles de una plantilla de consulta recién creada se incluyen en el cuerpo de la respuesta.

>[!NOTE]
>
>Las plantillas creadas con la API también se pueden ver en la pestaña Plantillas del servicio de consulta de la interfaz de usuario de Platform .

## Pasos siguientes

Al leer este documento, ahora tiene una mejor comprensión de cómo crear plantillas de consulta en el servicio de consulta. Consulte la [Información general sobre la IU](./overview.md)o [Guía de API del servicio de consulta](../api/getting-started.md) para obtener más información sobre las funcionalidades del servicio de consulta.

Consulte la [guía de extremo de consultas programadas](../api/scheduled-queries.md) para aprender a programar consultas mediante la API o la [Guía del Editor de consultas](./user-guide.md#scheduled-queries) para la interfaz de usuario.
