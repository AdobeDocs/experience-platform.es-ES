---
keywords: Experience Platform;home;popular topics;Authenticate;access
solution: Experience Platform
title: Autenticar y acceder a las API de Experience Platform
topic: tutorial
description: 'Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de realizar llamadas a las API de Experience Platform. '
translation-type: tm+mt
source-git-commit: 76e6e1a5484dce0a4640c2ce1f43cf7d84e049bf
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 1%

---


# Autenticar y acceder a [!DNL Experience Platform] las API

Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de realizar llamadas a [!DNL Experience Platform] las API.

## Autenticar para realizar llamadas de API

Para mantener la seguridad de sus aplicaciones y usuarios, todas las solicitudes a las API de E/S de Adobe deben autenticarse y autorizarse mediante estándares como OAuth y JSON Web Tokens (JWT). El JWT se utiliza junto con la información específica del cliente para generar su token de acceso personal.

Este tutorial trata los pasos de la autenticación mediante la creación de un token de acceso que se describe en el siguiente diagrama de flujo:
![](images/authentication/authentication-flowchart.png)

## Requisitos previos

Para realizar correctamente llamadas a [!DNL Experience Platform] API, necesita lo siguiente:

* Una organización de IMS con acceso a Adobe Experience Platform
* Una cuenta de Adobe ID registrada
* Un administrador Admin Console para agregarle como **desarrollador** y un **usuario** para un producto.

Las siguientes secciones explican los pasos para crear un Adobe ID y convertirse en desarrollador y usuario de una organización.

### Crear un Adobe ID

Si no tiene un Adobe ID, puede crearlo siguiendo los pasos siguientes:

1. Vaya a [Adobe Developer Console](https://console.adobe.io)
2. Haga clic en **[!UICONTROL crear una cuenta nueva]**
3. Completar el proceso de registro

## Convertirse en desarrollador y usuario de [!DNL Experience Platform] una organización

Antes de crear integraciones en la E/S de Adobe, su cuenta debe tener permisos de desarrollador para un producto en una organización de IMS. Encontrará información detallada sobre las cuentas de desarrollador del Admin Console en el documento [de](https://helpx.adobe.com/es/enterprise/using/manage-developers.html) asistencia para la administración de desarrolladores.

**Obtener acceso de desarrollador**

Póngase en contacto con un [!DNL Admin Console] administrador de su organización para agregarle como desarrollador para uno de los productos de su organización mediante el [[!Admin Console DNL]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

El administrador debe asignarle como desarrollador al menos un perfil de producto para continuar.

![](images/authentication/add-developer.png)

Una vez que se le asigne como desarrollador, tendrá privilegios de acceso para crear integraciones en E/S [Adobe](https://www.adobe.com/go/devs_console_ui). Estas integraciones son una canalización de aplicaciones y servicios externos a la API de Adobe.

**Obtener acceso de usuario**

El [!DNL Admin Console] administrador también debe agregarlo al producto como usuario.

![](images/authentication/assign-users.png)

De forma similar al proceso de adición de un desarrollador, el administrador debe asignarle al menos un perfil de producto para continuar.

![](images/authentication/assign-user-details.png)

## Generar credenciales de acceso en Adobe Developer Console

>[!NOTE]
>
>Si está siguiendo este documento desde la guía [para desarrolladores de](../privacy-service/api/getting-started.md)Privacy Service, ahora puede volver a esa guía para generar las credenciales de acceso exclusivas para [!DNL Privacy Service].

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Su `{IMS_ORG}` y `{API_KEY}` sólo debe generarse una vez y puede reutilizarse en futuras llamadas [!DNL Platform] de API. Sin embargo, `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos se describen en detalle a continuación.

### Configuración única

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vacío en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, haga clic en **[!UICONTROL Añadir API]** en la pantalla Información general _del_ proyecto.

![](images/authentication/add-api-button.png)

Aparece la pantalla _Añadir una API_ . Haga clic en el icono de producto para Adobe Experience Platform y, a continuación, seleccione API **[!UICONTROL de]** Experience Platform antes de hacer clic en **[!UICONTROL Siguiente]**.

![](images/authentication/add-platform-api.png)

Una vez seleccionada [!DNL Experience Platform] como la API que se agregará al proyecto, siga los pasos descritos en el tutorial sobre la [adición de una API a un proyecto mediante una cuenta de servicio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partir del paso &quot;Configurar API&quot;) para finalizar el proceso.

Una vez que se ha agregado la API al proyecto, la página de información general _del_ proyecto muestra las siguientes credenciales que son necesarias en todas las llamadas a [!DNL Experience Platform] las API:

* `{API_KEY}` (ID de cliente)
* `{IMS_ORG}` (ID de organización)

![](./images/authentication/api-key-ims-org.png)

### Autenticación para cada sesión

La credencial requerida final que debe recopilar es la suya `{ACCESS_TOKEN}`. A diferencia de los valores para `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para continuar usando [!DNL Platform] API.

Para generar un nuevo `{ACCESS_TOKEN}`token, siga los pasos para [generar un token](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) JWT en la guía de credenciales de la consola de desarrollador.

## Comprobación de las credenciales de acceso

Una vez recopiladas las tres credenciales necesarias, puede intentar realizar la siguiente llamada de API. Esta llamada lista todas las clases [!DNL Experience Data Model] (XDM) dentro del `global` contenedor del Registro de Esquemas:

**Formato API**

```http
GET /global/classes
```

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

## Usar Postman para autenticación JWT y llamadas de API

[Postman](https://www.postman.com/) es una herramienta popular para trabajar con las API de RESTful. Esta publicación [](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) Media describe cómo configurar postman para que realice automáticamente la autenticación JWT y la utilice para consumir las API de Adobe Experience Platform.

## Pasos siguientes

Al leer este documento, ha recopilado y probado correctamente las credenciales de acceso para [!DNL Platform] las API. Ahora puede seguir el ejemplo de las llamadas de API que se proporcionan en toda la [documentación](../landing/documentation/overview.md).

Además de los valores de autenticación recopilados en este tutorial, muchas [!DNL Platform] API también requieren que se proporcione un valor válido `{SANDBOX_NAME}` como encabezado. Consulte la descripción general [de los](../sandboxes/home.md) entornos limitados para obtener más información.