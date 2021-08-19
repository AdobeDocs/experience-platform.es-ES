---
keywords: activar destinos de flujo continuo de segmentos;activar destinos de flujo continuo de segmentos;activar datos
title: Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo
type: Tutorial
seo-title: Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform asignando segmentos a destinos de flujo continuo de segmento.
seo-description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform asignando segmentos a destinos de flujo continuo de segmento.
source-git-commit: c3e273c66ffe0542258e5418104e0bcf154f5235
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---


# Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en los destinos de flujo continuo de segmentos de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Para activar los datos en los destinos, debe haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), busque los destinos admitidos y configure el destino que desea utilizar.

## Seleccione el destino {#select-destination}

1. Vaya a **[!UICONTROL Connections > Destinations]** y seleccione la pestaña **[!UICONTROL Browse]**.

   ![Ficha Exploración de destino](../assets/ui/activate-segment-streaming-destinations/browse-tab.png)

1. Seleccione el botón **[!UICONTROL Add segments]** correspondiente al destino en el que desea activar los segmentos, como se muestra en la imagen siguiente.

   ![Activar botones](../assets/ui/activate-segment-streaming-destinations/activate-buttons-browse.png)

1. Cambie a la siguiente sección para [seleccionar sus segmentos](#select-segments).

## Seleccione los segmentos {#select-segments}

Utilice las casillas de verificación a la izquierda de los nombres de los segmentos para seleccionar los segmentos que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Seleccionar segmentos](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Asignación de atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Este paso solo se aplica a algunos destinos de flujo continuo de segmentos. Si el destino no tiene un paso **[!UICONTROL Mapping]**, vaya a [Schedule segment export](#scheduling).

Algunos destinos de flujo continuo de segmentos requieren que seleccione atributos de origen o áreas de nombres de identidad para asignarlos como identidades de destino en el destino.

1. En la página **[!UICONTROL Mapping]**, seleccione **[!UICONTROL Add new mapping]**.

   ![Añadir nueva asignación](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Seleccione la flecha a la derecha de la entrada **[!UICONTROL Source field]**.

   ![Seleccionar campo de origen](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. En la página **[!UICONTROL Seleccionar campo de origen]**, utilice las opciones **[!UICONTROL Select attributes]** o **[!UICONTROL Select identity namespace]** para cambiar entre las dos categorías de campos de origen disponibles. En los atributos de perfil y áreas de nombres de identidad disponibles [!DNL XDM], seleccione los que desee asignar al destino y, a continuación, elija **[!UICONTROL Seleccionar]**.

   ![Seleccionar página de campo de origen](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Seleccione el botón situado a la derecha de la entrada **[!UICONTROL Target field]**.

   ![Seleccionar campo de destino](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. En la página **[!UICONTROL Select target field]**, seleccione el espacio de nombres de la identidad de destino al que desea asignar el campo de origen y elija **[!UICONTROL Select]**.

   ![Seleccionar página de campo de destino](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para agregar más asignaciones, repita los pasos del 1 al 5.

### Aplicar transformación {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformación"
>abstract="Marque esta opción cuando utilice campos de origen sin hash, para que Adobe Experience Platform los hash automáticamente en la activación."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html?lang=en#apply-transformation" text="Más información en la documentación"

Cuando asigna atributos de origen sin hash a atributos de destino que el destino espera que tengan un hash (por ejemplo: `email_lc_sha256` o `phone_sha256`), marque la opción **Aplicar transformación** para que Adobe Experience Platform hash automáticamente los atributos de origen en la activación.

![Asignación de identidad](/help/destinations/assets/ui/activate-segment-streaming-destinations/mapping-summary.png)


## Programar exportación de segmentos {#scheduling}

1. En la página **[!UICONTROL Segment schedule]**, seleccione cada segmento y, a continuación, utilice los selectores **[!UICONTROL Start date]** y **[!UICONTROL End date]** para configurar el intervalo de tiempo para enviar datos a su destino.

   ![Programación de segmentos](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Algunos destinos requieren que seleccione el **[!UICONTROL Origin of audience]** para cada segmento mediante el menú desplegable debajo de los selectores de calendario. Si el destino no incluye este selector, omita este paso.

      ![ID de asignación](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Algunos destinos requieren que asigne manualmente [!DNL Platform] segmentos a su homólogo en el destino. Para ello, seleccione cada segmento e introduzca el ID de segmento correspondiente de la plataforma de destino en el campo **[!UICONTROL Mapping ID]**. Si el destino no incluye este campo, omita este paso.

      ![ID de asignación](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Algunos destinos requieren que introduzca un **[!UICONTROL ID de aplicación]** al activar segmentos [!DNL IDFA] o [!DNL GAID]. Si el destino no incluye este campo, omita este paso.

      ![ID de aplicación](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Seleccione **[!UICONTROL Siguiente]** para ir a la página [!UICONTROL Revisar].

## Consulte {#review}

En la página **[!UICONTROL Revisar]**, puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de control de datos.

![violación de la política de datos](../assets/common/data-policy-violation.png)

Si no se han detectado infracciones de directiva, seleccione **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

![Consulte](../assets/ui/activate-segment-streaming-destinations/review.png)

## Verificación de la activación de segmentos {#verify}

Compruebe la cuenta de destino. Si la activación se ha realizado correctamente, las audiencias se rellenan en la plataforma de destino.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
