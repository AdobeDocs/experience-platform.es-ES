---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;segment;segmentMembership;segment membership;Schema design;map;Map;
solution: Experience Platform
title: Mezcla de segmentación por perfil
topic: overview
description: Este documento proporciona información general sobre la clase de Perfil individual XDM.
translation-type: tm+mt
source-git-commit: 53575488c08f73a65a7f1cc5f803f9ead707ae48
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---


# [!UICONTROL Mezcla de segmentación] de perfil

[!UICONTROL La segmentación] de perfil es una mezcla estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La combinación proporciona un campo de mapa único que captura información relativa a la pertenencia a segmentos, incluidos los segmentos a los que pertenece el individuo, el último tiempo de calificación y el momento en que la pertenencia es válida hasta entonces.

>[!WARNING]
>
>Aunque el `segmentMembership` campo debe agregarse manualmente al esquema de perfil mediante esta combinación, no debe intentar rellenar o actualizar manualmente este campo. El sistema actualiza automáticamente la asignación de cada `segmentMembership` perfil a medida que se realizan trabajos de segmentación.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `segmentMembership` | Mapa | Un objeto map que describe las pertenencias a segmentos del individuo. La estructura de este objeto se describe en detalle a continuación. |

El siguiente es un mapa de ejemplo `segmentMembership` que el sistema ha rellenado para un perfil en particular. Las pertenencias a los segmentos se ordenan por Área de nombres, como indican las claves de nivel raíz del objeto. A su vez, las claves individuales de cada Área de nombres representan los ID de los segmentos de los que es miembro el perfil. Cada objeto de segmento contiene varios subcampos que proporcionan más detalles sobre la pertenencia:

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
| `xdm:version` | Versión del segmento para el que este perfil cumple los requisitos. |
| `xdm:lastQualificationTime` | Marca de hora de la última vez que este perfil se calificó para el segmento. |
| `xdm:validUntil` | Marca de hora del momento en el que se debe dejar de suponer que la pertenencia al segmento es válida. |
| `xdm:status` | Indica si la pertenencia al segmento se ha realizado como parte de la solicitud actual. Se aceptan los siguientes valores: <ul><li>`existing`:: El perfil ya formaba parte de la serie de sesiones antes de la solicitud y sigue siendo miembro.</li><li>`realized`:: El perfil está ingresando el segmento como parte de la solicitud actual.</li><li>`exited`:: El perfil está saliendo del segmento como parte de la solicitud actual.</li></ul> |
| `xdm:payload` | Algunas pertenencias a segmentos incluyen una carga útil que describe valores adicionales directamente relacionados con la pertenencia. Sólo se puede proporcionar una carga útil de un tipo determinado para cada abono. `xdm:payloadType` indica el tipo de carga útil (`boolean`, `number`, `propensity`o `string`), mientras que su propiedad secundaria proporciona el valor para el tipo de carga útil. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
