---
keywords: Experience Platform;inicio;temas populares;esquema;XDM;esquemas;esquemas;esquema;tipo de datos;tipo de datos;tipo de datos;tipo de datos;tipo de datos;divisa;
solution: Experience Platform
title: Tipo de datos de moneda
description: Este documento proporciona información general sobre el tipo de datos XDM de moneda.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 3%

---

# [!UICONTROL Moneda] tipo de datos

[!UICONTROL Moneda] es un tipo de datos XDM estándar que describe una cantidad de moneda, incluido el tipo de moneda y la fecha de conversión.

![](../images/data-types/currency.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `amount` | Doble | La cantidad de moneda definida por la variable `currencyCode`. |
| `conversionDate` | DateTime | Una marca de tiempo de cuándo se realizó la conversión de moneda. |
| `currencyCode` | Cadena | Un código ISO 4217 que indica el tipo de moneda que `amount` representa. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
