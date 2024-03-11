---
title: Instalación del SDK web mediante la extensión de etiqueta
description: Haga referencia a la biblioteca del SDK web mediante la recopilación de datos de Adobe Experience Cloud.
exl-id: ba8348c9-f642-4230-9f7f-4496d4154d83
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Instalación del SDK web mediante la extensión de etiqueta

Adobe ofrece una extensión de etiquetas específica para implementar y configurar el SDK web. Este método de implementación es el principal recomendado por el Adobe para implementar y mantener el código de recopilación de datos.

Una vez que conozca el [requisitos previos](overview.md)Además, puede implementar la extensión de etiqueta del SDK web siguiendo los pasos siguientes:

## Instalación de la extensión dentro de una etiqueta

1. Iniciar sesión en [experience.adobe.com](https://experience.adobe.com) usando sus credenciales de Adobe ID.
1. Vaya a **[!UICONTROL Recopilación de datos]** > **[!UICONTROL Etiquetas]**.
1. Seleccione la propiedad de etiqueta que desee o cree una.
1. Vaya a **[!UICONTROL Extensiones]**, luego seleccione la **[!UICONTROL Catálogo]** pestaña.
1. Busque e instale el **[!UICONTROL SDK web de Adobe Experience Platform]** extensión.
1. Seleccione la zona protegida y la secuencia de datos adecuadas para cada entorno y haga clic en **[!UICONTROL Guardar]**.

Consulte la documentación sobre cómo [configuración de la extensión de etiqueta del SDK web](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) para obtener más información.

## Publicar el código de etiqueta en desarrollo

La extensión del SDK web ya está instalada para esta etiqueta. Ahora puede publicar el código de etiqueta para utilizarlo en un entorno de desarrollo.

1. Vaya a **[!UICONTROL Flujo de publicación]**, luego seleccione **[!UICONTROL Añadir biblioteca]**.
1. Asigne a esta biblioteca cualquier nombre que desee, como &quot;Agregar biblioteca del SDK web&quot;. Configure las variables [!UICONTROL Entorno] menú desplegable a &quot;Desarrollo&quot;.
1. Seleccionar **[!UICONTROL Añadir todos los recursos modificados]**, luego haga clic en **[!UICONTROL Guardar y generar en desarrollo]**.

## Instalación del código del cargador en el sitio

Ahora que el código de etiqueta está publicado, puede agregarlo a su sitio web.

1. Vaya a **[!UICONTROL Entornos]** A continuación, haga clic en el icono Cuadro situado junto a &quot;Desarrollo&quot; para abrir una ventana modal que contenga instrucciones de instalación para este entorno.
1. Copie el código incrustado de y péguelo en la variable `<head>` de su sitio web.

## Complete la implementación y publique en producción

Consulte la [Información general sobre la extensión SDK web](../../tags/extensions/client/web-sdk/overview.md) para obtener más información sobre la propia extensión, y [Información general sobre etiquetas](../../tags/home.md) para obtener más información sobre cómo navegar por la interfaz de etiquetas.
