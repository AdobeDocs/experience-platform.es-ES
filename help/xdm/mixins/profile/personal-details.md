---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: Mezcla de datos de contacto personal
topic: overview
description: Este documento proporciona una visión general de la combinación de Detalles de contacto personales.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---


# [!UICONTROL Mezcla de detalles] de contacto personal

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre las actualizaciones [de nombres de](../name-updates.md) mezcla para obtener más información.

[!UICONTROL Datos] de contacto personales es una combinación estándar para la [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que describe la información de contacto de una persona.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `faxPhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de fax de la persona. |
| `homeAddress` | [Dirección postal](../../data-types/postal-address.md) | Describe la dirección residencial de la persona. |
| `homePhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono del domicilio de la persona. |
| `mobilePhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono móvil de la persona. |
| `personalEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | Describe la dirección de correo electrónico de la persona. |

Para obtener más información sobre la mezcla, consulte el repositorio público XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
