---
keywords: Experience Platform;inicio;temas populares;esquema;Esquema;XDM;campos;esquemas;Esquemas;númeroTeléfono;xdm:númeroTeléfono;tipoDeDatos;tipoDeDatos;tipoDeDatos;
solution: Experience Platform
title: Tipo de datos de número telefónico
description: Este documento proporciona información general sobre el tipo de datos XDM de Número de teléfono.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# [!UICONTROL Número de teléfono] tipo de datos

[!UICONTROL Número de teléfono] es un tipo de datos XDM estándar que describe los detalles de un número de teléfono.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propiedad | Descripción |
| --- | --- |
| `extension` | Número de marcado interno que se utiliza para llamar desde un intercambio privado, un operador o un panel de control. |
| `number` | El número de teléfono. Tenga en cuenta que el número de teléfono es una cadena y puede incluir caracteres significativos, como corchetes `()`, guiones `-`o caracteres para indicar identificadores de submarcado como extensiones `x` por ejemplo, `1-353(0)18391111` o `+613 9403600x1234`. |
| `primary` | Un valor booleano que indica si este es el número de teléfono principal del individuo. A diferencia de la dirección o la dirección de correo electrónico, puede haber varios números de teléfono principales; uno por canal de comunicación. El canal de comunicación se define por el tipo (indicado por el nombre de la propiedad principal): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`y `fax`. |
| `status` | Indica si el número de teléfono se puede usar actualmente. |
| `statusReason` | Descripción del estado actual. |
| `validity` | Un nivel de corrección técnica del número de teléfono. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el tipo de datos de número de teléfono, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
