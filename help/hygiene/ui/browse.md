---
title: Examinar órdenes de trabajo de higiene de los datos
description: Aprenda a ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 1%

---

# Examinar pedidos de trabajo de higiene de datos {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID de orden de trabajo"
>abstract="Cuando se envía una solicitud de higiene de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. En otras palabras, una orden de trabajo representa un proceso específico de higiene de datos, que incluye su estado actual y otros detalles relacionados. A cada orden de trabajo se le asigna automáticamente su propio ID exclusivo tras la creación."
>text="See the data hygiene UI guide to learn more."

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos en Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**.

Cuando se envía una solicitud de higiene de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. Una orden de trabajo representa un proceso específico de higiene de datos, como una caducidad programada del conjunto de datos, que incluye su estado actual y otros detalles relacionados.

Esta guía explica cómo ver y administrar las solicitudes de trabajo existentes en la interfaz de usuario de Adobe Experience Platform.

## Enumerar y filtrar órdenes de trabajo existentes

Al acceder por primera vez a la variable **[!UICONTROL Higiene de los datos]** en la interfaz de usuario de se muestra una lista de las solicitudes de trabajo existentes junto con sus detalles básicos.

![Imagen que muestra la variable [!UICONTROL Higiene de los datos] espacio de trabajo en la interfaz de usuario de Platform](../images/ui/browse/work-order-list.png)

La lista solo muestra los pedidos de trabajo de una categoría a la vez. Select **[!UICONTROL Consumidor]** para ver una lista de tareas de eliminación de registros, y **[!UICONTROL Conjunto de datos]** para ver una lista de caducidades programadas del conjunto de datos.

![Imagen que muestra la variable [!UICONTROL Conjunto de datos] ficha](../images/ui/browse/dataset-tab.png)

Seleccione el icono de canal (![Imagen del icono del canal](../images/ui/browse/funnel-icon.png)) para ver una lista de filtros para las órdenes de trabajo mostradas.

![Imagen de los filtros de orden de trabajo mostrados](../images/ui/browse/filters.png)

Según el tipo de orden de trabajo que visualice, hay diferentes opciones de filtro disponibles.

### Filtros para las eliminaciones de registros

Los filtros siguientes se aplican para registrar solicitudes de eliminación:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Estado] | Filtre en función del estado actual de la orden de trabajo:<ul><li>**[!UICONTROL Completado]**: El trabajo se ha completado.</li><li>**[!UICONTROL Error]**: El trabajo encontró un error y no se pudo completar.</li><li>**[!UICONTROL Procesamiento]**: La solicitud se ha iniciado y se está procesando.</li></ul> |
| [!UICONTROL Fecha de creación] | Filtre según el momento en que se realizó la orden de trabajo. |
| [!UICONTROL Fecha de actualización] | Filtre según el momento en que se actualizó por última vez la orden de trabajo. Las creaciones se cuentan como actualizaciones. |

### Filtros para las caducidades del conjunto de datos

Los filtros siguientes se aplican a las solicitudes de caducidad del conjunto de datos:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Estado] | Filtre en función del estado actual de la orden de trabajo:<ul><li>**[!UICONTROL Completado]**: El trabajo se ha completado.</li><li>**[!UICONTROL Pendiente]**: El trabajo se ha creado, pero aún no se ha ejecutado. A [solicitud de caducidad del conjunto de datos](./dataset-expiration.md) asume este estado antes de la fecha de eliminación programada. Una vez que llega la fecha de eliminación, el estado se actualiza a [!UICONTROL En ejecución] a menos que el trabajo se cancele de antemano.</li><li>**[!UICONTROL En ejecución]**: La solicitud de caducidad del conjunto de datos se ha iniciado y se está procesando.</li><li>**[!UICONTROL Cancelado]**: El trabajo se ha cancelado como parte de una solicitud de usuario manual.</li></ul> |
| [!UICONTROL Fecha de creación] | Filtre según el momento en que se realizó la orden de trabajo. |
| [!UICONTROL Fecha de caducidad] | Filtre las solicitudes de caducidad del conjunto de datos en función de la fecha de eliminación programada para el conjunto de datos en cuestión. |
| [!UICONTROL Fecha de actualización] | Filtre según el momento en que se actualizó por última vez la orden de trabajo. Las creaciones y caducidades se cuentan como actualizaciones. |

{style="table-layout:auto"}

## Ver los detalles de una orden de trabajo {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Estado por servicio"
>abstract="Las solicitudes de higiene de datos se procesan de forma independiente mediante varios servicios de Experience Platform. Esta sección describe el estado de procesamiento actual de la solicitud para cada servicio respectivo. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Número de identidades"
>abstract="Número de identidades cuyos registros se solicitaron que se actualizaran o eliminaran como parte de esta orden de trabajo. Las identidades incluidas en el recuento pueden no existir necesariamente en los conjuntos de datos afectados. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Respuesta de eliminación de registros"
>abstract="Cuando un proceso de eliminación de registros recibe una respuesta del sistema, estos mensajes se muestran en la sección **[!UICONTROL Resultado]** para obtener más información. Si se produce un problema mientras se procesa una orden de trabajo, en esta sección aparecerán mensajes de error relevantes para ayudarle a solucionar el problema. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

Seleccione el ID de una orden de trabajo enumerada para ver sus detalles.

![Imagen que muestra un ID de orden de trabajo seleccionado](../images/ui/browse/select-work-order.png)

Según el tipo de orden de trabajo seleccionado, se proporciona información y controles diferentes. Se tratan en las secciones siguientes.

### Registrar detalles de eliminación {#record-delete}

Los detalles de una solicitud de eliminación de registros incluyen su estado actual y el tiempo transcurrido desde que se realizó la solicitud. Cada solicitud también incluye un **[!UICONTROL Estado por servicio]** que proporciona detalles de estado individuales sobre cada servicio de flujo descendente involucrado en la eliminación. En el carril derecho, puede utilizar controles para actualizar el nombre y la descripción de la orden de trabajo.

![Imagen que muestra la página de detalles de una orden de trabajo de eliminación de registros](../images/ui/browse/record-delete-details.png)

### Detalles de caducidad del conjunto de datos {#dataset-expiration}

La página de detalles de una caducidad del conjunto de datos proporciona información sobre sus atributos básicos, incluida la fecha de caducidad programada en los días restantes antes de que se produzca la eliminación. En el carril derecho, puede utilizar controles para editar o cancelar la caducidad.

![Imagen que muestra la página de detalles de una orden de trabajo de caducidad del conjunto de datos](../images/ui/browse/ttl-details.png)

## Pasos siguientes

En esta guía se explica cómo ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Platform. Para obtener información sobre la creación de sus propias órdenes de trabajo, consulte la siguiente documentación:

* [Administrar caducidades del conjunto de datos](./dataset-expiration.md)
<!-- * [Manage record deletes](./record-delete.md) -->
