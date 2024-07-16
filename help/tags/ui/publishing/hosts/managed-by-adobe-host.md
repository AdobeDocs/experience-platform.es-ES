---
title: Información general sobre alojamientos administrados por Adobe
description: Obtenga información acerca de la opción de alojamiento predeterminada para implementar compilaciones de biblioteca de etiquetas en Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 88%

---

# Información general sobre alojamientos administrados por Adobe

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Los hosts administrados por Adobe son la configuración de host predeterminada para implementar las compilaciones de biblioteca de etiquetas en Adobe Experience Platform. Al crear una nueva propiedad a través de la interfaz de usuario de recopilación de datos, se crea un host predeterminado administrado por Adobe.

Con los hosts administrados por Adobe, las versiones de biblioteca se entregan a una red de distribución de contenido (CDN) de terceros con la que Adobe ha firmado un contrato. Estas CDN funcionan de forma independiente del Adobe, por lo que, incluso cuando Platform se esté manteniendo o no funcione, el código implementado seguirá funcionando normalmente en sus sitios y aplicaciones. El código incrustado de un host administrado por Adobe hace referencia al archivo de biblioteca principal en la CDN para que un dispositivo cliente pueda recuperar los archivos en tiempo de ejecución.

Este documento proporciona información general sobre los hosts administrados por Adobe en Platform y proporciona los pasos para crear un nuevo host administrado por Adobe en la IU.

## Akamai

Actualmente, el proveedor de CDN principal de Adobe es [Akamai](https://www.akamai.com/es). La CDN robusta de Akamai está diseñada para ofrecer contenido a un público global y de gran volumen de visitantes en línea. La CDN ejecuta redes redundantes de nodos de carga equilibrada y optimizados para ofrecer contenido lo más rápido posible a visitantes ubicados en todo el mundo.

En particular, Akamai ejecuta más de 137 000 servidores en más de 1150 redes de 87 países. En cuanto a la redundancia, la red de distribución de contenido (CDN) no solo enruta de un servidor a otro, sino que también puede enrutar de un nodo de servidores a otro según sea necesario. En otras palabras, cada nodo consta de varios servidores, de modo que un servidor que se está apagando nunca se convierte en un problema, ya que los demás servidores del mismo nodo pueden asumir el control.

Si se desactiva un nodo completo, Akamai se proporciona desde el nodo más cercano con el mismo contenido almacenado en la caché. Los nodos se seleccionan de forma dinámica en función de la ubicación del visitante, la carga de tráfico y otros factores, de forma que el contenido se proporciona de forma fiable desde el nodo local más adecuado para cada visitante.

Los archivos alojados en Akamai tienen un dominio de `assets.adobedtm.com`. Se puede hacer referencia a esto de forma segura o no (`http://` o `https://`) según su nombre en el `<script>` código incrustado.

>[!WARNING]
>
>Si la biblioteca no está disponible en la red de Akamai, Platform no puede evitar errores que puedan surgir como consecuencia de ella.

## Caché de versión de la biblioteca

Al utilizar hosts administrados por Adobe, las versiones de la biblioteca se almacenan en la caché en dos ubicaciones:

* [Almacenamiento en caché de Edge](#edge)
* [Almacenamiento en caché del explorador](#browser)

### Almacenamiento en caché de Edge {#edge}

El propósito principal de una CDN es distribuir de forma inteligente el contenido a servidores geográficamente más cercanos a los usuarios finales, de modo que los dispositivos cliente puedan recuperarlo con mayor rapidez. Las CDN logran esto haciendo que las copias del contenido estén disponibles en servidores distribuidos geográficamente en todo el mundo (&quot;nodos Edge&quot;).

Una vez que la versión se ha implementado en el host administrado por Adobe, la CDN distribuye la compilación en varios servidores centralizados (&quot;orígenes&quot;), que luego envía copias de la versión a varios nodos Edge del mundo para el almacenamiento en caché. Las versiones en caché de la versión almacenadas en estos nodos Edge se proporcionan finalmente a los dispositivos cliente.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Para los hosts administrados por Adobe, la primera biblioteca publicada en cualquier entorno nuevo puede tardar hasta cinco minutos en propagarse a toda la CDN.

Cuando un nodo perimetral recibe una solicitud para un archivo específico (como la compilación de su biblioteca), el nodo comprueba primero la hora de caducidad del archivo. Si el tiempo no ha caducado, el nodo perimetral proporciona la versión en caché. Si la hora ha caducado, el nodo perimetral solicita una copia nueva desde el origen más cercano, proporciona esa copia actualizada y, a continuación, la almacena en caché con una nueva hora de caducidad.

>[!NOTE]
>
>Además del almacenamiento en caché de nodos Edge, también puede haber redes intermedias (como redes corporativas o móviles) que realizan su propio almacenamiento en caché. Si las compilaciones no se almacenan en caché como se espera, estas redes pueden ser la causa subyacente.

#### Invalidación de caché de Edge {#invalidation}

Al cargar una nueva compilación de biblioteca, las cachés de todos los nodos perimetrales aplicables se invalidan. Esto significa que cada nodo considera que su versión en caché no es válida, independientemente de la fecha en que haya recuperado una copia nueva. La próxima vez que un nodo perimetral reciba una solicitud para ese archivo, el nodo recuperará una copia nueva desde el origen.

Debido a que Akamai tiene varios servidores de origen que replican archivos entre ellos y que no hay forma de saber qué origen obtuvo el archivo primero, es posible que estas solicitudes de nodo produzcan un origen que no tenga la versión más reciente. Luego almacenaría en caché la versión anterior de nuevo. Para evitar que esto ocurra, se hacen varias anulaciones de caché para cada nueva compilación en los siguientes intervalos:

* Inmediatamente después de la carga
* 5 minutos después de la carga
* 60 minutos después de la carga

Estas anulaciones de caché escalonadas dan tiempo a los grupos de servidores de origen para replicar la última versión del archivo entre ellos, de modo que todos tengan la última versión cuando se recupere el archivo.

### Almacenamiento en caché del explorador {#browser}

Las compilaciones de biblioteca también se almacenan en caché en el explorador mediante el uso del encabezado `cache-control` HTTP. Al utilizar hosts administrados por Adobe, no controla los encabezados que aparecen en las respuestas de API, por lo que se utiliza el Adobe predeterminado para el almacenamiento en caché. En otras palabras, no puede utilizar encabezados personalizados para hosts administrados por Adobe. Si necesita un `cache-control` encabezado personalizado, puede considerar [el alojamiento propio](self-hosting-libraries.md).

El tiempo de caducidad de la compilación de la biblioteca en caché del explorador (determinado por el encabezado `cache-control`) variará según el entorno de etiquetas que utilice:

| Entorno | `cache-control` valor |
| --- | --- |
| Desarrollo | `max-age=0, no-cache, no-store` |
| Ensayo | `max-age=0, no-cache, no-store` |
| Producción | `max-age=3600` |

Como se indica en la tabla anterior, el almacenamiento en caché del navegador no es compatible con los entornos de desarrollo y ensayo. Como tal, no debe utilizar los códigos incrustados de desarrollo o ensayo en contextos de alto tráfico o producción.

Los encabezados de control de caché solo se aplican a la compilación de la biblioteca principal. Los recursos secundarios debajo de la biblioteca principal siempre se consideran nuevos y, por lo tanto, no es necesario almacenarlos en caché en el explorador.

## Uso del hosting gestionado por Adobe en la IU de

La primera vez que se crea una propiedad en la IU de Platform o en la IU de recopilación de datos, se crea automáticamente un host administrado por Adobe. De forma predeterminada, todos los entornos disponibles que tienen propiedades utilizables inmediatamente también se asignan al host administrado por Adobe.

>[!NOTE]
>
>Si el host administrado por Adobe predeterminado no está asignado de todos los entornos, se puede eliminar. Si desea volver a un host administrado por Adobe después de hacerlo, puede crear un nuevo host siguiendo estos pasos:
>
>1. Seleccione la pestaña **[!UICONTROL Hosts]** de la propiedad y, a continuación, seleccione **[!UICONTROL Añadir host]**.
>1. Proporcione un nombre para el host, seleccione **[!UICONTROL Gestionado por Adobe]** como tipo de host y, a continuación, seleccione **[!UICONTROL Guardar]**.
>
>A continuación, puede volver a asignar sus entornos al host administrado por Adobe según sus preferencias.

## Pasos siguientes

Este documento proporciona información general sobre el alojamiento administrado por Adobe para bibliotecas de etiquetas en Adobe Experience Platform. Para obtener información sobre otras opciones de hosting, consulte la siguiente documentación:

* [Hosting SFTP](./sftp-host.md)
* [Bibliotecas de alojamiento propio](./self-hosting-libraries.md)

Para obtener más información sobre cómo administrar los hosts de sus entornos, consulte la [guía de entornos](../environments.md).
