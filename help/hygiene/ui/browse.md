---
title: Examinar órdenes de trabajo de higiene de los datos
description: Aprenda a ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
hide: true
hidefromtoc: true
source-git-commit: c2e7cf1859f6a2b277783cdec535ecc208703fac
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 2%

---

# Examinar pedidos de trabajo de higiene de datos

>[!CONTEXTUALHELP]
>id="platform_hygiene_workorders"
>title="ID de orden de trabajo"
>abstract="Cuando se envía una solicitud de higiene de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. En otras palabras, una orden de trabajo representa un proceso específico de higiene de datos, que incluye su estado actual y otros detalles relacionados. A cada orden de trabajo se le asigna automáticamente su propio ID exclusivo tras la creación. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

>[!IMPORTANT]
>
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido Escudo de Adobe para la atención médica.

Cuando se envía una solicitud de higiene de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. Una orden de trabajo representa un proceso específico de higiene de datos (como eliminar datos de consumidores), que incluye su estado actual y otros detalles relacionados.

Esta guía explica cómo ver y administrar las solicitudes de trabajo existentes en la interfaz de usuario de Adobe Experience Platform.

## Enumerar y filtrar órdenes de trabajo existentes

Al acceder por primera vez a la variable **[!UICONTROL Higiene de los datos]** en la interfaz de usuario de se muestra una lista de las solicitudes de trabajo existentes junto con sus detalles básicos.

![Imagen que muestra la variable [!UICONTROL Higiene de los datos] espacio de trabajo en la interfaz de usuario de Platform](../images/ui/browse/work-order-list.png)

La lista solo muestra los pedidos de trabajo de una categoría a la vez. Select **[!UICONTROL Consumidor]** para ver una lista de tareas de eliminación de consumidores, y **[!UICONTROL Conjunto de datos]** para ver una lista de programaciones de tiempo de vida (TTL) para conjuntos de datos.

![Imagen que muestra la variable [!UICONTROL Conjunto de datos] ficha](../images/ui/browse/dataset-tab.png)

Seleccione el icono de canal (![Imagen del icono del canal](../images/ui/browse/funnel-icon.png)) para ver una lista de filtros para las órdenes de trabajo mostradas.

![Imagen de los filtros de orden de trabajo mostrados](../images/ui/browse/filters.png)

En función de la pestaña que esté viendo, hay diferentes filtros disponibles:

| Filtro | Categoría | Descripción |
| --- | --- | --- |
| [!UICONTROL Estado] | [!UICONTROL Consumidor] &amp; [!UICONTROL Conjunto de datos] | Filtra en función del estado actual de la orden de trabajo. |
| [!UICONTROL Fecha de creación] | [!UICONTROL Consumidor] | Filtre en función del momento en que se realizó la solicitud de eliminación de consumidor. |
| [!UICONTROL Fecha de creación] | [!UICONTROL Conjunto de datos] | Filtre en función del momento en que se realizó la solicitud de eliminación de consumidor. |
| [!UICONTROL Fecha de eliminación] | [!UICONTROL Conjunto de datos] | Filtre en función de la fecha de eliminación programada por el TTL. |
| [!UICONTROL Fecha de actualización] | [!UICONTROL Conjunto de datos] | Filtre en función del momento en que se actualizó por última vez el TTL del conjunto de datos. Las creaciones y caducidades de TTL se cuentan como actualizaciones. |

{style=&quot;table-layout:auto&quot;}

## Ver los detalles de una orden de trabajo

Seleccione el ID de una orden de trabajo enumerada para ver sus detalles.

![Imagen que muestra un ID de orden de trabajo seleccionado](../images/ui/browse/select-work-order.png)

Según el tipo de orden de trabajo seleccionado, se proporciona información y controles diferentes. Se tratan en las secciones siguientes.

### Detalles de eliminación de clientes

<!-- (Not available for initial release)
>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."
-->

Los detalles de una solicitud de eliminación de consumidor son de solo lectura, y muestran sus atributos básicos, como su estado actual y el tiempo transcurrido desde que se realizó la solicitud.

![Imagen que muestra la página de detalles de una orden de trabajo de eliminación de consumidor](../images/ui/browse/consumer-delete-details.png)

### Detalles del TTL del conjunto de datos

La página de detalles de un TTL de conjunto de datos proporciona información sobre sus atributos básicos, incluida la fecha de caducidad programada en los días restantes antes de que se produzca la eliminación. En el carril derecho, puede utilizar controles para editar o cancelar el TTL.

![Imagen que muestra la página de detalles de una orden de trabajo TTL de conjunto de datos](../images/ui/browse/ttl-details.png)

## Pasos siguientes

En esta guía se explica cómo ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Platform. Para obtener información sobre la creación de sus propias órdenes de trabajo, consulte la siguiente documentación:

* [Eliminar un consumidor](./delete-consumer.md)
* [Programar un TTL de conjunto de datos](./ttl.md)
