---
title: Integración de Slack para alertas de cliente
description: Obtenga información sobre cómo conectar Adobe I/O Events a Slack mediante Adobe App Builder.
source-git-commit: c0fa0320b32e1bfe286d47a2e1af5ea1dcf74cb9
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# Integración de Slack para alertas de clientes

Adobe Experience Platform le permite usar un proxy webhook en [Adobe App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app) para recibir [Adobe I/O Events](https://developer.adobe.com/events/docs/guides/) en [!DNL Slack]. El proxy administra el protocolo de enlace de verificación de Adobe y convierte las cargas de evento en [!DNL Slack] mensajes, para que pueda recibir alertas de cara al cliente en su espacio de trabajo.

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* **Acceso a Adobe Developer Console**: un rol de Administrador del sistema o Desarrollador en una organización con App Builder habilitado.
* **Node.js y npm**: Node.js (se recomienda LTS), que incluye npm para instalar la CLI de Adobe y las dependencias del proyecto. Para obtener más información, consulte [Descargar Node.js](https://nodejs.org/) y [npm Guía de introducción](https://docs.npmjs.com/getting-started).
* **Adobe I/O CLI**: instale Adobe I/O CLI desde su terminal: `npm install -g @adobe/aio-cli`.
* **Aplicación de Slack con webhook entrante**: Una aplicación de Slack en su área de trabajo con **webhook entrante** habilitado. Consulte [Crear una aplicación de Slack](https://api.slack.com/apps) y la [guía de Webhooks entrantes de Slack](https://api.slack.com/messaging/webhooks) para crear la aplicación y obtener la URL del webhook (formato: `https://hooks.slack.com/...`).

## Configuración de un proyecto con plantilla {#templated-project}

Para configurar un proyecto con plantilla, inicie sesión en Adobe Developer Console y luego seleccione **[!UICONTROL Create project from template]** en la ficha **[!UICONTROL Home]**.

![Developer Console resalta la ficha Inicio y crea un proyecto a partir de una plantilla.](../images/alerts/slack-integration/developer-console-home.png)

Seleccione la plantilla **[!UICONTROL App Builder]**, luego ingrese un **[!UICONTROL Project Title]** y seleccione **[!UICONTROL Add workspace]**. Finalmente, seleccione **[!UICONTROL Save]**.

![Título del proyecto resaltado en Developer Console, Agregar Workspace y Guardar.](../images/alerts/slack-integration/developer-console-save.png)

Recibirá la confirmación de que su proyecto se ha creado y se le redirigirá a la ficha **[!UICONTROL Project overview]**. Desde aquí puede agregar **[!UICONTROL Project description]**.

![La ficha Información general del proyecto muestra los detalles del proyecto.](../images/alerts/slack-integration/developer-console-project.png)

## Inicializar proyecto {#initialize-project}

Una vez configurado el proyecto con plantilla, inicialícelo.

1. Abra el terminal e introduzca el siguiente comando para iniciar sesión en Adobe I/O.

   ```bash
   aio login
   ```

1. Inicialice la aplicación y proporcione un nombre.

   ```bash
   aio app init slack-webhook-proxy
   ```

1. Seleccione su `Organization` con las teclas de dirección y, a continuación, seleccione el `Project` que creó anteriormente en Developer Console. Seleccione `Only Templates Supported By My Org` para las plantillas que desea buscar.

   ![Terminal que muestra la selección de la organización y el proyecto y solo las plantillas admitidas por mi organización.](../images/alerts/slack-integration/terminal-organization-project.png)

1. A continuación, presione **Entrar** para omitir las plantillas e instalar una aplicación independiente.

   ![Terminal que muestra la selección de la organización y el proyecto y solo las plantillas admitidas por mi organización.](../images/alerts/slack-integration/terminal-skip-templates.png)

1. Especifique las funciones de la aplicación de Adobe I/O que desea habilitar para este proyecto. Utilice las teclas de dirección para desplazarse y seleccionar `Actions: Deploy Runtime actions`.

   ![Terminal que muestra las características de la aplicación con las acciones: acciones de implementación en tiempo de ejecución seleccionadas.](../images/alerts/slack-integration/terminal-app-features.png)

1. Utilice las teclas de dirección para desplazarse y seleccionar `Adobe Experience Platform: Realtime Customer Profile` para el tipo de acciones de ejemplo que desee crear.

   ![Terminal que muestra el tipo de acciones de ejemplo con Adobe Experience Platform: Perfil del cliente en tiempo real seleccionado.](../images/alerts/slack-integration/terminal-sample-actions.png)

1. Desplácese y seleccione `Pure HTML/JS` para la interfaz de usuario que desee agregar a la plantilla. Presione **Enter** para dejar las acciones de ejemplo como predeterminadas y luego presione **Enter** de nuevo para dejar el nombre como predeterminado.

   ![Terminal que muestra la selección de IU con HTML/JS puro seleccionado.](../images/alerts/slack-integration/terminal-ui-template.png)

   Recibirá una confirmación de que la inicialización de la aplicación ha finalizado.

1. Vaya al directorio del proyecto.

   ```bash
   cd slack-webhook-proxy
   ```

1. Añada la acción web.

   ```bash
   aio app add action
   ```

1. Seleccione `Only Action Templates Supported By My Org`. Aparecerá una lista de plantillas.

   ![Terminal que muestra la lista de plantillas de acción.](../images/alerts/slack-integration/terminal-action-templates.png)

1. Para seleccionar la plantilla, presione la barra espaciadora y luego navegue hasta `@adobe/generator-add-publish-events` con las flechas **Arriba** y **Abajo**. Finalmente, selecciona la plantilla presionando la **barra espaciadora** y presiona **Intro**.

   ![Terminal que muestra la plantilla.](../images/alerts/slack-integration/terminal-action-select-template.png)

   Se muestra una confirmación de que `npm package @adobe/generator-add-publish-events` se ha instalado.

1. Asigne un nombre a la acción `webhook-proxy`.

   ![Terminal que muestra la acción denominada webhook-proxy.](../images/alerts/slack-integration/terminal-add-action-name.png)

   Se muestra una confirmación de que la plantilla se ha instalado.

## Creación de las acciones de archivo e implementación {#create-file-actions}

Agregue el código proxy, establezca las variables de entorno y, a continuación, implemente. La acción estará disponible en Developer Console para su registro.

### Implementar el proxy de tiempo de ejecución {#runtime-proxy}

>[!NOTE]
>
>La verificación de firma y la gestión de desafíos son automáticas al utilizar el registro de acciones en tiempo de ejecución.

Vaya a la carpeta del proyecto y abra el archivo `actions/webhook-proxy/index.js`. Elimine el contenido y reemplace por lo siguiente:

```
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("runtime-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### Configure la acción en app.config.yaml {#app-config}

>[!IMPORTANT]
>
>La configuración de la acción en `app.config.yaml` es crítica. Debe usar `web: no` para crear una acción que no sea de web y que se pueda registrar como una acción de tiempo de ejecución en Developer Console.

Vaya a la carpeta del proyecto y abra `app.config.yaml`. Reemplace el contenido por lo siguiente:

```
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

### Variables de entorno {#environment-variables}

>[!IMPORTANT]
>
>La aplicación no se ejecutará sin un archivo .env correctamente configurado.

Para administrar las credenciales de forma segura, utilice variables de entorno. Modifique el archivo `.env` en la raíz del proyecto y agregue:

```
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### Implementar la acción {#deploy-action}

Una vez configuradas las variables de entorno, implemente la acción. Asegúrese de que está en la raíz del proyecto (`slack-webhook-proxy`) cuando ejecute este comando en el terminal:

```bash
aio app deploy
```

Se muestra una confirmación de que la implementación se ha realizado correctamente.

>[!IMPORTANT]
>
>La acción se implementará en Adobe I/O Runtime. La acción ahora estará disponible en Developer Console para su registro.

## Registre la acción con Adobe I/O Events {#register-events}

Una vez implementada la acción, regístrela como destino para Adobe I/O Events.

En Developer Console, abra el proyecto de App Builder y seleccione su **[!UICONTROL Workspace]**.

En la página de información general de Workspace, seleccione **[!UICONTROL Add service]** y **[!UICONTROL Event]**.

![La página de información general de Workspace resalta Agregar servicio y Evento.](../images/alerts/slack-integration/workspace-service-event.png)

En la página Agregar eventos, seleccione **[!UICONTROL Experience Platform]** y **[!UICONTROL Platform notifications]**, y después seleccione **[!UICONTROL Next]**.

![La página Agregar eventos muestra las notificaciones seleccionadas de Experience Platform y Platform.](../images/alerts/slack-integration/add-events.png)

Seleccione los eventos para los que desea recibir notificaciones y luego seleccione **[!UICONTROL Next]**.

![La página Agregar eventos muestra la lista de eventos a los que suscribirse.](../images/alerts/slack-integration/select-events.png)

Seleccione su credencial de autenticación de servidor a servidor y luego seleccione **[!UICONTROL Next]**.

![La página Agregar eventos muestra la selección de credenciales de autenticación de servidor a servidor.](../images/alerts/slack-integration/add-events-credentials.png)

Escriba un **[!UICONTROL Event registration name]** y un **[!UICONTROL Event registration description]** de borrado para el registro, y después seleccione **[!UICONTROL Next]**.

![La página Agregar eventos muestra los campos Nombre de registro de evento y Descripción de registro de evento.](../images/alerts/slack-integration/add-events-registration.png)

Seleccione **[!UICONTROL Runtime Action]** como método de entrega y la acción `slack-webhook-proxy/runtime-proxy` que creó y, a continuación, seleccione **[!UICONTROL Save configured events]**.

![La página Agregar eventos muestra el método de envío Acción de tiempo de ejecución y Guardar eventos configurados.](../images/alerts/slack-integration/add-events-runtime.png)

El proxy del gancho web ya está configurado. Se le devolverá a la página de proxy de webhook. Puede probar todo el flujo de extremo a extremo seleccionando el icono **[!UICONTROL Send sample event]** junto a cualquier evento configurado.

![La página de proxy de gancho web que muestra los eventos configurados y el icono Enviar evento de muestra.](../images/alerts/slack-integration/send-sample.png)
