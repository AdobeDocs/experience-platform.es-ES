---
keywords: Experience Platform;inicio;temas populares;
title: Guía de solución de problemas de preparación de datos
topic-legacy: troubleshooting
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre la preparación de datos de Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: 4bb21ce5861419964b80a827269e40ef3e6483f8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# [!DNL Data Prep] guía de solución de problemas

Este documento proporciona respuestas a las preguntas más frecuentes sobre Adobe Experience Platform [!DNL Data Prep], así como una guía de solución de problemas para errores comunes. Para obtener preguntas e información de solución de problemas con respecto a las API de Platform en general, consulte la [Guía de solución de problemas de la API de Adobe Experience Platform](../landing/troubleshooting.md).

## Preguntas frecuentes

A continuación se muestra una lista de las preguntas más frecuentes sobre [!DNL Data Prep] y sus respuestas.

### ¿Cómo se resuelven los errores de transformación?

[!DNL Data Prep] localiza todos los errores de transformación a la columna en la que se produjeron. Como resultado, esa columna se anula y el resto de la fila se seguirá procesando. Estos problemas de transformación se registran como **Advertencias**. Se recomienda revisar las advertencias periódicamente y ajustar la lógica de transformación para tener en cuenta los problemas de transformación. Esto aumentará la calidad de los datos introducidos en el Experience Platform.

Si las columnas están marcadas como **Requerido** se anulan debido a problemas de transformación, por lo que no se ingerirá la fila. Cuando la incorporación parcial de datos está habilitada, puede establecer el umbral de dichos rechazos antes de que falle todo el flujo. Si el atributo anulado no afectó a ninguna validación de nivel de esquema, la fila se seguirá incorporando.

También se rechazará cualquier fila que no sea válida aunque no tenga errores de transformación. Por ejemplo, un flujo de ingesta de datos puede tener una asignación de paso a través (sin lógica de transformación) a un campo requerido y no hay ningún valor entrante para ese atributo. Esta fila se rechazará.

### ¿Cómo puedo escapar de caracteres especiales en un campo?

Puede omitir los caracteres especiales de un campo utilizando `${...}`. Sin embargo, los archivos JSON que contienen campos con un punto (`.`) no son compatibles con este mecanismo. Cuando interactúa con jerarquías, si un atributo secundario tiene un punto (`.`), debe utilizar una barra invertida (`\`) para omitir caracteres especiales. Por ejemplo, `address` es un objeto que contiene el atributo `street.name`, esto puede denominarse `address.street\.name` en lugar de `address.street.name`.
