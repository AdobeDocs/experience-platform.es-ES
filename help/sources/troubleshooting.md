---
keywords: Experience Platform;inicio;temas populares;fuentes;ingesta;solución de problemas;fuentes;solución de problemas;fuentes preguntas frecuentes;faq;conectores de origen;conector de origen;preguntas frecuentes de conectores de origen;solución de problemas de conectores de origen;
solution: Experience Platform
title: Solución de problemas de fuentes
description: Este documento proporciona respuestas a las preguntas más frecuentes sobre las fuentes en Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# Guía de solución de problemas de fuentes

Este documento proporciona respuestas a las preguntas más frecuentes sobre las fuentes en Adobe Experience Platform. Para preguntas y solución de problemas relacionados con otras [!DNL Platform] servicios, incluidos los que se encuentran en todos los [!DNL Platform] API, consulte la [Guía de solución de problemas del Experience Platform](../landing/troubleshooting.md).

## Preguntas frecuentes

La siguiente es una lista de respuestas a las preguntas más frecuentes sobre las fuentes.

### ¿Tengo que hacer cambios en nuestra configuración de seguridad de red para habilitar las fuentes?

Es posible que deba realizar la lista de permitidos de ciertas direcciones IP para habilitar las fuentes. Para obtener más información, consulte la documentación de su conector de origen específico.

### ¿Qué tipos de autenticación son compatibles con las fuentes?

Las fuentes se pueden autenticar utilizando cadenas de conexión, nombres de usuario y contraseñas, o accediendo a tokens y claves. Puede encontrar detalles específicos sobre tipos de autenticación admitidos en la documentación del conector de origen especificado.

### ¿Por qué están fallando todas mis ejecuciones de flujo recientes?

Si nota que todas las ejecuciones de flujo recientes están fallando, es posible que sus credenciales hayan cambiado o caducado. Para solucionar este problema, intente actualizar la conexión con las credenciales más recientes.

### ¿Qué tipos de archivo se admiten?

Actualmente, los tipos de archivo admitidos son archivos delimitados, JSON y Parquet.

### ¿Cuáles son las restricciones en los nombres y tamaños de archivo?

La siguiente es una lista de restricciones que debe tener en cuenta para los archivos de los orígenes.

- Los nombres de los componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se elimina automáticamente.
- Los siguientes caracteres de URL reservados deben tener un escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no permitidos. Puntos de código como `\uE000`, aunque válido en nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caracteres de punto (.) y dos caracteres de punto (.).
- El número máximo de archivos por lote es de 1500, con un tamaño máximo de lote de 100 GB.
- El número máximo de propiedades o campos por fila es de 10 000.
- El número máximo de lotes que se pueden enviar por usuario, por minuto, es de 138.

### ¿Qué tipos de datos se admiten?

Los tipos de datos admitidos son números enteros, cadenas, booleanos, objetos datetime, matrices y objetos.

### ¿Qué formatos de fecha y hora se admiten?

Las fuentes admiten una amplia variedad de formatos de fecha y hora al introducir datos. Puede encontrar más información sobre los formatos de fecha y hora admitidos en la sección de fechas del [guía de gestión del formato de datos](../data-prep/data-handling.md#dates) en la documentación de preparación de datos.

### ¿Cómo aplico formato a las matrices en archivos CSV, JSON y Parquet?

Los archivos JSON y Parquet admiten matrices de forma nativa. Para estructuras planas, como CSV, no se admiten matrices. Sin embargo, las cadenas con varios valores se pueden dividir en una matriz utilizando funciones de preparación de datos como explode y join. Puede encontrar más información sobre estas funciones de preparación de datos en la [guía de funciones de preparación de datos](../data-prep/functions.md#string)

### ¿Qué fuentes admiten la ingesta parcial?

Todas las fuentes de ingesta por lotes admiten la ingesta parcial. Sin embargo, las fuentes de ingesta de flujo continuo no admiten la ingesta parcial.

### ¿Cuándo debo usar la ingesta parcial?

Debe utilizar la ingestión parcial si **not** tienen restricciones, como que todo el archivo se incorpore a Platform. Alternativamente, se debe utilizar la ingesta parcial si no le importa la ingesta de datos que puedan contener errores dentro de él.

### ¿Cuál es el umbral de error típico de ingesta parcial?

No hay ningún &quot;umbral de error típico&quot; para la ingesta parcial. En su lugar, este valor puede variar de un caso de uso a otro. De forma predeterminada, el umbral de error se establece en 5 %.

### ¿Cuánto tarda un estado de ejecución de flujo en actualizarse después de la creación de un nuevo flujo de datos?

Las ejecuciones de flujo no se generan instantáneamente y pueden tardar entre dos y tres minutos en actualizarse después de la `startTime`. La comprobación del estado de una ejecución de flujo, inmediatamente después de la creación de un nuevo flujo de datos, no devuelve información sobre el `lastRunDetails` como todavía no ha sucedido. Se recomienda permitir que el flujo de datos se genere unos minutos antes de comprobar el estado de la ejecución del flujo.