---
title: Información general de Privacy Console
description: Obtenga información sobre cómo monitorizar los flujos de trabajo relacionados con la privacidad en la interfaz de usuario de Adobe Experience Platform.
feature: Privacy
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 4%

---

# Información general de Privacy Console

La ficha [!UICONTROL Consola de privacidad] de la interfaz de usuario de Adobe Experience Platform proporciona una vista de panel de las operaciones relacionadas con la privacidad en Experience Platform, incluidas las órdenes de trabajo de higiene de los datos, las solicitudes de los interesados de Privacy Service y los registros de auditoría de las actividades de los usuarios de Experience Platform.

Para acceder al panel, seleccione **[!UICONTROL Consola de privacidad]** en el panel de navegación izquierdo.

![Imagen que muestra [!UICONTROL Consola de privacidad] seleccionada en el panel de navegación izquierdo de la interfaz de usuario de Experience Platform](../images/governance-privacy-security/privacy-console/left-nav.png)

Desde aquí, puede revisar los [widgets de monitorización](#widgets) disponibles proporcionados por la consola, o puede explorar una de las [guías de casos de uso](#use-case-guides) sobre las funcionalidades de privacidad de Experience Platform.

## Widgets

[!UICONTROL Consola de privacidad] proporciona varios widgets para ayudarle a supervisar sus operaciones de privacidad.

![Imagen que muestra [!UICONTROL Consola de privacidad] seleccionada en el panel de navegación izquierdo de la interfaz de usuario de Experience Platform](../images/governance-privacy-security/privacy-console/widgets.png)

>[!NOTE]
>
>Según las SKU que haya adquirido su organización, es posible que algunos de los widgets mencionados a continuación no estén disponibles.

La función de cada widget se explica a continuación:

| Nombre del widget | Descripción |
| --- | --- |
| Estado de orden de trabajo de higiene de datos | Muestra los estados de los procesos de eliminación de registros en [Higiene de datos](../../hygiene/home.md) para el lapso de tiempo seleccionado. Utilice el menú desplegable para cambiar el lapso de tiempo entre los últimos 7, 14 y 30 días. |
| Órdenes de trabajo recientes para higiene de datos | Muestra las [órdenes de trabajo de higiene de datos](../../hygiene/home.md) más recientes que está procesando el sistema. Utilice el menú desplegable para cambiar entre las órdenes de trabajo creadas recientemente y las órdenes de trabajo actualizadas recientemente. |
| Acciones más frecuentes | Muestra las acciones más frecuentes en Experience Platform capturadas por [registros de auditoría](./audit-logs/overview.md) para el lapso de tiempo seleccionado. Utilice el menú desplegable para cambiar el lapso de tiempo entre los últimos 7, 14 y 30 días. |
| Usuarios más activos | Muestra los usuarios de Experience Platform más activos dentro de su organización según lo capturado por [registros de auditoría](./audit-logs/overview.md) para el lapso de tiempo seleccionado. Utilice el menú desplegable para cambiar el lapso de tiempo entre los últimos 7, 14 y 30 días. |
| Solicitudes de interesados | Muestra la cantidad de solicitudes de interesados enviadas y completadas por [Privacy Service](../../privacy-service/home.md) durante un día determinado. |

{style="table-layout:auto"}

## Guías de casos de uso

La consola proporciona varias guías del producto que le presentan los flujos de trabajo de privacidad comunes en Experience Platform, incluidas instrucciones concisas sobre cómo configurar una implementación básica.

![Imagen que muestra [!UICONTROL Consola de privacidad] seleccionada en el panel de navegación izquierdo de la interfaz de usuario de Experience Platform](../images/governance-privacy-security/privacy-console/use-case-guide.png)

## Pasos siguientes

Para obtener más información sobre los distintos servicios de Experience Platform relacionados con casos de uso de privacidad, consulte la siguiente documentación:

* [Control de acceso basado en atributos](../../access-control/abac/overview.md)
* [Registros de auditoría](./audit-logs/overview.md)
* [Gobernanza de datos](../../data-governance/home.md)
* [Higiene de los datos](../../hygiene/home.md)
* [Privacy Service](../../privacy-service/home.md)
