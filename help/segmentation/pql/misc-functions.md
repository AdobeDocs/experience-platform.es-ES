---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones diversas
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 3%

---


# Funciones diversas

La siguiente función es una función diversa para [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Let

La `let` función permite almacenar una expresión como una variable para utilizarla posteriormente en una consulta.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Ejemplo**

La siguiente consulta de PQL obtiene todas las sumas de los totales de productos con la transacción en USD cuando la suma es buena de más de $100 y menos de $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Pasos siguientes

Ahora que ha aprendido sobre diversas funciones, puede usarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
