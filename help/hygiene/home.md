---
title: Información general sobre la higiene de los datos
description: La higiene de los datos de Adobe Experience Platform le permite administrar el ciclo de vida de sus datos mediante la actualización o depuración de registros obsoletos o inexactos.
exl-id: 104a2bb8-3242-4a20-b98d-ad6df8071a16
source-git-commit: 70a2abcc4d6e27a89e77d68e7757e4876eaa4fc0
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# Higiene de datos en Adobe Experience Platform

>[!IMPORTANT]
>
>Actualmente, la higiene de los datos solo está disponible para las organizaciones que han adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

Adobe Experience Platform proporciona un robusto conjunto de herramientas para administrar operaciones de datos grandes y complicadas con el fin de orquestar las experiencias de los consumidores. A medida que los datos se incorporan al sistema a lo largo del tiempo, cada vez es más importante administrar los almacenes de datos para que se utilicen como se espera, se actualicen cuando sea necesario corregir los datos incorrectos y se eliminen cuando las políticas organizativas lo consideren necesario.

Las funciones de higiene de datos de Platform le permiten administrar los datos almacenados mediante lo siguiente:

* Programación de caducidades automatizadas del conjunto de datos
* Eliminación de registros individuales de uno o todos los conjuntos de datos

>[!IMPORTANT]
>
>Las eliminaciones de registros están pensadas para utilizarse en la limpieza de datos, la eliminación de datos anónimos o la minimización de datos. Son **not** para su uso en solicitudes de derechos de interesados (cumplimiento) relacionadas con regulaciones de privacidad como el Reglamento General de Protección de Datos (RGPD). Para todos los casos de uso de cumplimiento de normas, utilice [Adobe Experience Platform Privacy Service](../privacy-service/home.md) en su lugar.

Estas actividades se pueden realizar utilizando la variable [[!UICONTROL Higiene de los datos] Espacio de trabajo de la interfaz de usuario](#ui) o [API de higiene de datos](#api). Cuando se ejecuta un trabajo de higiene de datos, el sistema proporciona actualizaciones de transparencia en cada paso del proceso. Consulte la sección sobre [plazos y transparencia](#timelines-and-transparency) para obtener más información sobre cómo se representa cada tipo de trabajo en el sistema.

## [!UICONTROL Higiene de los datos] Espacio de trabajo de la interfaz de usuario {#ui}

La variable [!UICONTROL Higiene de los datos] El espacio de trabajo en la interfaz de usuario de Platform le permite configurar y programar operaciones de higiene de datos, lo que ayuda a garantizar que los registros se mantengan según lo esperado.

Para ver los pasos detallados sobre la administración de tareas de higiene de datos en la interfaz de usuario, consulte la [Guía de la interfaz de usuario sobre higiene de datos](./ui/overview.md).

## API de higiene de datos {#api}

La variable [!UICONTROL Higiene de los datos] La interfaz de usuario de se basa en la API de higiene de datos, cuyos extremos están disponibles para su uso directo si prefiere automatizar sus actividades de higiene de datos. Consulte la [Guía de API de higiene de datos](./api/overview.md) para obtener más información.

## Plazos y transparencia

Las solicitudes de eliminación de registros y caducidad de conjuntos de datos tienen sus propias líneas de tiempo de procesamiento y proporcionan actualizaciones de transparencia en puntos clave de sus flujos de trabajo respectivos. Consulte las secciones siguientes para obtener más detalles sobre cada tipo de trabajo.

### Caducidad de conjuntos de datos {#dataset-expiration-transparency}

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

### Eliminar registros {#record-delete-transparency}

>[!IMPORTANT]
>
>Las eliminaciones de registros solo están disponibles para las organizaciones que han adquirido Adobe Healthcare Shield.

Lo siguiente ocurre cuando se produce una [solicitud de eliminación de registros](./ui/record-delete.md) se crea:

| Escenario | Tiempo después del envío de la solicitud | Descripción |
| --- | --- | --- |
| La solicitud se envía | 0 horas | Un administrador de datos o analista de privacidad envía una solicitud de eliminación de registros. La solicitud se puede ver en el [!UICONTROL Interfaz de usuario de higiene de datos] una vez presentada. |
| Búsqueda de perfiles actualizada | 3 horas | El cambio en los recuentos de perfiles causado por la identidad eliminada se refleja en [widgets de tablero](../dashboards/guides/profiles.md#profile-count-trend) y otros informes. |
| Segmentos actualizados | 24 horas | Una vez que se eliminan los perfiles, todos los relacionados [segmentos](../segmentation/home.md) se actualizan para reflejar su nuevo tamaño. |
| Recorridos y destinos actualizados | 26 horas | [Recorridos](https://experienceleague.adobe.com/docs/journey-optimizer/using/orchestrate-journeys/about-journeys/journey.html), [campañas](https://experienceleague.adobe.com/docs/journey-optimizer/using/campaigns/get-started-with-campaigns.html)y [destinos](../destinations/home.md) se actualizan según los cambios en segmentos relacionados. |
| Registros blandos eliminados en el lago de datos | 7 días | Los datos se eliminan fácilmente del lago de datos. |
| Vacuado de datos completado | 14 días | La variable [situación del trabajo de higiene](./ui/browse.md#view-details) actualizaciones para indicar que el trabajo se ha completado, lo que significa que la depuración de datos se ha completado en el lago de datos y que los registros relevantes se han eliminado con dificultad. |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

En este documento se ofrece una descripción general de las capacidades de higiene de datos de Platform. Para empezar a realizar solicitudes de higiene de datos en la interfaz de usuario, consulte la [Guía de la interfaz de usuario](./ui/overview.md). Para aprender a crear trabajos de higiene de datos mediante programación, consulte la [Guía de API de higiene de datos](./api/overview.md)
