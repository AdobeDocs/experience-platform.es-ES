---
keywords: Experience Platform;inicio;asignador;conjunto de asignaciones;asignación;
solution: Experience Platform
title: Información general sobre los conjuntos de asignaciones
topic: sobre validación
description: Aprenda a utilizar conjuntos de asignaciones con la preparación de datos de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4c06f621eb6fba8daa6501d56255cddbbcfdbda2
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---


# Información general sobre los conjuntos de asignaciones

Un conjunto de asignaciones es un conjunto de asignaciones que transforma los datos de un esquema a otro. Este documento proporciona información sobre cómo se componen los conjuntos de asignación, incluidos el esquema de entrada, el esquema de salida y las asignaciones.

## Primeros pasos

Esta descripción general requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

- [Preparación](./home.md) de datos: La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM).
- [Flujos de datos](../dataflows/home.md): Los flujos de datos son una representación de los trabajos de datos que mueven los datos a través de Platform. Los flujos de datos se configuran en distintos servicios, lo que ayuda a mover datos de conectores de origen a conjuntos de datos de destino, a [!DNL Identity] y [!DNL Profile], y a [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Métodos por los cuales se pueden enviar datos a  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): El marco estandarizado mediante el cual se  [!DNL Experience Platform] organizan los datos de experiencia del cliente.

## Sintaxis del conjunto de asignaciones

Un conjunto de asignaciones consta de un ID, un nombre, un esquema de entrada, un esquema de salida y una lista de asignaciones asociadas.

El siguiente JSON es un ejemplo de conjunto de asignaciones típico:

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
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
            "name" : "Id",
            "description" : "Identifier field"
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
| `outputSchema` | El esquema XDM al que se han transformado los datos de entrada se ajustará. |
| `mappings` | Matriz de asignaciones de campo a campo desde el esquema de origen al esquema de destino. |
| `sourceType` | Para cada asignación enumerada, su atributo `sourceType` indica el tipo de origen que se va a asignar. Puede ser uno de `ATTRIBUTE`, `STATIC` o `EXPRESSION`: <ul><li> `ATTRIBUTE` se utiliza para cualquier valor encontrado en la ruta de origen. </li><li>`STATIC` se utiliza para valores insertados en la ruta de destino. Este valor permanece constante y no se ve afectado por el esquema de origen.</li><li> `EXPRESSION` se utiliza para una expresión que se resuelve durante el tiempo de ejecución. Puede encontrar una lista de expresiones disponibles en la [guía de funciones de asignación](./functions.md).</li> </ul> |
| `source` | Para cada asignación enumerada, el atributo `source` indica el campo que desea asignar. Puede encontrar más información sobre cómo configurar su origen en la sección [sources](#sources). |
| `destination` | Para cada asignación enumerada, el atributo `destination` indica el campo o la ruta al campo, donde se coloca el valor extraído del campo `source`. Puede encontrar más información sobre cómo configurar sus destinos en la sección [destino](#destination). |
| `mappings.name` | (*Opcional*) Un nombre para la asignación. |
| `mappings.description` | (*Opcional*) Una descripción de la asignación. |

## Configuración de fuentes de asignación

En una asignación, `source` puede ser un campo, una expresión o un valor estático. En función del tipo de origen dado, el valor se puede extraer de varias formas.

### Campo en datos de columna

Cuando asigne un campo en datos de columnas, como un archivo CSV, utilice el tipo de origen `ATTRIBUTE`. Si el campo contiene `.` dentro de su nombre, utilice `\` para omitir el valor. A continuación se encuentra un ejemplo de esta asignación:

**Archivo CSV de muestra:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Asignación de muestras**

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

Cuando asigne un campo en datos anidados, como un archivo JSON, utilice el tipo de origen `ATTRIBUTE` . Si el campo contiene `.` dentro de su nombre, utilice `\` para omitir el valor. A continuación se encuentra un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Asignación de muestras**

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

Al asignar un campo dentro de una matriz, puede recuperar un valor específico mediante un índice. Para ello, utilice el tipo de origen `ATTRIBUTE` y el índice del valor que desea asignar. A continuación se encuentra un ejemplo de esta asignación:

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

**Asignación de muestras**

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

Con el tipo de origen `ATTRIBUTE` también puede asignar directamente una matriz a una matriz o un objeto a un objeto. A continuación se encuentra un ejemplo de esta asignación:

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

**Asignación de muestras**

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

### Operaciones iterativas en arreglos de discos

Con el tipo de origen `ATTRIBUTE`, puede recorrer en bucle iterativamente matrices y asignarlas a un esquema de destino mediante un índice comodín (`[*]`). A continuación se encuentra un ejemplo de esta asignación:

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

**Asignación de muestras**

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

Si desea asignar una constante o un valor estático, utilice el tipo de origen `STATIC` .  Al utilizar el tipo de origen `STATIC` , `source` representa el valor codificado que desea asignar a `destination`. A continuación se encuentra un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Asignación de muestras**

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

Si desea asignar una expresión, utilice el tipo de origen `EXPRESSION` . Puede encontrar una lista de las funciones aceptadas en la [guía de funciones de asignación](./functions.md). Al utilizar el tipo de origen `EXPRESSION` , `source` representa la función que desea resolver. A continuación se encuentra un ejemplo de esta asignación:

**Archivo JSON de muestra**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Asignación de muestras**

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

En una asignación, `destination` es la ubicación donde se insertará el valor extraído del `source`.

### Campo en el nivel raíz

Cuando desee asignar el valor `source` al nivel raíz de los datos transformados, siga el ejemplo siguiente:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Asignación de muestras**

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

Cuando desee asignar el valor `source` a un campo anidado en los datos transformados, siga el ejemplo siguiente:

**Archivo JSON de muestra**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Asignación de muestras**

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

Cuando desee asignar el valor `source` a un índice específico de una matriz en los datos transformados, siga el ejemplo siguiente:

**Archivo JSON de muestra**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Asignación de muestras**

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

Si desea recorrer en bucle iterativamente las matrices y asignar los valores al destino, puede utilizar un índice comodín (`[*]`). A continuación se puede ver un ejemplo de esto:

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

**Asignación de muestras**

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

Al leer este documento, ahora debe comprender cómo se construyen los conjuntos de asignaciones, incluido cómo configurar asignaciones individuales dentro de un conjunto de asignaciones. Para obtener más información sobre otras funciones de preparación de datos, lea la [información general de preparación de datos](./home.md). Para aprender a utilizar conjuntos de asignación dentro de la API de preparación de datos, lea la [Guía para desarrolladores de preparación de datos](./api/overview.md).