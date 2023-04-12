---
title: Autenticación
description: Obtenga información sobre cómo configurar la autenticación para la API de Adobe Experience Platform Edge Network Server.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# Autenticación {#authentication}

## Información general

La variable [!DNL Edge Network Server API] gestiona la recopilación de datos autenticados y no autenticados, según la fuente de los eventos y el dominio de recopilación de API.

Para cada solicitud, la variable [!DNL Server API] verifica el conjunto de datos [!DNL access type] configuración. Con esta configuración, los clientes pueden configurar un conjunto de datos para aceptar datos autenticados o tanto autenticados como no autenticados. De forma predeterminada, se aceptan ambos tipos de datos.

Para obtener más información sobre la configuración del tipo de acceso del conjunto de datos, consulte la documentación sobre cómo [crear y configurar un conjunto de datos](../edge/datastreams/overview.md#create).

A continuación se muestra un resumen del comportamiento, basado en el conjunto de datos [!DNL Access Type] y el punto final en el que se recibe la solicitud.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mixto (predeterminado) | No autentica la solicitud | Autenticar solicitud |
| autenticado | Autenticar solicitud | Autenticar solicitud |

Llamadas de API procedentes de un servidor privado en `server.adobedc.net` siempre debe estar autenticado.

## Requisitos previos {#prerequisites}

Antes de poder realizar llamadas a la variable [!DNL Server API], asegúrese de cumplir los siguientes requisitos previos:

* Tiene una cuenta de organización con acceso a Adobe Experience Platform.
* Su cuenta de Experience Platform tiene la variable `developer` y `user` funciones habilitadas para el perfil de producto de la API de Adobe Experience Platform. Póngase en contacto con su [Admin Console](../access-control/home.md) para habilitar estas funciones en su cuenta.
* Tiene un Adobe ID. Si no tiene un Adobe ID, vaya a la sección [Consola de Adobe Developer](https://developer.adobe.com/console) y cree una cuenta nueva.

## Recopilar credenciales {#credentials}

Para realizar llamadas a las API de Platform, primero debe completar la variable [tutorial de autenticación](../landing/api-authentication.md). Al completar el tutorial de autenticación, se proporcionan los valores para cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Los recursos del Experience Platform se pueden aislar en entornos limitados virtuales específicos. En las solicitudes a las API de plataforma, puede especificar el nombre y el ID del simulador de pruebas en el que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre los entornos limitados en el Experience Platform, consulte la [documentación general de entorno limitado](../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medio adicional:

* Content-Type: `application/json`

## Configuración de permisos de escritura de conjuntos de datos {#dataset-write-permissions}

Para configurar los permisos de escritura del conjunto de datos, vaya a la [Admin Console](https://adminconsole.adobe.com), busque el perfil de producto adjunto a la clave de API y establezca los siguientes permisos:

* En el [!UICONTROL Sandboxes] , seleccione el entorno limitado del conjunto de datos.
* En el [!UICONTROL Gestión de datos] seleccione **[!UICONTROL Administrar conjuntos de datos]** permiso.

## Solución de errores de autorización {#troubleshooting-authorization}

| Código de error | Mensaje de error | Descripción |
| --- | --- | --- |
| `EXEG-0500-401` | Token de autorización no válido | Este mensaje de error se muestra en cualquiera de las situaciones siguientes:  <ul><li>La variable `authorization` falta el valor del encabezado.</li><li>La variable `authorization` el valor del encabezado no incluye el valor requerido `Bearer` token.</li><li>El token de autorización proporcionado tiene un formato no válido.</li><li>El conjunto de datos requiere autenticación, pero a la solicitud le faltan encabezados obligatorios.</li></ul> |
| `EXEG-0501-401` | Token de autorización de usuario no válido | Este mensaje de error se muestra en cualquiera de las situaciones siguientes: <ul><li>A la llamada de API le falta el `x-user-token` encabezado.</li><li>El token de usuario proporcionado tiene un formato no válido.</li></ul> |
| `EXEG-0502-401` | Token de autorización no válido | Este mensaje de error se muestra cuando el token de autorización proporcionado tiene un formato válido (JWT), pero su firma no es válida. Marque la [tutorial de autenticación](../landing/api-authentication.md) para aprender a obtener un token de JWT válido. |
| `EXEG-0503-401` | Token de autorización no válido | Este mensaje de error se muestra cuando caduca el token de autorización proporcionado. Vaya a [tutorial de autenticación](../landing/api-authentication.md) para generar un nuevo token. |
| `EXEG-0504-401` | Falta el contexto de producto requerido | Este mensaje de error se muestra en cualquiera de las situaciones siguientes:  <ul><li>La cuenta de desarrollador no tiene acceso al contexto del producto de Adobe Experience Platform.</li><li>La cuenta de empresa aún no tiene derecho a Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Falta el ámbito del token de autorización necesario | Este error solo se aplica a la autenticación de cuentas de servicio. El mensaje de error se muestra cuando el token de autorización de servicio incluido en la llamada pertenece a una cuenta de servicio que no tiene acceso al `acp.foundation` Ámbito de IMS. |
| `EXEG-0506-401` | Espacio aislado no accesible para escritura | Este mensaje de error se muestra cuando la cuenta de desarrollador no tiene `WRITE` acceso al simulador para pruebas de Experience Platform en el que se define el conjunto de datos. |
