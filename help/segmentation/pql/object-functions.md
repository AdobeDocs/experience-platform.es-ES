---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Funciones de objeto
topic: developer guide
translation-type: tm+mt
source-git-commit: 84a5b992639c1cabfdeaec5262964c9873826592
workflow-type: tm+mt
source-wordcount: '108'
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