---
title: Recopilar análisis y aplicar personalización en aplicaciones ChatGPT (recopilación de datos MCP)
description: Utilice un servidor MCP híbrido + SDK web para aplicar el patrón Response y enviar eventos al Edge Network de Adobe Experience Platform y procesar la personalización dentro de una interfaz de usuario de la aplicación ChatGPT.
keywords: Adobe Experience Platform, Web SDK, Edge Network, MCP, aplicaciones ChatGPT, applyResponse, extremo de interacción, personalización, análisis
source-git-commit: c848f821ea911c82531c6784a17df0116572cd86
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Recopilar análisis y aplicar personalización en aplicaciones ChatGPT (recopilación de datos MCP)

Este caso de uso muestra cómo conectar una aplicación ChatGPT (servidor de protocolo de contexto de modelo + componentes de interfaz de usuario opcionales) a Adobe Experience Platform Edge Network. Este tipo de recopilación de datos le permite registrar análisis para interacciones conversacionales que invoquen sus herramientas y ofrecer decisiones de personalización desde Edge Network en un widget procesado por ChatGPT.

>[!NOTE]
>
>Este documento se mantiene en función de las últimas actualizaciones disponibles tanto de los equipos de recopilación de datos de Adobe como de las últimas actualizaciones tecnológicas de OpenAI. Como tal, Adobe prevé que este documento evolucionará con el tiempo y recomienda volver a buscar actualizaciones.

Este caso de uso prefiere un enfoque híbrido, que utilice una implementación del lado del servidor para recopilar datos y una implementación del lado del cliente para procesar contenido personalizado. Este enfoque es ideal, ya que la invocación de la herramienta MCP es el momento más confiable para recopilar análisis. El widget se ejecuta en un contexto de explorador y es el lugar correcto para almacenar la identidad (en una cookie) y aplicar decisiones de personalización.

Este caso de uso incluye un ejemplo de código totalmente operativo. Consulte la aplicación [ChatGPT + Adobe Experience Platform Edge](https://github.com/adobe/alloy-samples/tree/main/chatgpt-app) en el repositorio `alloy-samples` en GitHub para obtener instrucciones de implementación y código de ejemplo.

>[!IMPORTANT]
>
>Esta página describe una implementación de referencia diseñada para ilustrar un patrón de integración. Revise los requisitos de seguridad, privacidad, consentimiento y producción antes de adoptar el enfoque en su aplicación.

## Arquitectura

En un nivel superior, hay cinco partes móviles:

1. **Host MCP (ChatGPT)**: ChatGPT invoca herramientas expuestas por el servidor MCP y proporciona un identificador de usuario seudónimo estable en los metadatos de la solicitud.
1. **Servidor MCP (servidor)**: propiedad de su organización. Implementa herramientas como enumerar elementos, recuperar detalles o enviar solicitudes.
1. **Adobe IMS**: Problemas con los tokens de acceso que usa su servidor MCP para llamar a las API de recopilación de datos de Adobe.
1. **Adobe Experience Platform Edge Network**: recibe eventos de experiencia enviados por el servidor MCP y devuelve reconocimientos de análisis, actualizaciones de estado (como la identidad) y decisiones de personalización.
1. **IU web incrustada (widget de front-end procesado por el host MCP)**: muestra resultados estructurados y aplica metadatos de Adobe recibidos del servidor MCP back-end.

## Flujo de datos

1. **El usuario** solicita **ChatGPT** con su servidor MCP.
1. **ChatGPT** interpreta la intención del mensaje y llama a la **herramienta MCP del servidor** apropiada.
1. **El servidor MCP back-end** usa las API de recopilación de datos (`interact` punto final) para enviar un evento de experiencia a **Edge Network** para la recopilación de análisis y la personalización opcional.
1. **Edge Network** devuelve identificadores de respuesta, incluidas actualizaciones de estado y decisiones de personalización, a la **herramienta MCP back-end**.
1. **Herramienta MCP back-end** devuelve un resultado de herramienta que contiene datos empresariales en `structuredContent` y metadatos de Adobe en `_meta` a **ChatGPT**.
1. **ChatGPT** entrega el resultado de la herramienta al **widget de front-end**, que procesa los datos profesionales y aplica los metadatos de Adobe usando el comando `applyResponse` de la biblioteca de JavaScript de Web SDK. Este comando hidrata el estado del lado del cliente y procesa las decisiones de personalización aptas en la interfaz de usuario.

Las siguientes secciones describen en detalle cada paso.

## Paso 1: El usuario solicita ChatGPT usando su servidor MCP

Este paso es el punto de entrada para el flujo de trabajo. El usuario proporciona la intención en lenguaje natural:

```text
"Use the Adobe Office Information Tool to show me details about which office that is the most pet-friendly."
```

Consulte [Crear su servidor MCP](https://developers.openai.com/apps-sdk/build/mcp-server/) en la documentación de desarrolladores de OpenAI para obtener más información.

## Paso 2: ChatGPT interpreta la intención y llama a una herramienta MCP

En función de los metadatos del servidor MCP, ChatGPT interpreta la intención e invoca el controlador de herramientas adecuado en el servidor MCP. Esta llamada a la herramienta crea un punto de verdad del lado del servidor para la interacción que es independiente del éxito de procesamiento de la interfaz de usuario. Una de las herramientas puede tener los siguientes metadatos:

```json
{
  "name": "office_details",
  "description": "Fetch details for a single office by ID and return personalization handles for the UI.",
  "inputSchema": {
    "type": "object",
    "properties": {
      "sessionId": { "type": "string", "description": "Server-issued session identifier." },
      "officeId": { "type": "string", "description": "Office identifier." }
    },
    "required": ["sessionId", "officeId"],
    "additionalProperties": false
  },
  "_meta": {
    "ui": {
      "visibility": ["model", "app"]
    }
  }
}
```

Consulte [Definir herramientas](https://developers.openai.com/apps-sdk/plan/tools/) en la documentación de desarrolladores de OpenAI para obtener más información sobre cómo decirle a ChatGPT lo que hace cada herramienta MCP.

## Paso 3: El servidor MCP envía un evento de experiencia a Edge Network

Cuando el servidor MCP recibe una solicitud, déclencheur una llamada a Adobe Experience Platform Edge Network para registrar los datos de análisis y, opcionalmente, solicitar la toma de decisiones o la personalización. Dado que esta solicitud es de servidor a servidor, use el extremo [`interact`](https://developer.adobe.com/data-collection-apis/docs/endpoints/interact/) autenticado como parte de las [API de recopilación de datos](https://developer.adobe.com/data-collection-apis/docs/). Adobe recomienda usar un [área de nombres personalizada](https://experienceleague.adobe.com/es/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities) para pasar el identificador único de OpenAI. Asegúrese de que el área de nombres que crea en la interfaz de usuario de Identidades y el área de nombres de identidad que define en la llamada coincidan (con distinción de mayúsculas y minúsculas).

```sh
curl -X POST "https://server.adobedc.net/ee/v2/interact?datastreamId={DATASTREAM_ID}"
  -H "Authorization: Bearer {TOKEN}"
  -H "x-gw-ims-org-id: {ORG_ID}"
  -H "x-api-key: {API_KEY}"
  -H "Content-Type: application/json"
  -d '{
    "event": {
      "xdm": {
        "eventType": "office.details.view",
        "identityMap": {
          "{IDENTITY_NAMESPACE}": [
            { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
          ]
        },
        "timestamp": "YYYY-02-20T19:00:00.000Z"
      }
    },
    "query": {
      "personalization": {
        "decisionScopes": ["__view__"]
      }
    },
    "meta": {
      "state": {
        "entries": [
          { "key": "kndctr_orgid_cluster", "value": "{CLUSTER_HINT_IF_KNOWN}" },
          { "key": "kndctr_orgid_identity", "value": "{ECID_BLOB_IF_KNOWN}" }
        ]
      }
    }
  }'
```

## Paso 4: Edge Network devuelve controladores

Cuando Edge Network recibe su llamada a `interact`, responde con una matriz de `handle`. Esta matriz puede incluir decisiones de identidad y personalización, según la configuración del conjunto de datos. Una respuesta de ejemplo puede tener el siguiente aspecto:

```json
{
  "requestId": "60a2f...2294d",
  "handle": [
    {
      "type": "locationHint:result",
      "payload": [
        { "scope": "EdgeNetwork", "hint": "or2", "ttlSeconds": 1800 }
      ]
    },
    {
      "type": "state:store",
      "payload": [
        { "key": "kndctr_..._identity", "value": "CiYzM...snTI=", "maxAge": 34128000 },
        { "key": "kndctr_..._cluster", "value": "or2", "maxAge": 1800 }
      ]
    }
  ]
}
```

A continuación, el servidor MCP puede extraer información de la respuesta de Edge Network para conservar la información de identidad:

```ts
type EdgeHandle = { type: string; payload?: Array<{ key?: string; value?: string }> };

export function extractStateStore(handles: EdgeHandle[]) {
  const store = handles.find(h => h.type === "state:store");
  const entries = store?.payload ?? [];

  const identity = entries.find(e => e.key?.includes("_identity"))?.value;
  const cluster  = entries.find(e => e.key?.includes("_cluster"))?.value;

  return { identity, cluster };
}
```

## Paso 5: El servidor MCP devuelve la salida estructurada de la herramienta más los metadatos de Adobe a ChatGPT

La respuesta de la herramienta MCP incluye el resultado estructurado de la herramienta y la personalización de Edge Network.

* El objeto `structuredContent` contiene datos empresariales que ChatGPT puede leer y narrar con seguridad.
* El objeto `_meta` contiene identificadores de respuesta de Adobe y el servidor calculó `identityMap` para que el widget pueda leerlos sin exponer esos datos a ChatGPT. Mantener esta información en `_meta.adobe` le permite mantener la coherencia en la ubicación de los datos. Pasar el mismo `identityMap` hacia adelante ayuda al widget a utilizar la misma identidad personalizada en cualquier evento posterior del lado de la interfaz de usuario.

```json
{
  "content": "Displayed details for office seattle.",
  "structuredContent": {
    "office": {
      "id": "seattle",
      "name": "Seattle",
      "amenities": ["Pet Friendly", "Cafe", "Bike Storage"]
    }
  },
  "_meta": {
    "adobe": {
      "identityMap": {
        "{IDENTITY_NAMESPACE}": [
          { "id": "{PSEUDONYMOUS_SUBJECT_ID}", "primary": true }
        ]
      },
      "handles": [
        {
          "type": "state:store",
          "payload": [
            { "key": "kndctr_..._identity", "value": "..." }
          ]
        },
        {
          "type": "personalization:decisions",
          "payload": [
            { "id": "..." }
          ]
        }
      ]
    }
  }
}
```

Consulte [Resultados de la herramienta](https://developers.openai.com/apps-sdk/reference/#tool-results) en la Referencia del desarrollador de OpenAI para obtener más información.

## Paso 6: El widget procesa el resultado y aplica `_adobe.handles` usando `applyResponse`

El widget procesa los datos empresariales de `structuredContent` y luego lee los metadatos de Adobe de `_meta.adobe`. En ChatGPT, los mismos datos están disponibles para el widget a través de la capa de compatibilidad:

* `window.openai.toolOutput` contiene `structuredContent`
* `window.openai.toolResponseMetadata` contiene `_meta`

El widget utiliza el comando [`applyResponse`](../../js/commands/applyresponse.md) de la biblioteca Web SDK JavaScript para hidratar el estado del lado del cliente y procesar las decisiones de personalización devueltas por la llamada `interact` del lado del servidor. Asegúrese de llamar al comando [`configure`](../../js/commands/configure/overview.md) antes de llamar a `applyResponse`. Dado que el servidor MCP realizó una llamada a `interact`, no es necesario que llame inmediatamente al comando [`sendEvent`](../../js/commands/sendevent/overview.md) para la interacción de la invocación de la herramienta.

```js
// Configure the Web SDK before any other commands.
alloy("configure", {
  datastreamId: "YOUR_DATASTREAM_ID",
  orgId: "YOUR_EXPERIENCE_CLOUD_ORG_ID"
});

// Business data exposed to ChatGPT and the widget.
const { office } = window.openai?.toolOutput ?? {};

// Adobe metadata available only to the widget.
const adobe = window.openai?.toolResponseMetadata?.adobe ?? {};
const { identityMap, handles } = adobe;

// Hydrate client-side state and render personalization decisions from the
// server-side interact response.
alloy("applyResponse", {
  renderDecisions: true,
  responseBody: { handle: handles ?? [] }
});
```

Si posteriormente el widget envía eventos adicionales del lado de la interfaz de usuario, puede incluir los mismos `identityMap` en esas llamadas:

```js
alloy("sendEvent", {
  xdm: {
    eventType: "office.details.widgetView",
    identityMap
  }
});
```

Este patrón mantiene alineado el uso de identidad del lado del servidor y del lado de la interfaz de usuario, al tiempo que permite que la llamada de `interact` del lado del servidor siga siendo la fuente fiable para la recopilación y la toma de decisiones de análisis.

## Validación

Una vez configurados todos los pasos anteriores, puede validar lo siguiente:

* **Recopilación de datos:** Compruebe que los eventos alcanzan el conjunto de datos deseado y que cada evento se procesa según lo esperado.
* **Personalization:** Compruebe que Edge Network devuelve las decisiones y que su widget las procesa.

## Consideraciones de seguridad y privacidad

* Trate los identificadores de ChatGPT como confidenciales, aunque sean seudónimos.
* Asegúrese de aplicar las prácticas de consentimiento y control de datos de su organización a este flujo de trabajo.
* Adobe recomienda utilizar flujos de trabajo de OAuth 2.1 para la autorización.
* Asegúrese de que los tokens y secretos de acceso no lleguen nunca al cliente ni a la interfaz de usuario.
