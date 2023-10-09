---
title: Caducidad automatizada de conjuntos de datos
description: Obtenga información sobre cómo programar la caducidad de un conjunto de datos en la IU de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 45dac5647e44ac35d9821d407eddeee72523faf9
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 20%

---

# Caducidad automatizada de conjuntos de datos {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Eliminación de registros de cliente y conjuntos de datos no deseados o caducados"
>abstract="<h2>Descripción</h2><p>Para administrar el ciclo de vida de los datos de Experience Platform que no están relacionados con el cumplimiento normativo, puede eliminar los registros del consumidor y programar las fechas de caducidad para los conjuntos de datos. Para crear o administrar solicitudes de interesados, consulte el bloque de casos de uso “Cumplimiento de las solicitudes de privacidad de los interesados”.</p>"

El [[!UICONTROL Ciclo de datos] workspace](./overview.md) en la IU de Adobe Experience Platform le permite programar caducidades para conjuntos de datos. Cuando un conjunto de datos alcanza su fecha de caducidad, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos independientes para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez que los datos se eliminan de los tres servicios, la caducidad se marca como completada.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente los flujos de datos que puedan estar introduciendo datos en ese conjunto de datos para que los flujos de trabajo descendentes no se vean afectados negativamente.

Este documento explica cómo programar y automatizar las caducidades de los conjuntos de datos en la IU de Platform.

>[!NOTE]
>
>La caducidad del conjunto de datos no elimina datos de Adobe Experience Platform Edge Network en este momento. Sin embargo, no hay posibilidad de que los datos permanezcan dentro de la red perimetral después de que el conjunto de datos esté configurado para caducar. Esto se debe a que el contrato de licencia de servicio de 15 días para la caducidad del conjunto de datos se superpone con el periodo de 14 días en el que los datos existen dentro de la red perimetral antes de descartarse.

## Programar una caducidad del conjunto de datos {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instrucciones"
>abstract="<ul><li>Seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=es">Ciclo de vida de datos</a> en la navegación izquierda y, a continuación, seleccione <b>Crear solicitud</b>.</li><li>Si desea eliminar registros, haga lo siguiente:</li>   <li>Seleccione <b>Registro</b>.</li>   <li>Seleccione un conjunto de datos específico del que eliminar registros o elija la opción para eliminarlos de todos.</li>   <li>Proporcione las identidades de los consumidores cuyos registros deban eliminarse. Seleccione <b>Agregar identidad</b> para introducir las identidades de una en una o <b>Elegir archivos</b> para cargar un archivo JSON de identidades, en su lugar.</li>   <li>Si es necesario, seleccione <b>Plantilla</b> para ver el formato esperado del archivo JSON.</li><li>Consulte la documentación para obtener instrucciones si desea <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=es#schedule-dataset-expiration">programar fechas de caducidad para conjuntos de datos</a>.</li></ul>"

Para crear una solicitud, seleccione **[!UICONTROL Crear solicitud]** en la página principal del espacio de trabajo.

>[!IMPORTANT]
>
Los usuarios de Real-Time CDP, Adobe Journey Optimizer y Customer Journey Analytics tienen 20 órdenes de trabajo de caducidad de conjuntos de datos programados pendientes. Los usuarios de Healthcare Shield y Privacy and Security Shield tienen 50 órdenes de trabajo pendientes de vencimiento del conjunto de datos programado. Esto significa que puede tener 20 o 50 conjuntos de datos programados para eliminarse a la vez.<br>Por ejemplo, si tiene 20 caducidades programadas de conjuntos de datos y un conjunto de datos se va a eliminar mañana, no puede establecer más caducidades hasta que se haya eliminado ese conjunto de datos.

![El [!UICONTROL Ciclo de datos] workspace con [!UICONTROL Crear solicitud] resaltado.](../images/ui/ttl/create-request-button.png)

Aparecerá el flujo de trabajo de creación de solicitudes. En el [!UICONTROL Acción solicitada] , seleccione **[!UICONTROL Eliminar conjunto de datos]** para actualizar los controles para la programación de caducidad del conjunto de datos.

![El flujo de trabajo de creación de solicitudes con [!UICONTROL Eliminar conjunto de datos] opción resaltada.](../images/ui/ttl/dataset-selected.png)

### Seleccionar una fecha y un conjunto de datos {#select-date-and-dataset}

En el **[!UICONTROL Acción solicitada]** , seleccione una fecha en la que desee eliminar el conjunto de datos. Puede introducir la fecha manualmente (con el formato `mm/dd/yyyy`) o seleccione el icono de calendario (![Un icono de calendario.](../images/ui/ttl/calendar-icon.png)) para seleccionar la fecha en un cuadro de diálogo.

![Cuadro de diálogo de calendario con una fecha de caducidad seleccionada y resaltada para el conjunto de datos.](../images/ui/ttl/select-date.png)

Siguiente, en **[!UICONTROL Detalles del conjunto de datos]**, seleccione el icono de base de datos (![El icono de base de datos.](../images/ui/ttl/database-icon.png)) para abrir un cuadro de diálogo de selección de conjuntos de datos. Elija un conjunto de datos de la lista al que aplicar la caducidad y, a continuación, seleccione **[!UICONTROL Listo]**.

![El [!UICONTROL Seleccionar conjunto de datos] diálogo con un conjunto de datos seleccionado y [!UICONTROL Listo] resaltado.](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
Solo se muestran los conjuntos de datos que pertenecen a la zona protegida actual.

### Enviar la solicitud {#submit-request}

El [!UICONTROL Detalles del conjunto de datos] Esta sección se rellena para incluir la identidad y el esquema principales del conjunto de datos seleccionado. En **[!UICONTROL Solicitar configuración]**, introduzca un nombre y una descripción opcional para la solicitud, seguido de **[!UICONTROL Enviar]**.

![Una solicitud de caducidad del conjunto de datos completada con [!UICONTROL Solicitar configuración] y [!UICONTROL Enviar] botón resaltado.](../images/ui/ttl/submit.png)

A [!UICONTROL Confirmar solicitud] aparece el cuadro de diálogo. Se le pedirá que confirme el nombre del conjunto de datos y la fecha en la que se eliminará. Seleccionar **[!UICONTROL Enviar]** para continuar.

Una vez enviada la solicitud, se crea una orden de trabajo y aparece en la pestaña principal del [!UICONTROL Ciclo de datos] workspace. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
>
Consulte la sección de información general sobre [plazos y transparencia](../home.md#dataset-expiration-transparency) para obtener más información sobre cómo se procesan las caducidades del conjunto de datos una vez que se ejecutan.

## Editar o cancelar la caducidad de un conjunto de datos {#edit-or-cancel}

Para editar o cancelar la caducidad de un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos]** en la página principal del espacio de trabajo, y seleccione la caducidad del conjunto de datos en la lista.

En la página de detalles de la caducidad del conjunto de datos, el carril derecho muestra los controles para editar o cancelar la eliminación programada.

## Pasos siguientes

Este documento explica cómo programar la caducidad de los conjuntos de datos en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de minimización de datos en la interfaz de usuario, consulte [resumen de IU del ciclo vital de datos](./overview.md).

Para obtener información sobre cómo programar la caducidad de los conjuntos de datos mediante la API de higiene de datos, consulte la [guía de extremo de caducidad del conjunto de datos](../api/dataset-expiration.md).
