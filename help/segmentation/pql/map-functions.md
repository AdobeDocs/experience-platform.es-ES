---
solution: Experience Platform
title: Funciones de mapa de PQL
description: Profile Query Language (PQL) ofrece funciones para facilitar la interacción con mapas.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# Funciones de asignación

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con mapas. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Obtener

La función `get` se usa para recuperar el valor de un mapa para una clave determinada como objeto.

**Formato**

```sql
{MAP}.get({STRING})
```

**Ejemplo**

La siguiente consulta de PQL obtiene el valor del mapa de identidad para la clave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Claves

La función `keys` se usa para recuperar todas las claves de un mapa determinado como una matriz o lista.

**Formato**

```sql
{MAP}.keys()
```

**Ejemplo**

La siguiente consulta de PQL obtiene todas las claves del mapa `identityMap`.

```sql
identityMap.keys()
```

## Valores

La función `values` se usa para recuperar todos los valores de un mapa determinado como una matriz o lista.

**Formato**

```sql
{MAP}.values()
```

**Ejemplo**

La siguiente consulta de PQL obtiene todos los valores del mapa `identityMap`.

```sql
identityMap.values()
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de asignación, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
