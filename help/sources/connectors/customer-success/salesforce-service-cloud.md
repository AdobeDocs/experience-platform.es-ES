---
title: Información general sobre el conector Source de Salesforce Service Cloud
description: Obtenga información sobre cómo conectar Salesforce Service Cloud a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud] es una plataforma de éxito de clientes diseñada para automatizar los flujos de trabajo de servicios y optimizar la comunicación entre las empresas y sus clientes. Consolida las solicitudes de varios canales, como correo electrónico, teléfono, medios sociales y chat en directo, en una consola de agente unificada. Esto permite a los equipos de asistencia administrar &quot;casos&quot; con una vista de 360 grados del historial del cliente, lo que garantiza que las respuestas sean personalizadas y eficientes independientemente de cómo contacte con el cliente.

Puede usar el conector de origen [!DNL Salesforce Service Cloud] en Adobe Experience Platform Sources para conectar su cuenta de [!DNL Salesforce Service Cloud] y llevar los datos para usarlos en Experience Platform Services.

Lea este documento para aprender cómo configurar su cuenta de [!DNL Salesforce Service Cloud] y conectarla a Experience Platform.

## Requisitos previos {#prerequisites}

Lea esta sección para conocer la configuración de requisitos previos que debe completar para poder conectarse correctamente a Experience Platform.

### LISTA DE PERMITIDOS de direcciones IP {#allowlist}

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

### Recopilar credenciales necesarias {#credentials}

Debe proporcionar valores para las siguientes credenciales a fin de conectar su cuenta de [!DNL Salesforce Service Cloud] mediante la credencial de cliente de OAuth2.

| Credencial | Descripción |
| --- | --- |
| URL de entorno | Dirección URL de la instancia de origen [!DNL Salesforce Service Cloud]. |
| ID de cliente | El ID de cliente se utiliza junto con el secreto de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce Service Cloud]. |
| Secreto del cliente | El secreto de cliente se utiliza junto con el ID de cliente como parte de la autenticación OAuth2. Juntos, el ID de cliente y el secreto de cliente permiten que su aplicación funcione en nombre de su cuenta al identificar su aplicación en [!DNL Salesforce Service Cloud]. |
| Versión de API | La versión de la API de REST de la instancia [!DNL Salesforce Service Cloud] que está utilizando. El valor de la versión de la API debe tener formato decimal. Por ejemplo, si está usando la versión de API `52`, debe introducir el valor como `52.0`. Si este campo se deja en blanco, Experience Platform utilizará automáticamente la última versión disponible. |

Para obtener más información sobre el uso de OAuth para [!DNL Salesforce Service Cloud], lea la [[!DNL Salesforce Service Cloud] guía sobre flujos de autorización de OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Conectar [!DNL Salesforce Service Cloud] a Experience Platform mediante API

- [Crear una conexión base de Salesforce Service Cloud mediante la API de Flow Service](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
- [Crear un flujo de datos para una fuente de éxito de clientes mediante la API de Flow Service](../../tutorials/api/collect/customer-success.md)

## Conectar [!DNL Salesforce Service Cloud] a Experience Platform mediante la interfaz de usuario

- [Crear una conexión de origen de Salesforce Service Cloud en la interfaz de usuario](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [Crear un flujo de datos para una conexión de origen de éxito del cliente en la IU](../../tutorials/ui/dataflow/customer-success.md)
