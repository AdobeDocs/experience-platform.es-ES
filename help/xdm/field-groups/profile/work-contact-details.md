---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;diseño de esquema;mezcla;mezclas;detalles de trabajo;trabajo de perfil;
solution: Experience Platform
title: Grupo de campos de esquema Detalles de contacto de trabajo
topic-legacy: overview
description: Este documento proporciona una descripción general del grupo de campos de esquema Detalles de contacto de trabajo .
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 3%

---


# [!UICONTROL Grupo de campos de esquema ] Detalles de contacto de trabajo

>[!NOTE]
>
>Los nombres de varios grupos de campos de esquema han cambiado. Para obtener más información, consulte el documento [field group name updates](../name-updates.md) .

[!UICONTROL Detalles de contacto ] de trabajo es un grupo de campos de esquema estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). El grupo de campos proporciona varios campos que capturan información ocupacional relacionada con una persona individual, como la dirección del trabajo, el correo electrónico del trabajo, el número de teléfono del trabajo y las organizaciones a las que pertenece la persona.

![](../../images/field-groups/work-contact-details.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `workAddress` | [Dirección postal](../../data-types/postal-address.md) | Describe la dirección de trabajo de la persona. |
| `workEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | Describe la dirección de correo electrónico de trabajo de la persona. |
| `workPhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono del trabajo de la persona. |
| `organizations` | Cadena (Matriz) | Matriz de cadenas de forma libre que representan las organizaciones de las que es miembro la persona. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-work-details.schema.json)
