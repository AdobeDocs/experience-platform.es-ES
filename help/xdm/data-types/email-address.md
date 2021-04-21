---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dirección de correo electrónico;xdm:dirección de correo electrónico;correo electrónico;dirección de correo electrónico;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección de correo electrónico
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de la dirección de correo electrónico.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---

# [!UICONTROL Email address] tipo de datos

[!UICONTROL Email address] es un tipo de datos XDM estándar que describe los detalles de una dirección de correo electrónico.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propiedad | Descripción |
| --- | --- |
| `address` | La dirección técnica del correo electrónico tal como se define comúnmente en RFC2822 y los estándares posteriores (por ejemplo, `name@domain.com`). |
| `label` | Información de visualización adicional que puede estar disponible. Por ejemplo, si un correo electrónico tiene una visualización de dirección enriquecida de Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` se colocará en este campo. |
| `primary` | Indica si esta es la dirección de correo electrónico principal del individuo. Un perfil solo puede tener una dirección de correo electrónico `primary` en un momento determinado. |
| `status` | Indica si la dirección de correo electrónico se puede utilizar actualmente |
| `statusReason` | Una descripción del `status` actual. |
| `type` | La forma en que la cuenta se relaciona con la persona (como `work` o `personal`). |


Para obtener más información sobre el tipo de datos de dirección de correo electrónico, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
