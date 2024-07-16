---
solution: Experience Platform
title: Grupo de campos de esquema de detalles de pertenencia a segmento
description: Obtenga información acerca del grupo de campos de esquema Detalles de pertenencia a segmentos.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---


# [!UICONTROL Detalles de pertenencia a segmento] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento sobre [actualizaciones de nombre de grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de pertenencia a segmento] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). El grupo de campos proporciona un único campo de asignación que captura información sobre la pertenencia a segmentos, incluidos los segmentos a los que pertenece el individuo, la última hora de calificación y hasta cuándo es válida la pertenencia.

>[!WARNING]
>
>Aunque el campo `segmentMembership` debe agregarse manualmente al esquema de perfil mediante este grupo de campos, no debe intentar rellenar ni actualizar este campo manualmente. El sistema actualiza automáticamente la asignación `segmentMembership` para cada perfil a medida que se realizan los trabajos de segmentación.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `segmentMembership` | Mapa | Un objeto map que describe las pertenencias de segmentos del individuo. La estructura de este objeto se describe en detalle a continuación. |

{style="table-layout:auto"}

El siguiente es un ejemplo de asignación `segmentMembership` que el sistema ha rellenado para un perfil en particular. Las suscripciones a segmentos se ordenan por área de nombres, tal como indican las claves de nivel de raíz del objeto. A su vez, las claves individuales debajo de cada área de nombres representan los ID de los segmentos a los que pertenece el perfil. Cada objeto de segmento contiene varios subcampos que proporcionan más detalles sobre la pertenencia:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Propiedad | Descripción |
| --- | --- |
| `xdm:version` | La versión del segmento para el que se califica este perfil. |
| `xdm:lastQualificationTime` | Una marca de tiempo de la última vez que este perfil se clasificó para el segmento. |
| `xdm:validUntil` | Una marca de tiempo de cuando ya no se debe suponer que el abono del segmento es válido. Para audiencias externas, si no se establece este campo, la pertenencia al segmento solo se conservará durante 30 días a partir de `lastQualificationTime`. |
| `xdm:status` | Campo de cadena que indica si se ha realizado la inscripción a segmento como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`realized`: el perfil se califica para el segmento.</li><li>`exited`: el perfil está saliendo del segmento como parte de la solicitud actual.</li></ul> |
| `xdm:payload` | Algunas suscripciones a segmentos incluyen una carga útil que describe valores adicionales relacionados directamente con la pertenencia. Solo se puede proporcionar una carga útil de un tipo determinado para cada abono. `xdm:payloadType` indica el tipo de carga útil (`boolean`, `number`, `propensity` o `string`), mientras que su propiedad del mismo nivel proporciona el valor para el tipo de carga útil. |

{style="table-layout:auto"}

>[!NOTE]
>
>Cualquier pertenencia a segmento que esté en estado `exited` durante más de 30 días, según el `lastQualificationTime`, estará sujeta a eliminación.

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
