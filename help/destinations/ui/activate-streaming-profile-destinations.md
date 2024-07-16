---
title: Activación de audiencias en destinos de exportación de perfiles de flujo continuo
type: Tutorial
description: Obtenga información sobre cómo activar los datos de audiencia que tiene en Adobe Experience Platform enviando audiencias a destinos basados en perfiles de streaming.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: bc0f781e-60de-44a5-93cb-06b4a3148591
source-git-commit: 6b186030c66598cddcdfcf509b8863e10d4fd0a7
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---


# Activación de audiencias en destinos de exportación de perfiles de flujo continuo

>[!IMPORTANT]
> 
> * Para activar los datos y habilitar el [paso de asignación](#mapping) del flujo de trabajo, necesita los **[!UICONTROL permisos de control de acceso]**, **[!UICONTROL Activar destinos]**, **[!UICONTROL Ver perfiles]** y **[!UICONTROL Ver segmentos]** [para ver los destinos](/help/access-control/home.md#permissions).
> * Para activar datos sin pasar por el [paso de asignación](#mapping) del flujo de trabajo, necesita los **[!UICONTROL permisos de vista de destinos]**, **[!UICONTROL activar segmento sin asignación]**, **[!UICONTROL ver perfiles]** y **[!UICONTROL ver segmentos]** [permisos de control de acceso](/help/access-control/home.md#permissions).
> 
> Lea la [descripción general del control de acceso](/help/access-control/ui/overview.md) o póngase en contacto con el administrador del producto para obtener los permisos necesarios.

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en Adobe Experience Platform a destinos de perfil de flujo continuo (también denominados [destinos empresariales](/help/destinations/destination-types.md#streaming-profile-export)).

Este artículo se aplica a los siguientes tres destinos:

* [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [Destino de API HTTP](/help/destinations/catalog/streaming/http-destination.md).

## Requisitos previos {#prerequisites}

Para activar los datos en los destinos, debes haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), examine los destinos admitidos y configure el destino que desee utilizar.

## Seleccione su destino {#select-destination}

1. Vaya a **[!UICONTROL Conexiones > Destinos]** y seleccione la pestaña **[!UICONTROL Catálogo]**.

   ![Imagen que muestra la ficha de catálogo de destino.](../assets/ui/activate-streaming-profile-destinations/catalog-tab.png)

1. Seleccione **[!UICONTROL Activar audiencias]** en la tarjeta correspondiente al destino donde desea activar las audiencias, como se muestra en la imagen siguiente.

   ![Imagen que resalta el control Activar audiencias en la pestaña Catálogo de destinos.](../assets/ui/activate-streaming-profile-destinations/activate-audiences-button.png)

1. Seleccione la conexión de destino que desee usar para activar las audiencias y, a continuación, seleccione **[!UICONTROL Siguiente]**.

   ![Imagen que muestra una selección de dos destinos a los que puede conectarse.](../assets/ui/activate-streaming-profile-destinations/select-destination.png)

1. Pasa a la siguiente sección para [seleccionar tus audiencias](#select-audiences).

## Selección de audiencias {#select-audiences}

Para seleccionar las audiencias que desea activar en el destino, utilice las casillas de verificación que aparecen a la izquierda de los nombres de audiencia y luego seleccione **[!UICONTROL Siguiente]**.

Puede seleccionar entre varios tipos de audiencias, según su origen:

* **[!UICONTROL Servicio de segmentación]**: Audiencias generadas en Experience Platform por el servicio de segmentación. Consulte la [documentación de Audience Portal](../../segmentation/ui/audience-portal.md) para obtener más información.
* **[!UICONTROL Carga personalizada]**: audiencias generadas fuera de Experience Platform y cargadas en Platform como archivos CSV. Para obtener más información sobre audiencias externas, consulte la documentación sobre [importación de una audiencia](../../segmentation/ui/audience-portal.md#import-audience).
* Otros tipos de audiencias, originadas en otras soluciones de Adobe, como [!DNL Audience Manager].

![Imagen que resalta la selección de casillas de verificación en el paso Seleccionar audiencias del flujo de trabajo de activación.](../assets/ui/activate-streaming-profile-destinations/select-audiences.png)

## Seleccionar atributos de perfil {#select-attributes}

En el paso **[!UICONTROL Asignación]**, seleccione los atributos de perfil que desee enviar al destino de destino.

1. En la página **[!UICONTROL Seleccionar atributos]**, seleccione **[!UICONTROL Agregar nuevo campo]**.

   ![Imagen que resalta el control Agregar nuevo campo en el paso de asignación.](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Seleccione la flecha a la derecha de la entrada **[!UICONTROL Campo de esquema]**.

   ![Imagen que resalta cómo seleccionar un campo de origen en el paso de asignación.](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. En la página **[!UICONTROL Seleccionar campo]**, seleccione los atributos XDM que desee enviar al destino y, a continuación, elija **[!UICONTROL Seleccionar]**.

   ![Imagen que muestra una selección de campos XDM que puede seleccionar como campos de origen.](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)

1. Para agregar más campos, repita los pasos del 1 al 3 y después seleccione **[!UICONTROL Siguiente]**.

## Revisar {#review}

En la página **[!UICONTROL Revisar]**, puedes ver un resumen de tu selección. Seleccione **[!UICONTROL Cancelar]** para dividir el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos al destino.

![Resumen de la selección en el paso de revisión.](../assets/ui/activate-streaming-profile-destinations/review.png)

### Evaluación de directiva de consentimiento {#consent-policy-evaluation}

[La evaluación de directivas de consentimiento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) no se admite actualmente en las exportaciones a los tres destinos empresariales: Amazon Kinesis, Azure Event Hubs y la API HTTP.

Esto significa que los perfiles que no han aceptado ser segmentados *se incluyen* en las exportaciones a estos tres destinos.

<!--

If your organization purchased **Adobe Healthcare Shield** or **Adobe Privacy & Security Shield**, select **[!UICONTROL View applicable consent policies]** to see which consent policies are applied and how many profiles are included in the activation as a result of them. Read about [consent policy evaluation](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) for more information.

-->

### Comprobaciones de políticas de uso de datos {#data-usage-policy-checks}

En el paso **[!UICONTROL Revisar]**, el Experience Platform también comprueba si hay alguna infracción de la directiva de uso de datos. A continuación se muestra un ejemplo de infracción de una directiva. No puede completar el flujo de trabajo de activación de audiencia hasta que haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de directivas, lea acerca de [infracciones de directivas de uso de datos](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) en la sección de documentación de control de datos.

![infracción de directiva de datos](../assets/common/data-policy-violation.png)

### Filtrado de audiencias {#filter-audiences}

Además, en este paso puede utilizar los filtros disponibles en la página para mostrar solo las audiencias cuya programación o asignación se haya actualizado como parte de este flujo de trabajo.

![Grabación de pantalla que muestra los filtros de audiencia disponibles en el paso de revisión.](../assets/ui/activate-streaming-profile-destinations/filter-audiences-review-step.gif)

Si está satisfecho con su selección y no se han detectado infracciones de directivas, seleccione **[!UICONTROL Finalizar]** para confirmar su selección y comenzar a enviar datos al destino.

## Verificar activación de audiencia {#verify}

Los datos de [!DNL Experience Platform] exportados llegan al destino en formato JSON. Por ejemplo, el siguiente evento contiene el atributo de dirección de correo electrónico de un perfil que cumple los requisitos para una audiencia determinada y sale de otra. Las identidades de este cliente potencial son `ECID` y `email_lc_sha256`.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
