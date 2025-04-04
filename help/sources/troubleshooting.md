---
keywords: Experience Platform;inicio;temas populares;fuentes;ingesta;resolución de problemas;fuentes resolución de problemas;fuentes faq;conectores de origen;conectores de origen;conectores de origen;preguntas frecuentes;conectores de origen;resolución de problemas;
solution: Experience Platform
title: Solución de problemas de orígenes
description: Este documento proporciona respuestas a las preguntas frecuentes acerca de las fuentes de Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Guía de resolución de problemas de orígenes

Este documento proporciona respuestas a las preguntas frecuentes acerca de las fuentes de Adobe Experience Platform. Para obtener información y resolver problemas relacionados con otros servicios de [!DNL Experience Platform], incluidos los que se encuentran en todas las API de [!DNL Experience Platform], consulte la [guía de solución de problemas de Experience Platform](../landing/troubleshooting.md).

## Preguntas frecuentes

A continuación se muestra una lista de respuestas a las preguntas frecuentes acerca de las fuentes.

### ¿Tengo que realizar cambios en la configuración de seguridad de la red para habilitar las fuentes?

Es posible que tenga que realizar una lista de permitidos de ciertas direcciones IP para habilitar las fuentes. Para obtener más información, lea la documentación del conector de origen específico.

### ¿Qué tipos de autenticación admiten las fuentes?

Las fuentes se pueden autenticar mediante cadenas de conexión, nombres de usuario y contraseñas, o tokens y claves de acceso. Puede encontrar detalles específicos acerca de los tipos de autenticación admitidos en la documentación del conector de origen especificado.

### ¿Por qué fallan todas mis ejecuciones de flujo recientes?

Si observa que todas las ejecuciones de flujo recientes están fallando, es posible que las credenciales hayan cambiado o caducado. Para solucionar ese problema, intente actualizar la conexión con las credenciales más recientes.

### ¿Qué tipos de archivo se admiten?

Actualmente los tipos de archivo admitidos son archivos delimitados, JSON y Parquet.

### ¿Cuáles son las restricciones en los nombres y tamaños de archivo?

A continuación se muestra una lista de restricciones que debe tener en cuenta para los archivos de orígenes.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).
- El número máximo de archivos por lote es de 1500, con un tamaño máximo de lote de 100 GB.
- El número máximo de propiedades o campos por fila es de 10 000.
- El número máximo de lotes que se pueden enviar por usuario y minuto es 2000.

### ¿Qué tipos de datos son compatibles?

Los tipos de datos admitidos son enteros, cadenas, booleanos, objetos datetime, matrices y objetos.

### ¿Qué formatos de fecha y hora son compatibles?

El sistema de fuentes admite una amplia variedad de formatos de fecha y hora al ingerir datos. Encontrará más información sobre los formatos de fecha y hora admitidos en la sección de fechas de la [guía de administración de formato de datos](../data-prep/data-handling.md#dates) en la documentación de la preparación de datos.

### ¿Cómo formateo las matrices en archivos CSV, JSON y Parquet?

Los archivos JSON y Parquet admiten matrices de forma nativa. Para estructuras planas, como CSV, no se admiten matrices. Sin embargo, las cadenas con varios valores se pueden dividir en una matriz mediante funciones de preparación de datos como explode y join. Encontrará más información sobre estas funciones de preparación de datos en la [guía de funciones de preparación de datos](../data-prep/functions.md#string)

### ¿Qué fuentes admiten la ingesta parcial?

Todas las fuentes de ingesta por lotes admiten la ingesta parcial. Sin embargo, las fuentes de ingesta de flujo continuo no admiten la ingesta parcial.

### ¿Cuándo debo usar la ingesta parcial?

La ingesta parcial debería usarse si **no** tiene restricciones, como que todo el archivo se ingrese en Experience Platform. Alternativamente, se debe utilizar la ingesta parcial si no le importa ingerir datos que puedan contener errores dentro de ella.

### ¿Cuál es el umbral de error típico de ingesta parcial?

No hay ningún &quot;umbral de error típico&quot; para la ingesta parcial. En su lugar, este valor puede variar de un caso de uso a otro. De forma predeterminada, el umbral de error se establece en 5 %.

### ¿Cuánto tiempo tarda un estado de ejecución de flujo en actualizarse después de la creación de un nuevo flujo de datos?

Las ejecuciones de flujo no se generan de forma instantánea y pueden tardar entre dos y tres minutos en actualizarse después de su `startTime` designado. La comprobación del estado de una ejecución de flujo, inmediatamente después de la creación de un nuevo flujo de datos, no devuelve información sobre `lastRunDetails` de la ejecución de flujo, ya que aún no se ha producido. Se recomienda permitir que el flujo de datos se genere durante unos minutos antes de comprobar el estado de la ejecución del flujo.