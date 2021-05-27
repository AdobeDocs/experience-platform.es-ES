---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;detalles personales;diseño de esquema;grupo de campos;grupo de campos;
solution: Experience Platform
title: Grupo de campos de esquema de detalles de contacto personal
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de contacto personales .
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 6%

---


# [!UICONTROL Grupo de campos ] Detalle de contacto personal

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL Personal Contact ] Detailes un grupo de campos de esquema estándar para la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) clase que describe la información de contacto de una persona individual.

![](../../images/field-groups/personal-contact-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `faxPhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de fax de la persona. |
| `homeAddress` | [Dirección postal](../../data-types/postal-address.md) | Describe la dirección residencial de la persona. |
| `homePhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono de casa de la persona. |
| `mobilePhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono móvil de la persona. |
| `personalEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | Describe la dirección de correo electrónico de la persona. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
