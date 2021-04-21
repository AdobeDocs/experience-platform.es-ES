---
keywords: Experience Platform;inicio;temas populares;segmentación;Segmentación;Servicio de segmentación;pql;PQL;Idioma de consulta de perfil;funciones de asignación;mapa;
solution: Experience Platform
title: Funciones de mapa de PQL
topic-legacy: developer guide
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para facilitar la interacción con los mapas.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---

# Asignar funciones

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con los mapas. Puede encontrar más información sobre otras funciones de PQL en [[!DNL Profile Query Language] overview](./overview.md).

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

## Claves

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

Ahora que ha aprendido sobre las funciones de asignación, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la [información general del lenguaje de consulta de perfil](./overview.md).
