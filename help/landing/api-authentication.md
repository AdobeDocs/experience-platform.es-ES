---
solution: Experience Platform
title: Autenticar y acceder a las API de Experience Platform
type: Tutorial
description: Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de hacer llamadas a las API de Experience Platform.
role: Developer
feature: API
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2508'
ht-degree: 3%

---


# Autenticación y acceso a las API de Experience Platform

Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de realizar llamadas a las API de Experience Platform. Al final de este tutorial, habrá generado o recopilado las siguientes credenciales que se requieren como encabezados en todas las llamadas a la API de Experience Platform:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{ORG_ID}`

>[!TIP]
>
>Además de las tres credenciales anteriores, muchas API de Experience Platform también requieren que se proporcione un `{SANDBOX_NAME}` válido como encabezado. Consulte la [descripción general de las zonas protegidas](../sandboxes/home.md) para obtener más información sobre las zonas protegidas y la documentación de [extremo de administración de la zona protegida](/help/sandboxes/api/sandboxes.md#list) para obtener información sobre cómo enumerar las zonas protegidas disponibles para su organización.

Para mantener la seguridad de sus aplicaciones y usuarios, todas las solicitudes a las API de Experience Platform deben autenticarse y autorizarse con estándares como OAuth.

Este tutorial explica cómo recopilar las credenciales necesarias para autenticar las llamadas a la API de Experience Platform, tal como se describe en el diagrama de flujo siguiente. Puede recopilar la mayoría de las credenciales necesarias en la configuración inicial única. Sin embargo, el token de acceso debe actualizarse cada 24 horas.

![Requisitos del flujo de autenticación para la configuración inicial única y cada sesión subsiguiente.](./images/api-authentication/authentication-flowchart.png)

## Requisitos previos {#prerequisites}

Para realizar llamadas correctamente a las API de Experience Platform, debe tener lo siguiente:

* Una organización con acceso a Adobe Experience Platform.
* Un administrador de Admin Console que puede agregarle como desarrollador y como usuario de un perfil de producto.
* Un administrador del sistema de Experience Platform que puede otorgarle los controles de acceso basados en atributos necesarios para realizar operaciones de lectura o escritura en diferentes partes de Experience Platform a través de API.

También debe disponer de un Adobe ID para completar este tutorial. Si no tiene una Adobe ID, puede crearla siguiendo estos pasos:

1. Ir a [Adobe Developer Console](https://console.adobe.io).
2. Seleccione **[!UICONTROL Crear una nueva cuenta]**.
3. Complete el proceso de registro.

## Obtener acceso de desarrollador y usuario para Experience Platform {#gain-developer-user-access}

Antes de crear integraciones en Adobe Developer Console, la cuenta debe tener permisos de desarrollador y usuario para un perfil de producto de Experience Platform en Adobe Admin Console.

### Obtener acceso de desarrollador {#gain-developer-access}

Póngase en contacto con un administrador de Admin Console de su organización para agregarle como desarrollador a un perfil de productos de Experience Platform. Consulte la documentación de Admin Console para obtener instrucciones específicas sobre cómo [administrar el acceso de desarrollador para perfiles de producto](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Una vez que se le asigne como desarrollador, puede empezar a crear integraciones en [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Estas integraciones son una canalización de aplicaciones y servicios externos a las API de Adobe.

### Obtener acceso de usuario {#gain-user-access}

El administrador de Admin Console también debe agregarle como usuario al mismo perfil de producto. Con el acceso de los usuarios, puede ver en la interfaz de usuario el resultado de las operaciones de API que realiza.

Consulte la guía sobre [administración de grupos de usuarios en Admin Console](https://helpx.adobe.com/es/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) para obtener más información.

## Generación de una clave de API (ID de cliente) y un ID de organización {#generate-credentials}

>[!NOTE]
>
>Si está siguiendo este documento desde la [guía de API de Privacy Service](../privacy-service/api/getting-started.md), ahora puede volver a esa guía para generar las credenciales de acceso únicas de [!DNL Privacy Service].

Una vez que se le haya concedido acceso de desarrollador y usuario a Experience Platform mediante Admin Console, el siguiente paso es generar sus credenciales de `{ORG_ID}` y `{API_KEY}` en Adobe Developer Console. Estas credenciales solo deben generarse una vez y pueden reutilizarse en futuras llamadas a la API de Experience Platform.

>[!TIP]
>
>En lugar de ir a Developer Console, puede obtener todas las credenciales de autenticación que necesita para trabajar con las API de Experience Platform directamente desde las páginas de documentación de referencia de las API. [Más información](#get-credentials-functionality) sobre la nueva funcionalidad.

### Añadir Experience Platform a un proyecto {#add-platform-to-project}

Vaya a la [consola de desarrollador de Adobe](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre [creación de un proyecto vacío](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) en la documentación de Adobe Developer Console.

Una vez que haya creado un nuevo proyecto, seleccione **[!UICONTROL Agregar API]** en la pantalla **[!UICONTROL Información general del proyecto]**.

>[!TIP]
>
>Si está aprovisionado para varias organizaciones, utilice el selector de organizaciones en la esquina superior derecha de la interfaz para asegurarse de que se encuentra en la organización que necesita.

![Pantalla de Developer Console con la opción Agregar API resaltada.](./images/api-authentication/add-api.png)

Aparece la pantalla **[!UICONTROL Añadir una API]**. Seleccione el icono del producto para **[!UICONTROL Adobe Experience Platform]** y, a continuación, elija **[!UICONTROL Experience Platform API]** antes de seleccionar **[!UICONTROL Siguiente]**.

![Seleccione la API de Experience Platform en la pantalla Agregar una API.](./images/api-authentication/platform-api.png)

>[!TIP]
>
>Seleccione la opción **[!UICONTROL Ver documentos]** para navegar en una ventana separada del explorador a la [documentación de referencia de la API de Experience Platform](https://developer.adobe.com/experience-platform-apis/) completa.

### Seleccione el tipo de autenticación [!UICONTROL OAuth Server-to-Server] {#select-oauth-server-to-server}

A continuación, seleccione el tipo de autenticación **[!UICONTROL OAuth Server-to-Server]** para generar tokens de acceso y acceder a la API de Experience Platform. Asigne un nombre significativo a su credencial en el campo de texto **[!UICONTROL Nombre de credencial]** antes de seleccionar **[!UICONTROL Siguiente]**.

>[!IMPORTANT]
>
>El método **[!UICONTROL OAuth Server-to-Server]** es el único método de generación de tokens compatible a partir de ahora. El método **[!UICONTROL Service Account (JWT)]** compatible anteriormente está obsoleto y no se puede seleccionar para nuevas integraciones. Aunque las integraciones existentes que utilicen el método de autenticación JWT seguirán funcionando hasta el 30 de junio de 2025, Adobe recomienda migrar las integraciones existentes al nuevo método [!UICONTROL OAuth Server-to-Server] antes de esa fecha. Obtenga más información en la sección [!BADGE Obsoleto]{type=negative}[Generar un token web JSON (JWT)](#jwt).

![Seleccione el método de autenticación de servidor a servidor OAuth para la API de Experience Platform.](./images/api-authentication/oauth-authentication-method.png)

### Selección de los perfiles de producto para la integración {#select-product-profiles}

En la pantalla **[!UICONTROL Configurar API]**, seleccione **[!UICONTROL AEP-Default-All-Users]** junto con cualquier perfil de producto adicional al que desee obtener acceso.

>[!IMPORTANT]
>
>Para obtener acceso a determinadas funciones de Experience Platform, también necesita que un administrador del sistema le conceda los permisos de control de acceso basados en atributos necesarios. Obtenga más información en la sección [Obtener los permisos de control de acceso necesarios basados en atributos](#get-abac-permissions).

![Seleccione perfiles de producto para su integración.](./images/api-authentication/select-product-profiles.png)

Seleccione **[!UICONTROL Guardar la API configurada]** cuando esté listo.

En el tutorial de vídeo siguiente también se muestra una descripción detallada de los pasos descritos anteriormente para configurar una integración con la API de Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/31627/?learn=on&captions=spa)

### Recopilar credenciales {#gather-credentials}

Una vez que la API se ha agregado al proyecto, la página **[!UICONTROL Servidor a servidor OAuth]** del proyecto muestra las siguientes credenciales que son necesarias en todas las llamadas a las API de Experience Platform:

![Información de integración después de agregar una API en Developer Console.](./images/api-authentication/api-integration-information.png)

* `{API_KEY}` ([!UICONTROL ID de cliente])
* `{ORG_ID}` ([!UICONTROL ID de organización])

<!--

![](././images/api-authentication/api-key-ims-org.png)

<!--

In addition to the above credentials, you also need the generated **[!UICONTROL Client Secret]** for a future step. Select **[!UICONTROL Retrieve client secret]** to reveal the value, and then copy it for later use.

![](././images/api-authentication/client-secret.png)

-->

## Generación de un token de acceso {#generate-access-token}

El siguiente paso es generar una credencial `{ACCESS_TOKEN}` para usarla en llamadas a la API de Experience Platform. A diferencia de los valores de `{API_KEY}` y `{ORG_ID}`, se debe generar un nuevo token cada 24 horas para seguir usando las API de Experience Platform. Seleccione **[!UICONTROL Generar token de acceso]** que produce su token de acceso, como se muestra a continuación.

![Mostrar cómo generar token de acceso](././images/api-authentication/generate-access-token.png)

>[!TIP]
>
>También puede utilizar un entorno y una colección de Postman para generar tokens de acceso. Para obtener más información, lea la sección sobre [el uso de Postman para autenticar y probar las llamadas a la API](#use-postman).

## Cree y recupere credenciales de autenticación directamente en la documentación de referencia de la API {#get-credentials-functionality}

A partir de la versión de noviembre de 2024 de Experience Platform, podrá obtener las credenciales para usar las API de Experience Platform directamente desde las páginas de referencia de las API, sin necesidad de ir a [!UICONTROL Developer Console]. Vea el ejemplo siguiente desde la [API de Flow Service: página de destinos](https://developer.adobe.com/experience-platform-apis/references/destinations/).

![Obtener funcionalidad de credenciales resaltada en la parte superior de una página de referencia de API.](././images/api-authentication/get-credentials-highlighted.png)

Para obtener las credenciales para llamar a las API de Experience Platform, ve a cualquier página de referencia de la API de Experience Platform y selecciona **[!UICONTROL Iniciar sesión]** en la parte superior de la página. Inicia sesión con tu **[!UICONTROL cuenta personal]** o con **[!UICONTROL cuenta de empresa o escuela]**.

Después de iniciar sesión, seleccione **[!UICONTROL Crear nueva credencial]** para crear un nuevo conjunto de credenciales y poder acceder a las API de Experience Platform.

![Cree nuevas credenciales para acceder a las API de Experience Platform.](././images/api-authentication/create-credentials.gif)

A continuación, utilice el selector desplegable para abrir la ventana de credenciales, generar un token de acceso y obtener la clave de API y el ID de organización. Copie las credenciales en los bloques [**[!UICONTROL Try it]**](/help/release-notes/2024/may-2024.md#interactive-api-documentation) de las páginas de referencia de la API para empezar a trabajar con las API de Experience Platform.

![Use el selector desplegable para ver las credenciales y generar un token de acceso.](././images/api-authentication/view-copy-credentials.gif)

>[!TIP]
>
>El bloque de credenciales de la parte superior de la página permanece mostrado a medida que navega entre diferentes páginas de extremos en la documentación de referencia de la API de Experience Platform.

## [!BADGE Obsoleto]{type=negativo} Generar un token web JSON (JWT) {#jwt}

>[!WARNING]
>
>El método JWT para generar tokens de acceso ha quedado obsoleto. Todas las integraciones nuevas deben crearse con el [método de autenticación de servidor a servidor OAuth](#select-oauth-server-to-server). Adobe también requiere que migre las integraciones existentes al método OAuth antes del 30 de junio de 2025 para que las integraciones sigan funcionando. Lea la siguiente documentación importante:
> 
>* [Guía de migración para sus aplicaciones de JWT a OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)
>* [Guía de implementación para aplicaciones nuevas y antiguas con OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation/)
>* [Ventajas de usar el método de credenciales de servidor a servidor OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#why-oauth-server-to-server-credentials)

+++ Ver información obsoleta

El siguiente paso es generar un token web JSON (JWT) basado en las credenciales de la cuenta. Este valor se usa para generar la credencial `{ACCESS_TOKEN}` para usarla en llamadas a la API de Experience Platform, que deben regenerarse cada 24 horas.

>[!IMPORTANT]
>
>Para los fines de este tutorial, los pasos siguientes describen cómo generar un JWT en Developer Console. Sin embargo, este método de generación solo debe utilizarse con fines de prueba y evaluación.
>
>Para un uso normal, el JWT debe generarse automáticamente. Para obtener más información sobre cómo generar JWT mediante programación, consulte la [guía de autenticación de cuenta de servicio](https://www.adobe.io/developer-console/docs/guides/authentication/JWT/) en Adobe Developer.

Seleccione **[!UICONTROL Cuenta de servicio (JWT)]** en el panel de navegación izquierdo y, a continuación, seleccione **[!UICONTROL Generar JWT]**.

![](././images/api-authentication/generate-jwt.png)

En el cuadro de texto que aparece en **[!UICONTROL Generar JWT personalizado]**, pegue el contenido de la clave privada que generó anteriormente al agregar la API de Experience Platform a su cuenta de servicio. A continuación, seleccione **[!UICONTROL Generar token]**.

![](././images/api-authentication/paste-key.png)

La página se actualiza para mostrar el JWT generado, junto con un ejemplo de comando cURL que le permite generar un token de acceso. Para los propósitos de este tutorial, seleccione **[!UICONTROL Copiar]** junto a **[!UICONTROL JWT generado]** para copiar el token en su portapapeles.

![](././images/api-authentication/copy-jwt.png)

**Generar un token de acceso**

Una vez que haya generado un JWT, puede utilizarlo en una llamada de API para generar su `{ACCESS_TOKEN}`. A diferencia de los valores de `{API_KEY}` y `{ORG_ID}`, se debe generar un nuevo token cada 24 horas para seguir usando las API de Experience Platform.

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
| `{API_KEY}` | El `{API_KEY}` ([!UICONTROL ID de cliente]) que recuperó en un [paso anterior](#api-ims-secret). |
| `{SECRET}` | Secreto de cliente que recuperó en un [paso anterior](#api-ims-secret). |
| `{JWT}` | El JWT que generó en un [paso anterior](#jwt). |

>[!NOTE]
>
>Puede utilizar la misma clave de API, secreto de cliente y JWT para generar un nuevo token de acceso para cada sesión. Esto le permite automatizar la generación de tokens de acceso en las aplicaciones.

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
| `token_type` | El tipo of token devuelto. Para tokens de acceso, este valor siempre es `bearer`. |
| `access_token` | El `{ACCESS_TOKEN}` generado. Este valor, con el prefijo `Bearer`, es necesario como encabezado `Authentication` para todas las llamadas a la API de Experience Platform. |
| `expires_in` | Número de milisegundos que restan hasta que caduque el token de acceso. Una vez que este valor alcanza 0, se debe generar un nuevo token de acceso para seguir utilizando las API de Experience Platform. |

+++

## Probar credenciales de acceso {#test-credentials}

Una vez que haya recopilado las tres credenciales necesarias (token de acceso, clave de API e ID de organización) , puede intentar realizar la siguiente llamada de API. Esta llamada enumera todas las clases estándar [!DNL Experience Data Model] (XDM) disponibles para su organización. Importe y ejecute la llamada en [Postman](#use-postman).

>[!BEGINSHADEBOX]

**Solicitud**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}'
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

>[!ENDSHADEBOX]

>[!IMPORTANT]
>
>Aunque la llamada anterior es suficiente para probar las credenciales de acceso, tenga en cuenta que no podrá acceder ni modificar varios recursos sin tener los permisos de control de acceso basados en atributos adecuados. Obtenga más información en la sección **Obtener los permisos de control de acceso basados en atributos necesarios** a continuación.

## Obtenga los permisos de control de acceso basados en atributos necesarios {#get-abac-permissions}

Para acceder o modificar varios recursos dentro de Experience Platform, debe tener los permisos de control de acceso adecuados. Los administradores del sistema pueden otorgarle los [permisos que necesita](/help/access-control/ui/permissions.md). Obtenga más información en la sección acerca de [administrar credenciales de API para un rol](/help/access-control/abac/ui/permissions.md#manage-api-credentials-for-role).

Encontrará información detallada sobre cómo un administrador del sistema puede conceder los permisos necesarios para acceder a los recursos de Experience Platform a través de la API en el siguiente tutorial de vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/31627/?learn=on&t=159&captions=spa)

## Usar Postman para autenticar y probar llamadas a la API {#use-postman}

[Postman](https://www.postman.com/) es una herramienta popular que permite a los desarrolladores explorar y probar las API de RESTful. Puede utilizar las colecciones y los entornos de Experience Platform Postman para acelerar su trabajo con las API de Experience Platform. Obtenga más información sobre [el uso de Postman en Experience Platform](/help/landing/postman.md) y la introducción a las colecciones y los entornos.

Encontrará información detallada sobre el uso de Postman con colecciones y entornos de Experience Platform en los videotutoriales que se muestran a continuación:

**Descargar e importar un entorno de Postman para utilizarlo con las API de Experience Platform**

>[!VIDEO](https://video.tv.adobe.com/v/31627/?learn=on&t=106&captions=spa)

**Use una colección de Postman para generar tokens de acceso**

Descargue la [colección Postman del servicio Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) y vea el siguiente vídeo para aprender a generar tokens de acceso.

>[!VIDEO](https://video.tv.adobe.com/v/32727/?learn=on&captions=spa)

**Descargue colecciones Postman de API de Experience Platform e interactúe con las API**

>[!VIDEO](https://video.tv.adobe.com/v/32723/?learn=on&captions=spa)

<!--
This [Medium post](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describes how you can set up Postman to automatically perform JWT authentication and use it to consume Experience Platform APIs.
-->

## Administradores del sistema: Conceder control de acceso a API y desarrollador con permisos de Experience Platform {#grant-developer-and-api-access-control}

Para poder crear integraciones en Adobe Developer Console, la cuenta debe tener permisos de desarrollador y usuario para un perfil de producto de Experience Platform.

>[!NOTE]
>
>Solo los administradores del sistema tienen la capacidad de ver y administrar credenciales de API en Permisos.

### Añadir desarrolladores al perfil del producto {#add-developers-to-product-profile}

Vaya a [Admin Console](https://adminconsole.adobe.com/) e inicie sesión con su Adobe ID.

Seleccione **[!UICONTROL Productos]** de la barra de navegación y luego seleccione **[!UICONTROL Adobe Experience Platform]** de la lista de productos.

![La página de productos en Adobe Admin Console con el producto Adobe Experience Platform resaltado.](././images/api-authentication/products.png)

En la ficha **[!UICONTROL Perfiles de producto]**, seleccione **[!UICONTROL AEP-Default-All-Users]**. También puede utilizar la barra de búsqueda para buscar el perfil del producto introduciendo el nombre.

![La página de perfiles de producto con la barra de búsqueda y el producto AEP-Default-All-Users resaltados.](././images/api-authentication/select-product-profile.png)

Seleccione la ficha **[!UICONTROL Desarrolladores]** y luego seleccione **[!UICONTROL Agregar desarrollador]**.

![Se muestra la ficha de desarrolladores con la opción Agregar desarrolladores resaltada,](././images/api-authentication/add-developer1.png)

Aparecerá el cuadro de diálogo **[!UICONTROL Agregar desarrolladores]**. Escriba el **[!UICONTROL correo electrónico o nombre de usuario]** del desarrollador. [!UICONTROL Correo electrónico o nombre de usuario] válidos muestran los detalles del desarrollador. Seleccione **[!UICONTROL Guardar]**.

![Se ha rellenado el cuadro de diálogo Agregar desarrolladores con información de desarrolladores y se ha resaltado la opción Guardar.](././images/api-authentication/add-developer-email.png)

El desarrollador se ha agregado correctamente y aparece en la ficha **[!UICONTROL Desarrolladores]**.

![La pestaña de desarrolladores muestra la lista de todos los desarrolladores agregados con el desarrollador recién agregado resaltado.](././images/api-authentication/developer-added.png)

### Asignar credenciales de API a un rol

>[!NOTE]
>
>Solo un administrador del sistema puede asignar API a funciones en la interfaz de usuario de Experience Platform.

Para utilizar y realizar operaciones en las API de Experience Platform, un administrador del sistema debe agregar las credenciales de la API además del conjunto de permisos dado a una función. Obtenga más información en la sección acerca de [administrar credenciales de API para un rol](../access-control/abac/ui/permissions.md#manage-api-credentials-for-a-role).

En el tutorial de vídeo siguiente también se muestra una descripción detallada de los pasos descritos anteriormente para añadir desarrolladores a perfiles de producto y asignar API a funciones:

>[!VIDEO](https://video.tv.adobe.com/v/3446401/?learn=on&captions=spa)

## Recursos adicionales {#additional-resources}

Consulte los recursos adicionales vinculados a continuación para obtener más ayuda sobre cómo empezar a utilizar las API de Experience Platform

* [Autenticar y acceder a la página de tutoriales en vídeo de las API de Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=es)
* [Recopilación de Postman del servicio Identity Management](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) para generar tokens de acceso
* [Colecciones Postman de API de Experience Platform](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)

## Pasos siguientes {#next-steps}

Al leer este documento, ha recopilado y probado correctamente sus credenciales de acceso para las API de Experience Platform. Ahora puede seguir junto con las llamadas de API de ejemplo proporcionadas a lo largo de [documentación](../landing/documentation/overview.md).

Además de los valores de autenticación recopilados en este tutorial, muchas API de Experience Platform también requieren que se proporcione un `{SANDBOX_NAME}` válido como encabezado. Consulte la [información general sobre las zonas protegidas](../sandboxes/home.md) para obtener más detalles.
