---
keywords: Experience Platform;inicio;temas populares;
title: Guía de resolución de problemas de preparación de datos
description: Este documento proporciona respuestas a las preguntas frecuentes acerca de la preparación de datos de Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] guía de solución de problemas

Este documento proporciona respuestas a las preguntas frecuentes acerca de Adobe Experience Platform [!DNL Data Prep], así como una guía de solución de problemas para errores comunes. Si tiene preguntas e información de solución de problemas relacionados con las API de Platform en general, consulte la [Guía de solución de problemas de API de Adobe Experience Platform](../landing/troubleshooting.md).

## Preguntas frecuentes

A continuación se muestra una lista de las preguntas más frecuentes acerca de [!DNL Data Prep] y sus respuestas.

### ¿Cómo se resuelven los errores de transformación?

[!DNL Data Prep] localiza todos los errores de transformación en la columna en la que se produjeron. Como resultado, esa columna se anula y el resto de la fila se sigue procesando. Estos problemas de transformación se registran como **Advertencias**. Se recomienda revisar las advertencias periódicamente y ajustar la lógica de transformación para tener en cuenta los problemas de transformación. Esto aumentará la calidad de los datos introducidos en Experience Platform.

Si las columnas están marcadas como **Requerido** se anulan debido a problemas de transformación, la fila no se incorporará. Cuando la incorporación parcial de datos está habilitada, puede establecer el umbral de dichos rechazos antes de que falle todo el flujo. Si el atributo anulado no afectó a ninguna validación de nivel de esquema, la fila se seguirá introduciendo.

También se rechazará cualquier fila que no sea válida, incluso sin errores de transformación. Por ejemplo, un flujo de ingesta de datos puede tener una asignación de paso a través (sin lógica de transformación) a un campo obligatorio y no hay ningún valor entrante para ese atributo. Esta fila se rechazará.

### ¿Cómo puedo omitir los caracteres especiales de un campo?

Puede aplicar secuencias de escape a los caracteres especiales de un campo mediante `${...}`. Sin embargo, los archivos JSON que contienen campos con un punto (`.`) no son compatibles con este mecanismo. Al interactuar con jerarquías, si un atributo secundario tiene un punto (`.`), debe utilizar una barra invertida (`\`) para omitir caracteres especiales. Por ejemplo, `address` es un objeto que contiene el atributo `street.name`, esto se puede denominar `address.street\.name` en lugar de `address.street.name`.

### ¿Cuál es la longitud máxima de los campos calculados?

Los campos calculados tienen una longitud máxima de 4096 caracteres.