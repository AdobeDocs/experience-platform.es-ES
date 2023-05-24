---
title: Administrar caducidades de conjuntos de datos
description: Obtenga información sobre cómo programar la caducidad de un conjunto de datos en la IU de Adobe Experience Platform.
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 22%

---

# Administrar caducidades del conjunto de datos {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="Eliminación de registros de cliente y conjuntos de datos no deseados o caducados"
>abstract="<h2>Descripción</h2><p>Para administrar el ciclo de vida de los datos de Experience Platform que no están relacionados con el cumplimiento normativo, puede eliminar los registros del consumidor y programar las fechas de caducidad para los conjuntos de datos. Para crear o administrar solicitudes de interesados, consulte el bloque de casos de uso “Cumplimiento de las solicitudes de privacidad de los interesados”.</p>"

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de los datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido **Adobe Healthcare Shield** o **Adobe Escudo de seguridad y privacidad**. Estas funciones se lanzarán próximamente de forma general. Para obtener más información sobre su próxima disponibilidad, póngase en contacto con su representante de servicios de Adobe. Sin embargo, puede hacerlo inmediatamente [eliminar conjuntos de datos mediante [!UICONTROL Conjuntos de datos] IU](../../catalog/datasets/user-guide.md#delete).

El [[!UICONTROL Higiene de datos] workspace](./overview.md) en la IU de Adobe Experience Platform le permite programar caducidades para conjuntos de datos. Cuando un conjunto de datos alcanza su fecha de caducidad, el lago de datos, el servicio de identidad y el perfil del cliente en tiempo real comienzan procesos independientes para eliminar el contenido del conjunto de datos de sus respectivos servicios. Una vez que los datos se eliminan de los tres servicios, la caducidad se marca como completada.

>[!WARNING]
>
>Si un conjunto de datos está configurado para caducar, debe cambiar manualmente los flujos de datos que puedan estar introduciendo datos en ese conjunto de datos para que los flujos de trabajo descendentes no se vean afectados negativamente.

Este documento explica cómo programar y administrar las caducidades de los conjuntos de datos en la IU de Platform.

## Programar una caducidad del conjunto de datos {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="Instrucciones"
>abstract="<ul><li>Seleccione <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=es">Higiene de datos</a> en la navegación izquierda y, a continuación, <b>Crear solicitud</b>.</li><li>Si desea eliminar registros, haga lo siguiente:</li>   <li>Seleccione <b>Registro</b>.</li>   <li>Seleccione un conjunto de datos específico del que eliminar registros o elija la opción para eliminarlos de todos.</li>   <li>Proporcione las identidades de los consumidores cuyos registros deban eliminarse. Seleccione <b>Agregar identidad</b> para introducir las identidades de una en una o <b>Elegir archivos</b> para cargar un archivo JSON de identidades, en su lugar.</li>   <li>Si es necesario, seleccione <b>Plantilla</b> para ver el formato esperado del archivo JSON.</li><li>Consulte la documentación para obtener instrucciones si desea <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=es#schedule-dataset-expiration">programar fechas de caducidad para conjuntos de datos</a>.</li></ul>"

Para crear una nueva solicitud, seleccione **[!UICONTROL Crear solicitud]** en la página principal del espacio de trabajo.

![Imagen que muestra el [!UICONTROL Crear solicitud] botón seleccionado](../images/ui/ttl/create-request-button.png)

Aparecerá el cuadro de diálogo de creación de solicitudes. En el **[!UICONTROL Acción solicitada]** , seleccione **[!UICONTROL Eliminar conjunto de datos]** para actualizar los controles disponibles para la programación de caducidad del conjunto de datos.

![Imagen que muestra el [!UICONTROL Crear solicitud] botón seleccionado](../images/ui/ttl/dataset-selected.png)

### Seleccionar una fecha y un conjunto de datos

Aparecerá el cuadro de diálogo de creación de solicitudes. En el **[!UICONTROL Acción solicitada]** , seleccione una fecha en la que desee eliminar el conjunto de datos. Puede introducir la fecha manualmente (con el formato `mm/dd/yyyy`) o seleccione el icono de calendario (![Imagen del icono del calendario](../images/ui/ttl/calendar-icon.png)) para seleccionar la fecha en un cuadro de diálogo.

![Imagen que muestra una fecha de caducidad que se está configurando para el conjunto de datos](../images/ui/ttl/select-date.png)

Siguiente, en **[!UICONTROL Detalles del conjunto de datos]**, seleccione el icono de base de datos (![Imagen del icono de la base de datos](../images/ui/ttl/database-icon.png)) para abrir un cuadro de diálogo de selección de conjuntos de datos. Elija un conjunto de datos de la lista al que aplicar la caducidad y, a continuación, seleccione **[!UICONTROL Listo]**.

![Imagen que muestra un conjunto de datos seleccionado](../images/ui/ttl/select-dataset.png)

>[!NOTE]
Solo se muestran los conjuntos de datos que pertenecen a la zona protegida actual.

### Enviar la solicitud

El [!UICONTROL Detalles del conjunto de datos] Esta sección se rellena para incluir la identidad y el esquema principales del conjunto de datos seleccionado. En **[!UICONTROL Solicitar configuración]**, introduzca un nombre y una descripción opcional para la solicitud, seguido de **[!UICONTROL Enviar]**.

![Imagen que muestra el [!UICONTROL Enviar] botón seleccionado](../images/ui/ttl/submit.png)

Se le pedirá que confirme la fecha en la que se eliminará el conjunto de datos. Seleccionar **[!UICONTROL Enviar]** para continuar.

Una vez enviada la solicitud, se crea una orden de trabajo y aparece en la pestaña principal del [!UICONTROL Higiene de datos] workspace. Desde aquí puede supervisar el estado de la orden de trabajo a medida que procesa la solicitud.

>[!NOTE]
Consulte la sección de información general sobre [plazos y transparencia](../home.md#dataset-expiration-transparency) para obtener más información sobre cómo se procesan las caducidades del conjunto de datos una vez que se ejecutan.

## Editar o cancelar la caducidad de un conjunto de datos

Para editar o cancelar la caducidad de un conjunto de datos, seleccione **[!UICONTROL Conjunto de datos]** en la página principal del espacio de trabajo, y seleccione la caducidad del conjunto de datos en la lista.

En la página de detalles de la caducidad del conjunto de datos, el carril derecho muestra los controles para editar o cancelar la eliminación programada.

## Pasos siguientes

Este documento explica cómo programar la caducidad de los conjuntos de datos en la interfaz de usuario de Experience Platform. Para obtener información sobre cómo realizar otras tareas de higiene de datos en la interfaz de usuario, consulte la [información general sobre higiene de datos](./overview.md).

Para obtener información sobre cómo programar la caducidad de los conjuntos de datos mediante la API de higiene de datos, consulte la [guía de extremo de caducidad del conjunto de datos](../api/dataset-expiration.md).
