---
keywords: activar destinos de solicitud de perfil;activar datos;destinos de solicitud de perfil
title: Activar datos de audiencia en destinos de solicitud de perfil
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform asignando segmentos a destinos de solicitud de perfil.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Activar datos de audiencia en destinos de solicitud de perfil (Beta)

## Información general {#overview}

>[!IMPORTANT]
>
>Los destinos de solicitud de perfil en Adobe Experience Platform están actualmente en versión beta. La documentación y la funcionalidad están sujetas a cambios.

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en los destinos de solicitud de perfil de Adobe Experience Platform. Algunos ejemplos de destinos de solicitud de perfil son las conexiones [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y [Custom personalization](../../destinations/catalog/personalization/custom-personalization.md).

## Requisitos previos {#prerequisites}

Para activar los datos en los destinos, debe haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), busque los destinos admitidos y configure el destino que desea utilizar.

### Política de combinación de segmentos {#merge-policy}

Actualmente, los destinos de solicitud de perfil solo admiten la activación de segmentos que utilizan la directiva de combinación predeterminada. Si se intenta activar segmentos con una política de combinación diferente, se producirá un error en la página [[!UICONTROL Revisar]](#review).

## Seleccione el destino {#select-destination}

1. Vaya a **[!UICONTROL Connections > Destinations]** y seleccione la pestaña **[!UICONTROL Catalog]**.

   ![Ficha Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar segmentos]** en la tarjeta correspondiente al destino donde desee activar los segmentos, como se muestra en la imagen siguiente.

   ![Activar botones](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Seleccione la conexión de destino que desee utilizar para activar los segmentos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Seleccionar destino](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Cambie a la siguiente sección para [seleccionar sus segmentos](#select-segments).

## Seleccione los segmentos {#select-segments}

Utilice las casillas de verificación a la izquierda de los nombres de los segmentos para seleccionar los segmentos que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Seleccionar segmentos](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Programar exportación de segmentos {#scheduling}

De forma predeterminada, la página [!UICONTROL Segment schedule] muestra solo los segmentos recién seleccionados que eligió en el flujo de activación actual.

![Nuevos segmentos](../assets/ui/activate-profile-request-destinations/new-segments.png)

Para ver todos los segmentos que se activan en el destino, utilice la opción de filtrado y deshabilite el filtro **[!UICONTROL Mostrar solo segmentos nuevos]**.

![Todos los segmentos](../assets/ui/activate-profile-request-destinations/all-segments.png)

En la página **[!UICONTROL Segment schedule]**, seleccione cada segmento y, a continuación, utilice los selectores **[!UICONTROL Start date]** y **[!UICONTROL End date]** para configurar el intervalo de tiempo para enviar datos a su destino.

![Programación de segmentos](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Seleccione **[!UICONTROL Siguiente]** para ir a la página [!UICONTROL Revisar].

## Consulte {#review}

En la página **[!UICONTROL Revisar]**, puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de control de datos.

![violación de la política de datos](../assets/common/data-policy-violation.png)

Si no se han detectado infracciones de directiva, seleccione **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

![Consulte](../assets/ui/activate-profile-request-destinations/review.png)

## Verificación de la activación de segmentos {#verify}

Consulte la [documentación de monitorización de destino](../../dataflows/ui/monitor-destinations.md) para obtener información detallada sobre cómo monitorizar el flujo de datos a sus destinos.