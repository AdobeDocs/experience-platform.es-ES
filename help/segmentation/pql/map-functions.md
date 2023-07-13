---
solution: Experience Platform
title: Funciones de mapa PQL
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para facilitar la interacción con mapas.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 7%

---

# Funciones de asignación

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con los mapas. Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Obtenga

El `get` se utiliza para recuperar el valor de un mapa para una clave determinada.

**Formato**

```sql
{MAP}.get({STRING})
```

**Ejemplo**

La siguiente consulta PQL obtiene el valor del mapa de identidad de la clave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Claves

El `keys` se utiliza para recuperar todas las claves de un mapa determinado.

**Formato**

```sql
{MAP}.keys()
```

**Ejemplo**

La siguiente consulta PQL obtiene todas las claves para el mapa `identityMap`.

```sql
identityMap.keys()
```

## Valores

El `values` se utiliza para recuperar todos los valores de un mapa determinado.

**Formato**

```sql
{MAP}.values()
```

**Ejemplo**

La siguiente consulta PQL obtiene todos los valores del mapa `identityMap`.

```sql
identityMap.values()
```

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de asignación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
