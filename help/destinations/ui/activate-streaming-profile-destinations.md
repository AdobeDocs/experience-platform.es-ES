---
keywords: activar destinos de perfil;activar destinos;activar datos; activar destinos de marketing por correo electrónico; activar destinos de almacenamiento en la nube
title: Activar datos de audiencia en destinos de exportación de perfil de flujo continuo
type: Tutorial
seo-title: Activar datos de audiencia en destinos de exportación de perfil de flujo continuo
description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform enviando segmentos a destinos basados en perfiles de flujo continuo.
seo-description: Aprenda a activar los datos de audiencia que tiene en Adobe Experience Platform enviando segmentos a destinos basados en perfiles de flujo continuo.
source-git-commit: f0c854e1b6b89d499c720328fa5054611147772f
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Activar datos de audiencia en destinos de exportación de perfil de flujo continuo

## Información general {#overview}

En este artículo se explica el flujo de trabajo necesario para activar los datos de audiencia en destinos basados en perfiles de flujo continuo de Adobe Experience Platform, como Amazon Kinesis.

## Requisitos previos {#prerequisites}

Para activar los datos en los destinos, debe haber [conectado correctamente a un destino](./connect-destination.md). Si aún no lo ha hecho, vaya al [catálogo de destinos](../catalog/overview.md), busque los destinos admitidos y configure el destino que desea utilizar.

## Seleccione el destino {#select-destination}

1. Vaya a **[!UICONTROL Connections > Destinations]** y seleccione la pestaña **[!UICONTROL Browse]**.

   ![Ficha Exploración de destino](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. Seleccione el botón **[!UICONTROL Add segments]** correspondiente al destino en el que desea activar los segmentos, como se muestra en la imagen siguiente.

   ![Activar botones](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

1. Cambie a la siguiente sección para [seleccionar sus segmentos](#select-segments).

## Seleccione los segmentos {#select-segments}

Utilice las casillas de verificación a la izquierda de los nombres de los segmentos para seleccionar los segmentos que desea activar en el destino y, a continuación, seleccione **[!UICONTROL Siguiente]**.

![Seleccionar segmentos](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Seleccionar atributos de perfil {#select-attributes}

Seleccione los atributos de perfil que desea enviar al destino de destino.

>[!NOTE]
>
> Adobe Experience Platform prefiere la selección con cuatro atributos recomendados y utilizados comúnmente del esquema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Las exportaciones de archivos variarán de las siguientes maneras, en función de si se selecciona `segmentMembership.status`:
* Si se selecciona el campo `segmentMembership.status`, los archivos exportados incluyen **[!UICONTROL miembros activos]** en la instantánea completa inicial y miembros **[!UICONTROL activos]** y **[!UICONTROL caducados]** en las exportaciones incrementales posteriores.
* Si el campo `segmentMembership.status` no está seleccionado, los archivos exportados incluyen solo miembros **[!UICONTROL activos]** en la instantánea completa inicial y en las exportaciones incrementales posteriores.

![atributos recomendados](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. En la página **[!UICONTROL Select attributes]**, seleccione **[!UICONTROL Add new field]**.

   ![Añadir nueva asignación](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Seleccione la flecha a la derecha de la entrada **[!UICONTROL Schema field]**.

   ![Seleccionar campo de origen](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. En la página **[!UICONTROL Select field]**, seleccione los atributos XDM que desea enviar al destino y, a continuación, elija **[!UICONTROL Select]**.

   ![Seleccionar página de campo de origen](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Para agregar más asignaciones, repita los pasos del 1 al 3 y, a continuación, seleccione **[!UICONTROL Siguiente]**.

## Consulte {#review}

En la página **[!UICONTROL Revisar]**, puede ver un resumen de su selección. Seleccione **[!UICONTROL Cancelar]** para desglosar el flujo, **[!UICONTROL Atrás]** para modificar la configuración o **[!UICONTROL Finalizar]** para confirmar la selección y empezar a enviar datos al destino.

>[!IMPORTANT]
>
>En este paso, Adobe Experience Platform comprueba las infracciones de la directiva de uso de datos. A continuación se muestra un ejemplo en el que se infringe una política. No puede completar el flujo de trabajo de activación de segmentos hasta que no haya resuelto la infracción. Para obtener información sobre cómo resolver infracciones de políticas, consulte [Aplicación de políticas](../../rtcdp/privacy/data-governance-overview.md#enforcement) en la sección de documentación de control de datos.

![violación de la política de datos](../assets/common/data-policy-violation.png)

Si no se han detectado infracciones de directiva, seleccione **[!UICONTROL Finish]** para confirmar la selección y empezar a enviar datos al destino.

![Consulte](../assets/ui/activate-streaming-profile-destinations/review.png)

## Verificación de la activación de segmentos {#verify}

Los datos [!DNL Experience Platform] exportados llegan al destino de destino en formato JSON. Por ejemplo, el evento siguiente contiene el atributo de perfil de dirección de correo electrónico de una audiencia que se ha clasificado para un segmento determinado y ha salido de otro segmento. Las identidades de este cliente potencial son ECID y correo electrónico.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
