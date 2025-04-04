---
title: Activar datos de audiencia en destinos de flujo continuo
type: Tutorial
description: Obtenga información sobre cómo activar las audiencias que tiene en Adobe Experience Platform asignándolas a destinos de flujo continuo.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 6%

---


# Activar audiencias en destinos de flujo continuo

>[!IMPORTANT]
> 
> * Para activar audiencias y habilitar el [paso de asignación](#mapping) del flujo de trabajo, necesita los **[!UICONTROL permisos de control de acceso[Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]**](/help/access-control/home.md#permissions).
> * Para activar audiencias sin pasar por el [paso de asignación](#mapping) del flujo de trabajo, necesita **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar segmento sin asignación]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
>* Para exportar *identidades*, necesita el **[!UICONTROL permiso de control de acceso](/help/access-control/home.md#permissions) de]** Ver gráfico de identidad[. <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}
> 
> Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar audiencias en los destinos de flujo de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Para activar audiencias en destinos, debes haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

## Seleccione su destino {#select-destination}

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Pestaña Catálogo de destino que muestra varios destinos de streaming.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar audiencias]** en la tarjeta correspondiente al destino donde desea activar las audiencias, como se muestra en la imagen siguiente.

   ![Activar control resaltado en el catálogo de destinos.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Seleccione la conexión de destino que desee usar para activar las audiencias y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Una conexión de destino resaltada en el paso Seleccionar destino.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Pasa a la siguiente sección para [seleccionar tus audiencias](#select-audiences).

## Selección de audiencias {#select-audiences}

Para seleccionar las audiencias que desea activar en el destino, utilice las casillas de verificación que aparecen a la izquierda de los nombres de audiencia y luego seleccione **[!UICONTROL Siguiente]**.

Puede seleccionar entre varios tipos de audiencias, según su origen:

* **[!UICONTROL Servicio de segmentación]**: Audiencias generadas en Experience Platform por el servicio de segmentación. Consulte la [documentación de segmentación](../../segmentation/ui/overview.md) para obtener más información.
* **[!UICONTROL Carga personalizada]**: audiencias generadas fuera de Experience Platform y cargadas en Experience Platform como archivos CSV. Para obtener más información sobre audiencias externas, consulte la documentación sobre [importación de una audiencia](../../segmentation/ui/audience-portal.md#import-audience).
* Otros tipos de audiencias, originadas en otras soluciones de Adobe, como [!DNL Audience Manager].

![Varias audiencias resaltadas en el paso Seleccionar audiencias.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Asignar atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Este paso solo se aplica a algunos destinos de flujo de audiencia. Si el destino no tiene un paso de **[!UICONTROL Asignación]**, vaya a [programación de audiencias](#scheduling).
>
>Al activar audiencias en destinos de flujo continuo, también debe asignar *al menos un área de nombres de identidad de destino*, además de los atributos de perfil de destino. De lo contrario, las audiencias no se activarán en la plataforma de destino.
> ![Imagen del paso de asignación que muestra una asignación obligatoria del área de nombres de identidad.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Algunos destinos de flujo de audiencia requieren que seleccione atributos de origen o áreas de nombres de identidad para asignar como identidades de destino en el destino.

1. En la página **[!UICONTROL Asignación]**, seleccione **[!UICONTROL Agregar nueva asignación]**.

   ![Agregar nuevo control de asignación resaltado.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Seleccione la flecha a la derecha de la entrada **[!UICONTROL Source field]**.

   ![Seleccionar control de campo de origen resaltado.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. En la página **[!UICONTROL Seleccionar campo de origen]**, use las opciones **[!UICONTROL Seleccionar atributos]** o **[!UICONTROL Seleccionar área de nombres de identidad]** para cambiar entre las dos categorías de campos de origen disponibles. De los atributos de perfil y las áreas de nombres de identidad de [!DNL XDM] disponibles, seleccione los que desee asignar al destino y, a continuación, elija **[!UICONTROL Seleccionar]**.

   Use la opción **[!UICONTROL Mostrar solo campos con datos]** para mostrar solo los campos de esquema rellenados con valores. De forma predeterminada, solo se muestran los campos de esquema rellenados.

   ![Seleccionar página de campo de origen que muestra varios campos de origen disponibles.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Seleccione el botón a la derecha de la entrada **[!UICONTROL Campo de destino]**.

   ![Seleccionar campo de destino resaltado.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. En la página **[!UICONTROL Seleccionar campo de destino]**, seleccione el área de nombres de identidad de destino al que desee asignar el campo de origen y elija **[!UICONTROL Seleccionar]**.

   ![Seleccione la página de campo de destino que muestra las opciones disponibles para las asignaciones de campo de destino.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para agregar más asignaciones, repita los pasos del 1 al 5.

### Aplicar transformación {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformación"
>abstract="Marque esta opción cuando utilice campos de origen sin hash, para que Adobe Experience Platform aplique un algoritmo hash en ellos automáticamente en la activación."

Cuando asigne atributos de origen sin hash a atributos de destino que el destino espera que tengan hash (por ejemplo: `email_lc_sha256` o `phone_sha256`), marque la opción **Aplicar transformación** para que Adobe Experience Platform aplique automáticamente hash a los atributos de origen al activarlos.

![Aplicar control de transformación resaltado en el paso de asignación de identidad.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Programar exportación de público {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Fecha final"
>abstract="No está disponible la adición de una fecha de finalización para la programación de público."

De manera predeterminada, la página **[!UICONTROL Programación de audiencias]** muestra solamente las audiencias recién seleccionadas que eligió en el flujo de activación actual.

Para ver todas las audiencias que se están activando en su destino, use la opción de filtrado y deshabilite el filtro **[!UICONTROL Mostrar solo nuevas audiencias]**.

![Todas las audiencias](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. En la página **[!UICONTROL Programación de audiencias]**, seleccione cada audiencia y luego use los selectores **[!UICONTROL Fecha de inicio]** y **[!UICONTROL Fecha de finalización]** para configurar el intervalo de tiempo para enviar datos a su destino.

   ![Filtro de programación de audiencia resaltado.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Algunos destinos requieren que seleccione el **[!UICONTROL Origen de la audiencia]** para cada audiencia mediante el menú desplegable situado debajo de los selectores de calendario. Si el destino no incluye este selector, omita este paso.

     ![Se ha resaltado el menú desplegable de ID de asignación.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Algunos destinos requieren que asigne manualmente [!DNL Experience Platform] audiencias a su homólogo en el destino de destino. Para ello, seleccione cada audiencia e introduzca el ID de audiencia correspondiente de la plataforma de destino en el campo **[!UICONTROL ID de asignación]**. Si el destino no incluye este campo, omita este paso.

     ![Se ha resaltado el menú desplegable Origen de la audiencia.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Algunos destinos requieren que ingrese un **[!UICONTROL ID de aplicación]** al activar audiencias de [!DNL IDFA] o [!DNL GAID]. Si el destino no incluye este campo, omita este paso.

     ![Se ha resaltado el menú desplegable de ID de aplicación.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Seleccione **[!UICONTROL Siguiente]** para ir a la página [!UICONTROL Revisar].

## Revisar {#review}

En la página **[!UICONTROL Revisar]**, puedes ver un resumen de tu selección. Seleccione **[!UICONTROL Cancelar]** para dividir el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos al destino.

![Resumen de la selección en el paso de revisión.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Evaluación de directiva de consentimiento {#consent-policy-evaluation}

Si su organización ha adquirido **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué directivas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Lea acerca de [evaluación de directivas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

### Comprobaciones de políticas de uso de datos {#data-usage-policy-checks}

En el paso **[!UICONTROL Revisar]**, Experience Platform también comprueba si hay alguna infracción de la directiva de uso de datos. A continuación se muestra un ejemplo de infracción de una directiva. No puede completar el flujo de trabajo de activación de audiencia hasta que haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de directivas, lea acerca de [infracciones de directivas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección de documentación de control de datos.

![Ejemplo de una infracción de directiva de datos que se muestra en el flujo de trabajo de activación.](../assets/common/data-policy-violation.png)

### Filtrado de audiencias {#filter-audiences}

Además, en este paso puede utilizar los filtros disponibles en la página para mostrar solo las audiencias cuya programación o asignación se haya actualizado como parte de este flujo de trabajo. También puede alternar qué columnas de tabla desea ver.

![Grabación de pantalla que muestra los filtros de audiencia disponibles en el paso de revisión.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Si está satisfecho con su selección y no se han detectado infracciones de directivas, seleccione **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos al destino.

## Verificar activación de audiencia {#verify}

Consulte la [documentación de supervisión de destino](../../dataflows/ui/monitor-destinations.md) para obtener información detallada sobre cómo supervisar el flujo de datos a sus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
