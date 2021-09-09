---
keywords: Experience Platform;inicio;temas populares;esquema;esquema;XDM;campos;esquemas;esquemas;dispositivo;tipo de datos;tipo de datos;tipo de datos;moneda;
solution: Experience Platform
title: Tipo de datos de moneda
topic-legacy: overview
description: Este documento proporciona información general sobre el tipo de datos XDM de moneda.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 5%

---

#  Tipo de datos de moneda

 Moneda es un tipo de datos XDM estándar que describe una cantidad de moneda, incluido el tipo de moneda y la fecha de conversión.

![](../images/data-types/currency.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `amount` | Duplicada | Cantidad de moneda definida por `currencyCode`. |
| `conversionDate` | DateTime | Marca de fecha y hora en la que se realizó la conversión de moneda. |
| `currencyCode` | Cadena | Código ISO 4217 que indica el tipo de moneda que representa `amount`. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
