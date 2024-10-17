---
solution: Experience Platform
title: Funciones de objeto de PQL
description: Profile Query Language (PQL) ofrece funciones para facilitar la interacción con objetos.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 8%

---

# Funciones de objeto

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con objetos. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Es nulo

La función `isNull` determina si una referencia de objeto no existe como booleano.

**Formato**

```sql
{OBJECT}.isNull()
```

**Ejemplo**

La siguiente consulta de PQL comprueba si la dirección postal de la persona no existe.

```sql
person.homeAddress.isNull()
```

## No es nulo

La función `isNotNull` determina si existe una referencia a un objeto como booleano.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Ejemplo**

La siguiente consulta de PQL comprueba si existe la dirección particular de la persona.

```sql
person.homeAddress.isNotNull()
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de los objetos, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
