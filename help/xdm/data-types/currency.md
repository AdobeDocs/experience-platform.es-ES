---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquema;tipo de datos;tipo de datos;tipo de datos;tipo de datos;tipo de datos;divisa;
solution: Experience Platform
title: Tipo de datos de moneda
description: Obtenga información sobre el tipo de datos XDM de moneda.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 6%

---

# [!UICONTROL Tipo de datos Moneda]

[!UICONTROL Divisa] es un tipo de datos XDM estándar que describe una cantidad de moneda, incluido el tipo de moneda y la fecha de conversión.

![](../images/data-types/currency.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `amount` | Duplicada | La cantidad de moneda definida por `currencyCode`. |
| `conversionDate` | Fecha/Hora | Una marca de tiempo de cuándo se realizó la conversión de moneda. |
| `currencyCode` | Cadena | Un código ISO 4217 que indica el tipo de moneda que representa `amount`. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
