---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Mezcla de detalles de contacto del trabajo
topic: overview
description: Este documento proporciona una visión general de la combinación de detalles de contacto del trabajo.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 2%

---


# [!UICONTROL Mezcla de detalles] de contacto del trabajo

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre las actualizaciones [de nombres de](../name-updates.md) mezcla para obtener más información.

[!UICONTROL Detalles] de contacto de trabajo es una combinación estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La combinación proporciona varios campos que capturan información ocupacional relacionada con una persona individual, como dirección de trabajo, correo electrónico laboral, número de teléfono del trabajo y organizaciones a las que pertenece la persona.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `workAddress` | [Dirección postal](../../data-types/postal-address.md) | Describe la dirección de trabajo de la persona. |
| `workEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | Describe la dirección de correo electrónico del trabajo de la persona. |
| `workPhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono del trabajo de la persona. |
| `organizations` | Cadena (matriz) | Matriz de cadenas de formato libre que representan las organizaciones de las que es miembro la persona. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)