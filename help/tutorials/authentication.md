---
keywords: Experience Platform;inicio;temas populares;Autenticar;acceso
solution: Experience Platform
title: API de Experience Platform de autenticación y acceso
topic-legacy: tutorial
type: Tutorial
description: 'Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de hacer llamadas a las API de Experience Platform. '
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 4%

---


# Autenticar y acceder a las API [!DNL Experience Platform]

Este documento proporciona un tutorial paso a paso para obtener acceso a una cuenta de desarrollador de Adobe Experience Platform con el fin de realizar llamadas a las API [!DNL Experience Platform].

## Autenticar para realizar llamadas a la API

Para mantener la seguridad de sus aplicaciones y usuarios, todas las solicitudes a las API de Adobe I/O deben autenticarse y autorizarse mediante estándares como OAuth y Tokens web JSON (JWT). A continuación, el JWT se utiliza junto con información específica del cliente para generar su token de acceso personal.

Este tutorial cubre los pasos de autenticación mediante la creación de un token de acceso descritos en el siguiente diagrama de flujo:
![](images/authentication/authentication-flowchart.png)

## Requisitos previos

Para realizar correctamente llamadas a las API [!DNL Experience Platform] , necesita lo siguiente:

* Una organización de IMS con acceso a Adobe Experience Platform
* Una cuenta de Adobe ID registrada
* Un administrador Admin Console para agregarlo como **desarrollador** y **usuario** para un producto.

En las secciones siguientes se describen los pasos para crear un Adobe ID y convertirse en desarrollador y usuario de una organización.

### Crear una Adobe ID

Si no tiene un Adobe ID, puede crearlo siguiendo estos pasos:

1. Vaya a [Adobe Developer Console](https://console.adobe.io)
2. Seleccione **[!UICONTROL create a new account]**
3. Completar el proceso de registro

## Conviértase en desarrollador y usuario de [!DNL Experience Platform] para una organización

Antes de crear integraciones en Adobe I/O, la cuenta debe tener permisos de desarrollador para un producto en una organización de IMS. Puede encontrar información detallada sobre las cuentas de desarrollador en el Admin Console en el [documento de soporte](https://helpx.adobe.com/es/enterprise/using/manage-developers.html) para administrar desarrolladores.

**Obtener acceso de desarrollador**

Póngase en contacto con un administrador de [!DNL Admin Console] de su organización para agregarle como desarrollador para uno de los productos de su organización mediante [[!DNL Admin Console]](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

El administrador debe asignarle como desarrollador a al menos un perfil de producto para continuar.

![](images/authentication/add-developer.png)

Una vez que se le asigne como desarrollador, tendrá privilegios de acceso para crear integraciones en [Adobe I/O](https://www.adobe.com/go/devs_console_ui). Estas integraciones son una canalización de aplicaciones y servicios externos a la API de Adobe.

**Obtener acceso de los usuarios**

El administrador de [!DNL Admin Console] también debe agregarle al producto como usuario.

![](images/authentication/assign-users.png)

Al igual que el proceso para añadir un desarrollador, el administrador debe asignarle al menos un perfil de producto para continuar.

![](images/authentication/assign-user-details.png)

## Generar credenciales de acceso en Adobe Developer Console

>[!NOTE]
>
>Si está siguiendo este documento desde la [guía para desarrolladores de Privacy Service](../privacy-service/api/getting-started.md), ahora puede regresar a esa guía para generar las credenciales de acceso exclusivas de [!DNL Privacy Service].

Con Adobe Developer Console, debe generar las tres credenciales de acceso siguientes:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Los `{IMS_ORG}` y `{API_KEY}` solo deben generarse una vez y pueden reutilizarse en futuras llamadas a la API [!DNL Platform]. Sin embargo, el `{ACCESS_TOKEN}` es temporal y debe regenerarse cada 24 horas.

Los pasos se detallan a continuación.

### Configuración única

Vaya a [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e inicie sesión con su Adobe ID. A continuación, siga los pasos descritos en el tutorial sobre la [creación de un proyecto vacío](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) en la documentación de Adobe Developer Console.

Una vez creado un nuevo proyecto, seleccione **[!UICONTROL Add API]** en la pantalla **Información general del proyecto**.

![](images/authentication/add-api-button.png)

Aparece la pantalla **Add an API**. Seleccione el icono del producto para Adobe Experience Platform y, a continuación, elija **[!UICONTROL Experience Platform API]** antes de seleccionar **[!UICONTROL Next]**.

![](images/authentication/add-platform-api.png)

Una vez que haya seleccionado [!DNL Experience Platform] como la API que se agregará al proyecto, siga los pasos descritos en el tutorial sobre la [adición de una API a un proyecto mediante una cuenta de servicio (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (a partir del paso &quot;Configurar API&quot;) para finalizar el proceso.

Una vez añadida la API al proyecto, la página **Información general del proyecto** muestra las siguientes credenciales que son necesarias en todas las llamadas a las API [!DNL Experience Platform]:

* `{API_KEY}` (ID de cliente)
* `{IMS_ORG}` (ID de organización)

![](./images/authentication/api-key-ims-org.png)

### Autenticación para cada sesión

La credencial requerida final que debe recopilar es su `{ACCESS_TOKEN}`. A diferencia de los valores de `{API_KEY}` y `{IMS_ORG}`, se debe generar un nuevo token cada 24 horas para continuar usando las API [!DNL Platform].

Para generar un `{ACCESS_TOKEN}` nuevo, siga los pasos para [generar un token JWT](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) en la guía de credenciales de Developer Console.

## Probar credenciales de acceso

Una vez que haya recopilado las tres credenciales necesarias, puede intentar realizar la siguiente llamada de API. Esta llamada enumerará todas las clases [!DNL Experience Data Model] (XDM) dentro del contenedor `global` del Registro de esquemas:

**Formato de API**

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

## Uso de Postman para autenticación JWT y llamadas de API

[](https://www.postman.com/) Postmanes una herramienta popular para trabajar con las API de RESTful. Esta [publicación media](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) describe cómo configurar un postman para que realice automáticamente la autenticación JWT y la utilice para consumir las API de Adobe Experience Platform.

## Pasos siguientes

Al leer este documento, ha recopilado y probado correctamente sus credenciales de acceso para las API [!DNL Platform]. Ahora puede seguir junto con las llamadas de API de ejemplo que se proporcionan en la [documentación](../landing/documentation/overview.md).

Además de los valores de autenticación recopilados en este tutorial, muchas API [!DNL Platform] también requieren que se proporcione un `{SANDBOX_NAME}` válido como encabezado. Consulte la [información general de los entornos limitados](../sandboxes/home.md) para obtener más información.