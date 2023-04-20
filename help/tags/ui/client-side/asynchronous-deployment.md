---
title: Implementación asíncrona
description: Obtenga información sobre cómo implementar de forma asíncrona las bibliotecas de Adobe Experience Platform Launch en su sitio web.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 98%

---

# Implementación asíncrona {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Implementación asíncrona"
>abstract="Si esta opción está habilitada, cuando se analiza esta etiqueta de script, el explorador debe comenzar a cargar el archivo JavaScript, pero en lugar de esperar a que se cargue y ejecute la biblioteca, continuará analizando y procesando el resto del documento. Esto puede mejorar el rendimiento de la página web, pero tiene implicaciones importantes en cuanto a cómo se ejecutan determinadas reglas. Consulte la documentación para obtener más detalles."

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

El rendimiento y la implementación sin bloqueo de las bibliotecas de JavaScript requeridas por nuestros productos es cada vez más importante para los usuarios de Adobe Experience Cloud. Las herramientas como [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) recomiendan a los usuarios cambiar su forma de implementar las bibliotecas de Adobe en el sitio. Este artículo explica cómo utilizar las bibliotecas de JavaScript de Adobe de forma asíncrona.

## Síncrónica frente a asíncrona

### Implementación sincrónica

A menudo, las bibliotecas se cargan sincrónicamente en la etiqueta `<head>` de una página. Por ejemplo:

```markup
<script src="example.js"></script>
```

De forma predeterminada, el explorador analiza el documento y llega a esta línea y, a continuación, comienza a recuperar el archivo JavaScript del servidor. El explorador espera hasta que se devuelve el archivo y después analiza y ejecuta el archivo JavaScript. Por último, continúa analizando el resto del documento HTML.

Si el analizador encuentra la etiqueta `<script>` antes de procesar contenido visible, se retrasa la visualización del contenido. Si el archivo JavaScript que se carga no es absolutamente necesario para mostrar contenido a los usuarios, está exigiendo a los visitantes de forma innecesaria que esperen al contenido. Cuanto más grande sea la biblioteca, mayor será el tiempo de espera. Por este motivo, las herramientas de evaluación de rendimiento del sitio web como [!DNL Google PageSpeed] o [!DNL Lighthouse] suelen marcar los scripts cargados sincrónicamente.

Las bibliotecas de administración de etiquetas pueden crecer rápidamente si tienen que administrar muchas etiquetas.

### Implementación asíncrona

Puede cargar cualquier biblioteca de forma asíncrona añadiendo un atributo `async` a la etiqueta `<script>`. Por ejemplo:

```markup
<script src="example.js" async></script>
```

Esto indica al explorador que, cuando se analiza esta etiqueta de script, el explorador debe comenzar a cargar el archivo JavaScript, pero en lugar de esperar a que se cargue y ejecute la biblioteca, debe continuar analizando y procesando el resto del documento.

## Consideraciones para la implementación asíncrona

Como se ha descrito anteriormente, en las implementaciones síncronas, el explorador pausa el análisis, y el procesamiento de la página mientras se carga y ejecuta la biblioteca de etiqueta de Adobe Experience Platform. En implementaciones asíncronas, por el contrario, el explorador continúa analizando y procesando la página mientras se carga la biblioteca. Se debe tener en cuenta la variabilidad de cuándo puede finalizar la carga de la biblioteca de etiquetas en relación con el análisis de páginas y su renderización.

Primero, debido a que la biblioteca de etiqueta puede terminar de cargarse antes o después de haber analizado y ejecutado la parte inferior de la página, ya no debería llamar a `_satellite.pageBottom()` desde el código de página (`_satellite` no estará disponible hasta que se haya cargado la biblioteca). Esto se explica en [Carga asíncrona del código incrustado de etiquetas](#loading-the-tags-embed-code-asynchronously).

Segundo, la biblioteca de etiqueta puede terminar de cargarse antes o después de que se produzca el evento [`DOMContentLoaded`](https://developer.mozilla.org/es-ES/docs/Web/Events/DOMContentLoaded) del explorador (DOM preparado).

Debido a estos dos puntos, vale la pena mostrar cómo funcionan los tipos de evento [Library Loaded](../../extensions/client/core/overview.md#library-loaded-page-top), [Page Bottom](../../extensions/client/core/overview.md#page-bottom), [DOM Ready](../../extensions/client/core/overview.md#page-bottom), y [Window Loaded](../../extensions/client/core/overview.md#window-loaded) desde la extensión principal al cargar una biblioteca de etiqueta de forma asíncrona.

Si la propiedad de etiqueta contiene las cuatro reglas siguientes:

* Regla A: utiliza el tipo de evento Library Loaded
* Regla B: utiliza el tipo de evento Page Bottom
* Regla C: utiliza el tipo de evento DOM Ready
* Regla D: utiliza el tipo de evento Window Loaded

Independientemente de cuándo termine la carga de la biblioteca de etiquetas, se garantiza que se ejecutan todas las reglas y que se ejecutan en el orden siguiente:

Regla A → Regla B → Regla C → Regla D

Aunque siempre se aplica ese orden, algunas reglas se pueden ejecutar inmediatamente cuando la biblioteca de etiqueta termina de cargarse, mientras que otras pueden ejecutarse posteriormente. Lo siguiente ocurre cuando termina de cargarse la biblioteca de etiquetas:

1. La Regla A se ejecuta inmediatamente.
1. Si el evento de explorador `DOMContentLoaded` (DOM Ready) ya ha ocurrido, la Regla B y la Regla C se ejecutan inmediatamente. De lo contrario, la Regla B y la Regla C se ejecutan más adelante cuando se produce el evento [`DOMContentLoaded`](https://developer.mozilla.org/es-ES/docs/Web/Events/DOMContentLoaded).
1. Si el evento [`load`](https://developer.mozilla.org/es-ES/docs/Web/Events/load) del explorador (Window Loaded) ya se ha producido, la Regla D se ejecuta inmediatamente. De lo contrario, la regla D se ejecuta más adelante cuando se produce el evento [`load`](https://developer.mozilla.org/es-ES/docs/Web/Events/load). Tenga en cuenta que, si ha instalado la biblioteca de etiqueta según las instrucciones, la biblioteca de etiqueta *siempre* termina de cargarse antes de que se produzca el evento [`load`](https://developer.mozilla.org/es-ES/docs/Web/Events/load) del explorador.

Al aplicar estos principios a su propio sitio web, tenga en cuenta lo siguiente:

* **Una regla con el tipo de evento Library Loaded podría ejecutarse antes de que la capa de datos se cargue completamente.** Esto puede provocar que las acciones de la regla se ejecuten aunque falten ciertos datos. ya que los datos aún no estaban disponibles en la página. Estos tipos de problemas se pueden mitigar mediante el ajuste de la configuración de la regla. Como ejemplo, en lugar de tener una regla activada por el tipo de evento Library Loaded, puede utilizar el tipo de evento Custom Event o Direct Call activado por el código de página en cuanto termine de cargar la capa de datos.
* **El tipo de evento Page Bottom no proporciona un valor especial cuando la biblioteca se carga de forma asíncrona.**  En su lugar, puede usar Library Loaded, DOM Ready, Window Loaded u otros tipos de eventos.

Si ve que las cosas suceden sin orden, es probable que haya problemas de temporización. Es posible que las implementaciones que requieran una sincronización precisa necesiten utilizar detectores de eventos y el tipo de evento Custom Event o Direct Call para hacer que sus implementaciones sean más sólidas y coherentes.

## Carga asíncrona del código incrustado de etiquetas

Las etiquetas proporcionan un conmutador para activar la carga asíncrona al crear un código incrustado cuando se configura un [entorno](../publishing/environments.md). También puede configurar la carga asíncrona por su cuenta:

1. Agregue un atributo async a la etiqueta `<script>` para cargar el script de forma asíncrona.

   Para el código incrustado de etiquetas, significa cambiar esto:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   por esto:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Elimine cualquier código que pueda haber añadido anteriormente al final de la etiqueta:

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Este código indica a Platform que el analizador del explorador ha llegado al final de la página. Debido a que es probable que las etiquetas no se hayan cargado y ejecutado antes de este tiempo, la llamada a los resultados de `_satellite.pageBottom()` en un error y el tipo de evento Page Bottom puede no comportarse según lo esperado.
