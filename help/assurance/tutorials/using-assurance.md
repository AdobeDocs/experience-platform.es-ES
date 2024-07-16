---
title: Uso de Adobe Experience Platform Assurance
description: En esta guía se explica cómo utilizar Adobe Experience Platform Assurance una vez que se ha instalado e implementado.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 100%

---

# Uso de Adobe Experience Platform Assurance

En este tutorial se explica cómo utilizar Adobe Experience Platform Assurance. Para obtener instrucciones sobre cómo instalar e implementar la extensión de Adobe Experience Platform Assurance, lea el tutorial sobre la [implementación de la extensión Assurance](./implement-assurance.md).

## Creación de sesiones

Después de iniciar sesión en la [IU de Assurance](https://experience.adobe.com/assurance), puede seleccionar **[!UICONTROL Crear sesión]** para empezar a crear una sesión.

![El botón Crear sesión aparece resaltado y muestra dónde puede crear una sesión.](./images/using-assurance/create-session.png)

Aparece el cuadro de diálogo **[!UICONTROL Crear nueva sesión]**. Revise las instrucciones dadas y proceda a seleccionar **[!UICONTROL Iniciar]**.

![Se muestra el cuadro de diálogo Crear nueva sesión, que muestra instrucciones sobre cómo utilizar Assurance.](./images/using-assurance/create-new-session.png)

Ahora puede escribir un nombre para identificar la sesión y, a continuación, proporcionar una **[!UICONTROL URL básica]** (URL de vinculación profunda para la aplicación). Después de proporcionar estos detalles, seleccione **[!UICONTROL Siguiente]**.

>[!INFO]
>
>La URL base es la definición raíz utilizada para iniciar la aplicación desde una URL. Se genera una URL de sesión mediante la cual puede iniciar la sesión de Assurance. Un valor de ejemplo podría tener el siguiente aspecto: `myapp://default` en el campo **[!UICONTROL URL básica]**, escriba la definición de vínculo profundo base de su aplicación.

![Se muestra el flujo de trabajo completo de creación de una nueva sesión.](./images/using-assurance/create-session.gif)

## Conexión a una sesión

Después de crear una sesión, asegúrese de ver que el cuadro de diálogo **[!UICONTROL Crear nueva sesión]** ahora le muestra un vínculo, un código QR y un PIN.

![Se muestra un cuadro de diálogo con las opciones para conectarse a la sesión de Assurance.](./images/using-assurance/create-new-session-pin.png)

Si aparece este cuadro de diálogo, puede utilizar la aplicación de la cámara del dispositivo para escanear el código QR y abrir la aplicación, o bien copiar el vínculo y abrirlo en la aplicación. Cuando se inicie la aplicación, debería ver superpuesta la pantalla de introducción del PIN. Escriba el PIN del paso anterior y pulse **[!UICONTROL Conectar]**.

Puede comprobar que la aplicación está conectada a Assurance cuando se muestra el icono Adobe Experience Platform (Adobe rojo “A”) en la aplicación.

![Se muestra el flujo de trabajo completo de conexión de la aplicación a una sesión de Assurance.](./images/using-assurance/connect-session.gif)

## Exportación de una sesión

Para exportar una sesión de Assurance, en la página de detalles de las sesiones de la aplicación, seleccione **[!UICONTROL Exportar a JSON]** en una sesión.

![Exportación de una sesión](./images/using-assurance/export-session.png)

La opción de exportación respeta los resultados del filtro de búsqueda y solo exporta los eventos mostrados en la vista de eventos. Por ejemplo, si ha buscado eventos de “seguimiento” y, a continuación, selecciona **[!UICONTROL Exportar a JSON]**, solo se exportan los resultados del evento “seguimiento”.
