---
solution: Experience Platform
title: Funciones de objeto PQL
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para facilitar la interacción con objetos.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 6%

---

# Funciones de objeto

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con objetos. Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Es nulo

El `isNull` determina si no existe una referencia de objeto.

**Formato**

```sql
{OBJECT}.isNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si la dirección particular de la persona no existe.

```sql
person.homeAddress.isNull()
```

## No es nulo

El `isNotNull` determina si existe una referencia a un objeto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si existe la dirección particular de la persona.

```sql
person.homeAddress.isNotNull()
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de objeto, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
