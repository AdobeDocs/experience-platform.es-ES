---
solution: Experience Platform
title: Funciones de cadena de PQL
description: Profile Query Language (PQL) ofrece funciones para facilitar la interacción con cadenas.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 5%

---

# Funciones de cadena

[!DNL Profile Query Language] (PQL) ofrece funciones para facilitar la interacción con cadenas. Encontrará más información sobre otras funciones de PQL en la [[!DNL Profile Query Language] descripción general](./overview.md).

## Me gusta

La función `like` se usa para determinar si una cadena coincide con un patrón especificado como booleano.

**Formato**

```sql
{STRING_1} like {STRING_2}
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | La expresión que debe coincidir con la primera cadena. Existen dos caracteres especiales admitidos para crear una expresión: `%` y `_`. <ul><li>`%` se usa para representar cero o más caracteres.</li><li>`_` se usa para representar exactamente un carácter.</li></ul> |

**Ejemplo**

La siguiente consulta de PQL recupera todas las ciudades que contienen el patrón &quot;es&quot;.

```sql
city like "%es%"
```

## Comienza con

La función `startsWith` se usa para determinar si una cadena empieza con una subcadena especificada como booleano.

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

La siguiente consulta de PQL determina, con distinción entre mayúsculas y minúsculas, si el nombre de la persona comienza por &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## No empieza por

La función `doesNotStartWith` se usa para determinar si una cadena no comienza con una subcadena especificada como booleano.

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

La siguiente consulta de PQL determina, con distinción entre mayúsculas y minúsculas, si el nombre de la persona no comienza con &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Termina con

La función `endsWith` se usa para determinar si una cadena termina con una subcadena especificada como booleano.

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

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona termina con &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## No termina por

La función `doesNotEndWith` se usa para determinar si una cadena no termina con una subcadena especificada como booleano.

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

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona no termina con &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Contains

La función `contains` se usa para determinar si una cadena contiene una subcadena especificada como booleano.

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

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona contiene la cadena &quot;2010@gm&quot;.

```sql
person.emailAddress.contains("2010@gm")
```

## No contiene

La función `doesNotContain` se usa para determinar si una cadena no contiene una subcadena especificada como booleano.

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

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si la dirección de correo electrónico de la persona no contiene la cadena &quot;2010@gm&quot;.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Es igual a

La función `equals` se usa para determinar si una cadena es igual a la cadena especificada como booleano.

**Formato**

```sql
{STRING_1}.equals({STRING_2})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se va a comparar con la primera cadena. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción entre mayúsculas y minúsculas, si el nombre de la persona es &quot;John&quot;.

```sql
person.name.equals("John")
```

## No igual a

La función `notEqualTo` se usa para determinar si una cadena no es igual a la cadena especificada como booleano.

**Formato**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argumento | Descripción |
| --------- | ----------- |
| `{STRING_1}` | Cadena en la que se realizará la comprobación. |
| `{STRING_2}` | Cadena que se va a comparar con la primera cadena. |

**Ejemplo**

La siguiente consulta de PQL determina, con distinción de mayúsculas y minúsculas, si el nombre de la persona no es &quot;John&quot;.

```sql
person.name.notEqualTo("John")
```

## Iguala

La función `matches` se usa para determinar si una cadena coincide con una expresión regular específica. Consulte [este documento](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) para obtener más información sobre patrones coincidentes en expresiones regulares como valor booleano.

**Formato**

```sql
{STRING_1}.matches(STRING_2})
```

**Ejemplo**

La siguiente consulta de PQL determina, sin distinguir entre mayúsculas y minúsculas, si el nombre de la persona comienza por &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Si usa funciones de expresión regular como `\w`, **debe** omitir el carácter de barra invertida. Por lo tanto, en lugar de escribir solo `\w`, debe incluir una barra invertida adicional y escribir `\\w`.

## Grupo de expresiones regulares

La función `regexGroup` se usa para extraer información específica, basada en la expresión regular proporcionada como cadena.

**Formato**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Ejemplo**

La siguiente consulta de PQL se utiliza para extraer el nombre de dominio de una dirección de correo electrónico.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Si usa funciones de expresión regular como `\w`, **debe** omitir el carácter de barra invertida. Por lo tanto, en lugar de escribir solo `\w`, debe incluir una barra invertida adicional y escribir `\\w`.

## Pasos siguientes

Ahora que ha aprendido acerca de las funciones de cadena, puede utilizarlas en sus consultas de PQL. Para obtener más información acerca de otras funciones de PQL, lea la [descripción general de Profile Query Language](./overview.md).
