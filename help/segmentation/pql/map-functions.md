---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de mapa
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 6%

---


# Funciones de mapa

[!DNL Profile Query Language] (PQL) oferta funciones para facilitar la interacción con los mapas. Encontrará más información sobre otras funciones de PQL en la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

## Obtenga

La `get` función se utiliza para recuperar el valor de un mapa para una clave determinada.

**Formato**

```sql
{MAP}.get({STRING})
```

**Ejemplo**

La siguiente consulta PQL obtiene el valor del mapa de identidad de la clave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Teclas

La `keys` función se utiliza para recuperar todas las claves de un mapa determinado.

**Formato**

```sql
{MAP}.keys()
```

**Ejemplo**

La siguiente consulta PQL obtiene todas las claves del mapa `identityMap`.

```sql
identityMap.keys()
```

## Valores

La `values` función se utiliza para recuperar todos los valores de un mapa determinado.

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

Ahora que ha aprendido sobre las funciones de mapa, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.
