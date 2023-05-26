---
solution: Experience Platform
title: Resumen de origen de Marketing Cloud de Salesforce
description: Obtenga información sobre cómo conectar el Marketing Cloud de Salesforce a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: bc37d41d0f7b0ff0cf4d52242f41467f2891d613
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform proporciona asistencia para la ingesta de datos de sistemas de automatización de marketing de terceros. La compatibilidad con proveedores de automatización de marketing incluye [!DNL Salesforce Marketing Cloud].

## Requisitos previos

Antes de poder conectar su [!DNL Salesforce Marketing Cloud] de origen a Platform, debe asegurarse de que lo siguiente **ámbitos de permisos** están aprovisionados para su [!DNL Salesforce Marketing Cloud] combinación de ID de cliente y secreto de cliente:

* `campaign_read`
* `list_and_subscribers_read`

Puede solicitar ámbitos realizando una llamada a la variable `v2/userinfo` recurso de la [!DNL Salesforce Marketing Cloud] API. Consulte la [[!DNL Salesforce Marketing Cloud] Documento de ámbitos de permisos de integración de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obtener instrucciones sobre cómo solicitar y comparar ámbitos.

Para obtener más información sobre los ámbitos, incluida una lista de sus permisos y comportamientos relacionados, consulte esto [[!DNL Salesforce Marketing Cloud] Documento de API de REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>La ingesta de objetos personalizados no es compatible actualmente con [!DNL Salesforce Marketing Cloud] integración de origen.

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Connect [!DNL Salesforce Marketing Cloud] a Platform mediante API

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Salesforce Marketing Cloud] Vaya a Platform mediante las API:

* [Crear una conexión base de Marketing Cloud de Salesforce mediante la API de Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Cree un flujo de datos para una fuente de automatización de marketing mediante la API de Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] a Platform mediante la IU

La siguiente documentación proporciona información sobre cómo conectarse [!DNL Salesforce Marketing Cloud] a Platform mediante la interfaz de usuario:

* [Crear una conexión de origen de Marketing Cloud de Salesforce en la interfaz de usuario](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Cree un flujo de datos para una conexión de origen de automatización de marketing en la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md)
