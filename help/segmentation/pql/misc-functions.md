---
solution: Experience Platform
title: Funciones diversas de PQL
description: La siguiente función es una función variada para Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 3%

---

# Funciones varias

La siguiente función es una función miscelánea para [!DNL Profile Query Language] (PQL). Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Let

La función `let` permite almacenar una expresión como variable para usarla posteriormente en una consulta.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Ejemplo**

La siguiente consulta de PQL obtiene todas las sumas de totales de productos con la transacción en USD donde la suma es mayor que 100 dólares y menor que 1000 dólares.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Pasos siguientes

Ahora que ha aprendido acerca de diversas funciones, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
