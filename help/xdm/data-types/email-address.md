---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;emailAddress;xdm:emailAddress;correo electrónico;dirección de correo electrónico;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección de correo electrónico
description: Obtenga información sobre el tipo de datos XDM de dirección de correo electrónico.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# [!UICONTROL Tipo de datos de la dirección de correo electrónico]

[!UICONTROL La dirección de correo electrónico] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de una dirección de correo electrónico.

![](../images/data-types/email-address.png){width=450}

| Propiedad | Descripción |
| --- | --- |
| `address` | La dirección técnica del correo electrónico como se define comúnmente en RFC2822 y estándares subsiguientes (por ejemplo, `name@domain.com`).<br><br>En XDM, las direcciones de correo electrónico deben contener un dominio de nivel superior válido para pasar la validación. Consulte el siguiente [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) para obtener una lista completa de los dominios de nivel superior válidos según lo definido por la Autoridad de números asignados de Internet (IANA, Internet Assigned Numbers Authority ). |
| `label` | Información adicional para mostrar que puede estar disponible. Por ejemplo, si un correo electrónico tiene una visualización de dirección enriquecida de Microsoft Outlook de `John Smith smithjr@company.uk`, `John Smith` se colocaría en este campo. |
| `primary` | Indica si esta es la dirección de correo electrónico principal de la persona. Un perfil solo puede tener una dirección de correo electrónico `primary` en un momento determinado. |
| `status` | Indica si la dirección de correo electrónico se puede utilizar actualmente |
| `statusReason` | Una descripción de `status` actual. |
| `type` | La forma en que la cuenta se relaciona con la persona (como `work` o `personal`). |

{style="table-layout:auto"}


Para obtener más información sobre el tipo de datos de la dirección de correo electrónico, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
