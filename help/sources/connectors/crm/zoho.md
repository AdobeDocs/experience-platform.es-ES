---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Información general sobre el conector de origen Zoho CRM
description: Aprenda a conectar Zoho CRM a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform proporciona asistencia para la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con proveedores CRM incluye [!DNL Zoho CRM].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Recupere sus credenciales de autenticación para [!DNL Zoho CRM]

Antes de poder traer datos de su [!DNL Zoho CRM] cuenta a Platform, primero debe recuperar las credenciales para autenticar su [!DNL Zoho CRM] origen. Siga los pasos a continuación para recuperar el ID de cliente, el secreto de cliente, el token de acceso y el token de actualización.

### Registre la aplicación

El primer paso para recuperar las credenciales de autenticación es registrar la aplicación utilizando [[!DNL Zoho CRM] consola para desarrolladores](https://accounts.zoho.com/). Para registrar la aplicación, debe seleccionar el tipo de cliente de: JavaScript, aplicaciones móviles, basadas en la web, sin explorador o cliente propio. A continuación, proporcione valores para el nombre de la aplicación, la dirección URL de la página web y un URI de redirección autorizado que [!DNL Zoho CRM] puede utilizar para redirigirle con un token de concesión.

Un registro correcto devuelve su ID de cliente y secreto de cliente.

### Crear una solicitud de autorización

A continuación, debe crear un [solicitud de autorización](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) mediante una aplicación basada en web o un cliente propio. La solicitud de autorización devuelve el token de concesión, que a su vez le permite recuperar el token de acceso.

Al crear una solicitud de autorización, debe rellenar los valores de ambos **ámbitos** y **tipo de acceso**. Consulte esta sección [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) para obtener más información sobre los ámbitos, consulte **tipo de acceso** siempre debe configurarse como `offline`.

### Generar los tokens de acceso y actualización

Una vez que haya recuperado el token de concesión, puede generar su [tokens de acceso y actualización](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) realizando una solicitud de POST a `{ACCOUNTS_URL}/oauth/v2/token` al proporcionar el ID de cliente, el secreto de cliente, el token de concesión y el URI de redirección. Durante este paso, también debe incluir `grant_type` como parámetro y establezca el valor como `"authorization_code"`.

Una solicitud correcta devuelve los tokens de acceso y actualización, que puede utilizar para autenticarse.

Para ver los pasos detallados sobre la adquisición de credenciales, consulte la [[!DNL Zoho CRM] guía de autenticación](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connect [!DNL Zoho CRM] hasta [!DNL Platform] uso de API

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Zoho CRM] Vaya a Platform mediante las API o la interfaz de usuario de:

- [Crear un [!DNL Zoho CRM] conexión base mediante la API de Flow Service](../../tutorials/api/create/crm/zoho.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente CRM mediante la API de Flow Service](../../tutorials/api/collect/crm.md)

## Connect [!DNL Zoho CRM] hasta [!DNL Platform] uso de la IU

- [Crear un [!DNL Zoho CRM] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/crm/zoho.md)
- [Crear un flujo de datos para una conexión de origen CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
