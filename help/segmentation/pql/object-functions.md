---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;servicio de segmentación;pql;PQL;lenguaje de consulta de perfil;funciones de objeto;objeto
solution: Experience Platform
title: Funciones de objeto PQL
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para simplificar la interacción con los objetos.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 5%

---

# Funciones de objeto

[!DNL Profile Query Language] (PQL) ofrece funciones para simplificar la interacción con los objetos. Puede encontrar más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] información general](./overview.md).

## Is null

La variable `isNull` determina si no existe una referencia de objeto.

**Formato**

```sql
{OBJECT}.isNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si la dirección principal de la persona no existe.

```sql
person.homeAddress.isNull()
```

## No es nulo

La variable `isNotNull` determina si existe una referencia de objeto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si existe la dirección principal de la persona.

```sql
person.homeAddress.isNotNull()
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de objeto, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [Información general sobre el lenguaje de consulta de perfil](./overview.md).
