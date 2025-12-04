---
title: Uso de Adobe Experience Platform Assurance
description: En esta guía se explica cómo utilizar Adobe Experience Platform Assurance una vez que se ha instalado e implementado.
exl-id: 872c83d1-82e8-40d8-9b66-3e51a91a955f
source-git-commit: f8576e7f7e1da7351f7860cba27d5d09d0161132
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 28%

---

# Uso de Adobe Experience Platform Assurance

En este tutorial se explica cómo utilizar Adobe Experience Platform Assurance. Para obtener instrucciones sobre cómo instalar e implementar la extensión de Adobe Experience Platform Assurance, lea el tutorial sobre la [implementación de la extensión Assurance](./implement-assurance.md).

## Creación de sesiones

Después de iniciar sesión en la [IU de Assurance](https://experience.adobe.com/assurance), puede seleccionar **[!UICONTROL Create Session]** para comenzar a crear una sesión.

![El botón Crear sesión aparece resaltado y muestra dónde puede crear una sesión.](./images/using-assurance/create-session.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Create New Session]** con dos opciones para crear una sesión:

### Conexión de enlace profundo

Seleccione esta opción para generar una URL de sesión única, un código QR y un PIN. Escanee el código QR o abra manualmente el vínculo de sesión en la aplicación e introduzca el PIN para establecer la conexión.

Seleccione **[!UICONTROL Deep link connect]** y continúe seleccionando **[!UICONTROL Start]**.

![Se seleccionó la opción de conexión de vínculo profundo del cuadro de diálogo Crear nueva sesión.](./images/using-assurance/create-new-session-deep-link.png)

Ahora puede escribir un nombre para identificar la sesión y, a continuación, proporcionar **[!UICONTROL Base URL]** (URL de vinculación profunda para la aplicación). Después de proporcionar estos detalles, seleccione **[!UICONTROL Next]**.

>[!INFO]
>
>La URL base es la definición raíz utilizada para iniciar la aplicación desde una URL. Se genera una URL de sesión mediante la cual puede iniciar la sesión de Assurance. Un valor de ejemplo podría tener el siguiente aspecto: `myapp://default` En el campo **[!UICONTROL Base URL]**, escriba la definición de vínculo profundo base de su aplicación.

![Se muestran los campos de entrada de nombre de sesión y dirección URL base.](./images/using-assurance/create-session-form-deep-link.png)

### Conexión rápida

Almacene en déclencheur una conexión desde la aplicación y el dispositivo aparecerá en una lista de dispositivos disponibles. Seleccione **[!UICONTROL Quick connect]** para crear la sesión de Assurance.

#### Requisitos previos

Antes de usar Conexión rápida, asegúrese de que su aplicación tenga las versiones y la implementación de SDK necesarias:

**Requisitos de Android SDK:**

- Mobile Core v3.1.0 o posterior
- Adobe Journey Optimizer v3.1.0 o posterior
- Adobe Experience Platform Assurance v3.0.4 o posterior

**Requisitos de iOS SDK:**

- Mobile Core v5.2.0 o posterior
- Adobe Journey Optimizer v5.1.1 o posterior
- Adobe Experience Platform Assurance v5.0.0 o posterior

**Implementación:**

Su aplicación debe implementar la API [`startSession` &#x200B;](https://developer.adobe.com/client-sdks/home/base/assurance/api-reference/#startsession-quick-connect) para almacenar en déclencheur la conexión de Assurance. Esta llamada de API generalmente se incluye en un conjunto de acciones o se activa dentro de la aplicación.

#### Creación de una sesión de conexión rápida

![Se seleccionó la opción Crear nueva sesión del cuadro de diálogo que muestra Conexión rápida.](./images/using-assurance/create-new-session-quick-connect.png)

Seleccione **[!UICONTROL Quick connect]** y continúe seleccionando **[!UICONTROL Start]**. Verá la interfaz del selector de dispositivos:

1. **Almacene en Déclencheur la conexión de Assurance**: en su aplicación móvil o implementación, almacene en déclencheur la acción que inicia la conexión de Assurance mediante la API `startSession`. Esto hará que su dispositivo sea reconocible.

2. **Seleccione y conecte su dispositivo**. Una vez que su dispositivo aparezca en la lista de dispositivos disponibles, selecciónelo y haga clic en **[!UICONTROL Connect]**.

![La interfaz del selector de dispositivos de Conexión rápida muestra los dispositivos disponibles.](./images/using-assurance/quick-connect-device-picker.png)

## Conexión a una sesión

Los pasos para conectarse dependen del tipo de sesión que esté utilizando:

### Sesiones de conexión de enlace profundo

Para sesiones creadas con **[!UICONTROL Deep Link Connect]**:

1. Vaya a la página de detalles de la sesión (para sesiones existentes) o continúe desde la creación de la sesión para ver el vínculo, el código QR y el PIN
2. Utilice la aplicación de cámara del dispositivo para escanear el código QR o copie el vínculo y ábralo en la aplicación
3. Cuando se inicie la aplicación, verá superpuesta la pantalla de entrada de PIN. Escriba el PIN y presione **[!UICONTROL Connect]**

![Se muestra un cuadro de diálogo con las opciones para conectarse a la sesión de Assurance.](./images/using-assurance/deep-link-connection.png)

### Sesiones de conexión rápida

Para las sesiones creadas con **[!UICONTROL Quick Connect]** (identificables mediante una dirección URL de sesión que comienza con `adobeassurance://`), la conexión se produce automáticamente a través de la interfaz del selector de dispositivos:

1. Vaya a la página de detalles de la sesión (para sesiones existentes) o continúe desde la creación de la sesión
2. En la sección **[!UICONTROL Connect Device]** verá la interfaz del selector de dispositivos
3. Almacene en déclencheur el conjunto de acciones de su aplicación para que el dispositivo sea reconocible
4. Seleccione su dispositivo de la lista y haga clic en **[!UICONTROL Connect]**

![Interfaz de selector de dispositivos que muestra los dispositivos disponibles para conectar.](./images/using-assurance/quick-connect-device-picker.png)

### Comprobando conexión

Puede comprobar que la aplicación está conectada a Assurance cuando se muestra el icono Adobe Experience Platform (Adobe rojo “A”) en la aplicación.

## Exportación de una sesión

Para exportar una sesión de Assurance, en la página de detalles de sesiones de la aplicación, seleccione **[!UICONTROL Export to JSON]** en una sesión:

![Exportación de una sesión](./images/using-assurance/export-session.png)

La opción de exportación respeta los resultados del filtro de búsqueda y solo exporta los eventos mostrados en la vista de eventos. Por ejemplo, si buscó eventos de &quot;seguimiento&quot; y después seleccionó **[!UICONTROL Export to JSON]**, solo se exportan los resultados de eventos de &quot;seguimiento&quot;.