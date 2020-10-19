---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Tipo de datos de número telefónico
topic: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de Número de teléfono.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---


# [!UICONTROL Tipo de datos de número] de teléfono

[!UICONTROL El número] de teléfono es un tipo de datos XDM estándar que describe los detalles de un número de teléfono.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Propiedad | Descripción |
| --- | --- |
| `extension` | El número de marcado interno que se utiliza para llamar desde un intercambio privado, operador o centralita. |
| `number` | El número de teléfono. Tenga en cuenta que el número de teléfono es una cadena y puede incluir caracteres significativos como corchetes `()`, guiones `-`o caracteres para indicar identificadores de submarcado como extensiones `x` por ejemplo `1-353(0)18391111` o `+613 9403600x1234`. |
| `primary` | Un valor booleano que indica si este es el número de teléfono principal del individuo. A diferencia de la dirección o la dirección de correo electrónico, puede haber varios números de teléfono principales; uno por canal de comunicación. El canal de comunicación está definido por el tipo (indicado por el nombre de la propiedad principal): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`y `fax`. |
| `status` | Indica si el número de teléfono se puede usar actualmente. |
| `statusReason` | Descripción del estado actual. |
| `validity` | Nivel de exactitud técnica del número de teléfono. |

Para obtener más información sobre el tipo de datos de número de teléfono, consulte el repositorio público de XDM:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)