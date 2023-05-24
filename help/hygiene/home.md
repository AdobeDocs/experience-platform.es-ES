---
title: Resumen de higiene de datos
description: La higiene de los datos de Adobe Experience Platform le permite administrar el ciclo vital de sus datos actualizando o purgando registros obsoletos o inexactos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 2913e9e687843e566db4ebf2031e610d1891d4c9
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 1%

---

# Higiene de datos en Adobe Experience Platform

>[!IMPORTANT]
>
>Actualmente, la higiene de los datos solo está disponible para las organizaciones que han adquirido **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad**. Estas funciones se lanzarán próximamente de forma general. Para obtener más información sobre su próxima disponibilidad, póngase en contacto con su representante de servicios de Adobe. Sin embargo, puede hacerlo inmediatamente [eliminar conjuntos de datos mediante [!UICONTROL Conjuntos de datos] IU](../catalog/datasets/user-guide.md#delete).

Adobe Experience Platform proporciona un conjunto sólido de herramientas para administrar operaciones de datos grandes y complicadas a fin de organizar las experiencias de los consumidores. A medida que los datos se incorporan al sistema a lo largo del tiempo, es cada vez más importante administrar los almacenes de datos para que se utilicen según lo esperado, se actualicen cuando sea necesario corregir datos incorrectos y se eliminen cuando las políticas de la organización lo consideren necesario.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Estas actividades se pueden realizar utilizando la variable [[!UICONTROL Higiene de datos] IU de Workspace](#ui) o el [API de higiene de datos](#api). Cuando se ejecuta un trabajo de higiene de datos, el sistema proporciona actualizaciones de transparencia en cada paso del proceso. Consulte la sección sobre [plazos y transparencia](#timelines-and-transparency) para obtener más información sobre cómo se representa cada tipo de trabajo en el sistema.

## [!UICONTROL Higiene de datos] IU de Workspace {#ui}

El [!UICONTROL Higiene de datos] El espacio de trabajo de en la IU de Platform le permite configurar y programar operaciones de higiene de datos, lo que garantiza que los registros se mantengan según lo esperado.

Para ver los pasos detallados sobre la administración de tareas de higiene de datos en la IU, consulte la [Guía de IU de higiene de datos](./ui/overview.md).

## API de higiene de datos {#api}

El [!UICONTROL Higiene de datos] La interfaz de usuario de se basa en la API de higiene de datos, cuyos extremos están disponibles para que los utilice directamente si prefiere automatizar las actividades de higiene de datos. Consulte la [Guía de API de higiene de datos](./api/overview.md) para obtener más información.

## Cronología y transparencia

Las solicitudes de eliminación de registros y caducidad de conjuntos de datos tienen sus propias cronologías de procesamiento y proporcionan actualizaciones de transparencia en puntos clave de sus respectivos flujos de trabajo.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Lo siguiente ocurre cuando una [solicitud de caducidad del conjunto de datos](./ui/dataset-expiration.md) se ha creado:

| Escenario | Tiempo tras el vencimiento programado | Descripción |
| --- | --- | --- |
| Se ha enviado la solicitud | 0 horas | Un administrador de datos o analista de privacidad envía una solicitud para que un conjunto de datos caduque en un momento determinado. La solicitud es visible en [!UICONTROL IU de higiene de datos] después de enviarla, y permanece en estado pendiente hasta la hora de caducidad programada, después de la cual se ejecutará la solicitud. |
| Conjunto de datos perdido | 1 hora | El conjunto de datos se borra del [página de inventario de conjuntos de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario. Los datos dentro del lago de datos solo se eliminan de forma suave y permanecerán así hasta el final del proceso, después del cual se eliminarán de forma dura. |
| Recuento de perfiles actualizado | 30 horas | Según el contenido del conjunto de datos que se elimine, algunos perfiles pueden eliminarse del sistema si todos sus atributos de componentes están vinculados a ese conjunto de datos. 30 horas después de eliminar el conjunto de datos, cualquier cambio resultante en los recuentos de perfiles generales se refleja en [widgets de tablero](../dashboards/guides/profiles.md#profile-count-trend) y otros informes. |
| Segmentos actualizados | 48 horas | Una vez actualizados todos los perfiles afectados, todos los [segmentos](../segmentation/home.md) se actualizan para reflejar su nuevo tamaño. Según el conjunto de datos eliminado y los atributos por los que esté segmentando, el tamaño de cada segmento podría aumentar o disminuir como resultado de la eliminación. |
| Recorridos y destinos actualizados | 50 horas | [Recorridos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campañas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), y [destinos](../destinations/home.md) se actualizan según los cambios en segmentos relacionados. |
| Eliminación completa del hardware | 14 días | Todos los datos relacionados con el conjunto de datos se eliminan del lago de datos. El [estado del trabajo de higiene](./ui/browse.md#view-details) que eliminó el conjunto de datos se actualiza para reflejarlo. |

{style="table-layout:auto"}

<!-- ### Record deletes {#record-delete-transparency}

>[!IMPORTANT]
>
>Record deletes are only available for organizations that have purchased Adobe Healthcare Shield.

The following takes place when a [record delete request](./ui/record-delete.md) is created:

| Stage | Time after request submission | Description |
| --- | --- | --- |
| Request is submitted | 0 hours | A data steward or privacy analyist submits a record delete request. The request is visible in the [!UICONTROL Data Hygiene UI] after it has been submitted. |
| Profile lookups updated | 3 hours | The change in profile counts caused by the deleted identity are reflected in [dashboard widgets](../dashboards/guides/profiles.md#profile-count-trend) and other reports. |
| Segments updated | 24 hours | Once profiles are removed, all related [segments](../segmentation/home.md) are updated to reflect their new size. |
| Journeys and destinations updated | 26 hours | [Journeys](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campaigns](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html), and [destinations](../destinations/home.md) are updated according to changes in related segments. |
| Records soft deleted in data lake | 7 days | The data is soft deleted from the data lake. |
| Data vacuuming completed | 14 days | The [status of the hygiene job](./ui/browse.md#view-details) updates to indicate that the job has completed, meaning that data vacuuming has been completed on the data lake and the relevant records have been hard deleted. |

{style="table-layout:auto"} -->

## Pasos siguientes

Este documento proporciona una visión general de las capacidades de higiene de los datos de Platform. Para empezar a realizar solicitudes de higiene de datos en la interfaz de usuario, consulte la [Guía de IU](./ui/overview.md). Para aprender a crear trabajos de higiene de datos mediante programación, consulte la [Guía de API de higiene de datos](./api/overview.md)
