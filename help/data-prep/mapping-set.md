---
keywords: Experience Platform;inicio;asignador;conjunto de asignaciones;asignación;
solution: Experience Platform
title: Información general sobre conjuntos de asignaciones
description: Aprenda a utilizar conjuntos de asignaciones con la preparación de datos de Adobe Experience Platform.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 3%

---

# Información general sobre conjuntos de asignaciones

Un conjunto de asignaciones es un conjunto de asignaciones que transforma los datos de un esquema a otro. Este documento proporciona información sobre cómo se comprenden los conjuntos de asignaciones, incluidos el esquema de entrada, el esquema de salida y las asignaciones.

## Primeros pasos

Esta descripción general requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Preparación de datos](./home.md): la preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM).
- [Flujos de datos](../dataflows/home.md): los flujos de datos son una representación de los trabajos de datos que mueven datos a través de Platform. Los flujos de datos se configuran en diferentes servicios, lo que ayuda a mover datos de los conectores de origen a los conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): métodos mediante los cuales se pueden enviar datos a [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.

## Sintaxis del conjunto de asignaciones

Un conjunto de asignaciones consta de un ID, un nombre, un esquema de entrada, un esquema de salida y una lista de asignaciones asociadas.

El siguiente JSON es un ejemplo de un conjunto de asignaciones típico:

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Propiedad | Descripción |
| -------- | ----------- |
| `id` | Identificador único del conjunto de asignaciones. |
| `name` | Nombre del conjunto de asignaciones. |
| `inputSchema` | El esquema XDM para los datos entrantes. |
| `outputSchema` | El esquema XDM al que se han transformado los datos de entrada para ajustarse. |
| `mappings` | Matriz de asignaciones de campo a campo desde el esquema de origen al esquema de destino. |
| `sourceType` | Para cada asignación enumerada, sus `sourceType` attribute indica el tipo de origen que se va a asignar. Puede ser uno de `ATTRIBUTE`, `STATIC`, o `EXPRESSION`: <ul><li> `ATTRIBUTE` se utiliza para cualquier valor encontrado en la ruta de origen. </li><li>`STATIC` se utiliza para los valores insertados en la ruta de destino. Este valor permanece constante y no se ve afectado por el esquema de origen.</li><li> `EXPRESSION` se utiliza para una expresión, que se resolverá durante el tiempo de ejecución. Puede encontrar una lista de expresiones disponibles en la variable [guía de funciones de asignación](./functions.md).</li> </ul> |
| `source` | Para cada asignación enumerada, la variable `source` attribute indica el campo que desea asignar. Encontrará más información sobre cómo configurar el origen en la [sección de fuentes](#sources). |
| `destination` | Para cada asignación enumerada, la variable `destination` El atributo indica el campo o la ruta al campo donde el valor se extrae del `source` se colocará el campo. Encontrará más información sobre cómo configurar sus destinos en la [sección de destino](#destination). |
| `mappings.name` | (*Opcional*) Un nombre para la asignación. |
| `mappings.description` | (*Opcional*) Una descripción de la asignación. |

## Configuración de orígenes de asignación

En una asignación, la variable `source` puede ser un campo, una expresión o un valor estático. En función del tipo de origen dado, el valor se puede extraer de varias formas.

### Campo en datos de columnas

Al asignar un campo en datos de columnas, como un archivo CSV, utilice el `ATTRIBUTE` tipo de origen. Si el campo contiene `.` dentro de su nombre, utilice `\` para omitir el valor. A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo CSV de ejemplo:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Asignación de muestra**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo en datos anidados

Al asignar un campo en datos anidados, como un archivo JSON, utilice el `ATTRIBUTE` tipo de origen. Si el campo contiene `.` dentro de su nombre, utilice `\` para omitir el valor. A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo dentro de una matriz

Al asignar un campo dentro de una matriz, puede recuperar un valor específico mediante un índice. Para ello, utilice el `ATTRIBUTE` tipo de origen y el índice del valor que desea asignar. A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Matriz a matriz u objeto a objeto

Uso del `ATTRIBUTE` Tipo de origen, también se puede asignar directamente una matriz a una matriz o un objeto a un objeto. A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Operaciones iterativas en matrices

Uso del `ATTRIBUTE` tipo de origen, puede recorrer en bucle de forma iterativa las matrices y asignarlas a un esquema de destino mediante un índice comodín (`[*]`). A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Valor constante

Si desea asignar una constante o un valor estático, utilice el `STATIC` tipo de origen.  Al usar el `STATIC` tipo de origen, la variable `source` representa el valor codificado que desea asignar al `destination`. A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Asignación de muestra**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Datos transformados**

```json
{
    "userType:": "CUSTOMER"
}
```

### Expresiones

Si desea asignar una expresión, utilice el `EXPRESSION` tipo de origen. Puede encontrar una lista de funciones aceptadas en la [guía de funciones de asignación](./functions.md). Al usar el `EXPRESSION` tipo de origen, la variable `source` representa la función que desea resolver. A continuación se puede encontrar un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Asignación de muestra**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Datos transformados**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Configuración de destinos de asignación

En una asignación, la variable `destination` es la ubicación donde se extrae el valor del `source` se insertará.

### Campo en el nivel raíz

Cuando desee asignar el `source` al nivel raíz de los datos transformados, siga el ejemplo siguiente:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "name": "John Smith"
}
```

### Campo anidado

Cuando desee asignar el `source` a un campo anidado en los datos transformados, siga el ejemplo siguiente:

**Archivo JSON de muestra**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Asignación de muestra**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo en un índice de matriz específico

Cuando desee asignar el `source` a un índice específico en una matriz de los datos transformados, siga el ejemplo siguiente:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "piList": ["John Smith"]
}
```

### Operación de matriz iterativa

Si desea recorrer en bucle de forma iterativa las matrices y asignar los valores al destino, puede utilizar un índice comodín (`[*]`). A continuación puede ver un ejemplo de esto:

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Asignación de muestra**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Datos transformados**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Pasos siguientes

Al leer este documento, ahora debería comprender cómo se construyen los conjuntos de asignaciones, incluido cómo configurar asignaciones individuales dentro de un conjunto de asignaciones. Para obtener más información sobre otras funciones de la preparación de datos, lea la [Resumen de preparación de datos](./home.md). Para aprender a utilizar conjuntos de asignaciones dentro de la API de preparación de datos, lea la [Guía para desarrolladores de Data Prep](./api/overview.md).
