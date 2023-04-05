---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;segmento;segmentación;pertenencia a segmentos;pertenencia a segmentos;diseño de esquema;mapa;mapa;
solution: Experience Platform
title: Detalles de pertenencia a segmentos Grupo de campos de esquema
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de pertenencia a segmentos .
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---


# [!UICONTROL Detalles de pertenencia a segmentos] grupo de campos de esquema

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Consulte el documento en [actualizaciones del nombre del grupo de campos](../name-updates.md) para obtener más información.

[!UICONTROL Detalles de pertenencia a segmentos] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). El grupo de campos proporciona un único campo de mapa que captura información relacionada con la pertenencia a un segmento, incluidos los segmentos a los que pertenece el individuo, la última hora de calificación y el momento en que la pertenencia es válida hasta entonces.

>[!WARNING]
>
>Mientras que la variable `segmentMembership` debe agregarse manualmente al esquema de perfil mediante este grupo de campos, no debe intentar rellenar o actualizar este campo manualmente. El sistema actualiza automáticamente la variable `segmentMembership` para cada perfil a medida que se realizan trabajos de segmentación.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `segmentMembership` | Mapa | Un objeto map que describe las suscripciones a segmentos del individuo. La estructura de este objeto se describe en detalle a continuación. |

{style="table-layout:auto"}

El siguiente es un ejemplo `segmentMembership` mapa que el sistema ha rellenado para un perfil en particular. Las pertenencias a segmentos se ordenan por área de nombres, tal como indican las claves de nivel raíz del objeto. A su vez, las claves individuales de cada área de nombres representan los ID de los segmentos a los que pertenece el perfil. Cada objeto de segmento contiene varios subcampos que proporcionan más detalles sobre la pertenencia:

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
| `xdm:version` | La versión del segmento para el que se calificó este perfil. |
| `xdm:lastQualificationTime` | Marca de fecha y hora de la última vez que este perfil cumplía los requisitos para el segmento. |
| `xdm:validUntil` | Marca de fecha y hora en la que se debe suponer que la pertenencia al segmento ya no es válida. Para audiencias externas, si este campo no está establecido, la pertenencia al segmento solo se conservará durante 30 días desde el `lastQualificationTime`. |
| `xdm:status` | Campo de cadena que indica si la pertenencia al segmento se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`realized`: El perfil se califica para el segmento.</li><li>`exited`: El perfil sale del segmento como parte de la solicitud actual.</li></ul> |
| `xdm:payload` | Algunas suscripciones a segmentos incluyen una carga útil que describe valores adicionales directamente relacionados con la pertenencia. Solo se puede proporcionar una carga útil de un tipo determinado para cada pertenencia. `xdm:payloadType` indica el tipo de carga útil (`boolean`, `number`, `propensity`o `string`), mientras que su propiedad del mismo nivel proporciona el valor para el tipo de carga útil. |

{style="table-layout:auto"}

>[!NOTE]
>
>Cualquier pertenencia a un segmento que se encuentre en la `exited` durante más de 30 días, según la variable `lastQualificationTime`, estará sujeto a eliminación.

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
