---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;detalles personales;diseño de esquema;mezcla;Mixin;
solution: Experience Platform
title: Mezcla de detalles de contacto personal
topic-legacy: overview
description: Este documento proporciona una visión general de la mezcla de detalles de contacto personales.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 5%

---

# [!UICONTROL Personal Contact Details] mixto

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../name-updates.md) para obtener más información.

[!UICONTROL Personal Contact Details] es una mezcla estándar para la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) clase que describe la información de contacto para una persona individual.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `faxPhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de fax de la persona. |
| `homeAddress` | [Dirección postal](../../data-types/postal-address.md) | Describe la dirección residencial de la persona. |
| `homePhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono de casa de la persona. |
| `mobilePhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono móvil de la persona. |
| `personalEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | Describe la dirección de correo electrónico de la persona. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
