---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de consulta de perfil;diversas funciones;misc;
solution: Experience Platform
title: Funciones diversas de PQL
description: La siguiente función es una función miscelánea para el lenguaje de consulta de perfil (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Funciones varias

La siguiente función es una función miscelánea para [!DNL Profile Query Language] (PQL). Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Let

El `let` permite almacenar una expresión como variable para usarla posteriormente en una consulta.

**Formato**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Ejemplo**

La siguiente consulta PQL obtiene todas las sumas de totales de productos con la transacción en USD cuando la suma es buena a 100 $ y menor a 1000 $.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Pasos siguientes

Ahora que ha aprendido acerca de diversas funciones, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
