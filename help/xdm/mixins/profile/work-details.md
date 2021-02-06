---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;diseño de Esquema;mezcla;mezclas;detalles de trabajo;trabajo de perfil;
solution: Experience Platform
title: Mezcla de detalles de contacto de trabajo
topic: overview
description: Este documento proporciona una visión general de la combinación de detalles de contacto del trabajo.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 2%

---


# [!UICONTROL Work Contact ] Detailsmixin

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento en [actualizaciones de nombres de mezcla](../name-updates.md) para obtener más información.

[!UICONTROL Work Contact ] Detailsis es una mezcla estándar para la  [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md). La combinación proporciona varios campos que capturan información ocupacional relacionada con una persona individual, como dirección de trabajo, correo electrónico laboral, número de teléfono del trabajo y organizaciones a las que pertenece la persona.

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