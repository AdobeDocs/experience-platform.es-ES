---
title: Vista de depuración push
description: Esta guía detalla información sobre la vista Depuración push en Adobe Experience Platform Assurance.
exl-id: a9558ee2-2e80-4b0d-ab45-2020be85e634
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Vista de Push Debug

La vista de depuración push dentro de Adobe Experience Platform Assurance permite validar la configuración push de la aplicación y enviar un mensaje de prueba al dispositivo.

## Clientes

![Clientes push](./images/push-debug-view/clients.png)

La lista desplegable de clientes contiene una lista de cada cliente único que se ha conectado a esta sesión de Assurance. Un cliente es un dispositivo único o una instalación de aplicación única para un dispositivo. Por ejemplo, si se han conectado un dispositivo Android y un dispositivo iOS a la sesión, esos clientes aparecerían en la lista desplegable Clientes.

Después de reinstalar y volver a conectar la aplicación en un dispositivo, aparecerá otro cliente. Si ya existe un dispositivo con ese nombre, la nueva lista desplegable anexará un #2 al nombre.

Esta vista solo está habilitada para un único cliente, por lo que al seleccionar un cliente diferente se cambian los detalles en la pantalla.

## Validar configuración

El **[!UICONTROL Validar configuración]** valida y proporciona detalles adicionales sobre la configuración push de la aplicación. Existen tres paneles que realizan validaciones. Mostrarán una marca de verificación verde si todas las validaciones se realizan correctamente. Si hay tres marcas de verificación verdes, la aplicación se ha configurado correctamente para la mensajería push, está escribiendo tokens push en el perfil de usuario y tiene una superficie de aplicación asociada configurada.

Si algo no funciona como se espera, aparecerá una alerta con detalles sobre cómo solucionar ese problema:

![Estado no válido](./images/push-debug-view/invalid-state.png)

### Detalles del cliente

Este panel comprueba si el dispositivo está configurado correctamente. Esto incluye configurar la extensión en la IU de recopilación de datos, inicializar la extensión y sus requisitos previos en la aplicación y capturar el token push desde el dispositivo.

Si es válido, el panel mostrará el ECID del dispositivo, el token push y el nombre y tipo de la zona protegida de Edge.

### Detalles del perfil

Una vez que el cliente esté configurado correctamente, este panel comprobará si el dispositivo está escribiendo en el perfil. También valida que el token push del perfil coincida con el del dispositivo.

Si es válido, el panel mostrará el ECID del dispositivo, el token push, el ID de aplicación de la aplicación, la plataforma de mensajería y si el token push se ha incluido en la lista de denegados. El token se puede incluir en la lista de denegados por varios motivos, como que el usuario haya desinstalado la aplicación o que haya desactivado la mensajería push para la aplicación.

![Bloqueado](./images/push-debug-view/deny-list-blocked.png)

Por último, en la parte inferior del panel se encuentra un vínculo que abrirá este perfil específico en una nueva pestaña.

### Credenciales y configuración de AppStore

Este panel valida que el ID de aplicación y la plataforma de mensajería guardada en el perfil tengan una superficie de aplicación coincidente creada. Una superficie de aplicación es donde se cargan las credenciales push de la aplicación.

Si es válido, el perfil mostrará el nombre de la superficie de la aplicación, el ID de la aplicación y el nombre del servicio de mensajería.

Por último, en la parte inferior del panel hay un vínculo que abrirá esta superficie específica de la aplicación en una pestaña nueva.

## Enviar inserción de prueba

El **[!UICONTROL Enviar inserción de prueba]** se puede utilizar para enviar un mensaje de prueba al dispositivo.

Existen varios paneles que se pueden configurar para probar las distintas funciones push de iOS y Android. Una vez configurada, seleccione **[!UICONTROL Enviar notificación push de prueba]** para enviar el mensaje.

![Enviar notificación push](./images/push-debug-view/send.png)

### Mensaje

En el **[!UICONTROL Mensaje]** , puede proporcionar un título y un cuerpo para el mensaje. La función de notificación silenciosa también se puede activar aquí.

![Panel de mensajes](./images/push-debug-view/message-pane.png)

### Destino push

El **[!UICONTROL Destino push]** Este panel le permite personalizar qué superficie de aplicación y token push utilizar al enviar el mensaje push.

Esta información se proporciona de forma predeterminada si la variable **[!UICONTROL Validar configuración]** La pestaña muestra tres marcas de verificación verdes. Sin embargo, puede proporcionar su propio token push y su superficie de aplicación, aunque la aplicación no esté completamente configurada.

![Panel de destino](./images/push-debug-view/target-pane.png)

### Comportamiento de clic

Desde el **[!UICONTROL Comportamiento de clic]** , puede elegir cuál debe ser el comportamiento cuando se haga clic en la notificación push en el dispositivo. De forma predeterminada, se abre la aplicación, pero se puede abrir un vínculo profundo o una página web.

Si decide utilizar un vínculo profundo, el desarrollador de la aplicación debe crearlo por usted.

![Panel Comportamiento](./images/push-debug-view/click-behavior.png)

### Medios enriquecidos

El **[!UICONTROL Medios enriquecidos]** le permite añadir medios adicionales al mensaje, como una imagen, un vídeo o un GIF. El desarrollador de aplicaciones debe agregar código a la aplicación para habilitar esta función.

![Panel enriquecido](./images/push-debug-view/rich-pane.png)

### Botones

El **[!UICONTROL Botones]** permite añadir botones adicionales a la notificación push. Cada botón puede abrir la aplicación, abrir un vínculo profundo en la aplicación o abrir una página web.

El desarrollador de aplicaciones debe agregar código a la aplicación para habilitar esta función.

![Panel de botones](./images/push-debug-view/buttons-pane.png)

### Datos personalizados

El **[!UICONTROL Datos personalizados]** le permite añadir datos personalizados a la notificación push. Cada par clave/valor se envía como metadatos junto con el mensaje y los desarrolladores pueden utilizarlos para crear experiencias útiles y agregar un seguimiento adicional.

![Panel personalizado](./images/push-debug-view/custom-pane.png)

## Resultados de pruebas

Una vez enviado un mensaje, la variable **[!UICONTROL Resultados de prueba]** recibe datos de los servicios push del mensaje. Aquí puede ver si el mensaje llegó a los servicios de mensajería de Google/iOS:

![Resultados de la prueba](./images/push-debug-view/test-results.png)

Si se produjo algún problema, se muestra aquí:

![Error de resultados de prueba](./images/push-debug-view/test-error.png)

## Avanzadas

### Ver carga útil del mensaje

Junto a la **[!UICONTROL Enviar notificación push de prueba]** es un conjunto de puntos suspensivos con un menú emergente. Desde aquí puede ver la carga útil del mensaje. Esto le permite ver el mensaje exacto que se enviará al servicio de mensajería remota. Puede revisar esta carga útil o incluso copiarla y pegarla en una herramienta de prueba push de escritorio.

![Panel personalizado](./images/push-debug-view/message-payload.png)
