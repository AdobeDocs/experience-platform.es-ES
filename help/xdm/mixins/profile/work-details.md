---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;perfil individual;campos;esquemas;esquemas;diseño de esquema;mezcla;mezclas;detalles de trabajo;trabajo de perfil;
solution: Experience Platform
title: Mezcla de detalles de contacto de trabajo
topic-legacy: overview
description: Este documento proporciona una descripción general de la mezcla Detalles de contacto de trabajo .
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# [!UICONTROL Work Contact Details] mixto

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento sobre [mezcin name updates](../name-updates.md) para obtener más información.

[!UICONTROL Work Contact Details] es una mezcla estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La mezcla proporciona varios campos que capturan información ocupacional relacionada con una persona individual, como la dirección de trabajo, el correo electrónico de trabajo, el número de teléfono del trabajo y las organizaciones a las que pertenece la persona.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `workAddress` | [Dirección postal](../../data-types/postal-address.md) | Describe la dirección de trabajo de la persona. |
| `workEmail` | [Dirección de correo electrónico](../../data-types/email-address.md) | Describe la dirección de correo electrónico de trabajo de la persona. |
| `workPhone` | [Número de teléfono](../../data-types/phone-number.md) | Describe el número de teléfono del trabajo de la persona. |
| `organizations` | Cadena (Matriz) | Matriz de cadenas de forma libre que representan las organizaciones de las que es miembro la persona. |

Para obtener más información sobre la mezcla, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
