---
title: Información general sobre la extensión YouTube Video Tracking
description: Obtenga información sobre la extensión de etiqueta de seguimiento de vídeo de YouTube en Adobe Experience Platform.
exl-id: 703f7b04-f72f-415f-80d6-45583fa661bc
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 78%

---

# Información general sobre la extensión YouTube Video Tracking

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

**Requisitos previos**

Cada propiedad de etiqueta de Adobe Experience Platform requiere que se instalen y configuren las siguientes extensiones desde la pantalla Extensiones:

* Adobe Analytics
* Servicio de ID de visitante de Experience Cloud
* Extensión principal

Use el [&quot;Incrustar un reproductor con una etiqueta \&lt;iframe\>&quot;](https://developers.google.com/youtube/player_parameters#Manual_IFrame_Embeds) fragmento de código de los documentos de desarrollador de Google en la HTML de cada página web en la que se va a procesar un reproductor de vídeo.

La versión 2.0.1 de esta extensión admite la incrustación de uno o más vídeos de YouTube en una sola página web mediante la inserción de un atributo `id` con un valor único en la etiqueta iframe, y anexando `enablejsapi=1` y `rel=0` al final del valor del atributo `src` si no se ha incluido ya, por ejemplo. Por ejemplo:

`<iframe id="player1" width="560" height="315" src="https://www.youtube.com/embed/xpatB77BzYE?enablejsapi=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>`

Tenga en cuenta que esta extensión también está diseñada para comprobar dinámicamente si hay un valor de atributo de ID único, como `player1`, sin importar si existen los parámetros de cadena de consulta `enablejsapi` y `rel`, y si sus valores esperados son correctos. Como resultado, la etiqueta de scripts de YouTube se puede añadir a una página web con el atributo o sin él, `id` y si los parámetros de cadena de consulta `enablejsapi` y `rel` se incluyen o no.

>[!NOTE]
>
>En páginas con varios vídeos, tenga en cuenta que cada vídeo utiliza el mismo conjunto de configuraciones en la regla de etiquetas que se ejecuta en esa página. Por ejemplo, si crea una regla con un evento que se activa cuando se completa el 50 % del vídeo, cada vídeo de la página activará la regla en el punto de referencia del 50 %.

La extensión se basa en la siguiente lógica para reescribir los iFrames:

```javascript
document.onreadystatechange = function () {
 if (document.readyState === 'complete') {
```

Por lo tanto, hay un ligero parpadeo después de que se carga la página. Este comportamiento es predecible.

## Elementos de datos

Hay seis elementos de datos disponibles dentro de la extensión y ninguno de ellos requiere configuración.

* **Posición del cursor de reproducción:** Registra el lugar, en segundos, de la posición del cursor de reproducción en la cronología del vídeo, cuando se le hace referencia en una regla de etiquetas.
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
* **Seguimiento personalizado de referencias:** Se activa cuando el vídeo alcanza el porcentaje de umbral de vídeo especificado. Por ejemplo, si un vídeo dura 60 segundos y el punto de referencia especificado está en el 50 %, el evento se activará cuando la posición del cursor de reproducción esté en 30 segundos. El seguimiento de puntos de referencia se aplica tanto a las reproducciones iniciales como a las nuevas reproducciones. Tenga en cuenta que si el usuario busca en un punto de referencia, el evento no se activará. Los eventos de referencia solo se activan cuando el cursor de reproducción cruza la ubicación del punto de referencia calculada en la cronología y se está reproduciendo el vídeo.
* **Búfer de vídeo:** Se activa cuando el reproductor descarga una cierta cantidad de datos antes de que comience a reproducir el vídeo.
* **Vídeo finalizado:** Se activa cuando un vídeo termina por completo.

## Uso

Se puede configurar una regla de etiqueta para cada evento de vídeo (los siete eventos enumerados arriba). Cree una regla de etiqueta específica para cada evento que desee rastrear. Si no desea rastrear un evento, simplemente omita crear una regla para él.

Las reglas tienen tres acciones:

* **Establecer variables:** Configure las variables de Adobe Analytics (asigne a todos los elementos de datos incluidos todos o algunos de ellos).
* **Enviar señalización:** Envíe la señalización Adobe Analytics como una llamada de seguimiento de vínculos personalizados y proporcione un valor &quot;Nombre del vínculo&quot;.
* **Borrar variables:** Borre las variables de Adobe Analytics.

## Ejemplo de regla de etiquetas para Inicio de vídeo

Se deben incluir los siguientes objetos de extensión de vídeo.

* **Eventos**: &quot;Inicio de vídeo&quot; (con este evento, la regla se activa cuando el visitante comienza a reproducir un vídeo de YouTube).

* **Condición**: ninguna

* **Acciones**: use la acción **Extensión de Analytics** para &quot;Establecer variables&quot;, para asignar:

   * El evento de inicio de vídeo,
   * Un prop/eVar para el elemento de datos de la duración del vídeo
   * Un prop/eVar para el elemento de datos de ID de vídeo
   * Un prop/eVar para el elemento de datos del nombre del vídeo
   * Un prop/eVar para el elemento de datos de la URL de vídeo

  A continuación, incluya la acción &quot;Enviar señalización&quot; (`s.tl`) con el nombre de vínculo &quot;inicio de vídeo&quot;, seguida de una acción &quot;Borrar variables&quot;.

>[!TIP]
> 
>En el caso de las implementaciones en las que no se pueden usar varios eVars o props para cada elemento de vídeo, los valores de los elementos de datos se pueden concatenar en Experience Platform, analizarse en informes de clasificación con la herramienta Generador de reglas de clasificación, como se explica en [https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=es) y, luego, aplicarse como un segmento en Analysis Workspace.

Para concatenar valores de información del vídeo, cree un nuevo elemento de datos denominado Metadatos de vídeo y prográmelo para extraer todos los elementos de datos de vídeo (antes mencionados) y combinarlos. Por ejemplo:

```javascript
var r = [];

r.push('YouTube'); //Player Name
r.push(_satellite.getVar('Video ID'));
r.push(_satellite.getVar('Video Name'));
r.push(_satellite.getVar('Video Duration'));
r.push(_satellite.getVar('Extension Version'));

return r.join('|');
```

Para obtener más información sobre cómo crear y aprovechar los elementos de datos de forma eficaz en Experience Platform, lea la documentación de [elementos de datos](../../../ui/managing-resources/data-elements.md).
