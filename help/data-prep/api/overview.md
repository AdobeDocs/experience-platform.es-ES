---
keywords: Experience Platform;preparación de datos;api de preparación de datos;solución de problemas;API
title: Información general sobre la API de preparación de datos
topic: guide
description: La API de preparación de datos permite crear conjuntos y funciones de asignación mediante programación, lo que permite transformar los datos entre esquemas de origen y destino.
translation-type: tm+mt
source-git-commit: cae6dc80d0394db51dc97478b92459be64c64498
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---


# Guía de API del servicio de asignación

La preparación de datos permite a los ingenieros de datos asignar, transformar y validar datos desde y hacia el Modelo de datos de experiencia (XDM). La preparación de datos aparece como un paso de &quot;mapa&quot; en los procesos de ingesta de datos, incluido el flujo de trabajo de ingesta de CSV.

La API del servicio de asignación, también conocida como API de preparación de datos, incluye varios extremos descritos a continuación. Visite las guías de puntos finales individuales para obtener más información y consulte la [guía de introducción](./getting-started.md) para obtener información importante sobre los encabezados necesarios, leer llamadas de API de ejemplo y más.

## Funciones

Las funciones de conjunto de asignaciones permiten transformar los datos entre esquemas de origen y destino. Puede utilizar el extremo `/languages/el` para validar sus expresiones, así como obtener una lista de todas las funciones y operaciones disponibles del conjunto de asignaciones.

Para obtener información detallada sobre cómo utilizar las funciones de conjunto de asignaciones, lea la [guía de extremo de funciones](./functions.md).

## Conjunto de asignaciones

Los conjuntos de asignaciones se pueden utilizar para definir cómo se asignan los datos de un esquema de origen al de un esquema de destino. Puede utilizar el extremo `/mappingSets` de la API de preparación de datos para recuperar, crear, actualizar y validar conjuntos de asignación mediante programación.

Para obtener información detallada sobre cómo utilizar los conjuntos de asignaciones, lea la [guía de extremo del conjunto de asignaciones](./mapping-set.md).

## Pasos siguientes

Para empezar a realizar llamadas mediante la API del servicio de asignación, lea la [guía de introducción](./getting-started.md) y, a continuación, seleccione una de las guías de punto final para aprender a utilizar los puntos finales específicos.