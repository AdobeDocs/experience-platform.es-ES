---
title: Información general sobre la extensión de audio y vídeo de Adobe Medium Analytics (3.x SDK) for Audio and Video
description: Obtenga información acerca de la extensión de etiqueta de Adobe Media Analytics (SDK 3.x) para audio y vídeo en Adobe Experience Platform.
exl-id: 7289d57d-7e7f-4832-9469-3b5a62183a32
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 96%

---

# Extensión de Adobe Media Analytics (SDK 3.x) para audio y vídeo

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Utilice esta documentación para obtener información sobre la instalación, configuración y implementación de la extensión de audio y vídeo de Adobe Media Analytics (3.x SDK) (extensión Media Analytics). Se incluyen las opciones disponibles al utilizar esta extensión para generar una regla, así como ejemplos y vínculos a muestras.

La extensión Media Analytics (MA) agrega el SDK principal de JavaScript Media SDK (SDK Media 3.x). Esta extensión proporciona la funcionalidad para agregar la instancia de seguimiento `Media` a un sitio o proyecto de etiquetas. La extensión de MA requiere dos extensiones adicionales:

* [Extensión de Analytics](../analytics/overview.md)
* [Extensión de Experience Cloud ID](../id-service/overview.md)

>[!IMPORTANT]
>
>Esta extensión se implementa con Media SDK 3.x, que no es compatible con Media SDK 2.x. Si su página ya utiliza Media SDK 2.x, utilice [Adobe Media Analytics para la extensión](../media-analytics/overview.md) de audio y vídeo en lugar de esta extensión.

Después de incluir las tres extensiones mencionadas arriba en su proyecto de etiquetas, puede continuar de una de las dos maneras siguientes:

* Use las API de `Media` desde la aplicación web
* Incluya o cree una extensión específica del reproductor que asigne eventos específicos del reproductor de medios a las API en la instancia de seguimiento de `Media`. Esta instancia se expone a través de la extensión de MA.

## Instale y configure la extensión de MA

* **Instalación:** Para instalar la extensión MA, abra la propiedad de extensión, seleccione **[!UICONTROL Extensiones > Catálogo]**, pase el cursor sobre la extensión **[!UICONTROL Adobe Media Analytics (SDK 3.x) para audio y vídeo]**, y seleccione **[!UICONTROL Instalar]**.

* **Configuración:** Para configurar la extensión MA, abra la pestaña [!UICONTROL Extensiones], coloque el cursor del ratón sobre la extensión y seleccione **[!UICONTROL Configurar]**:

![Configuración de la extensión MA](../../../images/ext-ma-config.png)

### Opciones de Configuration:

| Opción | Descripción |
| :--- | :--- |
| Servidor API de colección | Define el Media Collection API Server (póngase en contacto con su representante de Adobe para obtener este servidor) |
| Versión de aplicación | La versión del SDK/aplicación del reproductor de medios |
| Nombre del reproductor | Nombre del reproductor de medios en uso, por ejemplo, &quot;AVPlayer&quot;, &quot;HTML5 Player&quot;, &quot;Mi reproductor personalizado&quot; |
| Canal | Propiedad del nombre del canal |
| Registro de depuración | Habilitar o deshabilitar el registro |
| Habilitar SSL | Habilitar o deshabilitar el envío de pings a través de HTTPS |
| Exportar API a objeto de ventana | Habilitar o deshabilitar la exportación de las API de Media Analytics al ámbito global |
| Nombre de variable | Una variable que utiliza para exportar las API de Media Analytics en el objeto `window` |

**Recordatorio:** La extensión de MA requiere las extensiones de [Analytics](../analytics/overview.md) y de [Experience Cloud ID](../id-service/overview.md). También debe agregar estas extensiones a la propiedad de extensión y configurarlas.

## Uso de la extensión MA

### Uso de una página web/aplicación JS

La extensión MA exporta las API de medios al objeto window global activando la configuración Exportar API al objeto window en la página [!UICONTROL Configuración]. Exporta las API bajo el nombre de la variable configurada. Por ejemplo, si el nombre de la variable está configurado para ser `ADB`, se puede acceder a las API de medios a través de `window.ADB.Media`.

>[!IMPORTANT]
>
>La extensión de MA exporta las API solo cuando `window["CONFIGURED_VARIABLE_NAME"]` no está definido y tampoco anula las variantes existentes.

1. **API de medios:** `window["CONFIGURED_VARIABLE_NAME"].Media`

   Esto expone todas las API y constantes de Media SDK: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. **Crear instancia de rastreador de medios:** `window["CONFIGURED_VARIABLE_NAME"].Media.getInstance`

   **Valor arrojado:** instancia de `Media` Tracker para hacer el seguimiento de una sesión de medios.

   ```javascript
   var Media = window["CONFIGURED_VARIABLE_NAME"].Media;
   
   var tracker = Media.getInstance();
   ```

1. Con la instancia de Media Tracker, siga la [documentación de la API de JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) para implementar el seguimiento de medios.

Puede obtener el reproductor de muestra aquí: [Reproductor de muestra MA](https://github.com/Adobe-Marketing-Cloud/media-sdks/tree/master/samples/launch/js/3.x). El reproductor de muestra actúa como referencia para exhibir cómo utilizar la extensión MA para admitir Media Analytics directamente desde una aplicación web.


### Uso de otras extensiones

La extensión de MA expone `media` como módulo compartido a otras extensiones. (Para obtener más información sobre los módulos compartidos, consulte [Shared Modules documentation](../../../extension-dev/web/shared.md).)

>[!IMPORTANT]
>
>Solo se puede acceder a los módulos compartidos desde otras extensiones. Es decir, una aplicación web/JavaScript no puede acceder a los módulos compartidos ni utilizar `turbine` (consulte la muestra de código que aparece a continuación) fuera de una extensión.

1. **API de medios:** `media` módulo compartido

   Esto expone todas las API y constantes de Media SDK: [https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)

1. Cree la instancia de seguimiento de Media como se indica a continuación:

   **Valor arrojado:** instancia de `Media` Tracker para hacer el seguimiento de una sesión de medios.

   ```javascript
   var Media =
     turbine.getSharedModule('adobe-media-analytics', 'media');
   
   var tracker = Media.getInstance();
   ```

1. Con la instancia de Media Tracker, siga la [documentación de la API de JS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/index.html) para implementar el seguimiento de medios.

>[!NOTE]
>
>**Prueba:** En esta versión, para probar la extensión debe cargarla en [Platform](../../../extension-dev/submit/upload-and-test.md), donde tiene acceso a todas las extensiones dependientes.
