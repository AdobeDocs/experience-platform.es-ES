---
title: Introducción al desarrollo de extensiones
description: Empiece a desarrollar sus propias extensiones de etiqueta en Adobe Experience Platform.
exl-id: 3925b928-0180-4a4f-aaa6-42f342089560
source-git-commit: 077d3ac5a34f052ef6293927d67e3cc8afb27563
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 80%

---

# Introducción al desarrollo de extensiones

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Para ayudarle con la utilización y la creación de extensiones, utilizaremos la herramienta de andamiaje de código abierto proporcionada por ingenieros de Adobe para crear los archivos y la estructura de archivos necesarios para su paquete de extensión con el objetivo de que lo único que le quede por hacer sea la parte más valiosa: escribir el código.

## Requisitos previos

* Instale [Node.js](https://nodejs.org/es/download/).

## Configuración de extensiones

Cree un directorio en el que se almacenarán los archivos de su extensión.

```shell
mkdir example && cd example
```

Esta guía utiliza la herramienta de andamiaje de extensiones para crear la estructura inicial de la extensión para que los desarrolladores puedan empezar a codificar rápidamente. Este proceso se puede realizar manualmente sin la herramienta de andamiaje si así lo desea.

Ejecute la herramienta andamiaje.

```shell
npx @adobe/reactor-scaffold
```

La herramienta andamiaje le pedirá algunas opciones de configuración iniciales como se indica a continuación:

* Nombre para mostrar: nombre visible de la extensión.
* Plataforma: especifica si la extensión está desarrollada para la web, dispositivos móviles o Edge
* Versión: versión de la extensión.
* Descripción: breve descripción del propósito de la extensión.
* Autor: nombre del autor de la extensión.

>[!NOTE]
> En el caso de las extensiones móviles, se plantean varias preguntas con respecto a la estructura de las aplicaciones de Android y iOS.

A continuación, la herramienta de andamiaje proporcionará opciones para la creación de la estructura de la extensión:

* [Vista de configuración de la extensión](./configuration.md): vista y archivo HTML a través de los cuales una extensión recopila la configuración global de un usuario.
* [Tipos de evento](./web/event-types.md): define una actividad para su observación. Por ejemplo, puede saber cuándo un usuario se desplaza rápidamente por el contenido o cuándo interactúa con un elemento de la página. Los eventos se pueden utilizar en reglas para realizar acciones.
* [Tipos de condición](./web/condition-types.md): los tipos de condición evalúan si algo es verdadero o falso.
Por ejemplo, esto puede devolver si el explorador del usuario es Chrome, si está utilizando un iPad o si el usuario se encuentra en un dominio específico.
* [Tipos de acciones](./web/action-types.md): acción que se realizará cuando se produzca un evento. Por ejemplo, enviar una señalización de análisis, mostrar una oferta, guardar una cookie o abrir un chat de asistencia.
* [Tipos de elementos de datos](./web/data-element-types.md): un tipo de elemento de datos recupera un fragmento de datos. Estos datos pueden encontrarse en el almacenamiento local, en una cookie, en un elemento DOM o en una ubicación personalizada.
* [Módulos compartidos](./web/shared.md) (solo web): un módulo compartido es un mecanismo mediante el cual las extensiones pueden comunicarse con otras extensiones.
* [Vistas](./web/views.md): cada tipo de evento, condición, acción o elemento de datos puede proporcionar una vista que permita al usuario proporcionar la configuración.
* URL de Exchange (solo web y Edge): cuando se publique una extensión en el catálogo público de Adobe, proporcione la URL de la lista aquí.
* Ruta del icono: Una ruta a un archivo de icono para la extensión.

>[!NOTE]
>
>* Las ejecuciones posteriores de la herramienta de andamiaje se saltarán la configuración inicial.
>* Se puede añadir más de un evento, condición o acción.
>* Solo puede existir una vista de configuración.

## Pasos siguientes

* Siga la [Información general del proceso de envío](./submit/overview.md) y prepárese para [validar](./submit/upload-and-test.md#validate) y [cargar](./submit/upload-and-test.md#integration) su extensión para probarla dentro del ecosistema de etiquetas.
