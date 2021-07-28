---
title: Versiones
description: Obtenga información acerca del concepto de las compilaciones y cómo funcionan en Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 58%

---

# Versiones

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Una compilación es el conjunto de archivos que contiene todo el código que se ejecuta en el dispositivo cliente.

Es una combinación de los cambios especificados dentro de la biblioteca, así como todo lo que se haya enviado, aprobado o publicado antes.

La compilación consiste en archivos de código del lado del cliente que se hacen referencia entre sí. Estos archivos se envían a su ubicación de alojamiento con el entorno y el host que ha elegido para la biblioteca. El código que implementa en el sitio señala a esta misma ubicación para que los archivos se puedan cargar cuando un usuario acceda al sitio o a la aplicación.

## Contenido del archivo

Una biblioteca define un conjunto discreto de recursos de etiquetas (extensiones, reglas y elementos de datos) que deben incluirse en ella.

Una compilación contiene todo el código del módulo (proporcionado por los desarrolladores de la extensión) y la configuración (introducida por usted) necesaria para alimentar los recursos contenidos en la biblioteca. Por ejemplo, si una extensión proporciona acciones que no se utilizan en las reglas, el código para realizar esas acciones no está contenido en la compilación.

Las compilaciones se dividen en el archivo de biblioteca principal y en muchos archivos más pequeños. En el código incrustado se hace referencia al archivo de biblioteca principal, que se carga en la página en el tiempo de ejecución. Contiene:

* El motor de reglas
* Toda la configuración de extensiones
* Todo el código y la configuración de los elementos de datos
* Todo el código y la configuración de los eventos de reglas
* Todo el código y la configuración de las condiciones
* El código y la configuración de los eventos para cualquier regla que tenga como evento Library Loaded o Page Bottom (ya que sabemos que se necesitan inmediatamente).

Los archivos más pequeños contienen código y configuración para acciones individuales que se cargan en la página según sea necesario. Cuando se activa una regla y se evalúan sus condiciones de forma que sea necesario ejecutar las acciones, el código y la configuración necesarios para esa acción específica se recuperan de uno de los archivos más pequeños. Esto significa que solo se carga el código necesario para realizar las acciones necesarias en la página, lo que hace que la biblioteca principal sea lo más pequeña posible.

## Formato del archivo

El formato de archivo predeterminado para las compilaciones es un paquete de archivos que contienen todo el código necesario para que las extensiones, los elementos de datos y las reglas se ejecuten de la manera que desee.

Sin embargo, en determinados casos puede preferir un archivo .zip que incluya los archivos en lugar del archivo ejecutable con código del lado del cliente. Por ejemplo, puede crear un archivo si usted mismo aloja su propia compilación y desea utilizar la compilación en otra implementación. Si proporciona cualquier cosa en la ruta autoalojada al campo de biblioteca, puede guardar el entorno. Junto con su nuevo código, se crea un enlace a la descarga archivada. Una vez creada la biblioteca, tiene la opción de implementar un archivo zip en Akamai y descargarlo desde `assets.adobedtm.com/...`.

>[!NOTE]
>
>No existe nada en esa ubicación hasta que realice una compilación.

Independientemente del formato de archivo, la compilación siempre se envía a la ubicación especificada por el host.

Para completar una versión, seleccione una biblioteca y haga clic en la opción Versión que está disponible en ese nivel del proceso de publicación (Build for Development, Build for Staging, etc.).

## Minificación

La minificación reduce el consumo de ancho de banda y mejora la velocidad al eliminar los datos que son innecesarios para la ejecución desde un archivo.

Para aumentar el rendimiento, Platform minifica todo, incluso:

* La biblioteca de etiquetas principal
* El código de módulo proporcionado por los desarrolladores de extensiones como parte de una extensión
* El código personalizado proporcionado por los usuarios de Platform 

>[!NOTE]
>
>Si el código de módulo y el código personalizado ya se han minificado, Platform vuelve a minificarlos. Esta segunda minificación no ofrece beneficios adicionales, pero no causa ningún daño y hace que Platform sea menos complejo y fácil de mantener.

Cualquier código del lado del cliente proporcionado señala a la versión minificada del código. Esto se ve en los nombres de archivo que siguen la convención de nomenclatura estándar para los archivos minificados:

`launch-%environment_id%.min.js`

Si desea ver el código no minificado, elimine .min del nombre del archivo:

`launch-%environment_id%.js`

Si un desarrollador de extensiones proporciona código minificado con su extensión, Platform no proporciona código no minificado en la compilación no minificada. Del mismo modo, si un usuario de Platform coloca el código minificado en un cuadro de código personalizado, dicho código se sigue minificando en compilaciones no minificadas. Platform no desminifica nada.

Para obtener más información sobre la minificación, consulte [este artículo de la ruta de acceso a la bandeja](https://blog.stackpath.com/glossary/minification/).

Al realizar una compilación, construirá primero la biblioteca no minificada y, a continuación, reducirá el tamaño de toda la biblioteca de una vez.
