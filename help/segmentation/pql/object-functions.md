---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;object functions;object;
solution: Experience Platform
title: Funciones de objeto
topic: developer guide
description: El lenguaje de Consulta de perfil (PQL) oferta funciones para simplificar la interacción con los objetos.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---


# Funciones de objeto

[!DNL Profile Query Language] (PQL) oferta funciones para simplificar la interacción con objetos. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

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