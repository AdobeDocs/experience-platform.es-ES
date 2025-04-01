---
title: Exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform
type: Tutorial
description: Obtenga información sobre cómo exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: d3bd76f5b36b6a6afcb67fe923eb8e4f3d7a9415
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 9%

---


# Exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform

>[!IMPORTANT]
> 
>Para activar los datos, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**[para ](/help/access-control/home.md#permissions). Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## **[!UICONTROL Exportar archivo ahora]** información general {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exportar archivo ahora"
>abstract="Seleccione este control para enviar una exportación completa de archivos, además de cualquier exportación programada previamente. La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform."

En este artículo se explica cómo usar la interfaz de usuario de Experience Platform para exportar archivos bajo demanda a destinos por lotes como [almacenamiento en la nube](/help/destinations/catalog/cloud-storage/overview.md) y [marketing por correo electrónico](/help/destinations/catalog/email-marketing/overview.md).

El control **[!UICONTROL Exportar archivo ahora]** le permite exportar un archivo completo sin interrumpir la programación de exportación actual de una audiencia programada anteriormente. Esta exportación se realiza además de las exportaciones programadas anteriormente y no cambia la frecuencia de exportación de la audiencia. La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform.

También puede utilizar las API de Experience Platform para este fin. Lea cómo [activar audiencias a petición en destinos por lotes a través de la API de activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Requisitos previos {#prerequisites}

Para exportar archivos bajo demanda a destinos por lotes, debe haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

## Cómo exportar archivos bajo demanda {#how-to-export-files-on-demand}

1. Vaya a **[!UICONTROL Conexiones > Destinos]**, seleccione la pestaña **[!UICONTROL Examinar]** y el símbolo de filtro para mostrar las conexiones existentes a los destinos por lotes que desee.

   ![Imagen que resalta cómo llegar a la ficha Examinar y filtrar los flujos de datos existentes.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleccione la conexión de destino deseada para inspeccionar el flujo de datos existente en el destino.

   ![Imagen que resalta un flujo de datos filtrado.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Seleccione la pestaña **[!UICONTROL Datos de activación]**, seleccione las audiencias para las que desea exportar archivos bajo demanda y seleccione el control **[!UICONTROL Exportar archivo ahora]** para almacenar en déclencheur una exportación única que enviará un archivo para cada audiencia seleccionada a su destino de lote.

   ![Imagen que resalta el botón Exportar archivo ahora.](../assets/ui/activate-on-demand/bulk-export-file-now.png)

4. Seleccione **[!UICONTROL Sí]** para confirmar y almacenar en déclencheur la exportación del archivo.

   ![Imagen que muestra el cuadro de diálogo de confirmación Exportar archivo ahora.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Aparece un mensaje de confirmación que le informa de que se ha iniciado la exportación del archivo.

   ![Imagen que muestra la confirmación de la activación ad hoc correcta.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. También puede cambiar a la pestaña **[!UICONTROL Flujo de datos se ejecuta]** para confirmar que la exportación del archivo se ha iniciado.

## Consideraciones {#considerations}

Tenga en cuenta las siguientes consideraciones al usar el control **[!UICONTROL Exportar archivo ahora]**:

* **[!UICONTROL Exportar archivo ahora]** solo funciona para audiencias cuya programación en el flujo de datos de activación por lotes se superpone con la fecha actual. Esto incluye audiencias con programaciones que no tienen fecha de finalización (frecuencia de exportación de **[!UICONTROL Una vez]**) o en las que la fecha de finalización aún no ha pasado.
* Al agregar una audiencia a un flujo de datos existente, espere al menos **una hora** antes de usar el control **[!UICONTROL Exportar archivo ahora]**.
* Si cambia la política de combinación de una audiencia o crea una audiencia que usa una nueva política de combinación, espere 24 horas hasta usar el control **[!UICONTROL Exportar archivo ahora]**.

## Mensajes de error de IU {#ui-error-messages}

Al usar el control **[!UICONTROL Exportar archivo ahora]**, podría encontrar cualquiera de los mensajes de error que se enumeran a continuación. Revise la tabla para comprender cómo abordarlos cuando aparecen.

| Mensaje de error | Resolución |
|---------|----------|
| La ejecución ya está en curso para la audiencia `segment ID` del pedido `dataflow ID` con el id. de ejecución `flow run ID` | Este mensaje de error indica que hay un flujo de activación ad-hoc en curso para una audiencia. Espere a que finalice el trabajo antes de volver a activar el trabajo de activación. |
| Las audiencias `<segment name>` no forman parte de este flujo de datos o están fuera del intervalo programado. | Este mensaje de error indica que las audiencias que seleccionó para activar no están asignadas al flujo de datos o que la programación de activación configurada para las audiencias ha caducado o aún no se ha iniciado. Compruebe si la audiencia está realmente asignada al flujo de datos y que la programación de activación de audiencia se superpone con la fecha actual. |

## Información relacionada {#related-information}

* [Activar audiencias en destinos por lotes bajo demanda mediante las API de Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md)
