---
title: Información general sobre Google Ads Source
description: Obtenga información sobre cómo conectar Google Ads a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 1f6257e0-213c-4723-a240-511c11c5833c
source-git-commit: ac90eea69f493bf944a8f9920426a48d62faaa6c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# [!DNL Google Ads] origen

>[!NOTE]
>
>El origen [!DNL Google Ads] está en la versión beta. Consulte [Resumen de fuentes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiqueta beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde un sistema de publicidad de terceros. Los proveedores de publicidad admiten [!DNL Google Ads].

## Requisitos previos {#prerequisites}

### LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Configuración de permisos en Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Google Ads] a Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/ui/overview.md).

### Recopilar credenciales necesarias

Debe proporcionar los valores adecuados a las siguientes credenciales para conectar correctamente su cuenta de [!DNL Google Ads] a Experience Platform.

| Credencial | Descripción |
| --- | --- |
| `clientCustomerId` | El id. de cliente es el número de cuenta que corresponde a la cuenta de cliente [!DNL Google Ads] que desea administrar con la API [!DNL Google Ads]. Este identificador sigue la plantilla de `123-456-7890`. |
| `loginCustomerId` | El identificador de cliente de inicio de sesión es el número de cuenta que corresponde con su cuenta de administrador [!DNL Google Ads] y se usa para recuperar los datos del informe de un cliente operativo específico. Para obtener más información sobre el ID de cliente de inicio de sesión, lea la [[!DNL Google Ads] documentación de la API](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| `developerToken` | El token de desarrollador le permite acceder a la API [!DNL Google Ads]. Puede usar el mismo token de desarrollador para realizar solicitudes en todas sus cuentas de [!DNL Google Ads]. Recupere su token de desarrollador al [iniciar sesión en su cuenta de administrador](https://ads.google.com/home/tools/manager-accounts/) y luego navegar a la página [!DNL API Center]. |
| `refreshToken` | El token de actualización forma parte de la autenticación [!DNL OAuth2]. Este token le permite volver a generar los tokens de acceso una vez caducados. |
| `clientId` | El ID de cliente se usa junto con el secreto de cliente como parte de la autenticación [!DNL OAuth2]. En conjunto, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Google]. |
| `clientSecret` | El secreto de cliente se usa junto con el ID de cliente como parte de la autenticación [!DNL OAuth2]. En conjunto, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Google]. |
| `googleAdsApiVersion` | Versión de API actual admitida por [!DNL Google Ads]. Aunque la versión más reciente es `v18`, la última versión compatible con Experience Platform es `v17`. |
| `connectionSpec.id` | La especificación de conexión devuelve las propiedades del conector de origen, incluidas las especificaciones de autenticación relacionadas con la creación de las conexiones base y origen. El id. de especificación de conexión para [!DNL Google Ads] es: `d771e9c1-4f26-40dc-8617-ce58c4b53702`. Este valor es necesario si está conectando su cuenta de [!DNL Google Ads] mediante la API de [!DNL Flow Service]. |

## Conectar [!DNL Google Ads] a Experience Platform

La siguiente documentación proporciona información sobre cómo conectar [!DNL Google Ads] a Experience Platform mediante API o la interfaz de usuario:

### Uso de API

* [Creación de una conexión base de Google Ads mediante la API de Flow Service](../../tutorials/api/create/advertising/ads.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Creación de un flujo de datos para una fuente de publicidad mediante la API de Flow Service](../../tutorials/api/collect/advertising.md)

### Uso de la IU

* [Crear una conexión de origen de Google Ads en la interfaz de usuario](../../tutorials/ui/create/advertising/ads.md)
* [Crear un flujo de datos para una conexión de origen de publicidad en la interfaz de usuario](../../tutorials/ui/dataflow/advertising.md)
