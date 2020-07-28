---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 5%

---


# Funciones de objeto

[!DNL Profile Query Language] (PQL) oferta funciones para simplificar la interacción con objetos. Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Es nulo

La `isNull` función determina si no existe una referencia de objeto.

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

La `isNotNull` función determina si existe una referencia de objeto.

**Format**

```sql
{OBJECT}.isNotNull()
```

**Ejemplo**

La siguiente consulta PQL comprueba si existe la dirección de la persona.

```sql
person.homeAddress.isNotNull()
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de objeto, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.