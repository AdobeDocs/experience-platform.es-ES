---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Lenguaje de Consulta de Perfil;funciones de mapa;mapa;
solution: Experience Platform
title: Funciones de mapa PQL
topic: developer guide
description: El lenguaje de Consulta de perfil (PQL) oferta funciones para facilitar la interacción con los mapas.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---


# Funciones de mapa

[!DNL Profile Query Language] (PQL) oferta funciones para facilitar la interacción con los mapas. Encontrará más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

## Obtenga

La función `get` se utiliza para recuperar el valor de un mapa para una clave determinada.

**Format**

```sql
{MAP}.get({STRING})
```

**Ejemplo**

La siguiente consulta PQL obtiene el valor del mapa de identidad para la clave `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Teclas

La función `keys` se utiliza para recuperar todas las claves de un mapa determinado.

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

La función `values` se utiliza para recuperar todos los valores de un mapa determinado.

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

Ahora que ha aprendido sobre las funciones de mapa, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de Consulta de Perfil](./overview.md).
