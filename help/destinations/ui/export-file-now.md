---
title: (Beta) Exportar archivos bajo demanda a destinos por lotes utilizando la interfaz de usuario del Experience Platform
type: Tutorial
description: Obtenga información sobre cómo exportar archivos bajo demanda a destinos por lotes mediante la interfaz de usuario del Experience Platform.
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# (Beta) Exportar archivos bajo demanda a destinos por lotes utilizando la interfaz de usuario del Experience Platform

>[!IMPORTANT]
>
>La variable **[!UICONTROL Exportar archivo ahora]** en Adobe Experience Platform se encuentra en versión beta. La documentación y la funcionalidad están sujetas a cambios.
>Póngase en contacto con su representante de Adobe para obtener acceso a esta funcionalidad.

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## **[!UICONTROL Exportar archivo ahora]** información general {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="Exportar archivo ahora"
>abstract="Seleccione este control para enviar una exportación completa de archivos, además de cualquier exportación programada previamente. La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform."

Este artículo explica cómo utilizar la interfaz de usuario del Experience Platform para exportar archivos bajo demanda a destinos por lotes como [almacenamiento en la nube](/help/destinations/catalog/cloud-storage/overview.md) y [marketing por correo electrónico](/help/destinations/catalog/email-marketing/overview.md) destinos.

La variable **[!UICONTROL Exportar archivo ahora]** permite exportar un archivo completo sin interrumpir la programación de exportación actual de un segmento previamente programado. Esta exportación se produce además de exportaciones programadas anteriormente y no cambia la frecuencia de exportación del segmento. La exportación de archivos se activa inmediatamente y recoge los resultados más recientes de las ejecuciones de segmentación de Experience Platform.

También puede utilizar las API de Experience Platform para este fin. Leer cómo [activar segmentos de audiencia según demanda a destinos por lotes mediante la API de activación ad-hoc](/help/destinations/api/ad-hoc-activation-api.md).

## Requisitos previos {#prerequisites}

Para exportar archivos bajo demanda a destinos por lotes, debe haber [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya a la [catálogo de destinos](../catalog/overview.md), busque los destinos compatibles y configure el destino que desea utilizar.

## Exportación de archivos bajo demanda {#how-to-export-files-on-demand}

1. Vaya a **[!UICONTROL Conexiones > Destinos]**, seleccione **[!UICONTROL Examinar]** y el símbolo de filtro para mostrar las conexiones existentes a los destinos de lote deseados.

   ![Imagen que resalta cómo llegar a la pestaña Examinar y filtrar los flujos de datos existentes.](../assets/ui/activate-on-demand/browse-tab.png)

2. Seleccione la conexión de destino que desee para inspeccionar el flujo de datos existente hasta el destino.

   ![Imagen que resalta un flujo de datos filtrado.](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. Seleccione el **[!UICONTROL Datos de activación]** y seleccione el segmento para el que desea exportar un archivo bajo demanda y seleccione la opción **[!UICONTROL Exportar archivo ahora]** para realizar una déclencheur de una exportación única que enviará un archivo al destino del lote.

   >[!IMPORTANT]
   >
   >Actualmente, la IU no admite la selección de varios segmentos para exportar archivos a la carta de forma masiva. Utilice la variable [API de activación ad hoc](/help/destinations/api/ad-hoc-activation-api.md) para ello.

   ![Imagen que resalta el botón Exportar archivo ahora.](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. Select **[!UICONTROL Sí]** para confirmar y almacenar en déclencheur la exportación de archivos.

   ![Imagen que muestra el cuadro de diálogo Exportar archivo ahora confirmación.](../assets/ui/activate-on-demand/confirm-activation.png)

5. Aparece un mensaje de confirmación que informa de que se ha iniciado la exportación del archivo.

   ![Imagen que muestra la confirmación de una activación ad hoc correcta.](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. También puede cambiar al **[!UICONTROL Ejecuciones de flujo de datos]** para confirmar que se ha iniciado la exportación del archivo.

## Consideraciones {#considerations}

Tenga en cuenta las siguientes consideraciones al usar la variable **[!UICONTROL Exportar archivo ahora]** control:

* **[!UICONTROL Exportar archivo ahora]** solo funciona para segmentos cuya programación en el flujo de datos de activación por lotes se superpone con la fecha actual. Esto incluye segmentos con programaciones que no tienen fecha de finalización (frecuencia de exportación de **[!UICONTROL Una vez]**), o donde la fecha de finalización aún no ha pasado.
* Cuando agregue un segmento a un flujo de datos existente, espere al menos 15 minutos hasta que use la variable **[!UICONTROL Exportar archivo ahora]** control.
* Si cambia la política de combinación de un segmento, o si crea un segmento que utiliza una nueva política de combinación, espere 24 horas hasta que utilice la variable **[!UICONTROL Exportar archivo ahora]** control.

## Mensajes de error de la interfaz de usuario {#ui-error-messages}

Al usar la variable **[!UICONTROL Exportar archivo ahora]** , puede encontrar cualquiera de los mensajes de error enumerados a continuación. Revise la tabla para comprender cómo abordarlos cuando aparecen.

| Mensaje de error | Resolución |
|---------|----------|
| Ejecutar ya en curso para el segmento `segment ID` para pedido `dataflow ID` con id de ejecución `flow run ID` | Este mensaje de error indica que un flujo de activación ad hoc está actualmente en curso para un segmento. Espere a que finalice el trabajo antes de activar de nuevo el trabajo de activación. |
| Segmentos `<segment name>` no forman parte de este flujo de datos ni están fuera del intervalo de programación. | Este mensaje de error indica que los segmentos que ha seleccionado para activar no están asignados al flujo de datos o que la programación de activación configurada para los segmentos ha caducado o aún no se ha iniciado. Compruebe si el segmento está asignado al flujo de datos y compruebe que la programación de activación de segmentos se superponga con la fecha actual. |

## Información relacionada {#related-information}

* [Activar segmentos de audiencia en destinos por lotes según demanda mediante las API de Experience Platform](/help/destinations/api/ad-hoc-activation-api.md)
* [Activar datos de audiencia en destinos de exportación de perfiles en lote](/help/destinations/ui/activate-batch-profile-destinations.md)
