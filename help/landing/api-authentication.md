---
keywords: Experience Platform;inicio;temas populares;Autenticar;acceso
solution: Experience Platform
title: API de Experience Platform de autenticación y acceso
topic-legacy: tutorial
type: Tutorial
description: Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de hacer llamadas a las API de Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 6%

---


# Autenticar y acceder a las API de Experience Platform

Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de hacer llamadas a las API de Experience Platform. Al final de este tutorial, habrá generado las siguientes credenciales que son necesarias para todas las llamadas a la API de plataforma:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Para mantener la seguridad de sus aplicaciones y usuarios, todas las solicitudes a las API de Adobe I/O deben autenticarse y autorizarse mediante estándares como OAuth y Tokens web JSON (JWT). Se utiliza un JWT junto con información específica del cliente para generar su token de acceso personal.

Este tutorial explica cómo recopilar las credenciales necesarias para autenticar llamadas a la API de plataforma, tal como se describe en el siguiente diagrama de flujo:

![](./images/api-authentication/authentication-flowchart.png)

## Requisitos previos

Para realizar correctamente llamadas a las API de Experience Platform, debe tener lo siguiente:

* Una organización de IMS con acceso a Adobe Experience Platform.
* Un administrador de Admin Console que puede agregarle como desarrollador y un usuario para un perfil de producto.

También debe tener un Adobe ID para completar este tutorial. Si no tiene un Adobe ID, puede crearlo siguiendo estos pasos:

1. Vaya a [Adobe Developer Console](https://console.adobe.io).
2. Seleccione **[!UICONTROL Create a new account]**.
3. Complete el proceso de registro.

## Obtener acceso de desarrollador y usuario para Experience Platform

Antes de crear integraciones en Adobe Developer Console, la cuenta debe tener permisos de desarrollador y usuario para un perfil de producto de Experience Platform en Adobe Admin Console.

### Obtener acceso de desarrollador

Póngase en contacto con un administrador de [!DNL Admin Console] de su organización para agregarle como desarrollador a un perfil de producto de Experience Platform mediante [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consulte la documentación [!DNL Admin Console] para obtener instrucciones específicas sobre cómo [administrar el acceso de los desarrolladores para perfiles de producto](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Una vez que esté asignado como desarrollador, puede empezar a crear integraciones en [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Estas integraciones son una canalización de aplicaciones y servicios externos a API de Adobe.

### Obtener acceso de los usuarios

El administrador de [!DNL Admin Console] también debe agregarle como usuario al mismo perfil de producto. Consulte la guía sobre [administración de grupos de usuarios en [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) para obtener más información.

## Generar una clave de API, el ID de organización de IMS y el secreto de cliente {#api-ims-secret}

>[!NOTE]
>
>Si está siguiendo este documento desde la [guía para desarrolladores de Privacy Service](../privacy-service/api/getting-started.md), ahora puede regresar a esa guía para generar las credenciales de acceso exclusivas de [!DNL Privacy Service].

Después de que se le haya otorgado acceso de desarrollador y usuario a Platform a través de [!DNL Admin Console], el siguiente paso es generar las credenciales `{IMS_ORG}` y `{API_KEY}` en Adobe Developer Console. Estas credenciales solo deben generarse una vez y pueden reutilizarse en futuras llamadas a la API de Platform.

### Agregar un Experience Platform a un proyecto

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Add API]** en la pantalla **[!UICONTROL Project Overview]**.

![](./images/api-authentication/add-api.png)

Aparece la pantalla **[!UICONTROL Add an API]**. Seleccione el icono del producto para Adobe Experience Platform y, a continuación, elija **[!UICONTROL Experience Platform API]** antes de seleccionar **[!UICONTROL Next]**.

![](./images/api-authentication/platform-api.png)

A partir de aquí, siga los pasos descritos en el tutorial sobre la [adición de una API a un proyecto mediante una cuenta de servicio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partir del paso &quot;Configurar API&quot;) para finalizar el proceso.

>[!IMPORTANT]
>
>En un paso determinado durante el proceso vinculado anteriormente, el explorador descarga automáticamente una clave privada y un certificado público asociado. Tenga en cuenta dónde se almacena esta clave privada en el equipo, ya que es necesaria en un paso posterior de este tutorial.

### Recopilar credenciales

Una vez añadida la API al proyecto, la página **[!UICONTROL Experience Platform API]** del proyecto muestra las siguientes credenciales necesarias en todas las llamadas a las API de Experience Platform:

* `{API_KEY}` ([!UICONTROL Client ID])
* `{IMS_ORG}` ([!UICONTROL Organization ID])

![](././images/api-authentication/api-key-ims-org.png)

Además de las credenciales anteriores, también necesita el **[!UICONTROL Client Secret]** generado para un paso futuro. Seleccione **[!UICONTROL Retrieve client secret]** para mostrar el valor y, a continuación, cópielo para utilizarlo posteriormente.

![](././images/api-authentication/client-secret.png)

## Generar un token web JSON (JWT) {#jwt}

El siguiente paso es generar un token web JSON (JWT) basado en las credenciales de su cuenta. Este valor se utiliza para generar las credenciales `{ACCESS_TOKEN}` que se pueden usar en las llamadas a la API de plataforma, que deben regenerarse cada 24 horas.

Seleccione **[!UICONTROL Service Account (JWT)]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Generate JWT]**.

![](././images/api-authentication/generate-jwt.png)

En el cuadro de texto proporcionado en **[!UICONTROL Generate custom JWT]**, pegue el contenido de la clave privada que generó anteriormente al agregar la API de Platform a su cuenta de servicio. A continuación, seleccione **[!UICONTROL Generate Token]**.

![](././images/api-authentication/paste-key.png)

La página se actualiza para mostrar el JWT generado, junto con un comando cURL de ejemplo que le permite generar un token de acceso. Para los fines de este tutorial, seleccione **[!UICONTROL Copy]** junto a **[!UICONTROL Generated JWT]** para copiar el token en el portapapeles.

![](././images/api-authentication/copy-jwt.png)

## Generar un token de acceso

Una vez que haya generado un JWT, puede utilizarlo en una llamada de API para generar su `{ACCESS_TOKEN}`. A diferencia de los valores de `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para continuar usando las API de Platform.

**Solicitud**

La siguiente solicitud genera un nuevo `{ACCESS_TOKEN}` basado en las credenciales proporcionadas en la carga útil. Este extremo solo acepta datos de formulario como carga útil y, por lo tanto, debe recibir un encabezado `Content-Type` de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propiedad | Descripción |
| --- | --- |
| `{API_KEY}` | El `{API_KEY}` ([!UICONTROL Client ID]) que recuperó en un [paso anterior](#api-ims-secret). |
| `{SECRET}` | El secreto de cliente que recuperó en un [paso anterior](#api-ims-secret). |
| `{JWT}` | El JWT que ha generado en un [paso anterior](#jwt). |

>[!NOTE]
>
>Puede utilizar la misma clave de API, secreto de cliente y JWT para generar un nuevo token de acceso para cada sesión. Esto le permite automatizar la generación de token de acceso en sus aplicaciones.

**Respuesta**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Propiedad | Descripción |
| --- | --- |
| `token_type` | Tipo de token que se devuelve. Para los tokens de acceso, este valor siempre es `bearer`. |
| `access_token` | El `{ACCESS_TOKEN}` generado. Este valor, con el prefijo `Bearer`, es necesario como encabezado `Authentication` para todas las llamadas a la API de Platform. |
| `expires_in` | Número de milisegundos restantes hasta que caduca el token de acceso. Una vez que este valor alcance 0, se debe generar un nuevo token de acceso para continuar usando las API de Platform. |

## Probar credenciales de acceso

Una vez que haya recopilado las tres credenciales necesarias, puede intentar realizar la siguiente llamada de API. Esta llamada enumera todas las clases estándar [!DNL Experience Data Model] (XDM) disponibles para su organización.

**Solicitud**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Respuesta**

Si su respuesta es similar a la que se muestra a continuación, sus credenciales son válidas y funcionan. (Esta respuesta se ha truncado para el espacio).

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Uso de Postman para autenticar y probar llamadas de API

[](https://www.postman.com/) Postmanes una herramienta popular que permite a los desarrolladores explorar y probar las API de RESTful. Esta [publicación media](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describe cómo configurar Postman para que realice automáticamente la autenticación JWT y la utilice para consumir API de plataforma.

## Pasos siguientes

Al leer este documento, ha recopilado y probado correctamente sus credenciales de acceso para las API de Platform. Ahora puede seguir junto con las llamadas de API de ejemplo que se proporcionan en la [documentación](../landing/documentation/overview.md).

Además de los valores de autenticación recopilados en este tutorial, muchas API de plataforma también requieren que se proporcione un `{SANDBOX_NAME}` válido como encabezado. Consulte la [información general de los entornos limitados](../sandboxes/home.md) para obtener más información.