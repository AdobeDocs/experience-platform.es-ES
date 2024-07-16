---
title: Información general sobre NetSuite Source de oracle
description: Obtenga información sobre cómo conectar NetSuite de Oracle a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
exl-id: 1dd30660-c990-4d3f-a64f-2a17e426f56d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 2%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>El origen [!DNL Oracle NetSuite] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform de proporciona asistencia para la ingesta de datos mediante un sistema de automatización de marketing de terceros. La compatibilidad con los proveedores de automatización de marketing incluye [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) es un paquete de administración empresarial basado en la nube que incluye soluciones ERP/financieras, CRM y de comercio electrónico.

Puede usar dos fuentes diferentes para ingerir datos de [!DNL Oracle NetSuite] en el Experience Platform:

* Usar el origen [!DNL Oracle NetSuite Activities] para introducir datos de eventos.
* Usar el origen [!DNL Oracle NetSuite Entities] para ingerir datos de clientes y contactos.

Vea la siguiente tabla para obtener más información sobre los dos orígenes de [!DNL Oracle NetSuite].

| Fuente | Tipo | Descripción |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Evento | Recupere las actividades programadas añadidas al calendario. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Cliente | Recupere datos específicos del cliente, incluidos detalles como nombres de clientes, direcciones e identificadores clave. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contacto | Recupere nombres de contactos, correos electrónicos, números de teléfono y cualquier campo personalizado relacionado con contactos asociado con clientes. |

## LISTA DE PERMITIDOS de direcciones IP {#ip-allow-list}

Es posible que sea necesario agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos {#prerequisites}

Para poder llevar los datos de [!DNL Oracle NetSuite] al Experience Platform, primero debe asegurarse de que dispone de lo siguiente:

* **Una cuenta de [!DNL Oracle NetSuite]**.
   * Póngase en contacto con [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) si todavía no tiene una cuenta válida.
* Una **suscripción activa** a cualquier producto de [!DNL Oracle NetSuite].
* Un **ID de cuenta**.
   * El origen [!DNL Oracle NetSuite] utiliza OAuth 2.0 para comunicarse con las API [!DNL Oracle NetSuite]. Si no tiene su ID de cuenta, visite la documentación de [!DNL Oracle] en [cómo recuperar su ID de cuenta](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* Una combinación de **ID de cliente** y **secreto de cliente**.
   * Se requieren el ID de cliente y el secreto de cliente para acceder a las API de [!DNL Oracle NetSuite]. Durante este paso, también debe asegurarse de que el administrador tenga:
      * Se ha habilitado la función OAuth 2.0 y se han configurado las funciones de OAuth 2.0 adecuadas.
      * Se han asignado usuarios a las funciones de OAuth 2.0 y se han creado los registros de integración necesarios.
* Un **token de acceso** y un **token de actualización**.
   * Consulte la guía [!DNL Oracle] en [Flujo de concesión de código de autorización de OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) para obtener información sobre cómo generar los tokens de acceso y actualización.

### Recopilar credenciales necesarias {#gather-credentials}

Para conectar [!DNL Oracle NetSuite] a Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID de cliente | Valor de ID de cliente que se genera al crear el registro de integración en [!DNL Oracle NetSuite]. Lea la guía [!DNL Oracle] sobre cómo [crear registros de integración](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obtener más información. | `7fce.....b42f`<br>El valor es una cadena de 64 caracteres. |
| Secreto del cliente | El valor secreto de cliente que se genera al crear el registro de integración. Lea la guía [!DNL Oracle] sobre cómo [crear registros de integración](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obtener más información. | `5c98.....1b46`<br>El valor es una cadena de 64 caracteres. |
| URL de prueba de autorización | (Opcional) Su URL de prueba de autorización de [!DNL NetSuite]. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Token de acceso | El token de acceso está en formato JSON Web Token (JWT) y solo es válido durante 60 minutos. Para obtener más información sobre cómo recuperar el token de acceso, lea la guía [!DNL Oracle] sobre la autorización de [OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br>: el valor es una cadena de 1024 caracteres con formato de token web JSON (JWT). |
| Actualizar token | Use la actualización para generar un nuevo token de acceso, una vez que caduque el token de acceso. El token de actualización es válido durante siete días. Para obtener más información sobre cómo recuperar el token de acceso, lea la guía [!DNL Oracle] sobre la autorización de [OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br>: el valor es una cadena de 1024 caracteres con formato de token web JSON (JWT). |
| URL de token de acceso | Extremo de token al que la aplicación envía las solicitudes del POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Una vez que caduca un token de actualización, debe crear una nueva cuenta en Experience Platform con los tokens actualizados.

## Conectar [!DNL Oracle NetSuite Activities] a Platform {#oracle-netsuite-activities}

La siguiente documentación proporciona información sobre cómo conectar [!DNL Oracle NetSuite Activities] a Platform mediante API o la interfaz de usuario:

* [Cree una conexión de origen y un flujo de datos para llevar [!DNL Oracle NetSuite Activities] datos a Platform mediante API](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Conecte su cuenta de  [!DNL Oracle NetSuite Activities] al Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Cree un flujo de datos para una conexión de origen mediante la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md).

## Conectar [!DNL Oracle NetSuite Entities] a Platform {#oracle-netsuite-entities}

La siguiente documentación proporciona información sobre cómo conectar [!DNL Oracle NetSuite Entities] a Platform mediante API o la interfaz de usuario:

* [Cree una conexión de origen y un flujo de datos para llevar [!DNL Oracle NetSuite Entities] datos a Platform mediante API](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Conecte su cuenta de  [!DNL Oracle NetSuite Entities] al Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Cree un flujo de datos para una conexión de origen mediante la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md).
