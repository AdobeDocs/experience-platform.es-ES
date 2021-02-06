---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones varias;misc;
solution: Experience Platform
title: Funciones varias de PQL
topic: developer guide
description: La siguiente función es una función diversa para el lenguaje de Consulta de Perfil (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Funciones diversas

La siguiente función es una función diversa para [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Let

La función `let` permite almacenar una expresión como una variable para usarla posteriormente en una consulta.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Ejemplo**

La siguiente consulta de PQL obtiene todas las sumas de los totales de productos con la transacción en USD cuando la suma es buena de más de $100 y menos de $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Pasos siguientes

Ahora que ha aprendido sobre diversas funciones, puede usarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
