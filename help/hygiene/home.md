---
title: Información general sobre la higiene de los datos
description: La higiene de los datos de Adobe Experience Platform le permite administrar el ciclo de vida de sus datos mediante la actualización o depuración de registros obsoletos o inexactos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 2%

---

# Higiene de datos en Adobe Experience Platform

>[!IMPORTANT]
>
>Actualmente, la higiene de los datos solo está disponible para las organizaciones que han adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

Adobe Experience Platform proporciona un robusto conjunto de herramientas para administrar operaciones de datos grandes y complicadas con el fin de orquestar las experiencias de los consumidores. A medida que los datos se incorporan al sistema a lo largo del tiempo, cada vez es más importante administrar los almacenes de datos para que se utilicen como se espera, se actualicen cuando sea necesario corregir los datos incorrectos y se eliminen cuando las políticas organizativas lo consideren necesario.

<!-- Platform's data hygiene capabilities allow you to manage your stored data through the following:

* Scheduling automated dataset expirations
* Deleting individual records from one or all datasets

>[!IMPORTANT]
>
>Record deletes are meant to be used for data cleansing, removing anonymous data, or data minimization. They are **not** to be used for data subject rights requests (compliance) as pertaining to privacy regulations like the General Data Protection Regulation (GDPR). For all compliance use cases, use [Adobe Experience Platform Privacy Service](../privacy-service/home.md) instead. -->

Estas actividades se pueden realizar utilizando la variable [[!UICONTROL Higiene de los datos] Espacio de trabajo de la interfaz de usuario](#ui) o [API de higiene de datos](#api). Cuando se ejecuta un trabajo de higiene de datos, el sistema proporciona actualizaciones de transparencia en cada paso del proceso. Consulte la sección sobre [plazos y transparencia](#timelines-and-transparency) para obtener más información sobre cómo se representa cada tipo de trabajo en el sistema.

## [!UICONTROL Higiene de los datos] Espacio de trabajo de la interfaz de usuario {#ui}

La variable [!UICONTROL Higiene de los datos] El espacio de trabajo en la interfaz de usuario de Platform le permite configurar y programar operaciones de higiene de datos, lo que ayuda a garantizar que los registros se mantengan según lo esperado.

Para ver los pasos detallados sobre la administración de tareas de higiene de datos en la interfaz de usuario, consulte la [Guía de la interfaz de usuario sobre higiene de datos](./ui/overview.md).

## API de higiene de datos {#api}

La variable [!UICONTROL Higiene de los datos] La interfaz de usuario de se basa en la API de higiene de datos, cuyos extremos están disponibles para su uso directo si prefiere automatizar sus actividades de higiene de datos. Consulte la [Guía de API de higiene de datos](./api/overview.md) para obtener más información.

## Plazos y transparencia

Las solicitudes de eliminación de registros y caducidad de conjuntos de datos tienen sus propias líneas de tiempo de procesamiento y proporcionan actualizaciones de transparencia en puntos clave de sus flujos de trabajo respectivos.

<!-- ### Dataset expirations {#dataset-expiration-transparency} -->

Lo siguiente ocurre cuando se produce una [solicitud de caducidad del conjunto de datos](./ui/dataset-expiration.md) se crea:

| Escenario | Tiempo después de la caducidad programada | Descripción |
| --- | --- | --- |
| La solicitud se envía | 0 horas | Un administrador de datos o analista de privacidad envía una solicitud para que un conjunto de datos caduque en un momento determinado. La solicitud se puede ver en el [!UICONTROL Interfaz de usuario de higiene de datos] una vez enviado, y permanece en estado pendiente hasta la hora de caducidad programada, tras la cual se ejecutará la solicitud. |
| El conjunto de datos se ha perdido | 1 hora | El conjunto de datos se abandona de la variable [página de inventario del conjunto de datos](../catalog/datasets/user-guide.md) en la interfaz de usuario de . Los datos dentro del lago de datos solo se eliminan de forma suave, y permanecerán así hasta el final del proceso, tras lo cual se eliminarán con dificultad. |
| Recuento de perfiles actualizado | 30 horas | Según el contenido del conjunto de datos que se elimine, algunos perfiles se pueden eliminar del sistema si todos sus atributos de componente están vinculados a ese conjunto de datos. 30 horas después de que se elimine el conjunto de datos, cualquier cambio resultante en los recuentos generales de perfil se reflejará en [widgets de tablero](../dashboards/guides/profiles.md#profile-count-trend) y otros informes. |
| Segmentos actualizados | 48 horas | Una vez actualizados todos los perfiles afectados, todos los relacionados [segmentos](../segmentation/home.md) se actualizan para reflejar su nuevo tamaño. En función del conjunto de datos que se haya eliminado y de los atributos en los que esté segmentando, el tamaño de cada segmento podría aumentar o disminuir como resultado de la eliminación. |
| Recorridos y destinos actualizados | 50 horas | [Recorridos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campañas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)y [destinos](../destinations/home.md) se actualizan según los cambios en segmentos relacionados. |
| Eliminación de disco completa | 14 días | Todos los datos relacionados con el conjunto de datos se eliminan de forma rígida del lago de datos. La variable [situación del trabajo de higiene](./ui/browse.md#view-details) que eliminó el conjunto de datos se actualiza para reflejarlo. |

{style=&quot;table-layout:auto&quot;}

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

En este documento se ofrece una descripción general de las capacidades de higiene de datos de Platform. Para empezar a realizar solicitudes de higiene de datos en la interfaz de usuario, consulte la [Guía de la interfaz de usuario](./ui/overview.md). Para aprender a crear trabajos de higiene de datos mediante programación, consulte la [Guía de API de higiene de datos](./api/overview.md)
