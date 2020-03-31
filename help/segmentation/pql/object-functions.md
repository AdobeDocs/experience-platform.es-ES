---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Funciones de objeto

El lenguaje de Consulta de Perfil (PQL) oferta funciones para simplificar la interacción con los objetos. Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Es nulo

La `isNull` función determina si no existe una referencia de objeto.

**Formato**

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

Ahora que ha aprendido sobre las funciones de objeto, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.