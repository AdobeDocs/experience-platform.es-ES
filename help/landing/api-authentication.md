---
keywords: Experience Platform;inicio;temas populares;Autenticar;acceso
solution: Experience Platform
title: API de Experience Platform de autenticación y acceso
type: Tutorial
description: Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de hacer llamadas a las API de Experience Platform.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 0a4883cff4f8e04dd0dd62a9e01435fa302a9e54
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 8%

---


# Autenticación y acceso a las API de Experience Platform

Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de hacer llamadas a las API de Experience Platform. Al final de este tutorial, habrá generado las siguientes credenciales que son necesarias para todas las llamadas a la API de plataforma:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

Para mantener la seguridad de sus aplicaciones y usuarios, todas las solicitudes a las API de Adobe I/O deben autenticarse y autorizarse mediante estándares como OAuth y Tokens web JSON (JWT). Se utiliza un JWT junto con información específica del cliente para generar su token de acceso personal.

Este tutorial explica cómo recopilar las credenciales necesarias para autenticar llamadas a la API de plataforma, tal como se describe en el siguiente diagrama de flujo:

![](./images/api-authentication/authentication-flowchart.png)

## Requisitos previos

Para realizar correctamente llamadas a las API de Experience Platform, debe tener lo siguiente:

* Una organización de IMS con acceso a Adobe Experience Platform.
* Un administrador de Admin Console que puede agregarle como desarrollador y un usuario para un perfil de producto.

También debe tener un Adobe ID para completar este tutorial. Si no tiene un Adobe ID, puede crearlo siguiendo estos pasos:

1. Vaya a [Consola de Adobe Developer](https://console.adobe.io).
2. Select **[!UICONTROL Crear una cuenta nueva]**.
3. Complete el proceso de registro.

## Obtener acceso de desarrollador y usuario para Experience Platform

Antes de crear integraciones en Adobe Developer Console, la cuenta debe tener permisos de desarrollador y usuario para un perfil de producto de Experience Platform en Adobe Admin Console.

### Obtener acceso de desarrollador

Póngase en contacto con un [!DNL Admin Console] administrador de su organización para agregarlo como desarrollador a un perfil de producto de Experience Platform mediante la función [[!DNL Admin Console]](https://adminconsole.adobe.com/). Consulte la [!DNL Admin Console] documentación para instrucciones específicas sobre cómo [administrar el acceso de los desarrolladores para perfiles de producto](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Una vez que esté asignado como desarrollador, puede empezar a crear integraciones en [Consola de Adobe Developer](https://www.adobe.com/go/devs_console_ui). Estas integraciones son una canalización de aplicaciones y servicios externos a API de Adobe.

### Obtener acceso de los usuarios

Su [!DNL Admin Console] El administrador también debe agregarle como usuario al mismo perfil de producto. Consulte la guía de [administración de grupos de usuarios en [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) para obtener más información.

## Generar una clave de API, el ID de organización de IMS y el secreto del cliente {#api-ims-secret}

>[!NOTE]
>
>Si está siguiendo este documento desde el [Guía de API del Privacy Service](../privacy-service/api/getting-started.md), ahora puede volver a esa guía para generar las credenciales de acceso exclusivas de [!DNL Privacy Service].

Una vez que haya obtenido acceso de desarrollador y usuario a Platform a través de [!DNL Admin Console], el siguiente paso es generar el `{ORG_ID}` y `{API_KEY}` credenciales en la consola de Adobe Developer. Estas credenciales solo deben generarse una vez y pueden reutilizarse en futuras llamadas a la API de Platform.

### Agregar un Experience Platform a un proyecto

Vaya a la [consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial en [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Añadir API]** en el **[!UICONTROL Información general del proyecto]** en el Navegador.

![](./images/api-authentication/add-api.png)

Aparece la pantalla **[!UICONTROL Añadir una API]**. Seleccione el icono del producto para Adobe Experience Platform y, a continuación, elija **[!UICONTROL API de Experience Platform]** antes de seleccionar **[!UICONTROL Siguiente]**.

![](./images/api-authentication/platform-api.png)

A partir de aquí, siga los pasos descritos en el tutorial de [adición de una API a un proyecto mediante una cuenta de servicio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partir del paso &quot;Configurar API&quot;) para finalizar el proceso.

>[!IMPORTANT]
>
>En un paso determinado durante el proceso vinculado anteriormente, el explorador descarga automáticamente una clave privada y un certificado público asociado. Tenga en cuenta dónde se almacena esta clave privada en el equipo, ya que es necesaria en un paso posterior de este tutorial.

### Recopilar credenciales

Una vez añadida la API al proyecto, la variable **[!UICONTROL API de Experience Platform]** para el proyecto muestra las siguientes credenciales que son necesarias en todas las llamadas a las API de Experience Platform:

* `{API_KEY}` ([!UICONTROL ID del cliente])
* `{ORG_ID}` ([!UICONTROL ID de organización])

![](././images/api-authentication/api-key-ims-org.png)

Además de las credenciales anteriores, también necesita el **[!UICONTROL Secreto del cliente]** para un paso futuro. Select **[!UICONTROL Recuperar secreto de cliente]** para mostrar el valor y, a continuación, cópielo para utilizarlo más adelante.

![](././images/api-authentication/client-secret.png)

## Generar un token web JSON (JWT) {#jwt}

El siguiente paso es generar un token web JSON (JWT) basado en las credenciales de su cuenta. Este valor se utiliza para generar su `{ACCESS_TOKEN}` credencial para su uso en llamadas de API de plataforma, que deben regenerarse cada 24 horas.

>[!IMPORTANT]
>
>Para los fines de este tutorial, los pasos siguientes describen cómo generar un JWT dentro de Developer Console. Sin embargo, este método de generación solo debe utilizarse con fines de prueba y evaluación.
>
>Para uso regular, el JWT debe generarse automáticamente. Para obtener más información sobre cómo generar JWT mediante programación, consulte la [guía de autenticación de cuenta de servicio](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) en Adobe Developer.

Select **[!UICONTROL Cuenta de servicio (JWT)]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Generar JWT]**.

![](././images/api-authentication/generate-jwt.png)

En el cuadro de texto que figura en **[!UICONTROL Generar JWT personalizado]**, pegue el contenido de la clave privada que generó anteriormente al agregar la API de Platform a su cuenta de servicio. A continuación, seleccione **[!UICONTROL Generar token]**.

![](././images/api-authentication/paste-key.png)

La página se actualiza para mostrar el JWT generado, junto con un comando cURL de ejemplo que le permite generar un token de acceso. Para los fines de este tutorial, seleccione **[!UICONTROL Copiar]** junto a **[!UICONTROL JWT generado]** para copiar el token en el portapapeles.

![](././images/api-authentication/copy-jwt.png)

## Generar un token de acceso

Una vez que haya generado un JWT, puede utilizarlo en una llamada de API para generar su `{ACCESS_TOKEN}`. A diferencia de los valores de `{API_KEY}` y `{ORG_ID}`, se debe generar un nuevo token cada 24 horas para continuar usando las API de Platform.

**Solicitud**

La siguiente solicitud genera un nuevo `{ACCESS_TOKEN}` en función de las credenciales proporcionadas en la carga útil. Este extremo solo acepta datos de formulario como carga útil y, por lo tanto, debe recibir una `Content-Type` encabezado de `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Propiedad | Descripción |
| --- | --- |
| `{API_KEY}` | La variable `{API_KEY}` ([!UICONTROL ID de cliente]) que recuperó en un [paso anterior](#api-ims-secret). |
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
| `access_token` | El `{ACCESS_TOKEN}`. Este valor, con el prefijo word `Bearer`, es necesario ya que la variable `Authentication` para todas las llamadas a la API de Platform. |
| `expires_in` | Número de milisegundos restantes hasta que caduca el token de acceso. Una vez que este valor alcance 0, se debe generar un nuevo token de acceso para continuar usando las API de Platform. |

## Probar credenciales de acceso

Una vez que haya recopilado las tres credenciales necesarias, puede intentar realizar la siguiente llamada de API. Esta llamada enumera todas las [!DNL Experience Data Model] (XDM) clases disponibles para su organización.

**Solicitud**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
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

[Postman](https://www.postman.com/) es una herramienta popular que permite a los desarrolladores explorar y probar las API de RESTful. Esta [Publicación media](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describe cómo configurar Postman para que realice automáticamente la autenticación JWT y la utilice para consumir las API de Platform.

## Pasos siguientes

Al leer este documento, ha recopilado y probado correctamente sus credenciales de acceso para las API de Platform. Ahora puede seguir el ejemplo de llamadas de API que se proporcionan a través de la [documentación](../landing/documentation/overview.md).

Además de los valores de autenticación recopilados en este tutorial, muchas API de plataforma también requieren una `{SANDBOX_NAME}` que se proporcionará como encabezado. Consulte la [información general sobre los entornos limitados](../sandboxes/home.md) para obtener más información.