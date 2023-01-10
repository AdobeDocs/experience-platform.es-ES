---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;diseño de esquema;grupo de campos;grupo de campos;iab;tcf;consentimiento;
solution: Experience Platform
title: Grupo de campos de consentimiento TCF 2.0 de IAB para esquemas de perfil
description: Este documento proporciona una descripción general del grupo de campos de esquema de consentimiento TCF 2.0 de IAB para la clase de perfil individual XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 1%

---

# [!UICONTROL Consentimiento TCF 2.0 de IAB] grupo de campos para esquemas de perfil

>[!NOTE]
>
>Este documento cubre el [!UICONTROL Consentimiento TCF 2.0 de IAB] grupo de campos de esquema para la clase XDM Individual Profile. Para el grupo de campos destinado a la clase XDM ExperienceEvent , consulte lo siguiente [documento](../event/iab.md) en su lugar.

[!UICONTROL Consentimiento TCF 2.0 de IAB] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) se utiliza para capturar una serie con marca de hora de cadenas de consentimiento IAB, con el fin de rastrear patrones de cambio de consentimiento a lo largo del tiempo.

![](../../images/field-groups/iab-profile.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `identityPrivacyInfo` | Mapa | Un objeto de tipo map que asocia los valores de identidad individuales de un cliente con diferentes cadenas de consentimiento TCF. A continuación se proporciona un ejemplo de la estructura de este objeto. |

{style=&quot;table-layout:auto&quot;}

El siguiente JSON muestra la estructura del `identityPrivacyInfo` mapa.

```json
{
  "identityPrivacyInfo": {
    "ECID": {
      "13782522493631189": {
        "identityIABConsent": {
          "consentTimestamp": "2020-04-11T05:05:05Z",
          "consentString": {
            "consentStandard": "IAB TCF",
            "consentStandardVersion": "2.0",
            "consentStringValue": "BObdrPUOevsguAfDqFENCNAAAAAmeAAA.PVAfDObdrA.DqFENCAmeAENCDA",
            "gdprApplies": true,
            "containsPersonalData": false
          }
        }
      }
    }
  }
}
```

Como se muestra en el ejemplo, cada clave de nivel raíz de `xdm:identityPrivacyInfo` corresponde a un área de nombres de identidad reconocida por Identity Service. A su vez, cada propiedad de área de nombres debe tener al menos una subpropiedad cuya clave coincida con el valor de identidad correspondiente del cliente para ese área de nombres. En este ejemplo, el cliente se identifica con un ID de Experience Cloud (`ECID`) valor de `13782522493631189`.

>[!NOTE]
>
>Aunque el ejemplo anterior utiliza un único espacio de nombres/par de valores para representar la identidad del cliente, puede agregar claves adicionales para otros espacios de nombres y cada área de nombres puede tener varios valores de identidad, cada uno con su propio conjunto de preferencias de consentimiento TCF.

Para cada valor de identidad, una `identityIABConsent` debe proporcionarse la propiedad , que proporciona el valor de consentimiento TCF para la identidad. El valor de esta propiedad debe cumplir la función [[!UICONTROL Cadena de consentimiento] tipo de datos](../../data-types/consent-string.md).

Consulte la guía de [Compatibilidad con IAB TCF 2.0 en Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información sobre el caso de uso de este grupo de campos. Para obtener más información sobre el propio grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
