---
keywords: activar destinos de solicitud de perfil;activar datos;destinos de solicitud de perfil
title: Activar datos de audiencia en destinos de solicitud de perfil
type: Tutorial
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform asignando segmentos a destinos de solicitud de perfil.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 26e7a3e78a4513aa69cdfbed7902509609e114cc
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Activar datos de audiencia en destinos de solicitud de perfil

>[!IMPORTANT]
> 
>Para activar los datos, necesita la variable **[!UICONTROL Administrar destinos]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions). Lea el [información general sobre el control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en los destinos de solicitud de perfil de Adobe Experience Platform. Cuando se usa junto con [segmentación de arista](../../segmentation/ui/edge-segmentation.md), estos destinos habilitan casos de uso de personalización de la misma página y de la página siguiente en sus propiedades web. Más información sobre [activación de casos de uso de personalización de la misma página y de la siguiente página](/help/destinations/ui/configure-personalization-destinations.md).

Algunos ejemplos de destinos de solicitud de perfil son los [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) y [Personalización personalizada](../../destinations/catalog/personalization/custom-personalization.md) conexiones.

## Requisitos previos {#prerequisites}

Para activar datos en destinos, debe haber [conectado a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya a la [catálogo de destinos](../catalog/overview.md), busque los destinos de personalización admitidos y configure el destino que desea utilizar.

### Política de combinación de segmentos {#merge-policy}

Actualmente, los destinos de solicitud de perfil solo admiten la activación de segmentos que utilizan la variable [Política de combinación activa/perimetral](../../segmentation/ui/segment-builder.md#merge-policies) se establece como predeterminado.

## Seleccione el destino {#select-destination}

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione **[!UICONTROL Catálogo]** pestaña .

   ![Ficha Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Select **[!UICONTROL Activar segmentos]** en la tarjeta correspondiente al destino de personalización donde desee activar los segmentos, como se muestra en la imagen siguiente.

   ![Activar botones](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Seleccione la conexión de destino que desee utilizar para activar los segmentos y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Seleccionar destino](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Mover a la siguiente sección a [seleccione sus segmentos](#select-segments).

## Seleccione los segmentos {#select-segments}

Utilice las casillas de verificación a la izquierda de los nombres de los segmentos para seleccionar los segmentos que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Seleccionar segmentos](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Beta) Asignación de atributos {#map-attributes}

>[!IMPORTANT]
>
>El paso de asignación, que permite la personalización basada en atributos para [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) y [destinos de personalización genéricos](/help/destinations/catalog/personalization/custom-personalization.md), se encuentra en la versión beta y es posible que su organización aún no tenga acceso a él. Esta documentación está sujeta a cambios.

Seleccione los atributos en función de los cuales desea habilitar los casos de uso de personalización para los usuarios. Esto significa que si el valor de un atributo cambia o si se agrega un atributo a un perfil, ese perfil se convertirá en miembro del segmento y se activará en el destino de personalización.

La adición de atributos es opcional y aún puede continuar con el paso siguiente y habilitar la personalización de la misma página y de la página siguiente sin seleccionar atributos. Si no añade ningún atributo en este paso, la personalización se seguirá realizando en función de la pertenencia al segmento y las cualificaciones de asignación de identidad para los perfiles.

![Imagen que muestra el paso de asignación con un atributo seleccionado](../assets/ui/activate-profile-request-destinations/mapping-step.png)

Para añadir atributos, seleccione la opción **[!UICONTROL Añadir nuevo campo]** controle y busque o vaya al campo de atributo XDM deseado, como se muestra a continuación.

![Registro de pantalla que muestra cómo seleccionar un atributo XDM en el paso de asignación](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

## Programar exportación de segmentos {#scheduling}

De forma predeterminada, la variable [!UICONTROL Programación de segmentos] muestra solo los segmentos recién seleccionados que eligió en el flujo de activación actual.

![Nuevos segmentos](../assets/ui/activate-profile-request-destinations/new-segments.png)

Para ver todos los segmentos que se activan en el destino, utilice la opción de filtrado y deshabilite la variable **[!UICONTROL Mostrar solo segmentos nuevos]** filtro.

![Todos los segmentos](../assets/ui/activate-profile-request-destinations/all-segments.png)

En el **[!UICONTROL Programación de segmentos]** , seleccione cada segmento y, a continuación, use la **[!UICONTROL Fecha de inicio]** y **[!UICONTROL Fecha final]** selectores para configurar el intervalo de tiempo para enviar datos al destino.

![Programación de segmentos](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Select **[!UICONTROL Siguiente]** para ir a la [!UICONTROL Consulte] página.

## Consulte {#review}

En el **[!UICONTROL Consulte]** , puede ver un resumen de su selección. Select **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración, o **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección documentación de control de datos .

![violación de la política de datos](../assets/common/data-policy-violation.png)

Si no se han detectado infracciones de directiva, seleccione **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

![Consulte](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->