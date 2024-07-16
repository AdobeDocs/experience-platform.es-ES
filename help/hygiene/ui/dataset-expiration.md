---
title: Caducidad automatizada de conjuntos de datos
description: Obtenga información sobre cómo programar la caducidad de un conjunto de datos en la IU de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 2aba88ac657e73a12be14d2c3a67dd5714513c97
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 18%

---

# Caducidades automatizadas de conjuntos de datos {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Eliminación de registros de cliente y conjuntos de datos no deseados o caducados"
>abstract="<h2>Descripción</h2><p>Para administrar el ciclo de vida de los datos de Experience Platform que no están relacionados con el cumplimiento normativo, puede eliminar los registros del consumidor y programar las fechas de caducidad para los conjuntos de datos. Para crear o administrar solicitudes de interesados, consulte el bloque de casos de uso “Cumplimiento de las solicitudes de privacidad de los interesados”.</p>"

El espacio de trabajo [[!UICONTROL Ciclo de vida de datos]](./overview.md) de la interfaz de usuario de Adobe Experience Platform le permite programar caducidades para conjuntos de datos. Cuando un conjunto de datos alcanza su fecha de caducidad, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos independientes para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez que los datos se eliminan de los tres servicios, la caducidad se marca como completada.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente los flujos de datos que puedan estar introduciendo datos en ese conjunto de datos para que los flujos de trabajo descendentes no se vean afectados negativamente.

Este documento explica cómo programar y automatizar las caducidades de los conjuntos de datos en la IU de Platform.

>[!NOTE]
>
>La caducidad del conjunto de datos no elimina datos del Edge Network de Adobe Experience Platform en este momento. Sin embargo, no es posible que los datos permanezcan dentro del Edge Network después de que el conjunto de datos esté configurado para que caduque. Esto se debe a que el contrato de licencia de servicio de 15 días para la caducidad del conjunto de datos se superpone con el periodo de 14 días en el que los datos existen dentro del Edge Network antes de descartarse.

La administración avanzada del ciclo de vida de datos admite eliminaciones de conjuntos de datos mediante el [extremo de caducidad del conjunto de datos](../api/dataset-expiration.md) y eliminaciones de ID (datos de nivel de fila) mediante identidades principales a través del [extremo de orden de trabajo](../api/workorder.md). También puede administrar la caducidad de los conjuntos de datos y [eliminaciones de registros](./record-delete.md) a través de la interfaz de usuario de Platform. Consulte la documentación vinculada para obtener más información.

>[!NOTE]
>
>El ciclo de vida de datos no admite la eliminación por lotes.

## Programación de una caducidad del conjunto de datos {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instrucciones"
>abstract="<ul><li>Seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=es">Ciclo de vida de datos</a> en la navegación izquierda y, a continuación, seleccione <b>Crear solicitud</b>.</li><li>Si desea eliminar registros, haga lo siguiente:</li>   <li>Seleccione <b>Registro</b>.</li>   <li>Seleccione un conjunto de datos específico del que eliminar registros o elija la opción para eliminarlos de todos.</li>   <li>Proporcione las identidades de los consumidores cuyos registros deban eliminarse. Seleccione <b>Agregar identidad</b> para introducir las identidades de una en una o <b>Elegir archivos</b> para cargar un archivo JSON de identidades, en su lugar.</li>   <li>Si es necesario, seleccione <b>Plantilla</b> para ver el formato esperado del archivo JSON.</li><li>Consulte la documentación para obtener instrucciones si desea <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=es#schedule-dataset-expiration">programar fechas de caducidad para conjuntos de datos</a>.</li></ul>"

Para crear una solicitud, seleccione **[!UICONTROL Crear solicitud]** en la página principal del área de trabajo.

>[!IMPORTANT]
>
>Los usuarios de Real-Time CDP, Adobe Journey Optimizer y Customer Journey Analytics tienen 20 órdenes de trabajo de caducidad de conjuntos de datos programados pendientes. Los usuarios de Healthcare Shield y Privacy and Security Shield tienen 50 órdenes de trabajo pendientes de vencimiento del conjunto de datos programado. Esto significa que puede tener 20 o 50 conjuntos de datos programados para eliminarse a la vez.<br>Por ejemplo, si tiene 20 caducidades programadas del conjunto de datos y un conjunto de datos se va a eliminar mañana, no puede establecer más caducidades hasta que se elimine ese conjunto de datos.

![Se ha resaltado el área de trabajo [!UICONTROL Ciclo de vida de datos] con [!UICONTROL Crear solicitud].](../images/ui/ttl/create-request-button.png)

Aparecerá el flujo de trabajo de creación de solicitudes. En la sección [!UICONTROL Acción solicitada], seleccione **[!UICONTROL Eliminar conjunto de datos]** para actualizar los controles para la programación de caducidad del conjunto de datos.

![Flujo de trabajo de creación de solicitud con la opción [!UICONTROL Eliminar conjunto de datos] resaltada.](../images/ui/ttl/dataset-selected.png)

### Seleccionar una fecha y un conjunto de datos {#select-date-and-dataset}

En la sección **[!UICONTROL Acción solicitada]**, seleccione una fecha en la que desee eliminar el conjunto de datos. Puede escribir la fecha manualmente (con el formato `mm/dd/yyyy`) o seleccionar el icono de calendario (![Un icono de calendario.](../images/ui/ttl/calendar-icon.png)) para seleccionar la fecha en un cuadro de diálogo.

![Cuadro de diálogo de calendario con una fecha de caducidad seleccionada y resaltada para el conjunto de datos.](../images/ui/ttl/select-date.png)

A continuación, en **[!UICONTROL Detalles del conjunto de datos]**, seleccione el icono de la base de datos (![El icono de la base de datos.](../images/ui/ttl/database-icon.png)) para abrir un cuadro de diálogo de selección de conjunto de datos. Elija un conjunto de datos de la lista al que aplicar la caducidad y, a continuación, seleccione **[!UICONTROL Listo]**.

![Cuadro de diálogo [!UICONTROL Seleccionar conjunto de datos] con un conjunto de datos seleccionado y [!UICONTROL Listo] resaltado.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>Solo se muestran los conjuntos de datos que pertenecen a la zona protegida actual.

### Enviar la solicitud {#submit-request}

La sección [!UICONTROL Detalles del conjunto de datos] se rellena para incluir la identidad y el esquema principales para el conjunto de datos seleccionado. En **[!UICONTROL Solicitar configuración]**, escriba un nombre y una descripción opcional para la solicitud, seguidos de **[!UICONTROL Enviar]**.

![Se completó una solicitud de caducidad del conjunto de datos con [!UICONTROL Solicitar configuración] y el botón [!UICONTROL Enviar] resaltados.](../images/ui/ttl/submit.png)

Aparecerá un cuadro de diálogo [!UICONTROL Confirmar solicitud]. Se le pedirá que confirme el nombre del conjunto de datos y la fecha en la que se eliminará. Seleccione **[!UICONTROL Enviar]** para continuar.

Una vez enviada la solicitud, se crea una orden de trabajo y aparece en la pestaña principal del espacio de trabajo [!UICONTROL Ciclo de vida de datos]. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
>Consulte la sección de información general sobre [cronologías y transparencia](../home.md#dataset-expiration-transparency) para obtener detalles sobre cómo se procesan las caducidades de los conjuntos de datos una vez que se ejecutan.

## Editar o cancelar la caducidad de un conjunto de datos {#edit-or-cancel}

Para editar o cancelar la caducidad de un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos]** en la página principal del área de trabajo y seleccione la caducidad del conjunto de datos en la lista.

En la página de detalles de la caducidad del conjunto de datos, el carril derecho muestra los controles para editar o cancelar la eliminación programada.

## Pasos siguientes

Este documento explica cómo programar la caducidad de los conjuntos de datos en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de minimización de datos en la interfaz de usuario, consulte la [descripción general de la interfaz de usuario del ciclo vital de datos](./overview.md).

Para obtener información sobre cómo programar la caducidad de los conjuntos de datos mediante la API de higiene de datos, consulte la [guía de extremo de caducidad de conjuntos de datos](../api/dataset-expiration.md).
