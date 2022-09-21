---
title: Volver a publicar una biblioteca
description: Obtenga información sobre cómo volver a publicar una biblioteca de etiquetas anterior en Adobe Experience Platform.
exl-id: 026b01f2-a93d-4e8a-9ed2-47c4f011e70f
source-git-commit: 77313baabee10e21845fa79763c7ade4e479e080
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 93%

---

# Volver a publicar una biblioteca

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las cinco bibliotecas más recientes publicadas en el entorno de producción en una propiedad web se conservan para recuperarlas más adelante. Esta función es útil cuando se encuentra un error en la biblioteca de producción y se necesita volver a un estado correcto anterior inmediatamente.

El proceso de recuperación depende de la configuración del entorno en el momento en que se publicó originalmente la biblioteca. Esto es importante porque la recuperación de una biblioteca archivada no cambia nada en el sitio activo, mientras que la recuperación de una biblioteca normal sí lo haría.

Las opciones disponibles son las siguientes:

* **Host: Administrado por Adobe, Archivo: Desactivado:** Si utiliza el host administrado por Adobe y no archiva la biblioteca, puede volver a publicar estas bibliotecas antiguas.

* **Host: Administrado por Adobe, Archivo: Activado:** Si utiliza el host administrado por Adobe y archiva la biblioteca, puede descargar estas bibliotecas antiguas.

* **Host: SFTP. Archivo: Activado o desactivado:** Si utiliza el host SFTP, se da por hecho que dispone de sus propias estrategias de archivo y no hay opciones de recuperación disponibles.

Las opciones de recuperación para propiedades móviles aún no están disponibles.

## Volver a publicar

Cada entorno de etiquetas proporciona un vínculo a un archivo de biblioteca. Se puede hacer referencia a cualquier biblioteca que cree en ese entorno con ese vínculo.

Cuando se crea en un entorno de ensayo o desarrollo, la compilación antigua se limpia y se implementa la nueva. Para su entorno de producción, este vínculo se actualiza para que indique la compilación más reciente, pero las cinco compilaciones más recientes se conservan antes de que se limpien.

Las cinco compilaciones más recientes de su entorno de producción son las que se pueden recuperar.

Cuando vuelve a publicar una biblioteca anterior, Platform actualiza el vínculo de entorno para que indique una de estas compilaciones anteriores que aún no se han limpiado.  Platform también envía una solicitud de depuración a la caché de nodos perimetrales de la CDN para indicar que la biblioteca se ha actualizado y que se debe recuperar una copia nueva del origen.

Esto significa que, cuando vuelve a publicar una biblioteca anterior:

* No se realizan cambios en ninguno de los recursos (ni en las revisiones históricas) de la propiedad de etiquetas

* La forma en que los entornos de ensayo y desarrollo calculan qué se encuentra en fase de desarrollo no varía

Tenga en cuenta la situación específica cuando se restaure una versión anterior debido a un problema con una regla específica. La revisión de regla que está en proceso de producción podría, por ejemplo, tener tres revisiones anteriores. Cuando ve esa regla en la interfaz de usuario para corregirla, sigue mostrando los cambios guardados más recientes en lugar de los que están actualmente en producción.

Por este motivo, Platform le notifica que una propiedad está en estado de republicación como recordatorio de que lo que está viendo en la interfaz de usuario de recopilación de datos está más alejado de la fase de producción de lo habitual. Esta notificación se puede omitir y aparece una vez por cada sesión de explorador la primera vez que se ve la propiedad.

### Volver a publicar una biblioteca anterior

![Volver a publicar una biblioteca](images/retrieve_republish.png)

Desde la pantalla Publicación:

1. Busque la biblioteca en la columna Publicado que desee volver a publicar.
1. Seleccione los puntos suspensivos (`...`) en la esquina superior derecha de la tarjeta de biblioteca.
1. Seleccione **[!UICONTROL Volver a publicar]**.

## Descargar

La descarga de una biblioteca archivada es más sencilla. No hace referencia directa a estos archivos .zip en ninguna parte, por lo que puede descargar la biblioteca más antigua en su equipo y ejecutar el proceso habitual.

### Cómo descargar una biblioteca anterior

![Descargar una biblioteca](images/retrieve_download.png)

Desde la pantalla Publicación:

1. Busque la biblioteca en la columna Publicado que desee descargar.
1. Seleccione los puntos suspensivos (`...`) en la esquina superior derecha de la tarjeta de biblioteca.
1. Seleccione **[!UICONTROL Descargar]**.
