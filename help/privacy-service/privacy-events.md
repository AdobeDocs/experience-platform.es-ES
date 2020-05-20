---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Suscripción a Eventos de privacidad
topic: privacy events
translation-type: tm+mt
source-git-commit: ab29c7771122267634dea24582b07f605abd7ed8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# Suscripción a Eventos de privacidad

Los Eventos de privacidad son mensajes proporcionados por Adobe Experience Platform Privacy Service, que aprovechan los Eventos de Adobe I/O enviados a un enlace web configurado para facilitar una automatización eficaz de las solicitudes de trabajo. Reducirán o eliminarán la necesidad de sondear la API de Privacy Service para comprobar si se ha completado un trabajo o si se ha alcanzado un determinado hito en un flujo de trabajo.

Actualmente existen cuatro tipos de notificaciones relacionadas con el ciclo vital de la solicitud de trabajo de privacidad:

| Tipo | Descripción |
--- | ---
| Trabajo completado | Todas las soluciones de Experience Cloud han informado y el estado global o general del trabajo se ha marcado como completado. |
| Error de trabajo | Una o más soluciones han informado de un error al procesar la solicitud. |
| Producto completado | Una de las soluciones asociadas con este trabajo ha completado su trabajo. |
| Error del producto | Una de las soluciones informó de un error al procesar la solicitud. |

Este documento proporciona los pasos para configurar una integración de las notificaciones de Privacy Service en Adobe I/O. Para obtener información general de alto nivel sobre Privacy Service y sus funciones, consulte la información general sobre [Privacy Service](home.md).

## Primeros pasos

Este tutorial utiliza **ngrok**, un producto de software que expone los servidores locales a la Internet pública a través de túneles seguros. Por favor, [instale ngrok](https://ngrok.com/download) antes de comenzar este tutorial para poder seguir y crear un weblink en su equipo local. Esta guía también requiere que descargue un repositorio GIT que contenga un servidor [Node.js](https://nodejs.org/) simple.

## Crear un servidor local

El servidor Node.js debe devolver un `challenge` parámetro enviado por una solicitud al extremo raíz (`/`). Configure el `index.js` archivo con el siguiente JavaScript para lograr esto:

```js
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
  response.send(request.originalUrl.split('?challenge=')[1]);
})

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'))
})
```

Con la línea de comandos, navegue al directorio raíz del servidor Node.js. A continuación, escriba los siguientes comandos:

1. `npm install`
1. `npm start`

Estos comandos instalan todas las dependencias e inicializan el servidor. Si tiene éxito, puede encontrar el servidor en ejecución en http://localhost:3000/.

## Creación de un gancho web con ngrok

Abra una nueva ventana de línea de comandos y vaya al directorio donde instaló ngrok anteriormente. Desde aquí, escriba el siguiente comando:

```shell
./ngrok http -bind-tls=true 3000
```

Una salida correcta es similar a la siguiente:

![Salida ngrok](images/privacy-events/ngrok-output.png)

Tenga en cuenta la `Forwarding` dirección URL (`https://212d6cd2.ngrok.io`), ya que se utilizará para identificar el enlace web en el siguiente paso.

## Crear un nuevo proyecto en Adobe Developer Console

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vacío en la documentación de Adobe Developer Console.

## Añadir Eventos de privacidad al proyecto

Una vez que haya terminado de crear un nuevo proyecto en la consola, haga clic en **[!UICONTROL Añadir evento]** en la pantalla Información general _del_ proyecto.

![](./images/privacy-events/add-event-button.png)

Aparece el cuadro de diálogo _Añadir eventos_ . Seleccione **[!UICONTROL Experience Cloud]** para filtrar la lista de los tipos de evento disponibles y, a continuación, seleccione Eventos **[!UICONTROL de]** Privacy Service antes de hacer clic en **[!UICONTROL Siguiente]**.

![](./images/privacy-events/add-privacy-events.png)

Aparece el cuadro de diálogo _Configurar registro_ de evento. Seleccione los eventos que desea recibir seleccionando las casillas correspondientes. Los Eventos que seleccione aparecerán en Eventos __suscritos en la columna izquierda. Cuando termine, haga clic en**[!UICONTROL  Siguiente ]**.

![](./images/privacy-events/choose-subscriptions.png)

La siguiente pantalla le solicita que proporcione una clave pública para el registro en el evento. Tiene la opción de generar automáticamente un par de claves o cargar su propia clave pública generada en la terminal.

A efectos de este tutorial, se sigue la primera opción. Haga clic en el cuadro de opciones para **[!UICONTROL Generar un par]** de claves y, a continuación, haga clic en el botón **[!UICONTROL Generar par]** de claves en la esquina inferior derecha.

![](./images/privacy-events/generate-key-value.png)

Cuando se genera el par de claves, el explorador lo descarga automáticamente. Debe almacenar el archivo usted mismo, ya que no se mantiene en la consola de desarrollador.

La siguiente pantalla le permite revisar los detalles del par de claves recién generado. Haga clic en **[!UICONTROL Siguiente]** para continuar.

![](./images/privacy-events/keypair-generated.png)

En la pantalla siguiente, especifique un nombre y una descripción para el registro de eventos. Lo mejor es crear un nombre único y fácilmente identificable para ayudar a diferenciar este registro de eventos de otros en el mismo proyecto.

![](./images/privacy-events/event-details.png)

Más abajo en la misma pantalla, se le ofrecen dos opciones para configurar cómo recibir eventos. Seleccione **[!UICONTROL Webgancho]** y proporcione la `Forwarding` URL para el ngrok webgancho que creó anteriormente en _[!UICONTROL URL]_de Webgancho. A continuación, seleccione su estilo de envío preferido (único o por lotes) antes de hacer clic en**[!UICONTROL  Guardar eventos ]**configurados para completar el registro de eventos.

![](./images/privacy-events/webhook-details.png)

La página de detalles del proyecto vuelve a aparecer, con Eventos de privacidad debajo de _[!UICONTROL Eventos]_en el panel de navegación izquierdo.

## Datos de evento de Vista

Una vez que haya registrado Eventos de privacidad con su proyecto y que los trabajos de privacidad se hayan procesado, puede realizar la vista de cualquier notificación recibida para ese registro. En la ficha **[!UICONTROL Proyectos]** de la consola de desarrollador, seleccione el proyecto en la lista para abrir la página Información general __ del producto. Desde aquí, seleccione Eventos **[!UICONTROL de]** privacidad en el panel de navegación izquierdo.

![](./images/privacy-events/events-left-nav.png)

Aparece la ficha Detalles __ del registro, que le permite vista de más información sobre el registro, editar su configuración o vista de los eventos reales recibidos desde la activación del vínculo web.

![](./images/privacy-events/registration-details.png)

Haga clic en la ficha **[!UICONTROL Seguimiento]** de depuración para vista de una lista de eventos recibidos. Haga clic en un evento de la lista para vista de sus detalles.

![](images/privacy-events/debug-tracing.png)

La sección _[!UICONTROL Carga útil]_proporciona detalles sobre el evento seleccionado, incluido su tipo de evento (`com.adobe.platform.gdpr.productcomplete`), como se indica en el ejemplo anterior.

## Pasos siguientes

Puede repetir los pasos anteriores para agregar nuevas integraciones para distintas direcciones de enlace web según sea necesario.