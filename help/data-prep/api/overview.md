---
keywords: Experience Platform;preparación de datos;api de preparación de datos;solución de problemas;API
title: Resumen de API de preparación de datos
description: La API de preparación de datos permite crear mediante programación conjuntos y funciones de asignación, lo que permite transformar los datos entre esquemas de origen y destino.
exl-id: 740944ae-93ba-4099-a65e-18d6b384c307
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 1%

---

# Guía de API del servicio de asignación

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de ingesta de datos, incluido el flujo de trabajo de ingesta de CSV.

La API del servicio de asignación, también conocida como API de preparación de datos, incluye varios extremos descritos a continuación. Visite las guías de extremos individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, la lectura de llamadas de API de ejemplo y mucho más.

## Funciones

Las funciones de conjunto de asignaciones le permiten transformar los datos entre esquemas de origen y destino. Puede usar el complemento `/languages/el` extremo para validar las expresiones y obtener una lista de todas las funciones y operaciones disponibles del conjunto de asignaciones.

Para obtener información detallada sobre cómo utilizar las funciones de conjunto de asignación, lea la [guía de extremo de funciones](./functions.md).

## Conjunto de asignaciones

Los conjuntos de asignaciones se pueden utilizar para definir cómo se asignan los datos de un esquema de origen al de un esquema de destino. Puede usar el complemento `/mappingSets` en la API de preparación de datos para recuperar, crear, actualizar y validar conjuntos de asignaciones mediante programación.

Para obtener información detallada sobre cómo utilizar los conjuntos de asignaciones, lea la [guía de extremo del conjunto de asignaciones](./mapping-set.md).

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio de asignación, lea la [guía de introducción](./getting-started.md) a continuación, seleccione una de las guías de extremos para aprender a utilizar los extremos específicos.
