---
title: Información general sobre la extensión BrightCove Video Tracking
description: Obtenga información sobre la extensión de la etiqueta de seguimiento de vídeo BrightCove en Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 38%

---

# Información general sobre la extensión BrightCove Video Tracking

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

## Requisitos previos

Cada propiedad de etiqueta en Adobe Experience Platform necesita las siguientes extensiones instaladas y configuradas en la pantalla Extension:

* Adobe Analytics
* Servicio de ID de visitante de Experience Cloud
* Extensiones principales instaladas

Utilice el fragmento de código &quot;Código incrustado en la página (avanzado)&quot; en el HTML de cada página web en la que se va a procesar un reproductor de vídeo. El fragmento HTML &quot;Código incrustado en la página (avanzado)&quot; se encuentra en la [documentación de Brightcove](https://studio.support.brightcove.com/publish/choosing-correct-embed-code.html#inpage). El siguiente vínculo proporciona más información sobre [cómo generar código incrustado para reproductores de vídeo publicados y de vista previa](https://es.studio.support.brightcove.com/players/generating-player-embed-code.html).

Esta extensión versión 1.1.0 admite la incrustación de varios vídeos BrightCove en una sola página web. Si hay varias propiedades `id` dentro de las etiquetas incrustadas avanzadas, asegúrese de que cada una de ellas tenga valores únicos. Por ejemplo, `player1`, `player2`, etc.

>[!NOTE]
>
>En páginas con varios vídeos, cada vídeo utiliza el mismo conjunto de configuración en la regla de etiqueta que se ejecuta en esa página. Por ejemplo, si crea una regla con un evento que se activa cuando se completa el 50 % del vídeo, cada vídeo de la página activa la regla en el punto de referencia del 50 %.

Si la página web que utiliza esta extensión interactúa con el vídeo antes de que el script relevante se haya cargado completamente, puede realizar dos acciones para solucionar el problema. En primer lugar, la biblioteca de etiquetas se puede cargar sincrónicamente y, en segundo lugar, coloque el elemento `<script type="text/javascript">\_satellite.pageBottom();\</script\>` antes de que el vídeo se incruste en la página.

Consulte la [documentación de la API BrightCove](https://docs.brightcove.com/brightcove-player/1.x/Player.html#vjsplayer) para obtener más información sobre los métodos y eventos de componentes utilizados en esta extensión.

## Elementos de datos

Hay siete elementos de datos disponibles dentro de la extensión, y ninguno de ellos requiere configuración.

* **Posición del cabezal de reproducción:** cuando se llama a este elemento de datos dentro de una regla de etiqueta, se registra en segundos, el lugar de la posición del cursor de reproducción en la cronología del vídeo.
* **ID de cuenta de vídeo:** este elemento de datos registra el ID de la cuenta de Brightcove que publicó el vídeo.
* **Duración del vídeo:** este elemento de datos registra la duración total, en segundos, del contenido del vídeo. Además, se puede crear una métrica calculada en Analytics para convertir el número en segundos a minutos u horas.
* **Compatibilidad con anuncios de vídeo:** este elemento de datos especifica si el vídeo admite publicidades o no.
* **ID de vídeo:** este elemento de datos especifica el ID de BrightCove asociado al vídeo.
* **Nombre del vídeo:** este elemento de datos especifica el nombre descriptivo o informal del vídeo.
* **Etiquetas de vídeo:** este elemento de datos especifica las secuencias de comandos específicas asociadas al vídeo.

## Eventos

Hay siete eventos disponibles en la extensión. Solo el seguimiento de puntos de referencia personalizados requiere configuración.

* **Seguimiento de puntos de referencia personalizados:** este evento se activa cuando el vídeo alcanza el porcentaje de umbral de vídeo especificado. Por ejemplo, si un vídeo dura 60 segundos y el punto de referencia especificado es del 50 %, el evento se déclencheur en la marca de 30 segundos.

>[!NOTE]
>
>Tenga en cuenta que este evento se activa cada vez que se alcanza este punto de referencia. Por ejemplo, si el usuario alcanza la marca del 50 %, busca el vídeo antes de la marca del 50 % y luego vuelve a alcanzar la marca del 50 % y el activador se activa otra vez.

* **Vídeo completado:** este evento déclencheur cuando un vídeo se completa.
* **Metadatos cargados de vídeo:** este evento se activa cuando el reproductor ha recibido la duración inicial y la información de dimensión.
* **Pausa de vídeo:** este evento se activa cuando se pone en pausa el vídeo.
* **Reanudación del vídeo:** este evento se desencadena cuando se reanuda el contenido del vídeo tras un evento de pausa.
* **Cambio en la pantalla de vídeo:**  el evento se déclencheur cuando el vídeo entra o sale del modo de pantalla completa.
* **Inicio de vídeo:** este evento se activa cuando el contenido de vídeo se inicia por primera vez.

## Uso

Se puede configurar una regla de etiqueta para cada evento de vídeo (los siete eventos enumerados arriba). Cree una regla de etiqueta específica para cada evento que desee rastrear. Si no desea rastrear un evento, simplemente omita para crear una regla para él.

Las reglas tienen tres acciones:

1. Configuran las variables de Adobe Analytics. (Cree elementos de datos para todos o algunos de los elementos de datos enumerados arriba).
1. Envían la señalización de Adobe Analytics.
1. Borran las variables de Adobe Analytics.

## Ejemplo de regla de etiqueta para &quot;Inicio de vídeo&quot;

Se deben incluir los siguientes objetos de extensión de vídeo:

* **Eventos**

   1. &quot;Inicio de vídeo&quot;: Con este evento, la regla se activa cuando el visitante comienza a reproducir un vídeo de BrightCove.

* **Condición**

   1. Ninguna

* **Acciones**

   1. En una acción &quot;Set Variables&quot; de Analytics, establezca:

      * El evento del **Inicio de vídeo** (ejemplo: event17)
      * Una prop/eVar para el elemento de datos **Nombre del vídeo** (ejemplo: eVar (10)
      * Una prop/eVar para el elemento de datos **Duración del vídeo** (ejemplo: eVar (11)
      * Una prop/eVar para el elemento de datos **Lugar del vídeo actual** (ejemplo: eVar (12)
   1. Acción &quot;Send Beacon&quot; de Analytics (`s.tl`)
   1. Acción &quot;Clear Variables&quot; de Analytics


>[!TIP]
>
>Para aquellos que no deseen aprovisionar varias eVars o propiedades para cada elemento de vídeo, existe un método alternativo. Los valores de los elementos de datos se pueden concatenar dentro de la interfaz de usuario de la recopilación de datos. A continuación, se analizan en informes de clasificación mediante la herramienta de clasificación del generador de reglas . Consulte la documentación [Herramienta del Generador de reglas de clasificación](https://experienceleague.adobe.com/docs/analytics/components/classifications/classifications-rulebuilder/classification-rule-builder.html?lang=es) para obtener más información. Finalmente, se aplican como un segmento en Analysis Workspace.
>
>Para ello, cree un nuevo elemento de datos denominado, por ejemplo, &quot;Metadatos de vídeo&quot; y prográmelo para extraer todos los elementos de datos de vídeo (enumerados arriba) y concatenarlos juntos.

```javascript
var r = [];

r.push( \_satellite.getVar( &#39;Video ID&#39; ) );

r.push( \_satellite.getVar( &#39;Video Name&#39; ) );

r.push( \_satellite.getVar( &#39;Video Duraction&#39; ) );


return r.join(&#39;|&#39;);
```
