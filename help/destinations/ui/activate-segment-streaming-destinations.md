---
title: Activar datos de audiencia en destinos de flujo continuo
type: Tutorial
description: Obtenga información sobre cómo activar las audiencias que tiene en Adobe Experience Platform asignándolas a destinos de flujo continuo.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 30ad6c32d8ae8a2a68dfafd78f306209ce49b6d5
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 6%

---


# Activar audiencias en destinos de flujo continuo

>[!IMPORTANT]
> 
> * Para activar audiencias y activar la variable [paso de asignación](#mapping) del flujo de trabajo, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
> * Para activar audiencias sin pasar por el [paso de asignación](#mapping) del flujo de trabajo, necesita el **[!UICONTROL Ver destinos]**, **[!UICONTROL Activar segmento sin asignación]**, **[!UICONTROL Ver perfiles]**, y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
>* Para exportar *identidades*, necesita el **[!UICONTROL Ver gráfico de identidad]** [permiso de control de acceso](/help/access-control/home.md#permissions). <br> ![Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleccione el área de nombres de identidad resaltada en el flujo de trabajo para activar audiencias en los destinos."){width="100" zoomable="yes"}
> 
> Lea el [información general de control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar audiencias en los destinos de flujo de Adobe Experience Platform.

## Requisitos previos {#prerequisites}

Para activar audiencias en destinos, debe tener [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

## Seleccione su destino {#select-destination}

1. Ir a **[!UICONTROL Conexiones > Destinos]** y seleccione la opción **[!UICONTROL Catálogo]** pestaña.

   ![Pestaña Catálogo de destino que muestra varios destinos de flujo continuo.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Seleccionar **[!UICONTROL Activar audiencias]** en la tarjeta correspondiente al destino donde desea activar sus audiencias, como se muestra en la siguiente imagen.

   ![Activar el control resaltado en el catálogo de destinos.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Seleccione la conexión de destino que desee utilizar para activar las audiencias y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Una conexión de destino resaltada en el paso Seleccionar destino.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Mover a la sección siguiente para [seleccionar las audiencias](#select-audiences).

## Selección de audiencias {#select-audiences}

Para seleccionar las audiencias que desea activar en el destino, utilice las casillas de verificación a la izquierda de los nombres de audiencia y luego seleccione **[!UICONTROL Siguiente]**.

Puede seleccionar entre varios tipos de audiencias, según su origen:

* **[!UICONTROL Servicio de segmentación]**: Audiencias generadas dentro de Experience Platform por el servicio de segmentación. Consulte la [documentación de segmentación](../../segmentation/ui/overview.md) para obtener más información.
* **[!UICONTROL Carga personalizada]**: Audiencias generadas fuera de Experience Platform y cargadas en Platform como archivos CSV. Para obtener más información acerca de las audiencias externas, consulte la documentación sobre [importación de una audiencia](../../segmentation/ui/overview.md#import-audience).
* Otros tipos de audiencias, procedentes de otras soluciones de Adobe, como [!DNL Audience Manager].

![Varias audiencias resaltadas en el paso Seleccionar audiencias.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Asignar atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Este paso solo se aplica a algunos destinos de flujo de audiencia. Si su destino no tiene un **[!UICONTROL Asignación]** paso, saltar a [programación de audiencia](#scheduling).
>
>Al activar audiencias en destinos de flujo continuo, también debe asignar *al menos un área de nombres de identidad de destino*, además de atributos de perfil de destinatario. De lo contrario, las audiencias no se activarán en la plataforma de destino.
> ![Imagen del paso de asignación que muestra una asignación de área de nombres de identidad obligatoria.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Algunos destinos de flujo de audiencia requieren que seleccione atributos de origen o áreas de nombres de identidad para asignar como identidades de destino en el destino.

1. En el **[!UICONTROL Asignación]** página, seleccione **[!UICONTROL Añadir nueva asignación]**.

   ![Agregar nuevo control de asignación resaltado.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Seleccione la flecha a la derecha de la **[!UICONTROL Campo de origen]** entrada.

   ![Seleccione el control de campo de origen resaltado.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. En el **[!UICONTROL Seleccionar campo de origen]** página, utilice el **[!UICONTROL Seleccionar atributos]** o el **[!UICONTROL Seleccionar área de nombres de identidad]** opciones para cambiar entre las dos categorías de campos de origen disponibles. De los disponibles [!DNL XDM] atributos de perfil y áreas de nombres de identidad, seleccione los que desee asignar al destino y, a continuación, elija **[!UICONTROL Seleccionar]**.

   Utilice el **[!UICONTROL Mostrar solo campos con datos]** active esta opción para mostrar solo los campos de esquema rellenados con valores. De forma predeterminada, solo se muestran los campos de esquema rellenados.

   ![Seleccionar página de campo de origen que muestra varios campos de origen disponibles.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Seleccione el botón a la derecha del **[!UICONTROL Campo de destino]** entrada.

   ![Seleccione el campo de destino resaltado.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. En el **[!UICONTROL Seleccionar campo de destino]** , seleccione el área de nombres de identidad de destino al que desea asignar el campo de origen y elija **[!UICONTROL Seleccionar]**.

   ![La página Seleccionar campo de destino muestra las opciones disponibles para las asignaciones de campo de destino.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para agregar más asignaciones, repita los pasos del 1 al 5.

### Aplicar transformación {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformación"
>abstract="Marque esta opción cuando utilice campos de origen sin hash, para que Adobe Experience Platform aplique un algoritmo hash en ellos automáticamente en la activación."

Cuando asigne atributos de origen sin hash a atributos de destino que el destino espera que tengan hash (por ejemplo: `email_lc_sha256` o `phone_sha256`), marque la **Aplicar transformación** para que Adobe Experience Platform agregue automáticamente los atributos de origen al activarlos.

![Aplique el control de transformación resaltado en el paso Asignación de identidad.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Programar exportación de público {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Fecha final"
>abstract="No está disponible la adición de una fecha de finalización para la programación de público."

De forma predeterminada, la variable **[!UICONTROL Programación de audiencia]** Esta página muestra únicamente las audiencias recién seleccionadas que eligió en el flujo de activación actual.

Para ver todas las audiencias que se están activando en su destino, utilice la opción de filtrado y deshabilite la **[!UICONTROL Mostrar solo las nuevas audiencias]** filtro.

![Todas las audiencias](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. En el **[!UICONTROL Programación de audiencia]** página, seleccione cada audiencia y utilice el **[!UICONTROL Fecha de inicio]** y **[!UICONTROL Fecha de finalización]** para configurar el intervalo de tiempo para enviar datos al destino.

   ![Filtro de programación de audiencia resaltado.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Algunos destinos requieren que seleccione **[!UICONTROL Origen de la audiencia]** para cada audiencia, utilice el menú desplegable situado debajo de los selectores de calendario. Si el destino no incluye este selector, omita este paso.

     ![Menú desplegable ID de asignación resaltado.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Algunos destinos requieren que los asigne manualmente [!DNL Platform] a su homólogo en el destino de destino. Para ello, seleccione cada audiencia e introduzca el ID de audiencia correspondiente en la plataforma de destino en **[!UICONTROL ID de asignación]** field. Si el destino no incluye este campo, omita este paso.

     ![Se ha resaltado el origen de la lista desplegable de audiencias.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Algunos destinos requieren que escriba un **[!UICONTROL ID de aplicación]** al activar [!DNL IDFA] o [!DNL GAID] audiencias. Si el destino no incluye este campo, omita este paso.

     ![Lista desplegable de ID de aplicación resaltada.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Seleccionar **[!UICONTROL Siguiente]** para ir a [!UICONTROL Revisar] página.

## Revisar {#review}

En el **[!UICONTROL Revisar]** , puede ver un resumen de su selección. Seleccionar **[!UICONTROL Cancelar]** para romper el flujo, **[!UICONTROL Atrás]** para modificar la configuración, o **[!UICONTROL Finalizar]** para confirmar la selección y comenzar a enviar datos al destino.

![Resumen de la selección en el paso de revisión.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Evaluación de directiva de consentimiento {#consent-policy-evaluation}

Si su organización ha adquirido **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**, seleccione **[!UICONTROL Ver directivas de consentimiento aplicables]** para ver qué directivas de consentimiento se aplican y cuántos perfiles se incluyen en la activación como resultado de ellas. Más información [evaluación de directiva de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obtener más información.

### Comprobaciones de políticas de uso de datos {#data-usage-policy-checks}

En el **[!UICONTROL Revisar]** paso, el Experience Platform también comprueba si hay alguna infracción de la política de uso de datos. A continuación se muestra un ejemplo de infracción de una directiva. No puede completar el flujo de trabajo de activación de audiencia hasta que haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de directivas, consulte [infracciones de políticas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección documentación de control de datos.

![Ejemplo de una infracción de la política de datos que se muestra en el flujo de trabajo de activación.](../assets/common/data-policy-violation.png)

### Filtrado de audiencias {#filter-audiences}

Además, en este paso puede utilizar los filtros disponibles en la página para mostrar solo las audiencias cuya programación o asignación se haya actualizado como parte de este flujo de trabajo. También puede alternar qué columnas de tabla desea ver.

![Grabación de pantalla que muestra los filtros de audiencia disponibles en el paso de revisión.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Si está satisfecho con la selección y no se han detectado infracciones de directivas, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y comenzar a enviar datos al destino.

## Verificar activación de audiencia {#verify}

Compruebe la [documentación de supervisión de destino](../../dataflows/ui/monitor-destinations.md) para obtener información detallada sobre cómo monitorizar el flujo de datos a sus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
