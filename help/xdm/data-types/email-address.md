---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;emailAddress;xdm:emailAddress;correo electrónico;dirección de correo electrónico;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de dirección de correo electrónico
description: Obtenga información sobre el tipo de datos XDM de dirección de correo electrónico.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# [!UICONTROL Correo electrónico] tipo de datos

[!UICONTROL Correo electrónico] es un tipo de datos XDM (Experience Data Model) estándar que describe los detalles de una dirección de correo electrónico.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Propiedad | Descripción |
| --- | --- |
| `address` | La dirección técnica del correo electrónico tal como se define comúnmente en RFC2822 y estándares subsiguientes (por ejemplo, `name@domain.com`).<br><br>En XDM, las direcciones de correo electrónico deben contener un dominio de nivel superior válido para pasar la validación. Consulte lo siguiente [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) para obtener una lista completa de los dominios de nivel superior válidos según lo definido por la Autoridad de números asignados de Internet (IANA, Internet Assigned Numbers Authority ). |
| `label` | Información adicional para mostrar que puede estar disponible. Por ejemplo, si un correo electrónico tiene una dirección enriquecida de Microsoft Outlook, se muestra `John Smith smithjr@company.uk`, `John Smith` se colocará en este campo. |
| `primary` | Indica si esta es la dirección de correo electrónico principal de la persona. Un perfil solo puede tener uno `primary` dirección de correo electrónico en un momento determinado. |
| `status` | Indica si la dirección de correo electrónico se puede utilizar actualmente |
| `statusReason` | Una descripción del actual `status`. |
| `type` | La forma en que la cuenta está relacionada con la persona (por ejemplo, `work` o `personal`). |

{style="table-layout:auto"}


Para obtener más información sobre el tipo de datos de la dirección de correo electrónico, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
