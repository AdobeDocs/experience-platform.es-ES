---
title: Información general sobre la extensión YouTube Video Tracking
description: Obtenga información sobre la extensión de la etiqueta de seguimiento de vídeo de YouTube en Adobe Experience Platform.
source-git-commit: 5da1fd18e0032c5e3d6695639f98a7ee683819f1
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 51%

---

# Información general sobre la extensión YouTube Video Tracking

>[!NOTE]
>
>Adobe Experience Platform Launch se está convirtiendo en un conjunto de tecnologías de recopilación de datos en Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

**Requisitos previos**

Cada propiedad de etiqueta en Adobe Experience Platform requiere que las siguientes extensiones estén instaladas y configuradas desde la pantalla Extensiones:

* Adobe Analytics
* Servicio de ID de visitante de Experience Cloud
* Extensión principal

Utilice el fragmento de código [&quot;Incrustar un reproductor utilizando una etiqueta \&lt;iframe\>&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) de los documentos de desarrollador de Google en el HTML de cada página web en la que se va a procesar un reproductor de vídeo.

Esta extensión, versión 2.0.1, admite la incrustación de uno o más vídeos de YouTube en una sola página web al insertar un atributo `id` con un valor único en la etiqueta de script de iframe y anexar `enablejsapi=1` y `rel=0` al final del valor de atributo `src`, si no se ha incluido ya. Por ejemplo:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Esta extensión también está diseñada para comprobar dinámicamente si hay un valor de atributo de ID único, como `player1`, independientemente de si existen los parámetros de cadena de consulta `enablejsapi` y `rel` y si los valores esperados son correctos. Como resultado, la etiqueta de scripts de YouTube se puede añadir a una página web con el atributo o sin él, `id` y si los parámetros de cadena de consulta `enablejsapi` y `rel` se incluyen o no.

>[!NOTE]
>
>En páginas con más de un vídeo, cada vídeo utiliza el mismo conjunto de configuración en la regla de etiqueta que se ejecuta en esa página. Por ejemplo, si crea una regla con un evento que se activa cuando se completa el 50 % del vídeo, cada vídeo de la página activará la regla en el punto de referencia del 50 %.

La extensión se basa en la siguiente lógica para reescribir los iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Por lo tanto, hay un ligero parpadeo después de que se cargue la página. Este comportamiento es predecible.

## Elementos de datos

Hay seis elementos de datos disponibles dentro de la extensión y ninguno de ellos requiere configuración.

* **Posición del cabezal de reproducción:** registra el lugar, en segundos, de la posición del cursor de reproducción en la cronología del vídeo, cuando se le llama dentro de una regla de etiqueta.
* **ID de vídeo:** Especifica el ID de YouTube asociado al vídeo.
* **Nombre del vídeo:** Especifica el nombre descriptivo o informal del vídeo.
* **Dirección URL del vídeo:** Arroja la URL de YouTube.com del vídeo que se está cargando o reproduciendo.
* **Duración del vídeo:** Registra la duración total, en segundos, del contenido de vídeo.
* **Versión de la extensión:** Este elemento de datos registra la versión de la extensión de seguimiento de YouTube, como “Video Tracking_YouTube_2.0.0”, por ejemplo.

## Eventos

Hay ocho eventos disponibles en la extensión, pero solo el seguimiento personalizado de puntos de referencia requiere configuración.

* **Listo para vídeo:** Se activa cuando se referencia el vídeo y está listo para reproducirse.
* **Inicio de vídeo:** Se activa cuando se inicia el vídeo por primera vez y cuando `player.getCurrentTime() === 0`
* **Nueva reproducción de vídeo:** Se activa cuando se referencia el vídeo y se vuelve a reproducir después del inicio. Este activador se iniciará en cada nueva reproducción.
* **Pausa de vídeo:** Se activa cuando se pausa el vídeo.
* **Reanudación del vídeo:** Se activa cuando se reanuda el vídeo y cuando `player.getCurrentTime() !== 0`
* **Seguimiento personalizado de referencias:** Se activa cuando el vídeo alcanza el porcentaje de umbral de vídeo especificado. Por ejemplo, si un vídeo dura 60 segundos y el punto de referencia especificado es del 50 %, el evento se déclencheur cuando la posición del cabezal de reproducción sea igual a 30 segundos. El seguimiento de puntos de referencia se aplica tanto a las reproducciones iniciales como a las nuevas reproducciones. Tenga en cuenta que si el usuario busca en un punto de referencia, el evento no se activará. Los eventos de punto de referencia solo se activan cuando el cabezal de reproducción cruza la ubicación del punto de referencia calculado en la cronología y se reproduce el reproductor de vídeo.
* **Búfer de vídeo:** Se activa cuando el reproductor descarga una cierta cantidad de datos antes de que comience a reproducir el vídeo.
* **Vídeo finalizado:** Se activa cuando un vídeo termina por completo.

## Uso

Se puede configurar una regla de etiqueta para cada evento de vídeo (los siete eventos enumerados arriba). Cree una regla de etiqueta específica para cada evento que desee rastrear. Si no desea rastrear un evento, simplemente omita para crear una regla para él.

Las reglas tienen tres acciones:

* **Establecer variables:** Configure las variables de Adobe Analytics (asigne a todos los elementos de datos incluidos todos o algunos de ellos).
* **Enviar baliza:** Envíe la baliza de Adobe Analytics como llamada de seguimiento de vínculo personalizado y proporcione un valor en el nombre del vínculo.
* **Borrar variables:** Borre las variables de Adobe Analytics.

## Ejemplo de regla de etiqueta para &quot;Inicio de vídeo&quot;

Se deben incluir los siguientes objetos de extensión de vídeo.

* **Eventos**: &quot;Inicio de vídeo&quot; (Este evento hace que la regla se active cuando el visitante comienza a reproducir un vídeo de YouTube).

* **Condición**: ninguna

* **Acciones**: Utilice la acción **Analytics extension** para &quot;Set Variables&quot; para asignar:

   * El evento de inicio de vídeo,
   * Un prop/eVar para el elemento de datos de la duración del vídeo
   * Un prop/eVar para el elemento de datos de ID de vídeo
   * Un prop/eVar para el elemento de datos del nombre del vídeo
   * Un prop/eVar para el elemento de datos de la URL de vídeo

   A continuación, incluya la acción &quot;Send Beacon&quot; (`s.tl`) con el nombre del vínculo &quot;video start&quot;, seguida de una acción &quot;Clear Variables&quot;.

>[!TIP]
> 
>En implementaciones en las que no se pueden usar varias eVars o propiedades para cada elemento de vídeo, los valores de los elementos de datos se pueden concatenar dentro de Platform y analizarse en los informes de clasificación mediante la herramienta Generador de reglas de clasificación , tal como se explica en [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=es), y luego aplicarse como un segmento en Analysis Workspace.

Para concatenar valores de información del vídeo, cree un nuevo elemento de datos denominado Metadatos de vídeo y prográmelo para que extraiga todos los elementos de datos de vídeo (mostrados arriba) y combinarlos. Por ejemplo:

```javascript
var r = ””;

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```
