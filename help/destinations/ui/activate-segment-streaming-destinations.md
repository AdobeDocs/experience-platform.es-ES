---
keywords: activar destinos de flujo continuo de segmentos;activar destinos de flujo continuo de segmentos;activar datos
title: Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo
type: Tutorial
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform asignando segmentos a destinos de flujo continuo de segmento.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 9bde403338187409892d76de68805535de03d59f
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Activar datos de audiencia en destinos de exportación de segmentos de flujo continuo

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en los destinos de flujo continuo de segmentos de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Para activar datos en destinos, debe haber [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya a la [catálogo de destinos](../catalog/overview.md), busque los destinos compatibles y configure el destino que desea utilizar.

## Seleccione el destino {#select-destination}

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione **[!UICONTROL Catálogo]** pestaña .

   ![Ficha Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Select **[!UICONTROL Activar segmentos]** en la tarjeta correspondiente al destino en el que desea activar los segmentos, como se muestra en la imagen siguiente.

   ![Activar botones](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Seleccione la conexión de destino que desee utilizar para activar los segmentos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Seleccionar destino](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Mover a la siguiente sección a [seleccione sus segmentos](#select-segments).

## Seleccione los segmentos {#select-segments}

Utilice las casillas de verificación a la izquierda de los nombres de los segmentos para seleccionar los segmentos que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Seleccionar segmentos](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Asignación de atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Este paso solo se aplica a algunos destinos de flujo continuo de segmentos. Si el destino no tiene un **[!UICONTROL Asignación]** paso, vaya a [Programar exportación de segmentos](#scheduling).

Algunos destinos de flujo continuo de segmentos requieren que seleccione atributos de origen o áreas de nombres de identidad para asignarlos como identidades de destino en el destino.

1. En el **[!UICONTROL Asignación]** página, seleccione **[!UICONTROL Añadir nueva asignación]**.

   ![Añadir nueva asignación](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Seleccione la flecha a la derecha del **[!UICONTROL Campo de origen]** entrada.

   ![Seleccionar campo de origen](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. En el **[!UICONTROL Seleccionar campo de origen]** utilice la **[!UICONTROL Seleccionar atributos]** o **[!UICONTROL Seleccionar área de nombres de identidad]** para cambiar entre las dos categorías de campos de origen disponibles. Desde la [!DNL XDM] atributos de perfil y áreas de nombres de identidad, seleccione los que desee asignar al destino y, a continuación, elija **[!UICONTROL Select]**.

   ![Seleccionar página de campo de origen](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Seleccione el botón situado a la derecha del **[!UICONTROL Campo de destino]** entrada.

   ![Seleccionar campo de destino](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione el área de nombres de identidad de destino al que desea asignar el campo de origen y elija **[!UICONTROL Select]**.

   ![Seleccionar página de campo de destino](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para agregar más asignaciones, repita los pasos del 1 al 5.

### Aplicar transformación {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformación"
>abstract="Marque esta opción cuando utilice campos de origen sin hash, para que Adobe Experience Platform los hash automáticamente en la activación."

Cuando asigna atributos de origen sin hash a atributos de destino que el destino espera que tengan un hash (por ejemplo: `email_lc_sha256` o `phone_sha256`), marque la casilla **Aplicar transformación** para que Adobe Experience Platform hash automáticamente los atributos de origen al activarlos.

![Asignación de identidad](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Programar exportación de segmentos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Fecha final"
>abstract="No está disponible la adición de una fecha de finalización para la programación de segmentos."

De forma predeterminada, la variable [!UICONTROL Programación de segmentos] muestra solo los segmentos recién seleccionados que eligió en el flujo de activación actual.

![Nuevos segmentos](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Para ver todos los segmentos que se activan en el destino, utilice la opción de filtrado y deshabilite la variable **[!UICONTROL Mostrar solo segmentos nuevos]** filtro.

![Todos los segmentos](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. En el **[!UICONTROL Programación de segmentos]** , seleccione cada segmento y, a continuación, use la **[!UICONTROL Fecha de inicio]** y **[!UICONTROL Fecha final]** selectores para configurar el intervalo de tiempo para enviar datos al destino.

   ![Programación de segmentos](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Algunos destinos requieren que seleccione el **[!UICONTROL Origen de la audiencia]** para cada segmento, utilice el menú desplegable debajo de los selectores de calendario. Si el destino no incluye este selector, omita este paso.

      ![ID de asignación](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Algunos destinos requieren que asigne manualmente [!DNL Platform] segmentos a su homólogo en el destino de destino. Para ello, seleccione cada segmento e introduzca el ID de segmento correspondiente de la plataforma de destino en la **[!UICONTROL ID de asignación]** campo . Si el destino no incluye este campo, omita este paso.

      ![ID de asignación](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Algunos destinos requieren que introduzca un **[!UICONTROL ID de la aplicación]** al activar [!DNL IDFA] o [!DNL GAID] segmentos. Si el destino no incluye este campo, omita este paso.

      ![ID de aplicación](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Select **[!UICONTROL Siguiente]** para ir a la [!UICONTROL Consulte] página.

## Revisión {#review}

En el **[!UICONTROL Consulte]** , puede ver un resumen de su selección. Select **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración, o **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

![Resumen de selección en la etapa de revisión.](/help/destinations/assets/ui/activate-segment-streaming-destinations/review.png)

### Evaluación de la directiva de consentimiento {#consent-policy-evaluation}

Si su organización ha adquirido **Adobe Escudo Sanitario** o **Protección de seguridad y privacidad de Adobe**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué políticas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Más información [evaluación de la política de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

### Comprobaciones de políticas de uso de datos {#data-usage-policy-checks}

En el **[!UICONTROL Consulte]** , el Experience Platform también comprueba si hay alguna infracción de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver violaciones de políticas, lea acerca de [infracciones de directiva de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección documentación de control de datos .

![violación de la política de datos](../assets/common/data-policy-violation.png)

### Filtrar segmentos. {#filter-segments}

Además, en este paso puede utilizar los filtros disponibles en la página para mostrar solo los segmentos cuya programación o asignación se haya actualizado como parte de este flujo de trabajo. También puede alternar qué columnas de tabla desea ver.

![Grabación de pantalla que muestra los filtros de segmento disponibles en el paso de revisión.](/help/destinations/assets/ui/activate-segment-streaming-destinations/filter-segments-review-step.gif)

Si está satisfecho con la selección y no se han detectado infracciones de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

## Verificación de la activación de segmentos {#verify}

Marque la [documentación de monitorización de destino](../../dataflows/ui/monitor-destinations.md) para obtener información detallada sobre cómo monitorizar el flujo de datos a sus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
