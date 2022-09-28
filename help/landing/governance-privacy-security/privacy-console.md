---
title: Información general de la Consola de privacidad
description: Obtenga información sobre cómo monitorizar los flujos de trabajo relacionados con la privacidad en la interfaz de usuario de Adobe Experience Platform.
source-git-commit: 4fa1b826d033ace6536af920b070e8eebbbf401c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# Información general de la Consola de privacidad

La variable [!UICONTROL Consola de privacidad] en la interfaz de usuario de Adobe Experience Platform, encontrará una vista de panel de las operaciones relacionadas con la privacidad en Platform, incluidas las solicitudes de trabajo sobre la higiene de los datos, las solicitudes del Privacy Service y los registros de auditoría para las actividades de usuario de Platform.

Para acceder al tablero, seleccione **[!UICONTROL Consola de privacidad]** en el panel de navegación izquierdo.

![Imagen que muestra [!UICONTROL Consola de privacidad] seleccionado en la navegación izquierda dentro de la interfaz de usuario de Platform](../images/governance-privacy-security/privacy-console/left-nav.png)

Desde aquí puede consultar los [widgets de monitorización](#widgets) proporcionado por la consola, o puede explorar una de varias [guías de caso de uso](#use-case-guides) en las funcionalidades de privacidad de Platform.

## Widgets

[!UICONTROL Consola de privacidad] proporciona varias utilidades para supervisar las operaciones de privacidad.

![Imagen que muestra [!UICONTROL Consola de privacidad] seleccionado en la navegación izquierda dentro de la interfaz de usuario de Platform](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Según los SKU que haya adquirido su organización, es posible que algunos de los widgets mencionados a continuación no estén disponibles.

La función de cada utilidad se explica a continuación:

| Nombre del widget | Descripción |
| --- | --- |
| Estado de la orden de trabajo de higiene de datos | Muestra los estados de los procesos de eliminación de consumidores en [Higiene de los datos](../../hygiene/home.md) para el lapso de tiempo seleccionado. Utilice el menú desplegable para cambiar el intervalo de tiempo entre los últimos 7 días, 14 días y 30 días. |
| Órdenes de trabajo recientes sobre higiene de datos | Muestra el más reciente [Higiene de los datos](../../hygiene/home.md) órdenes de trabajo que está procesando el sistema. Utilice la lista desplegable para cambiar entre las órdenes de trabajo creadas recientemente y las actualizadas recientemente. |
| Acciones más frecuentes | Muestra las acciones más frecuentes en Platform según la captura de [registros de auditoría](./audit-logs/overview.md) para el lapso de tiempo seleccionado. Utilice el menú desplegable para cambiar el intervalo de tiempo entre los últimos 7 días, 14 días y 30 días. |
| Usuarios más activos | Muestra los usuarios de Platform más activos de su organización según la captura de [registros de auditoría](./audit-logs/overview.md) para el lapso de tiempo seleccionado. Utilice el menú desplegable para cambiar el intervalo de tiempo entre los últimos 7 días, 14 días y 30 días. |
| Solicitudes de interesados de datos | Muestra el número de solicitudes de interesados enviadas y completadas por [Privacy Service](../../privacy-service/home.md) durante un día determinado. |

{style=&quot;table-layout:auto&quot;}

## Guías de casos de uso

La consola proporciona varias guías del producto que le presentan flujos de trabajo de privacidad comunes en Platform, incluidas instrucciones concisas sobre cómo configurar una implementación básica.

![Imagen que muestra [!UICONTROL Consola de privacidad] seleccionado en la navegación izquierda dentro de la interfaz de usuario de Platform](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Pasos siguientes

Para obtener más información sobre los distintos servicios de Platform que se vinculan a casos de uso de privacidad, consulte la siguiente documentación:

* [Control de acceso basado en atributos](../../access-control/abac/overview.md)
* [Registros de auditoría](./audit-logs/overview.md)
* [Gobierno de datos](../../data-governance/home.md)
* [Higiene de los datos](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
