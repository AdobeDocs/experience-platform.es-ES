---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;string functions;string;
solution: Experience Platform
title: Funciones de cadena
topic: developer guide
description: Perfil Consulta Language (PQL) oferta funciones para simplificar la interacción con cadenas.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 7%

---


# Funciones de cadena

[!DNL Profile Query Language] (PQL) oferta funciones para simplificar la interacción con cadenas. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Como

La `like` función se utiliza para determinar si una cadena coincide con un patrón especificado.

**Format**

```sql
{STRING_1} like {STRING_2}
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La expresión que se va a comparar con la primera cadena. Existen dos caracteres especiales admitidos para crear una expresión: `%` y `_`. <ul><li>`%` se utiliza para representar cero o más caracteres.</li><li>`_` se utiliza para representar exactamente un carácter.</li></ul> |

**Ejemplo**

La siguiente consulta PQL recupera todas las ciudades que contienen el patrón &quot;es&quot;.

```sql
city like "%es%"
```

## Comienza con

La `startsWith` función se utiliza para determinar si una cadena inicio con una subcadena especificada.

**Format**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a buscar dentro de la primera cadena. |
| `{BOOLEAN}` | Parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona inicio con &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Does not start with

La `doesNotStartWith` función se utiliza para determinar si una cadena no está en inicio con una subcadena especificada.

**Format**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a buscar dentro de la primera cadena. |
| `{BOOLEAN}` | Parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona no inicio con &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Finaliza con

La `endsWith` función se utiliza para determinar si una cadena termina con una subcadena especificada.

**Format**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a buscar dentro de la primera cadena. |
| `{BOOLEAN}` | Parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona termina en &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## No termina con

La `doesNotEndWith` función se utiliza para determinar si una cadena no termina con una subcadena especificada.

**Format**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a buscar dentro de la primera cadena. |
| `{BOOLEAN}` | Parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona no termina en &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

La `contains` función se utiliza para determinar si una cadena contiene una subcadena especificada.

**Format**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a buscar dentro de la primera cadena. |
| `{BOOLEAN}` | Parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona contiene la cadena &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## No contiene

La `doesNotContain` función se utiliza para determinar si una cadena no contiene una subcadena especificada.

**Format**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a buscar dentro de la primera cadena. |
| `{BOOLEAN}` | Parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona no contiene la cadena &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Es igual a

La `equals` función se utiliza para determinar si una cadena es igual a la cadena especificada.

**Format**

```sql
{STRING_1}.equals({STRING_2})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a comparar con la primera cadena. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona es &quot;John&quot;.

```sql
person.name.equals("John")
```

## Not equal to

La `notEqualTo` función se utiliza para determinar si una cadena no es igual a la cadena especificada.

**Format**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | La cadena en la que se va a realizar la comprobación. |
| `{STRING_2}` | La cadena que se va a comparar con la primera cadena. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción entre mayúsculas y minúsculas, si el nombre de la persona no es &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Coincide

La `matches` función se utiliza para determinar si una cadena coincide con una expresión regular específica. Consulte [este documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) para obtener más información sobre patrones coincidentes en expresiones regulares.

**Format**

```sql
{STRING_1}.matches(STRING_2})
```

**Ejemplo**

La siguiente consulta de PQL determina, sin distinguir entre mayúsculas y minúsculas, si el nombre de la persona inicio con &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

## Grupo de expresión regular

La `regexGroup` función se utiliza para extraer información específica, basándose en la expresión habitual proporcionada.

**Format**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Ejemplo**

La siguiente consulta de PQL se utiliza para extraer el nombre de dominio de una dirección de correo electrónico.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## Pasos siguientes

Ahora que ha aprendido sobre las funciones de cadena, puede utilizarlas dentro de sus consultas PQL. Para obtener más información sobre otras funciones de PQL, lea la descripción general [del lenguaje de Consulta de](./overview.md)Perfil.

