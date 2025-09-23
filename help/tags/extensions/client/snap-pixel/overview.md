---
title: Información general sobre la extensión Snap Pixel
description: Aprenda a utilizar la extensión de etiquetas Snap Pixel para capturar interacciones de usuario valiosas en Adobe Experience Platform.
last-substantial-update: 2025-09-17T00:00:00Z
source-git-commit: d846bd5dee5ce0ee8836dc25e20d9fd070714114
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Información general sobre la extensión [!DNL Snap Pixel]

[[!DNL Snap Pixel]](https://businesshelp.snapchat.com/s/article/snap-pixel-about) es una herramienta de análisis basada en JavaScript que te permite capturar valiosas interacciones del usuario en tu sitio web. Las acciones importantes de los visitantes, como compras, suscripciones u otras conversiones, se envían automáticamente a [Administrador de anuncios](http://ads.snapchat.com/), lo que le permite medir y optimizar el rendimiento de sus anuncios, campañas, rutas de conversión y mucho más.

La extensión de etiquetas [!DNL Snap Pixel] le permite integrar la funcionalidad [!DNL Snap Pixel] directamente en las bibliotecas de etiquetas del lado del cliente. Esta documentación describe cómo instalar la extensión e implementar sus funciones dentro de las reglas de administración de etiquetas.

La extensión de etiquetas [!DNL Snap Pixel] optimiza la integración de la funcionalidad [!DNL Snap Pixel] en las bibliotecas de etiquetas existentes del lado del cliente. Esta documentación describe cómo instalar la extensión y configurar sus características dentro de las [reglas](../../../ui/managing-resources/rules.md) de administración de etiquetas.

## Requisitos previos {#prerequisites}

Para usar la extensión, necesitará una cuenta de [!DNL Snap] válida con acceso a [!DNL Ads Manager]. Debe [crear un nuevo [!DNL Snap Pixel]](https://forbusiness.snapchat.com/advertising/snap-pixel#about) y copiar su ID de píxel para configurar la extensión de su cuenta. Si ya tiene un(a) [!DNL Snap Pixel], simplemente puede usar su ID.

Se recomienda usar [!DNL Snap Pixel] junto con [!DNL Snap Conversions API] para enviar los mismos eventos tanto del lado del cliente como del lado del servidor. Este método puede ayudar a recuperar eventos que puede que no sean capturados por el [!DNL Snap Pixel] solamente. Consulte la extensión de la API de [[!DNL Snap] Conversiones para el reenvío de eventos](../../server/snap/overview.md) para ver los pasos que debe seguir para integrarla en las implementaciones del lado del servidor. Tenga en cuenta que su organización debe tener acceso a [reenvío de eventos](../../../ui/event-forwarding/overview.md) para utilizar la extensión del lado del servidor.

## Instalación de la extensión {#install}

Para instalar la extensión [!DNL Snap Pixel], vaya a la IU de recopilación de datos o a la IU de Experience Platform y seleccione **[!UICONTROL Etiquetas]** en el panel de navegación izquierdo. Aquí, seleccione una propiedad a la que añadir la extensión o cree una nueva propiedad.

Una vez que haya seleccionado o creado la propiedad deseada, seleccione **[!UICONTROL Extensiones]** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **[!UICONTROL Catálogo]**. Busque la tarjeta [!UICONTROL Snap Pixel] y, a continuación, seleccione **[!UICONTROL Instalar]**.

![Se está seleccionando el botón [!UICONTROL Instalar] para la extensión [!UICONTROL Píxel de ajuste] en la IU de recopilación de datos.](./images/install.png)

En la vista de configuración que aparece, debe proporcionar el ID de píxel que copió anteriormente para vincular la extensión a su cuenta de. Puede pegar el ID directamente en la entrada o seleccionar un elemento de datos existente en su lugar.

Cuando termine, seleccione **[!UICONTROL Guardar]**.

![El identificador [!DNL Pixel] proporcionado como elemento de datos en la vista de configuración de la extensión.](./images/configure.png)

La extensión está instalada y ahora puede emplear sus distintas acciones en las reglas de etiquetas.

## Configuración de una regla de etiqueta {#rule}

[!DNL Snap Pixel] admite un conjunto de eventos estándar predefinidos, cada uno con contextos específicos y parámetros aceptados. Las acciones de regla disponibles en la extensión [!DNL Snap Pixel] se alinean con estos tipos de evento, lo que facilita la categorización y configuración de los eventos que se envían a [!DNL Snap] según su tipo.

Para fines de demostración, esta sección muestra cómo generar una regla que envíe eventos de compra a [!DNL Snap].

Para empezar, cree una nueva regla de etiquetas y defina las condiciones según sea necesario. Al configurar las acciones de la regla, elija [!DNL Snap Pixel] como extensión y, a continuación, seleccione **[!UICONTROL Enviar evento de compra]** como tipo de acción.

Una vez que haya terminado de configurar la acción [!UICONTROL Enviar evento de compra], seleccione **[!UICONTROL Conservar cambios]** para agregarla a la configuración de regla.

![El tipo de acción [!UICONTROL Enviar evento de compra] seleccionado para una regla en la IU de recopilación de datos.](./images/action-type.png)

Cuando esté satisfecho con la configuración general de la regla, seleccione **[!UICONTROL Guardar en biblioteca]**.

Para aplicar las actualizaciones, publique una nueva etiqueta [build](../../../ui/publishing/builds.md) para habilitar los cambios en la biblioteca.

## Confirmar que [!DNL Snap] está recibiendo datos {#confirm}

Una vez que la compilación actualizada se haya implementado en el sitio web, puede verificar que los datos se envíen según lo esperado activando eventos de conversión en el explorador y comprobando que aparezcan en [[!DNL Snap Events Manager]](https://businesshelp.snapchat.com/s/article/events-manager).

## Próximos pasos {#next-steps}

Esta guía explica cómo enviar datos a [!DNL Snap] mediante la extensión de etiqueta [!DNL Snap Pixel]. Si también planea enviar eventos del lado del servidor a [!DNL Snap], puede proceder a instalar y configurar [[!DNL Snap Conversions API event forwarding extension]](../../server/snap/overview.md).
