---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;phoneNumber;xdm:phoneNumber;tipo de datos;tipo de datos;tipo de datos;
solution: Experience Platform
title: Tipo de datos de número de teléfono
description: Obtenga información sobre el tipo de datos XDM Número de teléfono.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 16%

---

# [!UICONTROL Tipo de datos Número de teléfono]

[!UICONTROL Número de teléfono] es un tipo de datos XDM estándar que describe los detalles de un número de teléfono.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propiedad | Descripción |
| --- | --- |
| `extension` | El número de marcado interno que se utiliza para llamar desde una centralita privada o un operador. |
| `number` | El número de teléfono. Tenga en cuenta que el número de teléfono es una cadena y puede incluir caracteres clave como paréntesis `()`, guiones `-` o caracteres para indicar identificadores de marcado secundario como extensiones `x`, por ejemplo, `1-353(0)18391111` o `+613 9403600x1234`. |
| `primary` | Valor booleano que indica si se trata del número de teléfono principal de la persona. A diferencia de la dirección postal o de correo electrónico, puede haber varios números de teléfono principales, uno por canal de comunicación. El canal de comunicación está definido por el tipo (indicado por el nombre de la propiedad principal): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` y `fax`. |
| `status` | Indica si el número de teléfono se puede utilizar actualmente. |
| `statusReason` | Una descripción del estado actual. |
| `validity` | Un nivel de corrección técnica del número de teléfono. |

{style="table-layout:auto"}

Para obtener más información sobre el tipo de datos Número de teléfono, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
