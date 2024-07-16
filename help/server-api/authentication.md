---
title: Autenticación
description: Obtenga información sobre cómo configurar la autenticación para la API de Adobe Experience Platform Edge Network Server.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 7%

---

# Autenticación {#authentication}

## Información general

[!DNL Edge Network Server API] administra la recopilación de datos autenticados y no autenticados, según el origen de los eventos y el dominio de recopilación de API.

Para cada solicitud, [!DNL Server API] comprueba la configuración de la secuencia de datos [!DNL access type]. Con esta configuración, los clientes pueden configurar un conjunto de datos para aceptar datos autenticados o tanto datos autenticados como no autenticados. De forma predeterminada, se aceptan ambos tipos de datos.

Para obtener más información sobre la configuración del tipo de acceso a la secuencia de datos, consulte la documentación sobre cómo [crear y configurar una secuencia de datos](../datastreams/overview.md#create).

A continuación se muestra un resumen del comportamiento, basado en la configuración del conjunto de datos [!DNL Access Type] y el extremo en el que se recibe la solicitud.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mixto (predeterminado) | No autentica la solicitud | Autentica la solicitud |
| autenticado | Autentica la solicitud | Autentica la solicitud |

Las llamadas de API procedentes de un servidor privado en `server.adobedc.net` siempre se deben autenticar.

## Requisitos previos {#prerequisites}

Antes de realizar llamadas a [!DNL Server API], asegúrese de cumplir los siguientes requisitos previos:

* Tiene una cuenta de organización con acceso a Adobe Experience Platform.
* Su cuenta de Experience Platform tiene habilitados los roles `developer` y `user` para el perfil de producto de la API de Adobe Experience Platform. Póngase en contacto con el Admin Console de [](../access-control/home.md) para habilitar estos roles en su cuenta.
* Tiene un Adobe ID. Si no tienes un Adobe ID, ve a [Adobe Developer Console](https://developer.adobe.com/console) y crea una nueva cuenta.

## Recopilar credenciales {#credentials}

Para realizar llamadas a las API de Platform, primero debe completar el [tutorial de autenticación](../landing/api-authentication.md). Al completar el tutorial de autenticación, se proporcionan los valores de cada uno de los encabezados necesarios en todas las llamadas a la API de Experience Platform, como se muestra a continuación:

* Autorización: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Los recursos de Experience Platform se pueden aislar en zonas protegidas virtuales específicas. En las solicitudes a las API de Platform, puede especificar el nombre y el ID de la zona protegida en la que se realizará la operación. Son parámetros opcionales.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obtener más información sobre las zonas protegidas en Experience Platform, consulte la [documentación general sobre las zonas protegidas](../sandboxes/home.md).

Todas las solicitudes que contienen una carga útil (POST, PUT, PATCH) requieren un encabezado de tipo de medios adicional:

* Tipo de contenido: `application/json`

## Configurar permisos de escritura del conjunto de datos {#dataset-write-permissions}

Para configurar los permisos de escritura del conjunto de datos, vaya al [Admin Console](https://adminconsole.adobe.com), busque el perfil de producto adjunto a la clave de API y establezca los siguientes permisos:

* En la sección [!UICONTROL Zonas protegidas], seleccione la zona protegida de la secuencia de datos.
* En la sección [!UICONTROL Administración de datos], seleccione el permiso **[!UICONTROL Administrar conjuntos de datos]**.

## Solución de errores de autorización {#troubleshooting-authorization}

| Código de error | Mensaje de error | Descripción |
| --- | --- | --- |
| `EXEG-0500-401` | Token de autorización no válido | Este mensaje de error se muestra en cualquiera de las siguientes situaciones:  <ul><li>Falta el valor del encabezado `authorization`.</li><li>El valor del encabezado `authorization` no incluye el token `Bearer` requerido.</li><li>El token de autorización proporcionado tiene un formato no válido.</li><li>La secuencia de datos requiere autenticación, pero en la solicitud faltan los encabezados obligatorios.</li></ul> |
| `EXEG-0501-401` | Token de autorización de usuario no válido | Este mensaje de error se muestra en cualquiera de las siguientes situaciones: <ul><li>A la llamada de API le falta el encabezado `x-user-token` necesario.</li><li>El token de usuario proporcionado tiene un formato no válido.</li></ul> |
| `EXEG-0502-401` | Token de autorización no válido | Este mensaje de error se muestra cuando el token de autorización proporcionado tiene un formato válido (JWT), pero su firma no es válida. Consulte el [tutorial de autenticación](../landing/api-authentication.md) para obtener información sobre cómo obtener un token JWT válido. |
| `EXEG-0503-401` | Token de autorización no válido | Este mensaje de error se muestra cuando caduca el token de autorización proporcionado. Vaya al [tutorial de autenticación](../landing/api-authentication.md) para generar un nuevo token. |
| `EXEG-0504-401` | Falta el contexto de producto requerido | Este mensaje de error se muestra en cualquiera de las siguientes situaciones:  <ul><li>La cuenta de desarrollador no tiene acceso al contexto de producto de Adobe Experience Platform.</li><li>La cuenta de empresa aún no tiene derecho a Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Falta el ámbito de token de autorización requerido | Este error solo se aplica a la autenticación de cuentas de servicio. El mensaje de error se muestra cuando el token de autorización de servicio incluido en la llamada pertenece a una cuenta de servicio que no tiene acceso al ámbito IMS `acp.foundation`. |
| `EXEG-0506-401` | Zona protegida no accesible para escritura | Este mensaje de error se muestra cuando la cuenta de desarrollador no tiene acceso de `WRITE` a la zona protegida de Experience Platform en la que se define la secuencia de datos. |
