---
keywords: Experience Platform;inicio;temas populares;segmentación;segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones varias;misc;
solution: Experience Platform
title: Funciones diversas de PQL
topic-legacy: developer guide
description: La siguiente función es una función variada para el lenguaje de consulta de perfil (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Funciones diversas

La siguiente función es una función variada para [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Let

La función `let` permite almacenar una expresión como variable para usarla más adelante en una consulta.

**Format**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Ejemplo**

La siguiente consulta PQL obtiene todas las sumas de totales de productos con la transacción en USD donde la suma es buena a 100 $ y menor a 1000 $.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Pasos siguientes

Ahora que ha aprendido sobre funciones diversas, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
