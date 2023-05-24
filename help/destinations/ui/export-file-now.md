---
title: (Beta) Exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform
type: Tutorial
description: Obtenga información sobre cómo exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 8%

---

# (Beta) Exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario de Experience Platform

>[!IMPORTANT]
>
>El **[!UICONTROL Exportar archivo ahora]** en Adobe Experience Platform está actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.
>Póngase en contacto con el representante del Adobe para obtener acceso a esta funcionalidad.

>[!IMPORTANT]
> 
>Para activar los datos, necesita el **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## **[!UICONTROL Exportar archivo ahora]** descripción general {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exportar archivo ahora"
>abstract="Seleccione este control para enviar una exportación completa de archivos, además de cualquier exportación programada previamente. La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform."

En este artículo se explica cómo utilizar la interfaz de usuario de Experience Platform para exportar archivos bajo demanda a destinos por lotes como [almacenamiento en la nube](/help/destinations/catalog/cloud-storage/overview.md) y [marketing por correo electrónico](/help/destinations/catalog/email-marketing/overview.md) destinos.

El **[!UICONTROL Exportar archivo ahora]** permite exportar un archivo completo sin interrumpir la programación de exportación actual de un segmento programado anteriormente. Esta exportación se realiza además de las exportaciones programadas anteriormente y no cambia la frecuencia de exportación del segmento. La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform.

También puede utilizar las API de Experience Platform para este fin. Lea cómo [activar segmentos de audiencia a la carta en destinos por lotes mediante la API de activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Requisitos previos {#prerequisites}

Para exportar archivos bajo demanda a destinos por lotes, debe tener [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

## Cómo exportar archivos bajo demanda {#how-to-export-files-on-demand}

1. Ir a **[!UICONTROL Conexiones > Destinos]**, seleccione la **[!UICONTROL Examinar]** y el símbolo de filtro para mostrar las conexiones existentes a los destinos de lote deseados.

   ![Imagen que resalta cómo llegar a la pestaña examinar y filtrar los flujos de datos existentes.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleccione la conexión de destino deseada para inspeccionar el flujo de datos existente en el destino.

   ![Imagen que resalta un flujo de datos filtrado.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Seleccione el **[!UICONTROL Datos de activación]** y seleccione el segmento para el que desea exportar un archivo bajo demanda y seleccione la pestaña **[!UICONTROL Exportar archivo ahora]** para almacenar en déclencheur una exportación única que enviará un archivo al destino del lote.

   >[!IMPORTANT]
   >
   >Actualmente, la IU no admite la selección de varios segmentos para exportar archivos bajo demanda y por lotes. Utilice el [API de activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md) con ese fin.

   ![Imagen que resalta el botón Exportar archivo ahora.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Seleccionar **[!UICONTROL Sí]** para confirmar y almacenar en déclencheur la exportación de archivos.

   ![Imagen que muestra el diálogo de confirmación Exportar archivo ahora.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Aparece un mensaje de confirmación que le informa de que se ha iniciado la exportación del archivo.

   ![Imagen que muestra la confirmación de la activación ad hoc correcta.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. También puede cambiar al **[!UICONTROL Ejecuciones de flujo de datos]** para confirmar que se ha iniciado la exportación del archivo.

## Consideraciones {#considerations}

Tenga en cuenta las siguientes consideraciones al utilizar el **[!UICONTROL Exportar archivo ahora]** control:

* **[!UICONTROL Exportar archivo ahora]** solo funciona para segmentos cuya programación en el flujo de datos de activación por lotes se superpone con la fecha actual. Esto incluye segmentos con programaciones que no tienen fecha de finalización (frecuencia de exportación de **[!UICONTROL Una]**), o donde la fecha de finalización aún no haya pasado.
* Cuando agregue un segmento a un flujo de datos existente, espere al menos 15 minutos hasta que utilice el **[!UICONTROL Exportar archivo ahora]** control.
* Si cambia la política de combinación de un segmento, o si crea un segmento que utiliza una nueva política de combinación, espere 24 horas hasta que utilice el **[!UICONTROL Exportar archivo ahora]** control.

## Mensajes de error de IU {#ui-error-messages}

Al usar el **[!UICONTROL Exportar archivo ahora]** , podría encontrar cualquiera de los mensajes de error enumerados a continuación. Revise la tabla para comprender cómo abordarlos cuando aparecen.

| Mensaje de error | Resolución |
|---------|----------|
| La ejecución ya está en curso para el segmento `segment ID` para pedido `dataflow ID` con id de ejecución `flow run ID` | Este mensaje de error indica que hay un flujo de activación ad hoc en curso para un segmento. Espere a que finalice el trabajo antes de volver a activar el trabajo de activación. |
| Segmentos `<segment name>` no forman parte de este flujo de datos o están fuera del intervalo programado. | Este mensaje de error indica que los segmentos que seleccionó para activar no están asignados al flujo de datos o que la programación de activación configurada para los segmentos ha caducado o aún no se ha iniciado. Compruebe si el segmento está realmente asignado al flujo de datos y que la programación de activación del segmento se superpone con la fecha actual. |

## Información relacionada {#related-information}

* [Activar segmentos de audiencia en destinos por lotes bajo demanda mediante las API de Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Activar datos de audiencia en destinos de exportación de perfiles por lotes](/help/destinations/ui/activate-batch-profile-destinations.md)
