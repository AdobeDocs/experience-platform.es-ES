---
solution: Experience Platform
title: Funciones de cadena PQL
description: El lenguaje de consulta de perfil (PQL) ofrece funciones para facilitar la interacción con cadenas.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 7%

---

# Funciones de cadena

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con cadenas. Puede encontrar más información sobre otras funciones PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Like

El `like` se utiliza para determinar si una cadena coincide con un patrón especificado.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | La expresión que debe coincidir con la primera cadena. Existen dos caracteres especiales admitidos para crear una expresión: `%` y `_`. <ul><li>`%` se utiliza para representar cero o más caracteres.</li><li>`_` se utiliza para representar exactamente un carácter.</li></ul> |

**Ejemplo**

La siguiente consulta PQL recupera todas las ciudades que contienen el patrón &quot;es&quot;.

```sql
city like "%es%"
```

## Comienza con

El `startsWith` se utiliza para determinar si una cadena empieza con una subcadena especificada.

**Formato**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se busca dentro de la primera cadena. |
| `{BOOLEAN}` | Un parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona comienza con &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Does not start with

El `doesNotStartWith` se utiliza para determinar si una cadena no comienza con una subcadena especificada.

**Formato**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se busca dentro de la primera cadena. |
| `{BOOLEAN}` | Un parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona no comienza con &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Finaliza con

El `endsWith` se utiliza para determinar si una cadena termina con una subcadena especificada.

**Formato**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se busca dentro de la primera cadena. |
| `{BOOLEAN}` | Un parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona termina con &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## No termina por

El `doesNotEndWith` se utiliza para determinar si una cadena no termina con una subcadena especificada.

**Formato**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se busca dentro de la primera cadena. |
| `{BOOLEAN}` | Un parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona no termina con &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

El `contains` se utiliza para determinar si una cadena contiene una subcadena especificada.

**Formato**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se busca dentro de la primera cadena. |
| `{BOOLEAN}` | Un parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona contiene la cadena &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## No contiene

El `doesNotContain` se utiliza para determinar si una cadena no contiene una subcadena especificada.

**Formato**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se busca dentro de la primera cadena. |
| `{BOOLEAN}` | Un parámetro opcional para determinar si la comprobación distingue entre mayúsculas y minúsculas. De forma predeterminada, se establece en true. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona no contiene la cadena &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Es igual a

El `equals` se utiliza para determinar si una cadena es igual a la cadena especificada.

**Formato**

```sql
{STRING_1}.equals({STRING_2})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se va a comparar con la primera cadena. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona es &quot;John&quot;.

```sql
person.name.equals("John")
```

## Not equal to

El `notEqualTo` se utiliza para determinar si una cadena no es igual a la cadena especificada.

**Formato**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se va a comparar con la primera cadena. |

**Ejemplo**

La siguiente consulta PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona no es &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Devuelve como resultado 

El `matches` se utiliza para determinar si una cadena coincide con una expresión regular específica. Consulte la [este documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) para obtener más información sobre los patrones de coincidencia en expresiones regulares.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Ejemplo**

La siguiente consulta PQL determina, sin distinguir entre mayúsculas y minúsculas, si el nombre de la persona comienza con &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Si utiliza funciones de expresión regular como `\w`, usted **debe** escape del carácter de barra invertida. Así que, en lugar de escribir sólo `\w`, debe incluir una barra invertida y una escritura adicionales `\\w`.

## Grupo de expresiones regulares

El `regexGroup` se utiliza para extraer información específica, basada en la expresión regular proporcionada.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Ejemplo**

La siguiente consulta PQL se utiliza para extraer el nombre de dominio de una dirección de correo electrónico.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Si utiliza funciones de expresión regular como `\w`, usted **debe** escape del carácter de barra invertida. Así que, en lugar de escribir sólo `\w`, debe incluir una barra invertida y una escritura adicionales `\\w`.

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de cadena, puede utilizarlas en sus consultas PQL. Para obtener más información sobre otras funciones PQL, lea la [Introducción al lenguaje de consulta de perfil](./overview.md).
