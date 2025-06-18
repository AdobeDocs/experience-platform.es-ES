---
title: Información general sobre Salesforce Marketing Cloud Source
description: Obtenga información sobre cómo conectar Salesforce Marketing Cloud a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-05-17T00:00:00Z
source-git-commit: 0c0a58df4beae499008e52c118b40bed86ff0596
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 1%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto en enero de 2026. Una nueva fuente se publicará a finales de este año como alternativa. Una vez lanzada la nueva fuente, debe planificar la migración a la nueva fuente creando nuevas conexiones de cuenta y flujos de datos antes de finales de enero de 2026.

[!DNL Salesforce Marketing Cloud] le permite administrar y automatizar la participación de los clientes en correos electrónicos, móviles, medios sociales y publicidad, todo desde una plataforma. Con herramientas como Email Studio, Recorrido Builder y Audience Builder, puede crear campañas personalizadas y recorridos de cliente adaptados a su audiencia.

Puede usar el origen [!DNL Salesforce Marketing Cloud] para conectar su cuenta y llevar los datos a Adobe Experience Platform.

## Requisitos previos

Para poder conectar el origen de [!DNL Salesforce Marketing Cloud] a Experience Platform, debe asegurarse de que los siguientes **ámbitos de permisos** estén aprovisionados para la combinación de ID de cliente y secreto de cliente de [!DNL Salesforce Marketing Cloud]:

* `campaign_read`
* `list_and_subscribers_read`

Puede solicitar ámbitos realizando una llamada al recurso `v2/userinfo` de la API [!DNL Salesforce Marketing Cloud]. Consulte el [[!DNL Salesforce Marketing Cloud] documento Ámbitos de permisos de integración de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obtener instrucciones sobre cómo solicitar y comparar ámbitos.

Para obtener más información sobre los ámbitos, incluida una lista de sus permisos y comportamientos relacionados, consulte este [[!DNL Salesforce Marketing Cloud] documento de API de REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.

### LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Si no agrega las direcciones IP necesarias a la lista de permitidos, la cuenta de [!DNL Salesforce Marketing Cloud] no se conectará a Experience Platform.

### Autenticar en Experience Platform en Azure {#azure}

Debe proporcionar valores para las siguientes credenciales para conectar [!DNL Salesforce Marketing Cloud] a Experience Platform en [!DNL Azure].

| Credencial | Descripción |
| --- | --- |
| Host | Servidor host de la aplicación. Este suele ser su subdominio. **Nota:** Al escribir el valor `host`, debe especificar `{subdomain}.rest.marketingcloudapis.com`. Por ejemplo, si la dirección URL de host es `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, debe escribir `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/` como valor de host. |
| ID de cliente | Identificador de cliente asociado con la aplicación [!DNL Salesforce Marketing Cloud]. |
| Secreto del cliente | Secreto de cliente asociado a la aplicación [!DNL Salesforce Marketing Cloud]. |
| ID de especificación de conexión | La **especificación de conexión** proporciona las propiedades de conector de un origen de datos. Esto incluye detalles como especificaciones de autenticación y requisitos para crear conexiones **base** y **origen**. Para [!DNL Salesforce Marketing Cloud], el id. de especificación de conexión es: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Nota:** Esta credencial solo es necesaria cuando se conecta a través de API. |

### Autenticar en Experience Platform en Amazon Web Service (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta sección se aplica a las implementaciones de Experience Platform que se ejecutan en Amazon Web Service (AWS). Experience Platform que se ejecuta en AWS está disponible actualmente para un número limitado de clientes. Para obtener más información sobre la infraestructura de Experience Platform compatible, consulte la [descripción general de la nube múltiple de Experience Platform](../../../landing/multi-cloud.md).

Debe proporcionar valores para las siguientes credenciales a fin de conectar [!DNL Salesforce Marketing Cloud] a Experience Platform en AWS.

| Credencial | Descripción |
| --- | --- |
| Subdominio | La parte única de la URL de su instancia [!DNL Salesforce Marketing Cloud], que se usa para construir los extremos de la API. |
| ID de cliente | Identificador público de su aplicación, generado al crear un paquete instalado en [!DNL Salesforce Marketing Cloud] |
| Secreto del cliente | Una clave confidencial asociada a su ID de cliente, también generada en el paquete instalado. |
| ID de especificación de conexión | La **especificación de conexión** proporciona las propiedades de conector de un origen de datos. Esto incluye detalles como especificaciones de autenticación y requisitos para crear conexiones **base** y **origen**. Para [!DNL Salesforce Marketing Cloud], el id. de especificación de conexión es: `ea1c2a08-b722-11eb-8529-0242ac130003`. **Nota:** Esta credencial solo es necesaria cuando se conecta a través de API. |

Para obtener más información, lea la [[!DNL Salesforce] documentación sobre el token de acceso para integraciones de servidor a servidor](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/access-token-s2s.html).

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante API:

* [Conectar  [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la API de Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Cree un flujo de datos para una fuente de automatización de marketing mediante la API de Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario:

* [Conectar  [!DNL Salesforce Marketing Cloud] a Experience Platform en la interfaz de usuario](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Cree un flujo de datos para una conexión de origen de automatización de marketing en la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md)
