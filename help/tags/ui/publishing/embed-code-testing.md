---
title: Prueba de códigos incrustados con Adobe Experience Platform Debugger
description: Aprenda a utilizar Experience Platform Debugger para probar localmente los distintos códigos incrustados para Adobe Experience Platform en el sitio web.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 58%

---

# Prueba de códigos incrustados con Adobe Experience Platform Debugger

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un grupo de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Según vaya realizando cambios en las compilaciones de su biblioteca de etiquetas en Adobe Experience Platform, deberá probarlos antes de implementar la compilación en el entorno de producción. Si no tiene un entorno de ensayo o desarrollo dedicado para su sitio web, puede utilizar Adobe Experience Platform Debugger para probar localmente los distintos códigos incrustados del sitio.

## Requisitos previos

Este tutorial requiere una comprensión práctica del uso de entornos y códigos incrustados para etiquetas. Consulte la [información general de los entornos](./environments.md) para obtener más detalles.

Este tutorial también requiere que tenga instalada la extensión del explorador de Experience Platform Debugger. Experience Platform Debugger está disponible para el explorador Chrome. Utilice el siguiente vínculo para instalar la extensión antes de iniciar el tutorial:

* [Experience Platform Debugger para Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Abra Experience Platform Debugger en el sitio web

Utilice el explorador para ir al sitio web y abrir la extensión de Experience Platform Debugger. El sitio al que está conectado Experience Platform Debugger actualmente se muestra en la parte inferior de la ventana. Si las etiquetas se están ejecutando en el sitio, aparecerá en la pestaña [!UICONTROL Resumen].

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Si Experience Platform Debugger no se conecta en un principio, es posible que tenga que volver a cargar la pestaña del explorador que muestra el sitio web antes de intentarlo de nuevo.

## Reemplazar códigos incrustados

Una vez que Experience Platform Debugger se haya conectado a su sitio, seleccione **[!UICONTROL Launch]** en el panel de navegación izquierdo. Aquí puede ver información sobre la versión de la biblioteca que se está ejecutando en el sitio, incluido su entorno y las extensiones asociadas. Aquí, seleccione **[!UICONTROL Configuración]** para mostrar los controles para administrar códigos incrustados.

![](./images/embed-code-testing/launch-tab.png)

En [!UICONTROL Códigos incrustados de página], se muestra el código incrustado que está utilizando el sitio en este momento. Seleccione **[!UICONTROL Acciones]** en el lado derecho del código incrustado y, a continuación, seleccione **[!UICONTROL Reemplazar]**.

![](./images/embed-code-testing/replace.png)

Aparece una ventana emergente que le solicita que proporcione un código incrustado para reemplazar el actual. Tenga en cuenta que reemplazar el código incrustado con Experience Platform Debugger no cambia el código incrustado implementado en el sitio. En su lugar, solo reemplaza el código incrustado que se ejecuta localmente para que pueda probar y depurar su implementación.

Pegue el código incrustado que desee probar en el cuadro de texto proporcionado y, a continuación, seleccione **[!UICONTROL Aplicar]**.

![](./images/embed-code-testing/paste-code.png)

La pestaña **[!UICONTROL Configuración]** vuelve a aparecer y muestra que el código incrustado activo se ha sustituido por el que ha proporcionado. Ahora puede utilizar el explorador web para ver si el código incrustado que está probando funciona correctamente.

![](./images/embed-code-testing/code-replaced.png)

## Pasos siguientes

Este tutorial explica cómo cambiar localmente los códigos incrustados para realizar pruebas con Experience Platform Debugger. Consulte la [documentación de Experience Platform Debugger](../../../debugger/home.md) para obtener más información sobre sus diversas funciones.
