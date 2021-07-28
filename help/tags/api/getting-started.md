---
title: Introducción a la API de Reactor
description: Obtenga información sobre cómo empezar a usar la API de Reactor, incluidos los pasos para generar las credenciales de acceso necesarias.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 1%

---

# Introducción a la API de Reactor

Para utilizar la [Reactor API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml), cada solicitud debe incluir los siguientes encabezados de autenticación:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Esta guía explica cómo utilizar la consola de desarrollador de Adobe para recopilar los valores de cada uno de estos encabezados y así poder empezar a realizar llamadas a la API de Reactor.

## Obtener acceso de desarrollador a Adobe Experience Platform

Para poder generar valores de autenticación para la API de Reactor, debe tener acceso de desarrollador a Experience Platform. Para obtener acceso del desarrollador, siga los pasos iniciales en el [tutorial de autenticación del Experience Platform](http://www.adobe.com/go/platform-api-authentication-en). Una vez que llegue al paso &quot;Generar credenciales de acceso en Adobe Developer Console&quot;, vuelva a este tutorial para generar las credenciales específicas de la API de Reactor.

## Generar credenciales de acceso

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

El ID de su organización IMS (`{IMS_ORG}`) y la clave de API (`{API_KEY}`) se pueden reutilizar en futuras llamadas de API después de haberlas generado inicialmente. Sin embargo, el token de acceso (`{ACCESS_TOKEN}`) es temporal y debe regenerarse cada 24 horas.

Los pasos para generar estos valores se tratan en detalle a continuación.

### Configuración única

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) en la documentación de Developer Console.

Una vez creado un proyecto, seleccione **Agregar API** en la pantalla **Información general del proyecto**.

![](../images/api/getting-started/add-api-button.png)

Aparece la pantalla **Add an API**. Seleccione **API de reactor Experience Platform** de la lista de API disponibles antes de seleccionar **Siguiente**.

![](../images/api/getting-started/add-launch-api.png)

En la siguiente pantalla, se le pedirá que cree una credencial de token web de JSON (JWT) que genere un nuevo par de claves o que cargue su propia clave pública. Para este tutorial, seleccione la opción **Generate a key pair** y luego seleccione **Generate keypair** en la esquina inferior derecha.

![](../images/api/getting-started/create-jwt.png)

La siguiente pantalla confirma que el par de claves se ha generado correctamente y una carpeta comprimida que contiene un certificado público y una clave privada se descarga automáticamente al equipo. Esta clave privada se requiere en un paso posterior para generar un token de acceso.

Seleccione **Siguiente** para continuar.

![](../images/api/getting-started/keypair-generated.png)

La siguiente pantalla le solicita que seleccione uno o más perfiles de producto para asociarlos a la integración de API.

>[!NOTE]
>
>Su organización gestiona los perfiles de producto a través de Adobe Admin Console y contienen conjuntos específicos de permisos para funciones granulares. Los perfiles de producto y sus permisos solo los pueden administrar usuarios con privilegios de administrador en su organización. Si no está seguro de qué perfiles de producto desea seleccionar para la API, póngase en contacto con su administrador.

Seleccione los perfiles de producto que desee en la lista y, a continuación, seleccione **Guardar API configurada** para completar el registro de la API.

![](../images/api/getting-started/select-product-profile.png)

Una vez añadida la API al proyecto, la página del proyecto vuelve a aparecer en la página de la API de Experience Platform Reactor. Desde aquí, desplácese hacia abajo hasta la sección **Cuenta de servicio (JWT)** , que proporciona las siguientes credenciales de acceso necesarias en todas las llamadas a la API de Reactor:

* **ID** DE CLIENTE: El ID de cliente es el ID necesario  `{API_KEY}` que debe proporcionarse en el  `x-api-key` encabezado.
* **ID DE ORGANIZACIÓN**: El ID de organización es el  `{IMS_ORG}` valor que debe utilizarse en el  `x-gw-ims-org-id` encabezado.

![](../images/api/getting-started/access-creds.png)

### Autenticación para cada sesión

Ahora que tiene los valores `{API_KEY}` y `{IMS_ORG}`, el paso final está generando un valor `{ACCESS_TOKEN}`.

>[!NOTE]
>
>Estos tokens caducan a las 24 horas. Si utiliza esta integración para una aplicación, es aconsejable obtener el token de portador mediante programación desde la aplicación.

Tiene dos opciones para generar los tokens de acceso, según el caso de uso:

* [Generar tokens manualmente](#manual)
* [Generar tokens mediante programación](#program)

#### Generar tokens de acceso manualmente {#manual}

Abra la clave privada que descargó anteriormente en un navegador o editor de texto y copie su contenido. A continuación, vuelva a Developer Console y pegue la clave privada en la sección **Generate access token** de la página de la API de reactor para su proyecto antes de seleccionar **Generate Token**.

![](../images/api/getting-started/paste-private-key.png)

Se genera un nuevo token de acceso y se proporciona un botón para copiar el token en el portapapeles. Este valor se utiliza para el encabezado `Authorization` requerido y debe proporcionarse con el formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/token-generated.png)

#### Generar tokens de acceso mediante programación {#program}

Si utiliza la integración para una aplicación, puede generar mediante programación tokens de acceso a través de solicitudes de API. Para ello, debe obtener los siguientes valores:

* ID del cliente (`{API_KEY}`)
* Secreto de cliente (`{SECRET}`)
* Un token web JSON (`{JWT}`)

El ID de cliente y el secreto se pueden obtener de la página principal del proyecto, tal como se ve en el [paso anterior](#one-time-setup).

![](../images/api/getting-started/auto-access-creds.png)

Para obtener sus credenciales de JWT, vaya a **Service Account (JWT)** en el panel de navegación izquierdo y, a continuación, seleccione la pestaña **Generate JWT** . En esta página, en **Generate custom JWT**, pegue el contenido de su clave privada en el cuadro de texto proporcionado y, a continuación, seleccione **Generate Token**.

![](../images/api/getting-started/generate-jwt.png)

El JWT generado aparece a continuación una vez que ha finalizado el procesamiento, junto con un comando cURL de ejemplo que puede utilizar para probar el token si lo desea. Utilice el botón **Copy** para copiar el token en el portapapeles.

![](../images/api/getting-started/jwt-generated.png)

Una vez que haya recopilado sus credenciales, puede integrar la llamada de API siguiente en su aplicación para generar mediante programación tokens de acceso.

**Solicitud**

La solicitud debe enviar una carga útil `multipart/form-data`, que proporcione las credenciales de autenticación que se muestran a continuación:

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**Respuesta**

Una respuesta correcta devuelve un nuevo token de acceso, así como el número de segundos que quedan hasta que caduca.

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| Propiedad | Descripción |
| :-- | :-- |
| `access_token` | El valor del token de acceso recién generado. Este valor se utiliza para el encabezado `Authorization` requerido y debe proporcionarse con el formato `Bearer {ACCESS_TOKEN}`. |
| `expires_in` | Tiempo restante hasta que caduque el token, en milisegundos. Una vez que caduca un token, se debe generar uno nuevo. |

{style=&quot;table-layout:auto&quot;}

## Pasos siguientes

Al seguir los pasos de este tutorial, debe tener valores válidos para `{IMS_ORG}`, `{API_KEY}` y `{ACCESS_TOKEN}`. Ahora puede probar estos valores usándolos en una simple solicitud cURL a la API de Reactor.

Comience por intentar hacer una llamada API a [list all company](./endpoints/companies.md#list).

>[!NOTE]
>
>Es posible que no tenga ninguna empresa en su organización. En este caso, la respuesta será el estado HTTP 404 (no encontrado). Siempre que no obtenga un error 403 (prohibido), sus credenciales de acceso son válidas y funcionan.

Una vez que confirme que sus credenciales de acceso funcionan, siga explorando la documentación de referencia de otras API para conocer las muchas capacidades de la API.

## Recursos adicionales

Bibliotecas JWT y SDK: [https://jwt.io/](https://jwt.io/)

Desarrollo de la API de Postman: [https://www.postman.com/](https://www.postman.com/)
