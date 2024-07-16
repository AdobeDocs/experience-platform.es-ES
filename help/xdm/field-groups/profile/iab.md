---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;Diseño de esquema;grupo de campos;grupo de campos;iab;tcf;consentimiento;
solution: Experience Platform
title: Grupo de campos de consentimiento de IAB TCF 2.0 para esquemas de perfil
description: Obtenga información acerca del grupo de campos Esquema de consentimiento TCF 2.0 de IAB para la clase Perfil individual de XDM.
exl-id: 52a4fee8-d7f4-4f27-8e26-0c132985eb84
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# [!UICONTROL Grupo de campos de consentimiento TCF de IAB 2.0] para esquemas de perfil

>[!NOTE]
>
>Este documento cubre el grupo de campos de esquema [!UICONTROL Consentimiento TCF 2.0 de IAB] para la clase de perfil individual de XDM. Para el grupo de campos destinado a la clase XDM ExperienceEvent, consulte el siguiente [documento](../event/iab.md) en su lugar.

El consentimiento [!UICONTROL IAB TCF 2.0] es un grupo de campos de esquema estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que se usa para capturar una serie con marca de tiempo de cadenas de consentimiento IAB, con el fin de rastrear patrones de cambio de consentimiento a lo largo del tiempo.

![](../../images/field-groups/iab-profile.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `identityPrivacyInfo` | Mapa | Objeto de tipo map que asocia los valores de identidad individuales de un cliente con diferentes cadenas de consentimiento TCF. A continuación se proporciona un ejemplo de la estructura de este objeto. |

{style="table-layout:auto"}

El siguiente JSON muestra la estructura del mapa `identityPrivacyInfo`.

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

Como se muestra en el ejemplo, cada clave de nivel raíz de `xdm:identityPrivacyInfo` corresponde a un área de nombres de identidad reconocida por el servicio de identidad. A su vez, cada propiedad de área de nombres debe tener al menos una subpropiedad cuya clave coincida con el valor de identidad correspondiente del cliente para ese área de nombres. En este ejemplo, el cliente se identifica con un valor de ID de Experience Cloud (`ECID`) de `13782522493631189`.

>[!NOTE]
>
>Aunque el ejemplo anterior utiliza un único par espacio de nombres/valor para representar la identidad del cliente, puede agregar claves adicionales para otras áreas de nombres y cada área de nombres puede tener varios valores de identidad, cada uno con su propio conjunto de preferencias de consentimiento TCF.

Para cada valor de identidad, se debe proporcionar una propiedad `identityIABConsent`, que proporciona el valor de consentimiento TCF para la identidad. El valor de esta propiedad debe ajustarse al tipo de datos [[!UICONTROL Cadena de consentimiento]](../../data-types/consent-string.md).

Consulte la guía sobre la compatibilidad con [IAB TCF 2.0 en Platform](../../../landing/governance-privacy-security/consent/iab/overview.md) para obtener más información sobre el caso de uso de este grupo de campos. Para obtener más información sobre el propio grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-privacy.schema.json)
