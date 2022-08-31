---
title: Examinar órdenes de trabajo de higiene de los datos
description: Aprenda a ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Adobe Experience Platform.
exl-id: 76d4a809-cc2c-434d-90b1-23d88f29c022
source-git-commit: f246a014de7869b627a677ac82e98d4556065010
workflow-type: tm+mt
source-wordcount: '616'
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

Cuando se envía una solicitud de higiene de datos al sistema, se crea una orden de trabajo para ejecutar la tarea solicitada. Una orden de trabajo representa un proceso específico de higiene de datos, como una caducidad programada del conjunto de datos, que incluye su estado actual y otros detalles relacionados.

Esta guía explica cómo ver y administrar las solicitudes de trabajo existentes en la interfaz de usuario de Adobe Experience Platform.

## Enumerar y filtrar órdenes de trabajo existentes

Al acceder por primera vez a la variable **[!UICONTROL Higiene de los datos]** en la interfaz de usuario de se muestra una lista de las solicitudes de trabajo existentes junto con sus detalles básicos.

![Imagen que muestra la variable [!UICONTROL Higiene de los datos] espacio de trabajo en la interfaz de usuario de Platform](../images/ui/browse/work-order-list.png)

<!-- The list only shows work orders for one category at a time. Select **[!UICONTROL Consumer]** to view a list of consumer deletion tasks, and **[!UICONTROL Dataset]** to view a list of scheduled dataset expirations.

![Image showing the [!UICONTROL Dataset] tab](../images/ui/browse/dataset-tab.png) -->

Seleccione el icono de canal (![Imagen del icono del canal](../images/ui/browse/funnel-icon.png)) para ver una lista de filtros para las órdenes de trabajo mostradas.

![Imagen de los filtros de orden de trabajo mostrados](../images/ui/browse/filters.png)

| Filtro | Descripción |
| --- | --- |
| [!UICONTROL Estado] | Filtre en función del estado actual de la orden de trabajo:<ul><li>**[!UICONTROL Completado]**: El trabajo se ha completado.</li><li>**[!UICONTROL Pendiente]**: El trabajo se ha creado, pero aún no se ha ejecutado. A [solicitud de caducidad del conjunto de datos](./dataset-expiration.md) asume este estado antes de la fecha de eliminación programada. Una vez que llega la fecha de eliminación, el estado se actualiza a [!UICONTROL En ejecución] a menos que el trabajo se cancele de antemano.</li><li>**[!UICONTROL En ejecución]**: La solicitud de caducidad del conjunto de datos se ha iniciado y se está procesando.</li><li>**[!UICONTROL Cancelado]**: El trabajo se ha cancelado como parte de una solicitud de usuario manual.</li></ul> |
| [!UICONTROL Fecha de creación] | Filtre según el momento en que se realizó la orden de trabajo. |
| [!UICONTROL Fecha de caducidad] | Filtre las solicitudes de caducidad del conjunto de datos en función de la fecha de eliminación programada para el conjunto de datos en cuestión. |
| [!UICONTROL Fecha de actualización] | Filtre las solicitudes de caducidad del conjunto de datos en función del momento en que se actualizó la última vez la orden de trabajo. Las creaciones y caducidades se cuentan como actualizaciones. |

{style=&quot;table-layout:auto&quot;}

## Ver los detalles de una orden de trabajo {#view-details}

>[!CONTEXTUALHELP]
>id="platform_hygiene_statusbyservice"
>title="Estado por servicio"
>abstract="Las solicitudes de higiene de datos se procesan de forma independiente mediante varios servicios de Experience Platform. Esta sección describe el estado de procesamiento actual de la solicitud para cada servicio respectivo. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_numberofidentities"
>title="Número de identidades"
>abstract="Número de identidades que se solicitaron que se eliminaran como parte de esta orden de trabajo. Las identidades incluidas en el recuento pueden no existir necesariamente en los conjuntos de datos afectados. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

>[!CONTEXTUALHELP]
>id="platform_hygiene_responsemessages"
>title="Respuesta de eliminación del consumidor"
>abstract="Cuando un proceso de eliminación de consumidores recibe una respuesta del sistema, estos mensajes se muestran en la sección **[!UICONTROL Resultado]** para obtener más información. Si se produce un problema mientras se procesa una orden de trabajo, en esta sección aparecerán mensajes de error relevantes para ayudarle a solucionar el problema. Para obtener más información, consulte la guía de la interfaz de usuario sobre higiene de datos."

Seleccione el ID de una orden de trabajo enumerada para ver sus detalles.

![Imagen que muestra un ID de orden de trabajo seleccionado](../images/ui/browse/select-work-order.png)

<!-- Depending on the type of work order selected, different information and controls are provided. These are covered in the sections below.

### Consumer delete details {#consumer-delete}

The details of a consumer delete request are read-only, displaying its basic attributes such as its current status and the time elapsed since the request was made.

![Image showing the details page for a consumer delete work order](../images/ui/browse/consumer-delete-details.png)

### Dataset expiration details {#dataset-expiration} -->

La página de detalles de una caducidad del conjunto de datos proporciona información sobre sus atributos básicos, incluida la fecha de caducidad programada en los días restantes antes de que se produzca la eliminación. En el carril derecho, puede utilizar controles para editar o cancelar la caducidad.

![Imagen que muestra la página de detalles de una orden de trabajo de caducidad del conjunto de datos](../images/ui/browse/ttl-details.png)

## Pasos siguientes

En esta guía se explica cómo ver y administrar los pedidos de trabajo de higiene de datos existentes en la interfaz de usuario de Platform. Para obtener información sobre cómo crear sus propias órdenes de trabajo, consulte la guía de [programación de una caducidad del conjunto de datos](./dataset-expiration.md).
