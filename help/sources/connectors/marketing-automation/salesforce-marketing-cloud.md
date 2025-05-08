---
solution: Experience Platform
title: Información general sobre Salesforce Marketing Cloud Source
description: Obtenga información sobre cómo conectar Salesforce Marketing Cloud a Adobe Experience Platform mediante API o la interfaz de usuario.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2025-04-29T00:00:00Z
source-git-commit: ce96dbc64845fddb40ebee709828c56d51a6c6ba
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>El origen [!DNL Salesforce Marketing Cloud] quedará obsoleto en enero de 2026. Una nueva fuente se publicará a finales de este año como alternativa. Una vez lanzada la nueva fuente, debe planificar la migración a la nueva fuente creando nuevas conexiones de cuenta y flujos de datos antes de finales de enero de 2026.

Adobe Experience Platform permite la ingesta de datos desde fuentes externas, al tiempo que le ofrece la capacidad de estructurar, etiquetar y mejorar los datos entrantes mediante los servicios de Experience Platform. Puede introducir datos de una variedad de fuentes, como aplicaciones de Adobe, almacenamiento basado en la nube, bases de datos y muchas otras.

Experience Platform es compatible con la ingesta de datos desde sistemas de automatización de marketing de terceros. Los proveedores de automatización de marketing admiten [!DNL Salesforce Marketing Cloud].

## Requisitos previos

Para poder conectar el origen de [!DNL Salesforce Marketing Cloud] a Experience Platform, debe asegurarse de que los siguientes **ámbitos de permisos** estén aprovisionados para la combinación de ID de cliente y secreto de cliente de [!DNL Salesforce Marketing Cloud]:

* `campaign_read`
* `list_and_subscribers_read`

Puede solicitar ámbitos realizando una llamada al recurso `v2/userinfo` de la API [!DNL Salesforce Marketing Cloud]. Consulte el [[!DNL Salesforce Marketing Cloud] documento Ámbitos de permisos de integración de API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>) para obtener instrucciones sobre cómo solicitar y comparar ámbitos.

Para obtener más información sobre los ámbitos, incluida una lista de sus permisos y comportamientos relacionados, consulte este [[!DNL Salesforce Marketing Cloud] documento de API de REST](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>La integración de origen de [!DNL Salesforce Marketing Cloud] no admite actualmente la ingesta de objetos personalizados.

## LISTA DE PERMITIDOS de direcciones IP

Debe añadir direcciones IP específicas de la región a la lista de permitidos antes de conectar los orígenes a Experience Platform. Para obtener más información, lea la guía de [inclusión en la lista de permitidos de direcciones IP para conectarse a Experience Platform](../../ip-address-allow-list.md).

>[!WARNING]
>
>Si no agrega las direcciones IP necesarias a la lista de permitidos, la cuenta de [!DNL Salesforce Marketing Cloud] no se conectará a Experience Platform.

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante API

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante API:

* [Crear una conexión base de Salesforce Marketing Cloud mediante la API de Flow Service](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Exploración de tablas de datos mediante la API de Flow Service](../../tutorials/api/explore/tabular.md)
* [Cree un flujo de datos para una fuente de automatización de marketing mediante la API de Flow Service](../../tutorials/api/collect/marketing-automation.md)

## Conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario

La siguiente documentación proporciona información sobre cómo conectar [!DNL Salesforce Marketing Cloud] a Experience Platform mediante la interfaz de usuario:

* [Crear una conexión de origen de Salesforce Marketing Cloud en la interfaz de usuario](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Cree un flujo de datos para una conexión de origen de automatización de marketing en la interfaz de usuario](../../tutorials/ui/dataflow/marketing-automation.md)
