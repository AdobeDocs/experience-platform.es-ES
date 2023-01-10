---
keywords: Experience Platform;inicio;temas populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Información general sobre el conector de origen Zoho CRM
description: Obtenga información sobre cómo conectar Zoho CRM a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform permite la ingesta de datos de fuentes externas, al tiempo que permite estructurar, etiquetar y mejorar los datos entrantes mediante [!DNL Platform] servicios. Puede ingerir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos desde un sistema CRM de terceros. La compatibilidad con los proveedores de CRM incluye [!DNL Zoho CRM].

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no agrega las direcciones IP específicas de su región a su lista de permitidos, puede que se produzcan errores o que no se produzca un rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Recupere las credenciales de autenticación para [!DNL Zoho CRM]

Antes de poder obtener los datos de su [!DNL Zoho CRM] a Platform, primero debe recuperar sus credenciales para autenticar su [!DNL Zoho CRM] fuente. Siga los pasos a continuación para recuperar el ID de cliente, el secreto de cliente, el token de acceso y el token de actualización.

### Registrar la aplicación

El primer paso para recuperar las credenciales de autenticación es registrar la aplicación mediante el [[!DNL Zoho CRM] consola de desarrollador](https://accounts.zoho.com/). Para registrar la aplicación, debe seleccionar el tipo de cliente de: JavaScript, aplicaciones móviles basadas en web, aplicaciones móviles que no son de navegador o cliente propio. A continuación, proporcione valores para el nombre de su aplicación, la URL de su página web y un URI de redirección autorizado que [!DNL Zoho CRM] puede utilizar para redirigirle con un token de concesión.

Un registro correcto devuelve el ID de cliente y el secreto de cliente.

### Crear una solicitud de autorización

A continuación, debe crear un [solicitud de autorización](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) usar una aplicación basada en web o un cliente propio. La solicitud de autorización devuelve el token de concesión, que a su vez le permite recuperar el token de acceso.

Al crear una solicitud de autorización, debe rellenar los valores para **ámbitos** y **tipo de acceso**. Consulte esta [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) para obtener más información sobre los ámbitos, utilice su **tipo de acceso** siempre debe configurarse como `offline`.

### Generar los tokens de acceso y actualización

Una vez que haya recuperado el token de concesión, puede generar el [acceso y actualización de tokens](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) realizando una solicitud de POST a `{ACCOUNTS_URL}/oauth/v2/token` al proporcionar su ID de cliente, secreto de cliente, token de concesión y URI de redirección. Durante este paso, también debe incluir `grant_type` como parámetro y establezca el valor como `"authorization_code"`.

Una solicitud correcta devolverá los tokens de acceso y actualización, que puede utilizar para autenticarse.

Para ver los pasos detallados sobre la adquisición de sus credenciales, consulte la [[!DNL Zoho CRM] guía de autenticación](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connect [!DNL Zoho CRM] a [!DNL Platform] uso de API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Zoho CRM] a Platform mediante API o la interfaz de usuario:

- [Cree un [!DNL Zoho CRM] conexión base mediante la API de servicio de flujo](../../tutorials/api/create/crm/zoho.md)
- [Exploración de tablas de datos mediante la API de servicio de flujo](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para un origen CRM mediante la API de servicio de flujo](../../tutorials/api/collect/crm.md)

## Connect [!DNL Zoho CRM] a [!DNL Platform] uso de la interfaz de usuario

- [Cree un [!DNL Zoho CRM] conexión de origen en la interfaz de usuario](../../tutorials/ui/create/crm/zoho.md)
- [Crear un flujo de datos para una conexión de origen CRM en la interfaz de usuario](../../tutorials/ui/dataflow/crm.md)
