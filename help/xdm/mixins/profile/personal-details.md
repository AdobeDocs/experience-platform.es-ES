---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;perfil individual;campos;esquemas;Esquemas;detalles personales;diseño de Esquema;mezcla;Mezcla;
solution: Experience Platform
title: Mezcla de detalles de contacto personal
topic: overview
description: Este documento proporciona una visión general de la combinación de Detalles de contacto personales.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 5%

---


# [!UICONTROL Información de contacto personal ] Detailsmixin

>[!NOTE]
>
>Los nombres de varias mezclas han cambiado. Consulte el documento en [actualizaciones de nombres de mezcla](../name-updates.md) para obtener más información.

[!UICONTROL La ] información de contacto personal es una combinación estándar para la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) clase que describe la información de contacto de una persona.

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
