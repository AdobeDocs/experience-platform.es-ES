---
title: Origen de flujo de Shopify
description: Aprenda a crear una conexión de origen y un flujo de datos para ingerir datos de flujo continuo de la instancia de Shopify a Adobe Experience Platform
badge: Beta
exl-id: 4c83c08d-c744-4167-9e3b-ed9a995943f4
source-git-commit: feb05d5bddc4135c5fe14d3ec5d8fad62c5e2236
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# [!DNL Shopify Streaming]

>[!NOTE]
>
>La variable [!DNL Shopify Streaming] el origen está en versión beta. Lea el [información general sobre fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes con etiquetas beta.

Adobe Experience Platform es compatible con la ingesta de datos de aplicaciones de flujo continuo. La compatibilidad con los proveedores de flujo continuo incluye [!DNL Shopify].

## Requisitos previos {#prerequisites}

En la siguiente sección se describen los pasos previos para completar antes de usar la variable [!DNL Shopify Streaming] fuente.

Debe tener una [!DNL Shopify] cuenta de socio para conectarse a la [!DNL Shopify] API. Si todavía no tiene una cuenta de socio, regístrese utilizando el [[!DNL Shopify] panel de socios](https://www.shopify.com/partners).

### Cree la aplicación

Con un [!DNL Shopify] cuenta de socio, ahora puede continuar y crear su aplicación mediante el panel de socios. Para obtener información detallada sobre cómo crear su aplicación en [!DNL Shopify], lea la [[!DNL Shopify] guía de introducción](https://www.shopify.com/partners/blog/17056443-how-to-generate-a-shopify-api-token).

Una vez creada la aplicación, recupere la **ID de cliente** y **secreto de cliente** de la variable **credenciales de cliente** de la pestaña [!DNL Shopify] panel de socios. El ID de cliente y el secreto de cliente se utilizarán en los pasos siguientes para recuperar el código de autorización y el token de acceso.

### Recuperar el código de autorización

A continuación, recupere el código de autorización introduciendo el `myshopify.com` Dirección URL en el explorador, junto con cadenas de consulta que definen la clave de API, los ámbitos y el URI de redirección.

El formato de esta URL es el siguiente:

**Formato de API**

```http
https://{SHOP}.myshopify.com/admin/oauth/authorize?client_id={API_KEY}&scope={SCOPES}&redirect_uri={REDIRECT_URI}
```

| Parámetro | Descripción |
| --- | --- |
| `shop` | Su subdominio `myshopify.com` URL. |
| `api_key` | Su [!DNL Shopify] ID de cliente. Puede recuperar el ID de cliente desde la variable **credenciales de cliente** de la pestaña [!DNL Shopify] panel de socios. |
| `scopes` | Tipo de acceso que desea definir. Por ejemplo, puede definir ámbitos como `scope=write_orders,read_customers` para permitir permisos para modificar pedidos y leer clientes. |
| `redirect_uri` | Dirección URL de la secuencia de comandos que generará el token de acceso. |

**Solicitud**

```http
https://connnectors-test.myshopify.com/admin/oauth/authorize?client_id=l6fiviermmzpram5i1spfub99shms3j9&scope=write_orders,read_customers&redirect_uri=https://acme.com
```

**Respuesta**

Una respuesta correcta devolverá su dirección URL de redireccionamiento, incluido el código de autorización necesario para generar el token de acceso.

```http
https://www.acme.com/?code=k6j2palgrbljja228ou8c20fmn7w41gz&hmac=68c9163f772eecbc8848c90f695bca0460899c125af897a6d2b0ebbd59d3a43b&shop=connnectors-test.myshopify.com&state=123456×tamp=1658305460
```

### Recupere el token de acceso

Ahora que tiene su ID de cliente, secreto de cliente y código de autorización, puede recuperar su token de acceso. Para recuperar el token de acceso, realice una solicitud de POST al `myshopify.com` URL al anexar esta URL con [!DNL Shopify's] Punto final de API: `/admin/oauth/access_token`.

**Formato de API**

```https
POST /{SHOP}.myshopify.com/admin/oauth/access_token
```

**Solicitud**

La siguiente solicitud genera un token de acceso para su [!DNL Shopify] instancia.

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

Una respuesta correcta devuelve los ámbitos de token de acceso y permiso.

```json
{
  "access_token": "shpca_wjhifwfc91psjtldysxd6rqli371tx54",
  "scope": "write_orders,read_customers"
}
```

## Creación de un enlace web para la transmisión por secuencias [!DNL Shopify] data {#webhook}

Los Webhooks permiten que las aplicaciones permanezcan sincronizadas con su [!DNL Shopify] datos o realizar una acción después de que se produzca un evento determinado en una tienda. Para flujo continuo [!DNL Shopify] datos para el Experience Platform, los webhooks se pueden utilizar para definir el extremo http y los temas de suscripción.

**Solicitud**

La siguiente solicitud crea un enlace web para su [!DNL Shopify Streaming] datos.

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
| `webhook.address` | El extremo http donde se envían los mensajes de flujo continuo. |
| `webhook.topic` | El tema de su suscripción a weblink. Para obtener más información, lea la [[!DNL Shopify] guía de temas del evento de weblink](https://shopify.dev/docs/api/admin-rest/2023-04/resources/webhook#event-topics). |
| `webhook.format` | El formato de los datos. |

**Respuesta**

Una respuesta correcta devuelve información en el enlace web, incluyendo su correspondiente `id`, dirección y otra información de metadatos.

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

A continuación se muestra una lista de las limitaciones conocidas que puede encontrar al utilizar vínculos web con la variable [!DNL Shopify Streaming] fuente.

* No se garantiza que pueda organizar el orden de envío de diferentes temas para el mismo recurso. Por ejemplo, es posible que una `products/update` weblink se entrega antes de una `products/create` gancho.
* Puede configurar su weblink para que entregue eventos de weblock a un punto final al menos una vez. Esto significa que un punto final puede recibir el mismo evento más de una vez. Puede buscar eventos de weblinks duplicados comparando los `X-Shopify-Webhook-Id` a eventos anteriores.
* [!DNL Shopify] trata las respuestas de estado HTTP 2xx como notificaciones correctas. Cualquier otra respuesta del código de estado se considera como un error. [!DNL Shopify] proporciona un mecanismo de reintento para notificaciones de weblock fallidas. Si hay **no hay respuesta después de esperar cinco segundos**, [!DNL Shopify] reintenta la conexión **19 veces** durante el siguiente **48 horas**. Si aún no hay respuestas al final del periodo de reintento, [!DNL Shopify] elimina el vínculo web.

## Pasos siguientes

Los siguientes tutoriales proporcionan los pasos para conectar su [!DNL Shopify Streaming] fuente para el Experience Platform mediante la API y la IU:

* [Creación de una conexión de origen de Shopify Streaming y un flujo de datos mediante la API de servicio de flujo](../../tutorials/api/create/ecommerce/shopify-streaming.md)
* [Crear una conexión de origen de Shopify Streaming y un flujo de datos en la interfaz de usuario](../../tutorials/ui/create/ecommerce/shopify-streaming.md)
