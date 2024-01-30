---
title: Información general de origen de NetSuite de oracle
description: Obtenga información sobre cómo conectar NetSuite de Oracle a Adobe Experience Platform mediante API o la interfaz de usuario.
last-substantial-update: 2024-01-30T00:00:00Z
badge: Beta
source-git-commit: 632cff3ee4ca82d391e9a1df0cb38d903e8a5428
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# [!DNL Oracle NetSuite]

>[!NOTE]
>
>El [!DNL Oracle NetSuite] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

El Experience Platform de proporciona asistencia para la ingesta de datos mediante un sistema de automatización de marketing de terceros. La compatibilidad con proveedores de automatización de marketing incluye [!DNL Oracle NetSuite].

[[!DNL Oracle NetSuite]](https://www.netsuite.com/) es un paquete de gestión empresarial basado en la nube que incluye soluciones ERP/financieras, CRM y de comercio electrónico.

Puede utilizar dos fuentes diferentes para introducir datos de [!DNL Oracle NetSuite] al Experience Platform:

* Utilice el [!DNL Oracle NetSuite Activities] origen para introducir datos de eventos.
* Utilice el [!DNL Oracle NetSuite Entities] origen para introducir datos de clientes y contactos.

Consulte la siguiente tabla para obtener más información sobre ambos [!DNL Oracle NetSuite] fuentes.

| Fuente | Tipo | Descripción |
| --- | --- | --- |
| [[!DNL Oracle NetSuite Activities]](#oracle-netsuite-activities) | Evento | Recupere las actividades programadas añadidas al calendario. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Cliente | Recupere datos específicos del cliente, incluidos detalles como nombres de clientes, direcciones e identificadores clave. |
| [[!DNL Oracle NetSuite Entities]](#oracle-netsuite-entities) | Contacto | Recupere nombres de contactos, correos electrónicos, números de teléfono y cualquier campo personalizado relacionado con contactos asociado con clientes. |

## LISTA DE PERMITIDOS de direcciones IP {#ip-allow-list}

Es posible que sea necesario agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Requisitos previos {#prerequisites}

Antes de que pueda traer su [!DNL Oracle NetSuite] datos al Experience Platform, primero debe asegurarse de que dispone de lo siguiente:

* **Un [!DNL Oracle NetSuite] account**.
   * Contacto [[!DNL Oracle NetSuite]](https://www.NetSuite.com/portal/company/contactus.shtml) si todavía no tiene una cuenta válida.
* Un **suscripción activa** a cualquier [!DNL Oracle NetSuite] producto.
* Un **ID de cuenta**.
   * El [!DNL Oracle NetSuite] El origen utiliza OAuth 2.0 para comunicarse con el [!DNL Oracle NetSuite] API. Si no tiene su ID de cuenta, visite la [!DNL Oracle] documentación sobre [Obtenga información sobre cómo recuperar su ID de cuenta](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_1498754928.html#Finding-Your-NetSuite-Account-ID).
* A **ID de cliente** y **secreto de cliente** combinación.
   * Se requieren el ID de cliente y el secreto de cliente para acceder a [!DNL Oracle NetSuite] API. Durante este paso, también debe asegurarse de que el administrador tenga:
      * Se ha habilitado la función OAuth 2.0 y se han configurado las funciones de OAuth 2.0 adecuadas.
      * Se han asignado usuarios a las funciones de OAuth 2.0 y se han creado los registros de integración necesarios.
* Un **token de acceso** y una **token de actualización**.
   * Consulte la [!DNL Oracle] guía sobre [Flujo de concesión de código de autorización de OAuth 2.0](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158074210415.html#OAuth-2.0-Authorization-Code-Grant-Flow) para obtener información sobre cómo generar los tokens de acceso y actualización.

### Recopilar credenciales necesarias {#gather-credentials}

Para poder conectarse [!DNL Oracle NetSuite] En Platform, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción | Ejemplo |
| --- | --- | --- |
| ID de cliente | El valor de ID de cliente que se genera al crear el registro de integración en [!DNL Oracle NetSuite]. Lea el [!DNL Oracle] guía sobre cómo [creación de registros de integración](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obtener más información. | `7fce.....b42f`<br>El valor es una cadena de 64 caracteres. |
| Secreto de cliente | El valor secreto de cliente que se genera al crear el registro de integración. Lea el [!DNL Oracle] guía sobre cómo [creación de registros de integración](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_157771733782.html#procedure_157838925981) para obtener más información. | `5c98.....1b46`<br>El valor es una cadena de 64 caracteres. |
| URL de prueba de autorización | (Opcional) Su [!DNL NetSuite] URL de prueba de autorización. | `https://{ACCOUNT_ID}.app.netsuite.com<br>/app/login/oauth2/authorize.nl?response_type=code<br>&redirect_uri=https%3A%2F%2Fapi.github.com<br>&scope=rest_webservices<br>&state=ykv2XLx1BpT5Q0F3MRPHb94j<br>&client_id={CLIENT_ID}` |
| Token de acceso | El token de acceso está en formato JSON Web Token (JWT) y solo es válido durante 60 minutos. Para obtener más información sobre cómo recuperar el token de acceso, lea la [!DNL Oracle] guía sobre [Autorización de OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......f4V0`<br> El valor es una cadena de 1024 caracteres con formato de token web JSON (JWT). |
| Actualizar token | Use la actualización para generar un nuevo token de acceso, una vez que caduque el token de acceso. El token de actualización es válido durante siete días. Para obtener más información sobre cómo recuperar el token de acceso, lea la [!DNL Oracle] guía sobre [Autorización de OAuth 2.0 para NetSuite](https://docs.oracle.com/en/cloud/saas/netsuite/ns-online-help/section_158081952044.html#Step-Two-POST-Request-to-the-Token-Endpoint). | `eyJr......dmxM`<br> El valor es una cadena de 1024 caracteres con formato de token web JSON (JWT). |
| URL de token de acceso | Extremo de token al que la aplicación envía las solicitudes del POST. | `https://{ACCOUNT_ID}.suitetalk.api.netsuite.com<br>/services/rest/auth/oauth2/v1/token` |

>[!IMPORTANT]
>
>Una vez que caduca un token de actualización, debe crear una nueva cuenta en Experience Platform con los tokens actualizados.

## Connect [!DNL Oracle NetSuite Activities] a Platform {#oracle-netsuite-activities}

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Oracle NetSuite Activities] Vaya a Platform mediante las API o la interfaz de usuario de:

* [Crear una conexión de origen y un flujo de datos para traer [!DNL Oracle NetSuite Activities] datos a Platform mediante API](../../tutorials/api/create/marketing-automation/oracle-netsuite-activities.md).
* [Conecte su [!DNL Oracle NetSuite Activities] cuenta de al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md).
* [Crear un flujo de datos para una conexión de origen mediante la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md).

## Connect [!DNL Oracle NetSuite Entities] a Platform {#oracle-netsuite-entities}

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Oracle NetSuite Entities] Vaya a Platform mediante las API o la interfaz de usuario de:

* [Crear una conexión de origen y un flujo de datos para traer [!DNL Oracle NetSuite Entities] datos a Platform mediante API](../../tutorials/api/create/marketing-automation/oracle-netsuite-entities.md).
* [Conecte su [!DNL Oracle NetSuite Entities] cuenta de al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md).
* [Crear un flujo de datos para una conexión de origen mediante la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md).
