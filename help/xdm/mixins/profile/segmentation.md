---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;segmento;segmentación;pertenencia a segmentos;pertenencia a segmentos;diseño de esquema;mapa;mapa;
solution: Experience Platform
title: Mezcla de detalles de pertenencia a segmentos
topic-legacy: overview
description: Este documento proporciona una descripción general de la mezcla de Detalles de pertenencia a segmentos .
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# [!UICONTROL Segment Membership Details] mixto

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../name-updates.md) para obtener más información.

[!UICONTROL Segment Membership Details] es una mezcla estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La mezcla proporciona un campo de mapa único que captura información relacionada con la pertenencia al segmento, incluidos los segmentos a los que pertenece el individuo, la última hora de calificación y cuándo la pertenencia es válida hasta entonces.

>[!WARNING]
>
>Aunque el campo `segmentMembership` debe agregarse manualmente al esquema de perfil mediante esta mezcla, no debe intentar rellenar o actualizar este campo manualmente. El sistema actualiza automáticamente el mapa de `segmentMembership` para cada perfil a medida que se realizan trabajos de segmentación.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `segmentMembership` | Mapa | Un objeto map que describe las suscripciones a segmentos del individuo. La estructura de este objeto se describe en detalle a continuación. |

El siguiente es un ejemplo de asignación `segmentMembership` que el sistema ha rellenado para un perfil en particular. Las pertenencias a segmentos se ordenan por área de nombres, tal como indican las claves de nivel raíz del objeto. A su vez, las claves individuales de cada área de nombres representan los ID de los segmentos a los que pertenece el perfil. Cada objeto de segmento contiene varios subcampos que proporcionan más detalles sobre la pertenencia:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
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
| `xdm:validUntil` | Marca de fecha y hora en la que se debe suponer que la pertenencia al segmento ya no es válida. |
| `xdm:status` | Indica si la pertenencia al segmento se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`existing`: El perfil ya formaba parte del segmento antes de la solicitud y continúa manteniendo su pertenencia.</li><li>`realized`: El perfil está introduciendo el segmento como parte de la solicitud actual.</li><li>`exited`: El perfil sale del segmento como parte de la solicitud actual.</li></ul> |
| `xdm:payload` | Algunas suscripciones a segmentos incluyen una carga útil que describe valores adicionales directamente relacionados con la pertenencia. Solo se puede proporcionar una carga útil de un tipo determinado para cada pertenencia. `xdm:payloadType` indica el tipo de carga útil (`boolean`,  `number`,  `propensity` o  `string`), mientras que su propiedad del mismo nivel proporciona el valor para el tipo de carga útil. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
