---
title: Shopify Streaming Source
description: Aprenda a crear una conexión de origen y un flujo de datos para introducir datos de flujo continuo de su instancia de Shopify a Adobe Experience Platform
badge: Beta
last-substantial-update: 2023-04-26T00:00:00Z
exl-id: ae991913-68b5-4bbb-b8a5-e566d67a4c1a
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>El [!DNL Shopify Streaming] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform es compatible con la ingesta de datos desde aplicaciones de flujo continuo. Los proveedores de streaming admiten [!DNL Shopify].

## Requisitos previos {#prerequisites}

En la siguiente sección se describen los pasos necesarios que deben seguirse antes de utilizar [!DNL Shopify Streaming] origen.

Debe tener un válido [!DNL Shopify] cuenta de socio para conectarse a [!DNL Shopify] API. Si todavía no tiene una cuenta de socio, regístrese en [[!DNL Shopify] panel de socios](https://www.shopify.com/partners).

### Cree su aplicación

Con un válido [!DNL Shopify] cuenta de socio, ahora puede continuar y crear la aplicación mediante el panel socios. Para ver los pasos detallados sobre cómo crear la aplicación en [!DNL Shopify], lea la [[!DNL Shopify] guía de introducción](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Una vez creada la aplicación, recupere el **ID de cliente** y **secreto de cliente** desde el **credenciales de cliente** de la pestaña [!DNL Shopify] panel de socios. El ID de cliente y el secreto de cliente se utilizarán en los siguientes pasos para recuperar el código de autorización y el token de acceso.

### Recupere el código de autorización

A continuación, recupere el código de autorización introduciendo el de su dominio `myshopify.com` Dirección URL en el explorador, junto con cadenas de consulta que definen la clave de API, los ámbitos y el URI de redirección.

El formato de esta URL es el siguiente:

**Formato de API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parámetro | Descripción |
| --- | --- |
| `shop` | Su subdominio `myshopify.com` URL. |
| `api_key` | Su [!DNL Shopify] ID de cliente. Puede recuperar su ID de cliente desde el **credenciales de cliente** de la pestaña [!DNL Shopify] panel de socios. |
| `scopes` | El tipo de acceso que desea definir. Por ejemplo, puede establecer ámbitos como `scope=write_orders,read_customers` para permitir permisos para modificar pedidos y leer clientes. |
| `redirect_uri` | Dirección URL del script que generará el token de acceso. |

**Solicitud**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Respuesta**

Una respuesta correcta devuelve la dirección URL de redireccionamiento, incluido el código de autorización necesario para generar el token de acceso.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Recuperación del token de acceso

Ahora que tiene su ID de cliente, secreto de cliente y código de autorización, puede recuperar su token de acceso. Para recuperar el token de acceso, realice una solicitud de POST al `myshopify.com` URL al anexar esta URL con [!DNL Shopify's] Extremo de API: `/admin/oauth/access_token`.

**Formato de API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Solicitud**

La siguiente solicitud genera un token de acceso para su [!DNL Shopify] ejemplo.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/oauth/access_token' \
  -H 'developer-token: {DEVELOPER_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'Cookie: _master_udr=xxx; request_method=POST'
  -d '{
    "client_id": "l6fiviermmzpram5i1spfub99shms3j9",
    "client_secret": "dajn3caxz9s7ti624ncyv_m4f60jnwi3ii3y3k",
    "code": "k6j2palgrbljja228ou8c20fmn7w41gz"
}'
```

**Respuesta**

Una respuesta correcta devuelve el token de acceso y los ámbitos de permisos.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Crear un webhook para streaming [!DNL Shopify] datos {#webhook}

Los webhooks permiten que las aplicaciones permanezcan sincronizadas con su [!DNL Shopify] datos o realizar una acción después de que un evento en particular se produzca en una tienda. Para streaming [!DNL Shopify] datos para el Experience Platform, se pueden utilizar webhooks para definir el extremo http y los temas para la suscripción.

**Solicitud**

La siguiente solicitud crea un webhook para su [!DNL Shopify Streaming] datos.

```shell
curl -X POST \
  'https://connnectors-test.myshopify.com/admin/api/2022-07/webhooks.json' \
  -H 'X-Shopify-Access-Token: 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' \
  -H 'Content-Type: application/json' \; request_method=POST' \
  -d '{
  "webhook": {
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "format": "json"
  }
}'
```

| Parámetro | Descripción |
| --- | --- | 
| `webhook.address` | Punto final http al que se envían los mensajes de flujo continuo. |
| `webhook.topic` | El tema de la suscripción al webhook. Para obtener más información, lea la [[!DNL Shopify] guía de temas de eventos de webhook](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | El formato de los datos. |

**Respuesta**

Una respuesta correcta devuelve información sobre el gancho web, incluido su correspondiente `id`, dirección y otra información de metadatos.

```json
{
  "webhook": {
    "id": 1091138715786,
    "address": "https://dcs.adobedc.net/collection/9d411a24aa3c0a3eded92bac6c64d0da986ee7a8212f87168c5fb42d9ddc3227",
    "topic": "orders/create",
    "created_at": "2022-07-20T07:15:23-04:00",
    "updated_at": "2022-07-20T07:15:23-04:00",
    "format": "json",
    "fields": [],
    "metafield_namespaces": [],
    "api_version": "2021-10",
    "private_metafield_namespaces": []
  }
}
```

### Limitaciones {#limitations}

A continuación se muestra una lista de limitaciones conocidas que pueden surgir al utilizar los webhooks con [!DNL Shopify Streaming] origen.

* No se garantiza que pueda organizar el orden de entrega de diferentes temas para el mismo recurso. Por ejemplo, es posible que un `products/update` el webhook se envía antes de que `products/create` gancho web.
* Puede configurar el webhook para que envíe eventos de webhook a un punto final al menos una vez. Esto significa que un extremo puede recibir el mismo evento más de una vez. Puede buscar eventos de webhook duplicados comparando la variable `X-Shopify-Webhook-Id` encabezado para eventos anteriores.
* [!DNL Shopify] trata las respuestas de estado HTTP 2xx como notificaciones correctas. Cualquier otra respuesta del código de estado se considera un error. [!DNL Shopify] proporciona un mecanismo de reintento para las notificaciones fallidas de ganchos web. Si hay **no hay respuesta después de esperar cinco segundos**, [!DNL Shopify] reintenta la conexión **19 veces** en el transcurso del siguiente **48 horas**. Si al final del periodo de reintento aún no hay respuestas, [!DNL Shopify] elimina el webhook.

## Pasos siguientes

Los siguientes tutoriales proporcionan pasos sobre cómo conectar su [!DNL Shopify Streaming] origen al Experience Platform mediante la API y la IU:

* [Cree una conexión de origen y un flujo de datos de Shopify Streaming mediante la API de Flow Service](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Cree una conexión de origen y un flujo de datos de Shopify Streaming en la interfaz de usuario](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
