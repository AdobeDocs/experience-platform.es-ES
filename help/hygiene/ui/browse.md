---
title: Examinar órdenes de trabajo de higiene de los datos
description: Aprenda a ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '411'
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
>Actualmente, las funciones de higiene de datos de Adobe Experience Platform solo están disponibles para las organizaciones que han adquirido el Escudo de la salud.

Cuando se envía una solicitud de higiene de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. Una orden de trabajo representa un proceso de higiene de datos específico, como un tiempo de vida programado (TTL) para un conjunto de datos, que incluye su estado actual y otros detalles relacionados.

Esta guía explica cómo ver y administrar las solicitudes de trabajo existentes en la interfaz de usuario de Adobe Experience Platform.

## Enumerar y filtrar órdenes de trabajo existentes

Al acceder por primera vez a la variable **[!UICONTROL Higiene de los datos]** en la interfaz de usuario de se muestra una lista de las solicitudes de trabajo existentes junto con sus detalles básicos.

![Imagen que muestra la variable [!UICONTROL Higiene de los datos] espacio de trabajo en la interfaz de usuario de Platform](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of time-to-live (TTL) schedules for datasets.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Seleccione el icono de canal (![Imagen del icono del canal](../images/ui/browse/funnel-icon.png)) para ver una lista de filtros para las órdenes de trabajo mostradas.

![Imagen de los filtros de orden de trabajo mostrados](../images/ui/browse/filters.png)

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Estado] | Filtra en función del estado actual de la orden de trabajo. |
| [!UICONTROL Fecha de creación] | Filtre en función del momento en que se realizó la solicitud TTL del conjunto de datos. |
| [!UICONTROL Fecha de eliminación] | Filtre en función de la fecha de eliminación programada por el TTL. |
| [!UICONTROL Fecha de actualización] | Filtre en función del momento en que se actualizó por última vez el TTL del conjunto de datos. Las creaciones y caducidades de TTL se cuentan como actualizaciones. |

{style=&quot;table-layout:auto&quot;}

## Ver los detalles de una orden de trabajo

Seleccione el ID de una orden de trabajo enumerada para ver sus detalles.

![Imagen que muestra un ID de orden de trabajo seleccionado](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Consumer delete response"
>abstract="When a consumer deletion process receives a response from the system, these messages are displayed under the **[!UICONTROL Result]** section. If a problem occurs while a work order is processing, any relevant error messages will appear in this section to help you troubleshoot the issue. To learn more, see the data hygiene UI guide."


The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset TTL details -->

La página de detalles de un TTL de conjunto de datos proporciona información sobre sus atributos básicos, incluida la fecha de caducidad programada en los días restantes antes de que se produzca la eliminación. En el carril derecho, puede utilizar controles para editar o cancelar el TTL.

![Imagen que muestra la página de detalles de una orden de trabajo TTL de conjunto de datos](../images/ui/browse/ttl-details.png)

## Pasos siguientes

En esta guía se explica cómo ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Platform. Para obtener información sobre cómo crear sus propias órdenes de trabajo, consulte la guía de [programación de un TTL de conjunto de datos](./ttl.md).
