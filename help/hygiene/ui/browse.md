---
title: Examinar órdenes de trabajo del ciclo vital de datos
description: Obtenga información sobre cómo ver y administrar las solicitudes de trabajo del ciclo vital de datos existentes en la interfaz de usuario de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 566f1b6478cd0de0691cfb2301d5b86fbbfece52
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 27%

---

# Examinar órdenes de trabajo sobre el ciclo de datos {#browse-work-orders}

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID de orden de trabajo"
>abstract="Cuando se envía una solicitud de ciclo de vida de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. En otras palabras, una orden de trabajo representa un proceso de ciclo de vida de datos específico, que incluye su estado actual y otros detalles relacionados. A cada orden de trabajo se le asigna automáticamente su propio ID exclusivo tras la creación."
>text="See the data lifecycle UI guide to learn more."

Cuando se envía una solicitud de ciclo de vida de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. Una orden de trabajo representa un proceso específico del ciclo vital de los datos, como una caducidad programada del conjunto de datos, que incluye su estado actual y otros detalles relacionados.

Esta guía explica cómo ver y administrar las órdenes de trabajo existentes en la interfaz de usuario de Adobe Experience Platform.

## Enumerar y filtrar órdenes de trabajo existentes

Cuando accede por primera vez al espacio de trabajo **[!UICONTROL Ciclo de vida de los datos]** en la interfaz de usuario, se muestra una lista de las órdenes de trabajo existentes junto con sus detalles básicos.

![Imagen que muestra el espacio de trabajo [!UICONTROL Ciclo de vida de datos] en la IU de Platform](../images/ui/browse/work-order-list.png)

La lista sólo muestra las órdenes de trabajo de una categoría cada vez. Seleccione **[!UICONTROL Consumidor]** para ver una lista de tareas de eliminación de registros y **[!UICONTROL Conjunto de datos]** para ver una lista de caducidades programadas de conjuntos de datos.

![Imagen que muestra la ficha [!UICONTROL Conjunto de datos]](../images/ui/browse/dataset-tab.png)

Seleccione el icono de canal (![Imagen del icono de canal](../images/ui/browse/funnel-icon.png)) para ver una lista de filtros para las órdenes de trabajo mostradas.

![Imagen de los filtros de orden de trabajo mostrados](../images/ui/browse/filters.png)

Según el tipo de orden de trabajo que visualice, hay disponibles diferentes opciones de filtro.

### Filtros para eliminaciones de registros

Los siguientes filtros se aplican a las solicitudes de eliminación de registros:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Estado] | Filtro basado en el estado actual de la orden de trabajo:<ul><li>**[!UICONTROL Completado]**: el trabajo se ha completado.</li><li>**[!UICONTROL Error]**: el trabajo encontró un error y no se pudo completar.</li><li>**[!UICONTROL Procesando]**: la solicitud se ha iniciado y se está procesando en este momento.</li></ul> |
| [!UICONTROL Fecha de creación] | Filtro basado en el momento en que se realizó la orden de trabajo. |
| [!UICONTROL Fecha de actualización] | Filtro basado en el momento en que se actualizó la orden de trabajo por última vez. Las creaciones se cuentan como actualizaciones. |

### Filtros para caducidades de conjuntos de datos

Los siguientes filtros se aplican a las solicitudes de caducidad del conjunto de datos:

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Estado] | Filtro basado en el estado actual de la orden de trabajo:<ul><li>**[!UICONTROL Completado]**: el trabajo se ha completado.</li><li>**[!UICONTROL Pendiente]**: el trabajo se ha creado pero aún no se ha ejecutado. Una [solicitud de caducidad del conjunto de datos](./dataset-expiration.md) asume este estado antes de la fecha programada de eliminación. Una vez que llegue la fecha de eliminación, el estado se actualiza a [!UICONTROL Ejecutando] a menos que el trabajo se cancele de antemano.</li><li>**[!UICONTROL Ejecutando]**: la solicitud de caducidad del conjunto de datos se ha iniciado y se está procesando en este momento.</li><li>**[!UICONTROL Cancelado]**: el trabajo se ha cancelado como parte de una solicitud manual del usuario.</li></ul> |
| [!UICONTROL Fecha de creación] | Filtro basado en el momento en que se realizó la orden de trabajo. |
| [!UICONTROL Fecha de caducidad] | Filtrar solicitudes de caducidad de conjuntos de datos en función de la fecha de eliminación programada para el conjunto de datos en cuestión. |
| [!UICONTROL Fecha de actualización] | Filtro basado en el momento en que se actualizó la orden de trabajo por última vez. Las creaciones y caducidades se cuentan como actualizaciones. |

{style="table-layout:auto"}

## Ver los detalles de una orden de trabajo {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Estado por servicio"
>abstract="Las solicitudes sobre el ciclo de vida de datos se procesan de forma independiente mediante varios servicios de Experience Platform. Esta sección describe el estado de procesamiento actual de la solicitud para cada servicio respectivo. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Número de identidades"
>abstract="Número de identidades cuyos registros se solicitó actualizar o eliminar como parte de esta orden de trabajo. Las identidades incluidas en el recuento pueden no existir necesariamente en los conjuntos de datos afectados. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Respuesta de eliminación de registros"
>abstract="Cuando un proceso de eliminación de registros recibe una respuesta del sistema, estos mensajes se muestran en la sección **[!UICONTROL Resultado]** para obtener más información. Si se produce un problema mientras se procesa una orden de trabajo, en esta sección aparecerán mensajes de error relevantes para ayudarle a solucionar el problema. Para obtener más información, consulte la guía de la interfaz de usuario sobre el ciclo de vida de datos."

Seleccione el ID de una orden de trabajo de la lista para ver sus detalles.

![Imagen que muestra un identificador de orden de trabajo seleccionado](../images/ui/browse/select-work-order.png)

Según el tipo de orden de trabajo seleccionada, se proporciona información y controles diferentes. Estas se tratan en las secciones siguientes.

### Registrar detalles de eliminación {#record-delete}

Los detalles de una solicitud de eliminación de registro incluyen su estado actual y el tiempo transcurrido desde que se realizó la solicitud. Cada solicitud también incluye una sección **[!UICONTROL Estado por servicio]** que proporciona detalles de estado individuales sobre cada servicio descendente involucrado en la eliminación. En el carril derecho, puede utilizar controles para actualizar el nombre y la descripción de la orden de trabajo.

![Imagen que muestra la página de detalles de una orden de trabajo de eliminación de registros](../images/ui/browse/record-delete-details.png)

### Detalles de caducidad del conjunto de datos {#dataset-expiration}

La página de detalles de una caducidad del conjunto de datos proporciona información sobre sus atributos básicos, incluida la fecha de caducidad programada en los días restantes antes de que se produzca la eliminación. En el carril derecho, puede utilizar controles para editar o cancelar la caducidad.

![Imagen que muestra la página de detalles de una orden de trabajo de caducidad del conjunto de datos](../images/ui/browse/ttl-details.png)

## Pasos siguientes

En esta guía se explica cómo ver y administrar las solicitudes de trabajo del ciclo vital de datos existentes en la IU de Platform. Para obtener información sobre la creación de sus propias órdenes de trabajo, consulte la siguiente documentación:

* [Administrar caducidades del conjunto de datos](./dataset-expiration.md)
* [Administración de eliminaciones de registros](./record-delete.md)
