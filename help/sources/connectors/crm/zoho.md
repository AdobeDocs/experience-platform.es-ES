---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Información general sobre el conector Source Zoho CRM
description: Aprenda a conectar Zoho CRM a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!WARNING]
>
>El origen [!DNL Zoho CRM] quedará obsoleto a finales de junio de 2025.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de [!DNL Experience Platform]. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Zoho CRM].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Recuperar sus credenciales de autenticación para [!DNL Zoho CRM]

Para poder llevar los datos de su cuenta de [!DNL Zoho CRM] a Experience Platform, primero debe recuperar las credenciales para autenticar el origen de [!DNL Zoho CRM]. Siga los pasos a continuación para recuperar el ID de cliente, el secreto de cliente, el token de acceso y el token de actualización.

### Registre la aplicación

El primer paso para recuperar las credenciales de autenticación es registrar la aplicación mediante [[!DNL Zoho CRM] developer console](https://accounts.zoho.com/). Para registrar la aplicación, debe seleccionar el tipo de cliente de: JavaScript, aplicaciones móviles, basadas en la web, sin explorador o cliente propio. A continuación, proporcione valores para el nombre de su aplicación, la dirección URL de su página web y un URI de redirección autorizado que [!DNL Zoho CRM] pueda usar para redirigirle con un token de concesión.

Un registro correcto devuelve su ID de cliente y secreto de cliente.

### Crear una solicitud de autorización

A continuación, debe crear una [solicitud de autorización](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) mediante una aplicación basada en web o un cliente propio. La solicitud de autorización devuelve el token de concesión, que a su vez le permite recuperar el token de acceso.

Al crear una solicitud de autorización, debe rellenar los valores de **ámbitos** y **tipo de acceso**. Consulte este [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) para obtener más información sobre los ámbitos, mientras que el **tipo de acceso** siempre debe establecerse en `offline`.

### Generar los tokens de acceso y actualización

Una vez que haya recuperado el token de concesión, puede generar sus [tokens de acceso y actualización](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) realizando una petición POST a `{ACCOUNTS_URL}/oauth/v2/token` y proporcionando al mismo tiempo su ID de cliente, secreto de cliente, token de concesión y URI de redirección. Durante este paso, también debe incluir `grant_type` como parámetro y establecer el valor como `"authorization_code"`.

Una solicitud correcta devuelve los tokens de acceso y actualización, que puede utilizar para autenticarse.

Para ver los pasos detallados sobre cómo adquirir sus credenciales, consulte la [[!DNL Zoho CRM] guía de autenticación](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conectar [!DNL Zoho CRM] a [!DNL Experience Platform] mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Zoho CRM] a Experience Platform mediante API o la interfaz de usuario:

- [Crear una conexión base  [!DNL Zoho CRM] mediante la API de Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)

## Conectar [!DNL Zoho CRM] a [!DNL Experience Platform] mediante la interfaz de usuario

- [Crear una  [!DNL Zoho CRM] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/crm/zoho.md)
- [Crear un flujo de datos para una conexión de origen CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
