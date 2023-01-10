---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dirección de correo electrónico;xdm:dirección de correo electrónico;correo electrónico;dirección de correo electrónico;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección de correo electrónico
description: Este documento proporciona información general sobre el tipo de datos XDM de la dirección de correo electrónico.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL Dirección de correo electrónico] tipo de datos

[!UICONTROL Dirección de correo electrónico] es un tipo de datos estándar del Modelo de datos de experiencia (XDM) que describe los detalles de una dirección de correo electrónico.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propiedad | Descripción |
| --- | --- |
| `address` | La dirección técnica del correo electrónico tal como se define comúnmente en RFC2822 y las normas posteriores (por ejemplo, `name@domain.com`).<br><br>En XDM, las direcciones de correo electrónico deben contener un dominio de nivel superior válido para pasar la validación. Consulte lo siguiente [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) para obtener una lista completa de los dominios de nivel superior válidos definidos por la Autoridad de números asignados de Internet (IANA). |
| `label` | Información de visualización adicional que puede estar disponible. Por ejemplo, si un correo electrónico tiene una dirección enriquecida de Microsoft Outlook, se muestra la `John Smith smithjr@company.uk`, `John Smith` se colocarían en este campo. |
| `primary` | Indica si esta es la dirección de correo electrónico principal del individuo. Un perfil solo puede tener uno `primary` dirección de correo electrónico en un momento determinado. |
| `status` | Indica si la dirección de correo electrónico se puede utilizar actualmente |
| `statusReason` | Una descripción de la `status`. |
| `type` | La forma en que la cuenta se relaciona con la persona (por ejemplo, `work` o `personal`). |

{style=&quot;table-layout:auto&quot;}


Para obtener más información sobre el tipo de datos de dirección de correo electrónico, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
