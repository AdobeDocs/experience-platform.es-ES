---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones de objeto;objeto;
solution: Experience Platform
title: Funciones de objeto PQL
topic: developer guide
description: El lenguaje de Consulta de perfil (PQL) oferta funciones para simplificar la interacción con los objetos.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 4%

---


# Funciones de objeto

[!DNL Profile Query Language] (PQL) oferta funciones para simplificar la interacción con objetos. Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Es nulo

La función `isNull` determina si no existe una referencia de objeto.

**Format**

```sql
{OBJECT}.isNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si la dirección de la persona no existe.

```sql
person.homeAddress.isNull()
```

## No es nulo

La función `isNotNull` determina si existe una referencia de objeto.

**Formato**

```sql
{OBJECT}.isNotNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si existe la dirección de la persona.

```sql
person.homeAddress.isNotNull()
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de objeto, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).