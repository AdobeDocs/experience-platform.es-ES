---
title: Información general sobre Advanced Data Lifecycle Management
description: La administración avanzada del ciclo de vida de los datos permite administrar el ciclo de vida de los datos mediante la actualización o depuración de registros obsoletos o inexactos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a1502e8f1515ff73840b2926f5be355032dd4bab
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Administración avanzada del ciclo de vida de los datos en Adobe Experience Platform

Adobe Experience Platform proporciona un conjunto sólido de herramientas para administrar operaciones de datos grandes y complicadas a fin de organizar las experiencias de los consumidores. A medida que los datos se incorporan al sistema a lo largo del tiempo, es cada vez más importante administrar los almacenes de datos para que se utilicen según lo esperado, se actualicen cuando sea necesario corregir datos incorrectos y se eliminen cuando las políticas de la organización lo consideren necesario.

<!-- Experience Platform's data lifecycle capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Estas actividades se pueden realizar usando el área de trabajo de la interfaz de usuario [[!UICONTROL Data Lifecycle]](#ui) o la [API de higiene de datos](#api). Cuando se ejecuta un trabajo del ciclo vital de datos, el sistema proporciona actualizaciones de transparencia en cada paso del proceso. Consulte la sección sobre [cronologías y transparencia](#timelines-and-transparency) para obtener más información sobre cómo se representa cada tipo de trabajo en el sistema.

>[!NOTE]
>
>La administración avanzada del ciclo de vida de datos admite eliminaciones de conjuntos de datos mediante el [extremo de caducidad del conjunto de datos](./api/dataset-expiration.md) y eliminaciones de ID (datos de nivel de fila) mediante identidades principales a través del [extremo de orden de trabajo](./api/workorder.md). También puede administrar [caducidades de conjuntos de datos](./ui/dataset-expiration.md) y [eliminaciones de registros](./ui/record-delete.md) a través de la interfaz de usuario de Experience Platform. Consulte la documentación vinculada para obtener más información. Tenga en cuenta que el ciclo de vida de datos no admite la eliminación por lotes.

## Área de trabajo de IU [!UICONTROL Data Lifecycle] {#ui}

El área de trabajo [!UICONTROL Data Lifecycle] de la interfaz de usuario de Experience Platform le permite configurar y programar operaciones del ciclo vital de datos, lo que le ayuda a garantizar que los registros se mantengan según lo esperado.

Para ver los pasos detallados sobre la administración de tareas de ciclo de vida de datos en la interfaz de usuario, consulte la [guía de IU de ciclo de vida de datos](./ui/overview.md).

## API de higiene de datos {#api}

La interfaz de usuario [!UICONTROL Data Lifecycle] se basa en la API de higiene de datos, cuyos extremos están disponibles para que los use directamente si prefiere automatizar las actividades del ciclo vital de datos. Consulte la [Guía de API de higiene de datos](./api/overview.md) para obtener más información.

## Cronología y transparencia {#timelines-and-transparency}

[Eliminación de registros](./ui/record-delete.md) y las solicitudes de caducidad de conjuntos de datos tienen sus propias escalas de tiempo de procesamiento y proporcionan actualizaciones de transparencia en puntos clave de sus respectivos flujos de trabajo.

>[!TIP]
>
>Para supervisar su uso actual en relación con los límites de cuotas, consulte la [Guía de referencia de cuotas](./api/quota.md).\
>Para ver las reglas de asignación de derechos, los límites mensuales, las escalas de tiempo de SLA y las directivas de administración de excepciones, consulte la [eliminación de registros (IU)](./ui/record-delete.md#quotas) y la [documentación de la orden de trabajo (API)](./api/workorder.md#quotas).

Lo siguiente ocurre cuando se crea una [solicitud de caducidad del conjunto de datos](./ui/dataset-expiration.md):

| Prueba | Tiempo tras el vencimiento programado | Descripción |
| --- | --- | --- |
| Se ha enviado la solicitud | 0 horas | Un administrador de datos o analista de privacidad envía una solicitud para que un conjunto de datos caduque en un momento determinado. La solicitud es visible en el [!UICONTROL Data Lifecycle UI] después de enviarse y permanece en un estado pendiente hasta la hora de caducidad programada, después de la cual se ejecutará. |
| El conjunto de datos se borra del lago de datos | 1 hora | El conjunto de datos se quitó de la [página de inventario del conjunto de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario. Los datos dentro del lago de datos solo se eliminan de forma suave y permanecerán así hasta el final del proceso, después del cual se eliminarán de forma dura. |
| El conjunto de datos se ha eliminado del servicio de perfil | 3 horas | A partir de este punto, las operaciones que incluyen la segmentación por lotes y de flujo continuo, la previsualización o estimación, la exportación y el acceso a entidades ya no leerán los datos de este conjunto de datos. Los datos del servicio de perfil solo se eliminan de forma suave y permanecerán así hasta el final del proceso, después del cual se eliminarán de forma dura. |
| Recuento de perfiles y audiencias actualizadas | 48 horas | Una vez que se hayan actualizado todos los perfiles afectados, todas las [audiencias](../segmentation/home.md) relacionadas se actualizarán para reflejar su nuevo tamaño. Según el conjunto de datos eliminado y los atributos por los que esté segmentando, el tamaño de cada audiencia podría aumentar o disminuir debido a la eliminación. En este punto, cualquier cambio resultante en los recuentos generales de perfiles se reflejará en [widgets de tablero](../dashboards/guides/profiles.md#profile-count-trend) y otros informes. |
| Recorridos y destinos actualizados | 50 horas | Los [Recorridos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=es), [campañas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=es) y [destinos](../destinations/home.md) se actualizan según los cambios en segmentos relacionados. |
| Eliminación completa del hardware | 15 días | Todos los datos relacionados con el conjunto de datos se eliminan del lago de datos y del servicio de perfil. El [estado del trabajo del ciclo de vida de datos](./ui/browse.md#view-details) que eliminó el conjunto de datos se ha actualizado para reflejarlo. |

{style="table-layout:auto"}

>[!IMPORTANT]
>
>Las eliminaciones de conjuntos de datos en Amazon Web Service (AWS) están sujetas a una latencia de unas tres horas antes de que los cambios se apliquen completamente. Esto incluye hasta dos horas para que el conjunto de datos se marque para su eliminación, seguidas de una hora adicional antes de que se elimine completamente del sistema. Por el contrario, las solicitudes de eliminación para instancias de Experience Platform que utilizan el lago de datos de Azure producen cambios inmediatos en las funciones empresariales.
>
>Para los usuarios de AWS, este retraso puede afectar a la segmentación por lotes, la segmentación por flujo continuo, las vistas previas, las estimaciones, las exportaciones y el acceso a los datos. Esta latencia solo afecta a los clientes que utilizan AWS, ya que los usuarios del lago de datos de Azure experimentan actualizaciones inmediatas. Para los usuarios de AWS, las solicitudes de eliminación pueden tardar hasta tres horas en propagarse completamente a través de todos los sistemas afectados. Ajuste sus expectativas en consecuencia.


<!-- ### Record deletes {#record-delete-transparency}

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Lifecycle UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html?lang=es), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html?lang=es), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the lifecycle job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Próximos pasos

Este documento proporciona una descripción general de las funciones del ciclo vital de datos de Experience Platform. Para empezar a realizar solicitudes de higiene de datos en la interfaz de usuario, consulte la [guía de la interfaz de usuario](./ui/overview.md). Para aprender a crear trabajos del ciclo de vida de datos mediante programación, consulte la [Guía de API de higiene de datos](./api/overview.md)
